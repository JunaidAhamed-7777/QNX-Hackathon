# Three candidate-generation and selection passes
Research date: 4 November 2026. The goal is one novel, useful project with natural breadth, not unrelated features glued together. These passes are analytical comparisons, not experiments or market-validation results.

## Pass 1: eight materially different concepts
| Idea | Core proposition | Natural applicability | Best primary category | Decisive risk |
| --- | --- | --- | --- | --- |
| **Faultline** | Turn a failure sequence into an executable contract, minimized reproducer and before/after evidence | Host tools, native services, simulated robotics and mobility | Developer Tooling & Host Tools | Becoming a thin profiler dashboard |
| **LeaseLine** | A command-lease/session protocol rejects commands left over after service restart | Robot controllers, mobility, medical-equipment simulation, IPC | Developer Tooling & Host Tools, if delivered as a reusable test/validation tool | Protocol correctness and recovery corner cases |
| **Boundary** | A native execution boundary rejects stale or invalid commands from an unreliable planner | Robotics and mobility, process isolation, security | Robotics & Medical or Automotive & Mobility | Familiar safety-supervisor pitch; excessive autonomy scope |
| **PortPassport** | Executable Linux-to-QNX compatibility evidence plus one useful real port | OSS ports, build tooling, native libraries | Open-Source Contribution & Ports | Choosing a worthwhile unported library and proving usefulness |
| **Virtual I/O Forge** | Faultable virtual devices built as QNX resource managers | Device testing, robots, mobility, simulated medical interfaces | Developer Tooling & Host Tools | An isolated device simulator may lack a strong story |
| **Priority Lens** | Explain observed scheduling/IPC deadline failures with source-linked evidence | Low-level performance, native services, host debugging | Developer Tooling & Host Tools | Duplicating Momentics and overstating causality |
| **Capability Rehearsal** | Test least-privilege service policies and explain denied operations | Native security, developer education, host tools | Developer Tooling & Host Tools, if delivered as a reusable test/validation tool | Privilege complexity and existing policy generators |
| **Alarm Commons** | Reproducible arbitration of competing simulated alarms under overloaded services | Medical simulation, robots, low-level scheduling | Robotics & Medical | Weak domain validation and safety claims |

Category assessments above are conditional on the finished implementation. The official **Low-level Software** category means board-support components or QNX DDK device drivers, not generic IPC, protocols or security. LeaseLine's proposed tooling fit requires a reusable validation product, not only a protocol library. Domain simulations alone do not establish Robotics & Medical or Automotive & Mobility eligibility. [Category definitions](https://qnx.devpost.com/rules).

### Breadth test
A strong broad idea shares a mechanism across applications. Faultline's failure-contract engine could test either a native server or a synthetic sensor pipeline. A separate robot game, medical dashboard and vehicle simulator would not be genuine breadth.

### Initial shortlist
Faultline, LeaseLine, PortPassport and Boundary survive. Virtual I/O Forge is useful as an adapter inside Faultline. Priority Lens becomes optional supporting visualization. Capability Rehearsal and Alarm Commons remain alternatives if later evidence changes the decision.

