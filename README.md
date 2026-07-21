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

## Status — 16 filed (2026-07-21)

Filed issues, live status via GitHub badges. `pending` = drafted, not yet filed.

| Tool | Issue | Status |
|---|---|---|
| `selenium` | [#17805](https://github.com/SeleniumHQ/selenium/issues/17805) — [🐛 Bug]: By.className()/By.id() escape a leading non-ASCII Unicode digit to the wrong A... | ![](https://img.shields.io/github/issues/detail/state/SeleniumHQ/selenium/17805) |
| `ajv` | [#2650](https://github.com/ajv-validator/ajv/issues/2650) — discriminator rejects schemas whose tag values are Object.prototype member names (toStr... | ![](https://img.shields.io/github/issues/detail/state/ajv-validator/ajv/2650) |
| `allure2` | [#3426](https://github.com/allure-framework/allure2/issues/3426) — JUnit XML reader drops all testcases inside nested <testsuite> elements | ![](https://img.shields.io/github/issues/detail/state/allure-framework/allure2/3426) |
| `appium` | [#22523](https://github.com/appium/appium/issues/22523) — 🐞 bug: Virtual Sensor per-type endpoints registered at /sensors/ (plural), unreachable ... | ![](https://img.shields.io/github/issues/detail/state/appium/appium/22523) |
| `cypress` | [#34303](https://github.com/cypress-io/cypress/issues/34303) — cy.contains(regex) with a global/sticky (g/y) flag matches only a subset of elements: l... | ![](https://img.shields.io/github/issues/detail/state/cypress-io/cypress/34303) |
| `goja` | [#717](https://github.com/dop251/goja/issues/717) — TypedArray.prototype.toSorted ignores the view's byteOffset, so subarray().toSorted() s... | ![](https://img.shields.io/github/issues/detail/state/dop251/goja/717) |
| `gatling` | [#4701](https://github.com/gatling/gatling/issues/4701) — EL: #{randomUuid()} sets the UUID version nibble to 0 instead of 4 (Version4Mask is 2L ... | ![](https://img.shields.io/github/issues/detail/state/gatling/gatling/4701) |
| `k6` | [#6181](https://github.com/grafana/k6/issues/6181) — GaugeSink reports max = 0 when all gauge samples are negative (missing maxSet guard in ... | ![](https://img.shields.io/github/issues/detail/state/grafana/k6/6181) |
| `JsonPath` | [#1076](https://github.com/json-path/JsonPath/issues/1076) — Array slice [from:to] with a negative from wraps around and returns duplicate elements | ![](https://img.shields.io/github/issues/detail/state/json-path/JsonPath/1076) |
| `karate` | [#2974](https://github.com/karatelabs/karate/issues/2974) — Numeric match == compares via double, so distinct integers above 2^53 match as equal | ![](https://img.shields.io/github/issues/detail/state/karatelabs/karate/2974) |
| `locust` | [#3472](https://github.com/locustio/locust/issues/3472) — get_response_time_percentile counts None (async) requests in the denominator, deflating... | ![](https://img.shields.io/github/issues/detail/state/locustio/locust/3472) |
| `playwright` | [#41891](https://github.com/microsoft/playwright/issues/41891) — [Bug]: <meter>/<progress> ignore associated <label> in accessible name; getByRole({ nam... | ![](https://img.shields.io/github/issues/detail/state/microsoft/playwright/41891) |
| `rest-assured` | [#1874](https://github.com/rest-assured/rest-assured/issues/1874) — JsonPath: large negative JSON numbers overflow to -Infinity (sign-blind float/double se... | ![](https://img.shields.io/github/issues/detail/state/rest-assured/rest-assured/1874) |
| `robotframework` | [#5722](https://github.com/robotframework/robotframework/issues/5722) — Var.from_params drops an empty value_separator, which Variable.from_params preserves | ![](https://img.shields.io/github/issues/detail/state/robotframework/robotframework/5722) |
| `bruno` | [#8691](https://github.com/usebruno/bruno/issues/8691) — jsonToBru produces unparseable output when a value contains a newline plus ''' | ![](https://img.shields.io/github/issues/detail/state/usebruno/bruno/8691) |
| `wiremock` | [#3508](https://github.com/wiremock/wiremock/issues/3508) — equalToXml with namespaceAwareness=NONE returns a false no-match (swallowed NullPointer... | ![](https://img.shields.io/github/issues/detail/state/wiremock/wiremock/3508) |

