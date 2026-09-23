# RRULEF

## Objective
유일한 불변 목표: **최대 가동률 / 최소 유휴시간**.

정책이나 임계값은 목표가 아니라 수단입니다. 실측상 더 나은 방법이 있으면 교체합니다.

## Baseline A — 10-minute budget
현재 비교 기준:
1. 실행 시작 시각 기록.
2. 작은 작업을 수행하고 각 작업의 duration 기록.
3. 누적 작업시간이 10분 미만이면 즉시 다음 유효 작업을 계속 수행.
4. 10분 이상이면 다음 wake를 가능한 한 이르게 확보한 뒤 handoff.
5. 10분은 runtime timeout 회피를 위한 초기 경험값이며 고정 규칙이 아님.

## Measure
각 실행에서 가능한 범위에서 다음을 기록합니다.
- active_work_sec: 실질 작업 시간
- work_end_time: 실제 실질 작업 종료 시각
- actual_next_start_time: 다음 실행 실제 시작 시각
- idle_gap_sec: work_end_time부터 actual_next_start_time까지의 실제 공백
- handoff_overhead_sec: handoff 결정부터 다음 wake 확보/상태 저장 완료까지
- run_elapsed_sec: 실행 시작부터 종료까지
- tasks_completed
- timeout_or_forced_stop
- scheduled_next_wake: 요청한 다음 wake 시각
- scheduler_jitter_sec: scheduled_next_wake와 실제 다음 시작의 차이. 진단용이며 최적화 목표 자체가 아님.

핵심 평가지표:
- utilization: 실질 작업 시간 대비 실질 작업 시간과 실제 idle gap의 합에서 차지하는 비율
- idle_gap_sec는 작을수록 좋음.
- timeout/강제중단으로 미완료 작업이 손실되면 실패 비용으로 기록.

## Jitter handling
스케줄러 지터 자체를 제거하는 것은 목표가 아닙니다. 지터는 외생 변수로 취급합니다.
최적화 대상은 **이전 실질 작업 종료부터 다음 실제 실행 시작까지의 idle gap**입니다.

따라서:
- scheduled wake와 actual start 차이는 진단용으로 기록합니다.
- 수십 초 지터를 줄이기 위해 실질 작업 시간을 희생하지 않습니다.
- 지터가 존재해도 전체 utilization이 높아지는 handoff/wake 메커니즘을 우선합니다.

## Optimization loop
한 번에 한 가지 메커니즘만 바꾸고 baseline과 비교합니다.

우선 실험 후보:
- Baseline A: 고정 10분 cutoff
- Adaptive cutoff: 현재 경과시간, 예상 다음 task 시간, handoff 안전마진을 함께 보고 다음 작업 착수 여부 결정
- handoff를 cutoff 직전에 하는 방식 vs 다음 wake를 먼저 확보한 뒤 계속 작업하는 방식
- 실제 idle gap을 가장 작게 만드는 near-future wake 재앵커링 방식
- timeout 없이 안전하게 사용할 수 있는 실질 작업시간 상한 추정

더 높은 가동률 또는 더 낮은 유휴시간을 만들지 못하는 규칙은 유지하지 않습니다.


## Integrated research supervisor
RRULEF now acts as the integration layer over two READ_ONLY evidence sources:
- `amzsdq/tEST`: scheduler/self-update semantics, lead-time and wake evidence.
- `amzsdq/workwork`: runtime-boundary, pre-arm, and handoff/admission evidence.

Those repositories are evidence sources only; RRULEF research writes stay in this repository.

Stable execution semantics are defined in `CONTROL_KERNEL.md`. Dynamic treatment state is defined in `state/controller.json`; changing frontier/target values should not be duplicated into the automation prompt.

### Current integration experiment
H1 tests one change only: add a start-of-turn crash-insurance pre-arm while retaining a verified final rearm as the authoritative fast continuation. Runtime target remains 600s and nominal lead remains 180s during this treatment. If H1 adds overhead/overlap without measurable recovery benefit, roll back to final-only.
