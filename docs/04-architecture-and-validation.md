# Faultline architecture and validation plan
Planning only; no implementation or QNX runtime test is claimed.

## Components
| Component | Responsibility | Deliberate boundary |
| --- | --- | --- |
| Host CLI | Validate scenario, start bounded run, collect artifacts, report outcome | No dependency on UI or internet during replay |
| Target agent | Launch and supervise only owned test fixtures, apply allowed fault actions | No arbitrary process killing or production fault injection |
| Native fixtures | Known baseline/corrected QNX IPC behavior | Intentionally constructed bugs, clearly labeled |
| Event recorder | Correlate request/session/action IDs and target monotonic times | Explicit gaps and schema versions |
| Contract evaluator | Compute PASS/FAIL/INCONCLUSIVE from evidence | Never infer success from absent logs |
| Reducer | Remove actions and rerun with repeatability policy | Bounded trials; no global-minimality claim |
| Evidence bundle | Preserve manifests, scenarios, observations, outcomes and replay instructions | Exclude credentials, proprietary SDK/images |
| Host viewer | Explain results, comparisons and trial history | UI is presentation, not source of truth |

## Proposed repository layout
```
docs/                 # Research, decisions, setup, tutorial and roadmap
host/                 # Python CLI, schemas, evaluator, reducer, report generation
target/               # Original QNX C/C++ agent and IPC fixtures
scenarios/            # Versioned named experiment descriptions
viewer/               # Optional React/TypeScript evidence viewer
tests/                # Host tests, fixtures and QNX integration scripts
examples/             # Baseline/corrected native service; later sensor pipeline
```
This is a future layout proposal. Only documentation exists at this planning stage.

## Experiment lifecycle
1. Validate schema and permit only a documented set of test actions.
2. Check target identity/version and fixture build revision.
3. Allocate an isolated run ID and run-owned process set.
4. Start fixture processes, establish readiness and capture configuration.
5. Execute scenario actions with recorded intended and observed times.
6. Collect target events; detect dropped or incomplete evidence.
7. Evaluate contracts; run cleanup even after failure.
8. Write immutable artifacts and a report.
9. If reduction is requested, preserve the original and run bounded candidate reductions.
10. Compare the same scenario against the corrected fixture.

Only processes created for that run are eligible for deliberate termination. Cleanup uses process identity and run ownership, not an unverified reusable PID alone.

## Scenario model
A scenario needs:
- schema version, name, description and fixture version;
- target/platform requirements;
- seed, where randomness is used;
- readiness preconditions;
- ordered fault actions and explicit trigger conditions;
- request/session identifiers;
- contract definitions;
- overall timeout and cleanup policy;
- repeat count and reproduction threshold.

Prefer event-triggered actions (“after request accepted”) over guessed sleeps where possible. A recorded seed controls generator choices, not kernel scheduling.

## Evidence model
Each run should contain a manifest, original scenario, target events, process exit states, evaluation results, tool versions and replay instructions. Include code revision, QNX version, toolchain version, guest resources, clock assumptions and whether kernel tracing was enabled.

The viewer must show:
- original versus reduced sequence;
- all reducer trials and outcomes;
- expected versus observed contract state;
- source-defined event and session identifiers;
- missing or untrusted evidence warnings;
- baseline versus corrected results;
- provenance and limitations.

Keep immutable raw records separate from generated summaries. Treat imported reports as untrusted data; do not execute embedded commands or render unescaped HTML.

## QNX-specific implementation notes
[MsgSend](https://qnx.com/developers/docs/8.0/com.qnx.doc.neutrino.lib_ref/topic/m/msgsend.html) and [TimerTimeout](https://www.qnx.com/developers/docs/8.0/com.qnx.doc.neutrino.lib_ref/topic/t/timertimeout.html) support the first experiment. Verify both SEND and REPLY blocking cases. TimerTimeout is one-shot, and intervening kernel operations matter. An unblock-enabled receiving server must implement cancellation correctly.

A [resource-manager adapter](https://qnx.com/developers/docs/8.0/com.qnx.doc.neutrino.user_guide/topic/os_intro_RESMGR.html) may later expose a synthetic sensor through ordinary file operations. It is optional until the core fixture is reliable.

[tracelogger](https://qnx.com/developers/docs/8.0/com.qnx.doc.neutrino.utilities/topic/t/tracelogger.html) needs appropriate privileges and an instrumented kernel. Use supported parsing/export via [traceparser](https://www.qnx.com/developers/docs/8.0/com.qnx.doc.neutrino.lib_ref/topic/t/traceparser.html) or official tooling. Do not reverse-engineer a proprietary trace format unnecessarily. Application-event evidence must remain sufficient for the MVP.

## Test layers
| Layer | Tests | Required evidence |
| --- | --- | --- |
| Host unit | Schema validation, evaluators, reducer bookkeeping, escaping | Automated results |
| Host fault handling | Missing/truncated/corrupt events, duplicate IDs, disconnected target | INCONCLUSIVE or explicit error, never false PASS |
| QNX integration | Real request/reply, timeout states, owned-process crash/cleanup | Target logs and process outcomes |
| Baseline regression | Known failure against naive fixture | Named contract violation across declared trials |
| Corrected regression | Same scenario against corrected fixture | Observed passing trials, no broad guarantee |
| Reducer validation | Seeded longer scenario with removable actions | Original/reduced cases and all trials |
| Reproducibility | Clean setup by independent reviewer | Exact commands, versions and outputs |
| Presentation | Under-three-minute demo and codelab | Working links and actual target proof |

## Benchmarks and claims
Measure runtime, bundle size, number of reduction trials and observed target latency distributions only after instrumentation exists. Publish sample counts and environment. Do not invent target improvement percentages in advance.

QEMU can validate functional state transitions and reproducible experiment procedure. It cannot establish physical worst-case execution times or clinical/vehicle safety. Use “observed in this configuration,” not “guaranteed under all conditions.”

## Security and distribution
No production targets, real medical devices or vehicles. Bind any local dashboard conservatively, authenticate a remote target connection when applicable, and do not expose control endpoints publicly. Avoid security-setting changes without required permission.

Publish only original source and appropriately licensed dependencies. Never commit QNX SDKs, license files, activation links, credentials, target images or private logs unless rights and redaction are separately verified.