## Pass 2: prior art and adversarial screening
### What is already solved
- [QNX HAM](https://www.qnx.com/developers/docs/8.0/com.qnx.doc.ham/topic/hamover.html) already provides monitoring and staged recovery. A restart daemon is not the new contribution.
- [Momentics](https://www.qnx.com/products/neutrino-rtos/qnx-momentics.html) and [Toolkit trace views](https://qnx.com/developers/docs/8.0/com.qnx.doc.qnxtoolkit.user_guide/topic/managing_traces.html) already provide kernel-event profiling, timelines, CPU and event views.
- [Toolkit commands](https://qnx.com/developers/docs/8.0/com.qnx.doc.qnxtoolkit.user_guide/topic/qnx_toolkit_contribution_points.html) include export and custom-event handling. JSON/CSV export alone is not novelty.
- QNX already publishes a [Linux porting guide](https://qnx.com/developers/docs/qnxeverywhere/com.qnx.doc.qpg/topic/about.html).
- QNX already supports a [robotics ecosystem](https://qnx.software/en/industries/robotics); merely placing a robot simulation on QNX is insufficient differentiation.
- [Security-policy tooling](https://www.qnx.com/developers/docs/8.0/com.qnx.doc.security.system/topic/manual/using_security_policies.html) already helps generate policies from observed behavior.

This is targeted prior-art research, not an exhaustive patent or competitive search. “First ever” is not established.

### Qualitative comparison
| Criterion | Faultline | LeaseLine | PortPassport | Boundary |
| --- | --- | --- | --- | --- |
| Distinctive demo | Strong if a failure is minimized and replayed | Strong if stale commands are demonstrably rejected | Depends heavily on selected port | Visually strong but familiar |
| Fit for software-only/cloud work | Strong, subject to QNX runtime gate | Strong, same gate | Strong, toolchain and dependency gates | Moderate; full robotics stack is avoidable |
| QNX-specific depth | IPC, pulses, timeouts, resource managers | IPC and restart/session behavior | ABI/build/platform adaptation | Isolation and messaging |
| Correctness burden | Bounded experiments and honest evidence | High state-machine burden | Varies by port | High if called a safety system |
| Natural breadth | Same engine, multiple workloads | Same protocol, multiple controllers | Same framework, multiple ports | Mostly controller applications |
| Solo delivery risk | Medium | High | Medium | High |
| Decision | **Select** | Keep as later experiment | Strong fallback | Reject for initial scope |

These judgments are planning assessments, not externally measured scores.

### Why not merge every idea?
Faultline can host a virtual device and later test a command-lease protocol without needing to deliver a universal porting assistant or security-policy engine. Preserve a narrow product: **make one failure reproducible, understandable and testable**.

## Pass 3: sharpen the selected project
**Working name: Faultline.** Repository name remains QNX-Hackathon until renamed by the owner.

### User and outcome
A developer has a service failure that appears after a particular delay, restart or stale reply. Ordinary logs show symptoms but do not supply a compact test. Faultline gives that developer:
1. An executable failure scenario.
2. Explicit contracts with observed evidence.
3. A reduced event sequence that still reproduces the violation.
4. A comparison against the corrected implementation.
5. A shareable bundle another developer can rerun.

### Defensible novelty hypothesis
The contribution is the **combination of QNX-native failure contracts, controlled scenario replay, sequence reduction and before/after evidence** in one usable workflow. The new code must implement these capabilities, not just wrap an existing profiler. Novelty remains a hypothesis until further competitor review and working validation.

### Strongest hero demonstrations
- **Native IPC cancellation:** a timeout does not release a client because the receiving server mishandles unblock/cancellation behavior. Ground the test in [TimerTimeout semantics](https://www.qnx.com/developers/docs/8.0/com.qnx.doc.neutrino.lib_ref/topic/t/timertimeout.html).
- **Stale-session control:** sensor restart followed by a delayed stale response causes a naive controller to use obsolete data. A session-aware version rejects it. This is a deliberately constructed test fixture, not an accusation against QNX.

Select one hero after real target experiments. Start with the smaller native IPC fixture; add the synthetic cart/sensor narrative only if it clarifies the same engine.

### Prize-category breadth
- Primary: **Developer Tooling & Host Tools**.
- Technical depth: native QNX IPC/state semantics. This is **not** a claim of eligibility for the named Low-level Software award, which requires board-support or DDK driver work.
- Demonstration connection: **Robotics & Medical** and **Automotive & Mobility**, using a synthetic sensor/controller workload, without clinical or vehicle-safety claims. These examples show applicability, not automatic eligibility for either named category.
- Reusability: public original source and a clean adapter interface may help the OSS community, but no port award is claimed without a substantive qualifying port.
- Bonus evidence: a runnable codelab and meaningful QNX-specific behavior.

This breadth is usefulness and judging relevance, not a claim that the entry can collect all category prizes.

## Rejected positioning
Do not say “a new watchdog,” “a universal debugger,” “certified safety,” “deterministic replay of any thread schedule,” “autonomous code repair,” or “guaranteed winner.” Say exactly which controlled scenarios run, which assertions are checked, and where evidence is incomplete.

## Final selection
Proceed with Faultline planning, with **QNX execution and licensing as Gate 0**. If that gate cannot be passed on an authorized cloud setup, retain the host-side planning artifacts and reconsider a demonstrably QNX-supporting host tool. Do not silently replace QNX execution with a fake target.
