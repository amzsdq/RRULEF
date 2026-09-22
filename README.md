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
각 실행에서 최소한 다음을 기록해 비교합니다.
- active_work_sec: 실질 작업 시간
- idle_gap_sec: 이전 실행 종료 → 다음 실행 시작 공백
- handoff_overhead_sec: 작업 중단 결정 → 다음 wake 확보까지
- run_elapsed_sec: 실행 시작 → 종료
- tasks_completed
- timeout_or_forced_stop
- next_wake_sec: 종료 시점 → 다음 예약 시점

핵심 평가지표:
- utilization = active_work_sec / (active_work_sec + idle_gap_sec)
- idle_gap_sec는 작을수록 좋음.
- timeout/강제중단으로 미완료 작업이 손실되면 실패 비용으로 기록.

## Optimization loop
한 번에 한 가지 메커니즘만 바꾸고 baseline과 비교합니다.
우선 실험 후보:
- 고정 10분 cutoff
- 최근 실행시간/오버헤드 기반 adaptive cutoff
- handoff를 cutoff 직전에 하는 방식 vs 다음 wake를 선확보하는 방식
- 다음 wake 간격 최소화

더 높은 가동률 또는 더 낮은 유휴시간을 만들지 못하는 규칙은 유지하지 않습니다.
