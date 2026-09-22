# Measurement integrity for the sustained-work sample

Before canonical state write, the previous state was re-read and remains unchanged, so the 06:45:30 predecessor endpoint has not been concurrently overwritten.

For the current sample:
- actual start is the observed automation start, 2026-09-23T06:55:54+09:00.
- previous work end is 2026-09-23T06:45:30+09:00.
- resulting idle gap is 624 sec.
- previous active work is 63 sec, so the closed pair is valid.
- scheduler jitter relative to the predecessor's requested 06:58 wake is -126 sec, but this is diagnostic only and is not used to shorten useful work.

Canonicalization guard remains: current active_work_sec and work_end_time will be written only from completed work at the end of this wake; no projected future endpoint will be stored.

The continuation has already been secured before final durable-state write.