# Exact paired-evidence correction — 2026-09-23 12:26 KST

## Finding
The 12:23 evidence table was too restrictive: it omitted historical artifacts that explicitly recorded both predecessor `active_work_sec` and the following end-to-start `idle_gap_sec`. Those values satisfy the existing DIRECT/DERIVED_VALID acceptance rule on their face and should not be discarded merely because they predate the current JSON schema.

## Recovered exact pairs
| predecessor active_work_sec | following idle_gap_sec | paired utilization | source |
|---:|---:|---:|---|
| 20 | 319 | 0.05899705 | `analysis/2026-09-22T2339_clean-pair-and-admission.md` |
| 105 | 261 | 0.28688525 | `analysis/2026-09-22T2345_active-duration-admission.md` |
| 32 | 304 | 0.09523810 | `analysis/2026-09-22T2350_active-duration-treatment.md` |
| 480 | 251 | 0.65663475 | `runs/2026-09-23T030454+0900-frontier-600.json` + `state/frontier-evidence.json` |

The 61-second idle-only sample remains excluded because its artifact explicitly says `active_work_sec: not claimed`.

## Interpretation
The corrected exact table has n=4, not n=1. It strongly supports the qualitative conclusion that bookkeeping-sized runs waste the fixed boundary cost and that materially longer useful-work blocks improve utilization. It still does not justify fitting a precise adaptive cutoff because idle cost varies across pairs and the active durations are sparse/non-random. The verified no-forced-stop frontier remains 480 seconds; 600 seconds remains an uncompleted target/admission.

## Experimental discipline
No mechanism is changed by this correction. The sole treatment variable remains same-wake useful-work duration. Scheduler jitter remains diagnostic only.