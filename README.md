# QA / testing-tools OSS bug hunt

Correctness & robustness bugs found in widely-used QA / testing tools via property-based &
differential testing, each reproduced at runtime and cross-checked before reporting.

**Method:** for each tool, recent bug-fix commits map the fragile seams; the unfixed sibling code
paths are read, a minimal repro is built, and the divergence is confirmed by executing the real tool
against a reference oracle. Every finding below was re-verified in a clean context (runtime execution
+ two independent skeptic models) before filing.

**Honesty:** an aggressive first pass surfaced 107 candidates; a full runtime + cross-vendor +
dedup gate cut that to the confirmed set below. If any issue is intended/by-design, it gets closed
with an apology — the false-positive tail is real and owned, not hidden.

> Security-class findings (HTTP parsing / prototype-pollution) are **not** listed here — they go
> through each project's private disclosure channel, never a public issue.

## Status

Filed issues, live status via GitHub badges. `pending` = drafted, not yet filed.

<!--TABLE-->
_(populated as issues are filed)_

