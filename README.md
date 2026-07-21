# qa-tools-oss-bug-hunt

A list of correctness & robustness bugs I found in widely-used QA / testing tools with an
AI-assisted property-based & differential testing setup, part of a broader effort to scale
property-based testing ([DepTyCheck](https://github.com/buzden/deptycheck)) across the OSS ecosystem.

Every bug below has a minimal, runnable reproducer, verified by executing the real tool against a
reference oracle. If something turns out not to be a real bug, sorry — just close it; I read every
issue and follow up.

## Stats (GitHub-verified, 2026-07-21)

| Metric | Value |
|---|---|
| Issues filed | **39** across **16** projects (≤3 per project, paced) |
| Method | property-based & differential bug-cousin hunting, runtime-verified |
| Confirmed set | 107 candidates → **79** survived a full runtime + cross-vendor + dedup gate (~21% cut as FP/by-design) |
| Filed so far | 39 public issues (remaining public paced over following days) |
| Security-class | reported **privately** per each project's disclosure policy — **not** listed here |

> **Self-audit.** Every filing was re-verified in a clean context before publishing: the repro was
> re-executed at runtime, and two independent skeptic models (a Claude reviewer + an OpenAI reviewer
> via cross-vendor quorum) had to agree it is a real defect, not by-design/known/spurious. An
> aggressive first pass surfaced 107 candidates; the gate cut ~23 (already-fixed-upstream,
> documented-contract, not-reachable-from-user-code, by-design, sibling-shares-pattern). The
> false-positive tail is real and owned — if a maintainer marks one intended, it gets closed with an
> apology, not defended.

## Issues filed

### [SeleniumHQ/selenium](https://github.com/SeleniumHQ/selenium)

- ![status](https://img.shields.io/github/issues/detail/state/SeleniumHQ/selenium/17805) [#17805](https://github.com/SeleniumHQ/selenium/issues/17805) — [🐛 Bug]: By.className()/By.id() escape a leading non-ASCII Unicode digit to the wrong ASCII code point, colliding with a different class name
- ![status](https://img.shields.io/github/issues/detail/state/SeleniumHQ/selenium/17807) [#17807](https://github.com/SeleniumHQ/selenium/issues/17807) — [🐛 Bug]: By.name() runs String.format twice; a '%' in the name throws or corrupts the CSS fallback selector

### [ajv-validator/ajv](https://github.com/ajv-validator/ajv)

- ![status](https://img.shields.io/github/issues/detail/state/ajv-validator/ajv/2650) [#2650](https://github.com/ajv-validator/ajv/issues/2650) — discriminator rejects schemas whose tag values are Object.prototype member names (toString, constructor, ...)
- ![status](https://img.shields.io/github/issues/detail/state/ajv-validator/ajv/2651) [#2651](https://github.com/ajv-validator/ajv/issues/2651) — JTD compileParser rejects valid JSON encodings of enum values (raw byte compare against the JSON.stringify form)

### [allure-framework/allure2](https://github.com/allure-framework/allure2)

- ![status](https://img.shields.io/github/issues/detail/state/allure-framework/allure2/3426) [#3426](https://github.com/allure-framework/allure2/issues/3426) — JUnit XML reader drops all testcases inside nested <testsuite> elements
- ![status](https://img.shields.io/github/issues/detail/state/allure-framework/allure2/3427) [#3427](https://github.com/allure-framework/allure2/issues/3427) — JUnit XML reader ignores Surefire <flakyFailure>/<flakyError>: test not marked flaky, retry attempts dropped
- ![status](https://img.shields.io/github/issues/detail/state/allure-framework/allure2/3428) [#3428](https://github.com/allure-framework/allure2/issues/3428) — xUnit.net XML reader drops the skip <reason>: skipped tests show no status message

### [appium/appium](https://github.com/appium/appium)

- ![status](https://img.shields.io/github/issues/detail/state/appium/appium/22523) [#22523](https://github.com/appium/appium/issues/22523) — 🐞 bug: Virtual Sensor per-type endpoints registered at /sensors/ (plural), unreachable at the spec path /sensor/{type}
- ![status](https://img.shields.io/github/issues/detail/state/appium/appium/22526) [#22526](https://github.com/appium/appium/issues/22526) — 🐞 bug: W3C 'timeout' / 'script timeout' errors return HTTP 408 instead of the spec-mandated 500

### [cypress-io/cypress](https://github.com/cypress-io/cypress)

- ![status](https://img.shields.io/github/issues/detail/state/cypress-io/cypress/34303) [#34303](https://github.com/cypress-io/cypress/issues/34303) — cy.contains(regex) with a global/sticky (g/y) flag matches only a subset of elements: lastIndex leaks across elements in the cy-contains-regex pseudo
- ![status](https://img.shields.io/github/issues/detail/state/cypress-io/cypress/34304) [#34304](https://github.com/cypress-io/cypress/issues/34304) — cy.selectFile() on a <label>: getInputFromLabel builds a #id selector from the label's for attribute without CSS.escape, so valid ids containing CSS-special characters fail or throw
- ![status](https://img.shields.io/github/issues/detail/state/cypress-io/cypress/34305) [#34305](https://github.com/cypress-io/cypress/issues/34305) — cy.contains(text) cannot find input[type=submit] by partial value: submit inputs go through whole-word CSS [value~=] while every other element gets a substring match

### [dop251/goja](https://github.com/dop251/goja)

- ![status](https://img.shields.io/github/issues/detail/state/dop251/goja/717) [#717](https://github.com/dop251/goja/issues/717) — TypedArray.prototype.toSorted ignores the view's byteOffset, so subarray().toSorted() sorts the wrong elements
- ![status](https://img.shields.io/github/issues/detail/state/dop251/goja/718) [#718](https://github.com/dop251/goja/issues/718) — String.prototype.split('') splits by Unicode code points instead of UTF-16 code units
- ![status](https://img.shields.io/github/issues/detail/state/dop251/goja/719) [#719](https://github.com/dop251/goja/issues/719) — TypedArray.prototype.filter writes result elements at the wrong offset when Symbol.species returns a non-zero-offset view

### [gatling/gatling](https://github.com/gatling/gatling)

- ![status](https://img.shields.io/github/issues/detail/state/gatling/gatling/4701) [#4701](https://github.com/gatling/gatling/issues/4701) — EL: #{randomUuid()} sets the UUID version nibble to 0 instead of 4 (Version4Mask is 2L << 62, should be 4L << 12)
- ![status](https://img.shields.io/github/issues/detail/state/gatling/gatling/4702) [#4702](https://github.com/gatling/gatling/issues/4702) — substring(pattern).find(n) with n >= 1 always returns not-found: the loop guard tests pattern.length instead of text.length
- ![status](https://img.shields.io/github/issues/detail/state/gatling/gatling/4703) [#4703](https://github.com/gatling/gatling/issues/4703) — EL: negative index with magnitude > length throws uncaught IndexOutOfBoundsException on Array / java.util.List / tuple (Seq returns a clean Failure)

### [grafana/k6](https://github.com/grafana/k6)

- ![status](https://img.shields.io/github/issues/detail/state/grafana/k6/6181) [#6181](https://github.com/grafana/k6/issues/6181) — GaugeSink reports max = 0 when all gauge samples are negative (missing maxSet guard in metrics/sink.go)

### [json-path/JsonPath](https://github.com/json-path/JsonPath)

- ![status](https://img.shields.io/github/issues/detail/state/json-path/JsonPath/1076) [#1076](https://github.com/json-path/JsonPath/issues/1076) — Array slice [from:to] with a negative from wraps around and returns duplicate elements
- ![status](https://img.shields.io/github/issues/detail/state/json-path/JsonPath/1077) [#1077](https://github.com/json-path/JsonPath/issues/1077) — Negative array index on set/delete/map throws a raw IndexOutOfBoundsException while read supports it
- ![status](https://img.shields.io/github/issues/detail/state/json-path/JsonPath/1078) [#1078](https://github.com/json-path/JsonPath/issues/1078) — Single-quoted string arguments to path functions are dropped or corrupted; only double quotes work

### [karatelabs/karate](https://github.com/karatelabs/karate)

- ![status](https://img.shields.io/github/issues/detail/state/karatelabs/karate/2974) [#2974](https://github.com/karatelabs/karate/issues/2974) — Numeric match == compares via double, so distinct integers above 2^53 match as equal
- ![status](https://img.shields.io/github/issues/detail/state/karatelabs/karate/2975) [#2975](https://github.com/karatelabs/karate/issues/2975) — match ... contains only deep ignores element multiplicity, producing a false-positive match on differing multisets
- ![status](https://img.shields.io/github/issues/detail/state/karatelabs/karate/2976) [#2976](https://github.com/karatelabs/karate/issues/2976) — #(!^part) schema macro false-passes on a list of objects (NOT_CONTAINS omitted from partial-match branch)

### [locustio/locust](https://github.com/locustio/locust)

- ![status](https://img.shields.io/github/issues/detail/state/locustio/locust/3472) [#3472](https://github.com/locustio/locust/issues/3472) — get_response_time_percentile counts None (async) requests in the denominator, deflating all reported percentiles

### [microsoft/playwright](https://github.com/microsoft/playwright)

- ![status](https://img.shields.io/github/issues/detail/state/microsoft/playwright/41891) [#41891](https://github.com/microsoft/playwright/issues/41891) — [Bug]: <meter>/<progress> ignore associated <label> in accessible name; getByRole({ name }) and toHaveAccessibleName fail
- ![status](https://img.shields.io/github/issues/detail/state/microsoft/playwright/41899) [#41899](https://github.com/microsoft/playwright/issues/41899) — [Bug]: getByRole treats input[type=search] with a broken/non-datalist list attribute as combobox; Chrome computes searchbox

### [rest-assured/rest-assured](https://github.com/rest-assured/rest-assured)

- ![status](https://img.shields.io/github/issues/detail/state/rest-assured/rest-assured/1874) [#1874](https://github.com/rest-assured/rest-assured/issues/1874) — JsonPath: large negative JSON numbers overflow to -Infinity (sign-blind float/double selection)
- ![status](https://img.shields.io/github/issues/detail/state/rest-assured/rest-assured/1875) [#1875](https://github.com/rest-assured/rest-assured/issues/1875) — JsonPath: array.properties GPath spread returns null (drops all data) when the first array element lacks a properties key (Groovy 5 regression)
- ![status](https://img.shields.io/github/issues/detail/state/rest-assured/rest-assured/1876) [#1876](https://github.com/rest-assured/rest-assured/issues/1876) — XmlPath: a negative list index on a hyphenated element name throws a misleading parameter "..." was used but not defined error

### [robotframework/robotframework](https://github.com/robotframework/robotframework)

- ![status](https://img.shields.io/github/issues/detail/state/robotframework/robotframework/5722) [#5722](https://github.com/robotframework/robotframework/issues/5722) — Var.from_params drops an empty value_separator, which Variable.from_params preserves
- ![status](https://img.shields.io/github/issues/detail/state/robotframework/robotframework/5723) [#5723](https://github.com/robotframework/robotframework/issues/5723) — SectionHeader.from_params(Token.INVALID_HEADER) raises KeyError because zip truncates 7 registered types against 6 default names

### [usebruno/bruno](https://github.com/usebruno/bruno)

- ![status](https://img.shields.io/github/issues/detail/state/usebruno/bruno/8691) [#8691](https://github.com/usebruno/bruno/issues/8691) — jsonToBru produces unparseable output when a value contains a newline plus '''
- ![status](https://img.shields.io/github/issues/detail/state/usebruno/bruno/8695) [#8695](https://github.com/usebruno/bruno/issues/8695) — auth:ntlm parsing throws TypeError when the domain line is absent
- ![status](https://img.shields.io/github/issues/detail/state/usebruno/bruno/8696) [#8696](https://github.com/usebruno/bruno/issues/8696) — A key starting with ~ is serialized bare and re-parses as a disabled entry with the ~ stripped

### [wiremock/wiremock](https://github.com/wiremock/wiremock)

- ![status](https://img.shields.io/github/issues/detail/state/wiremock/wiremock/3508) [#3508](https://github.com/wiremock/wiremock/issues/3508) — equalToXml with namespaceAwareness=NONE returns a false no-match (swallowed NullPointerException) for any document with 2+ sibling elements, even against itself
- ![status](https://img.shields.io/github/issues/detail/state/wiremock/wiremock/3509) [#3509](https://github.com/wiremock/wiremock/issues/3509) — Multipart aMultipart().withName(...).withFileName(...) silently drops the name constraint: both write the same Content-Disposition map key, so the second overwrites the first
- ![status](https://img.shields.io/github/issues/detail/state/wiremock/wiremock/3510) [#3510](https://github.com/wiremock/wiremock/issues/3510) — matchesXPath with a boolean-valued expression matches even when the boolean is FALSE, so any XML body matches count(//x)=99, 1 = 2, or contains('abc','z')

## Not listed here

- **Security-class findings** (HTTP request/response parsing desync, prototype-pollution) go through
  each project's private disclosure channel — GitHub private advisory / security email — never a
  public issue.
- **Remaining public findings** are drafted and paced over the following days (≤3 per project) to
  avoid burst-filing.
