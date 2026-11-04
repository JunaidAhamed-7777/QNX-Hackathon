# Faultline: five refinement passes
Date: 4 November 2026. These are five distinct design-review passes performed before the roadmap. None is a claim that software was built or benchmarked. Each records a question, criticism, resulting decision and evidence needed.

## Pass 1 — Is the problem valuable and the novelty credible?
**Question:** Why would a QNX developer use this instead of logs, Momentics or a watchdog?

**Criticism:** A dashboard showing a process crashing has little value beyond existing tools. A synthetic bug can also look contrived if no reusable output leaves the demo.

**Decision:** The product's unit of value is a **runnable reproducer and explicit failure contract**, not a chart. A user should receive a scenario, build identifiers, target configuration, evidence records and an exact replay command. The same scenario must run against a baseline and a corrected implementation.

**Primary persona:** A developer maintaining two or more native QNX services whose failure behavior depends on a sequence of delays, crashes or reconnects. Secondary persona: an educator teaching request/reply cancellation and restart semantics.

**Job to be done:** “I can occasionally observe a failure. Give me the smallest controlled sequence that demonstrates it, a clear statement of what was violated, and evidence that my change survives it.”

**Novelty boundary:** [HAM](https://www.qnx.com/developers/docs/8.0/com.qnx.doc.ham/topic/hamover.html) already monitors and recovers services; [Toolkit](https://qnx.com/developers/docs/8.0/com.qnx.doc.qnxtoolkit.user_guide/topic/managing_traces.html) already visualizes traces. Faultline tests such systems and packages actionable experiments. It does not claim to invent recovery or tracing.

**Outputs:** scenario schema, contract definitions, one concise product story, comparison matrix in the idea document.

**Validation:** Give an independent developer only the bundle and setup instructions. They must reproduce the named outcome and locate the evidence without the author narrating it. If that fails, the central proposition is not delivered.

## Pass 2 — Is QNX indispensable to the architecture?
**Question:** Could the same demo be a generic HTTP dashboard with QNX logos?

**Criticism:** The participant's web strengths could lead to overinvestment in UI before the native behavior exists.

**Decision:** Build a real QNX vertical slice first. Native C/C++ fixtures expose QNX message/pulse behavior. A Python host runner manages bounded experiments and produces reports; a React/TypeScript viewer is optional presentation. The CLI must remain independently usable.

**Mechanisms:**
- Request/reply IPC with source-defined request, session and sequence identifiers.
- Explicit SEND/REPLY blocking and timeout/cancellation cases using the documented [MsgSend](https://qnx.com/developers/docs/8.0/com.qnx.doc.neutrino.lib_ref/topic/m/msgsend.html) and [TimerTimeout](https://www.qnx.com/developers/docs/8.0/com.qnx.doc.neutrino.lib_ref/topic/t/timertimeout.html) semantics.
- A virtual sensor resource manager as a later workload adapter; [resource managers](https://qnx.com/developers/docs/8.0/com.qnx.doc.neutrino.user_guide/topic/os_intro_RESMGR.html) provide a genuinely QNX-native device-like interface.
- Kernel-trace correlation only after application-event evidence works and permissions are verified.

**Hero fixture:** A deliberately broken cancellation path contrasted with a corrected path. With an unblock-enabled channel, a timeout can notify the server, which must complete cancellation appropriately. Cover both relevant blocking states and arm a one-shot timeout immediately before the intended operation. Verify exact behavior on the installed QNX version instead of deriving code blindly from prose.

**Architecture change:** The sensor/cart story is a second fixture, not the foundational runtime. A three-process robot pipeline is not required to prove the first result.

**Validation:** Actual target compile/run logs, two-process IPC proof, bounded cleanup, and a repeatable baseline violation. No host-only simulation counts as passing this gate.

## Pass 3 — Can the evidence withstand skeptical review?
**Question:** What does “replayable,” “causal,” or “passes” really mean?

**Criticism:** Thread scheduling is nondeterministic, event delivery may be incomplete, and emulated timing is not hardware timing. A sequence minimizer can make false claims if it mistakes flaky absence for a pass.

**Decision:** Guarantee only **repeatable injection intent**, not identical scheduling. Store exact observed order, target timestamps and identifiers. State causal relationships only where the instrumentation establishes them; otherwise label correlations.

**Contract examples:**
1. Every test request reaches a terminal completion/error state, or the run is explicitly timed out.
2. Responses from an obsolete session are never accepted by the corrected test controller.
3. Recovery reaches a specified test state within the configured observed deadline, with “not established” if evidence is missing.

**Three outcomes:** PASS, FAIL and INCONCLUSIVE. Missing records, parser errors, target loss, incomplete cleanup or truncated traces must not become PASS.

**Sequence reduction:** Remove a fault event or group, rerun the scenario a declared number of times, retain a reduction only when the same violation reproduces at the declared threshold. Preserve original and reduced cases, every trial result and the chosen threshold. Call it “reduced reproducer,” not “globally minimal” unless that stronger property is actually established.

**Clock discipline:** Measure target-side assertions in a single target monotonic clock domain. Host transport delay does not belong in target timing. Record host load, guest resources, tracing state, sample counts and instrumentation overhead.

**Validation:** Corrupt an event stream, reorder duplicate records, kill a run mid-flight, drop the target connection and feed malformed scenarios. All must produce intelligible failure/inconclusive results, not attractive but false reports.

## Pass 4 — Does one project naturally tell a broad, memorable story?
**Question:** How can it reach multiple areas without diluting the central product?

**Criticism:** A portfolio of miniature domain demos can consume the schedule and still fail to prove a reusable tool.

**Decision:** Use one engine, one schema and one report pipeline. First workload: native IPC service. Optional second workload: a synthetic cart sensor/controller/actuator recorder. “Medical” remains a possible testing application, not a validated clinical feature.

**Demo structure, under three minutes:**
- 0:00–0:20: show the real QNX target and the developer's problem.
- 0:20–0:50: run the baseline scenario and show the named violated contract.
- 0:50–1:25: reduce a longer scenario to a compact reproducer; display actual trials, not a staged claim.
- 1:25–2:05: run the corrected fixture against the same sequence and contrast evidence.
- 2:05–2:35: show the reusable adapter or second workload, if complete.
- 2:35–2:55: open the bundle, replay command, source and tutorial.

This is a proposed storyboard, not recorded evidence. The finished demonstration must be uploaded to YouTube and publicly visible, with its URL in the submission. [Video requirements](https://qnx.devpost.com/rules).

**Category decision:** Developer Tooling & Host Tools remains primary. Native IPC behavior provides technical depth but does not satisfy the named Low-level Software category's board-support/DDK-driver definition. The synthetic domain scenario explains impact, not automatic robotics or mobility category eligibility. Open-source availability is useful but does not substitute for a qualifying port. The rules permit one Overall prize and one Bonus, not simultaneous category sweeps.

**Tutorial decision:** Build a self-contained “QNX cancellation failure to reproducible regression test” codelab, with expected output, troubleshooting and an explanation of what QEMU does not prove. The tutorial must teach something even to a reader who never uses the UI.

**Validation:** A viewer can explain the problem, QNX-specific mechanism and practical output after watching once. Remove any screen that requires a long verbal explanation or hides the raw evidence.

## Pass 5 — Can this be finished honestly within the window?
**Question:** What could invalidate the plan, and what gets cut first?

**Criticism:** License/host setup can consume the project. A polished UI can conceal a missing runtime. Tracing and minimization are more difficult than their names suggest.

**Decision:** Use explicit gates and timeboxes. Gate 0 is actual licensed QNX execution on a permitted cloud arrangement. The observed cloud host did not have the needed tools or exposed KVM, and differs from the documented Ubuntu route. Do not call feasibility proven.

**MVP:**
- One native IPC fixture, baseline and corrected versions.
- Three bounded fault actions: receive/reply delay, owned-process termination, and controlled stale/test response behavior as applicable.
- A small versioned scenario schema and three explicit contracts.
- CLI execution, JSON evidence and readable HTML report.
- Bounded sequence reduction with recorded repeatability.
- Reproducible build/run instructions and one codelab.

**Stretch order:** second workload → standalone reproducer bundle → supported kernel-trace correlation → HAM adapter. Only add the next item after MVP acceptance.

**Cut:** complete ROS stack, physical hardware dependency, autonomous driving, medical operation, custom kernel logger, LLM control loop, automatic code repair, complex 3D environment and claims of certification.

**Stop/pivot conditions:** no authorized cloud execution route; no reliable baseline bug; no useful reproducer beyond existing tools; or a core test that repeatedly produces misleading outcomes. Report the constraint and choose a smaller demonstrably QNX-supporting host tool if appropriate. Do not fake target execution.

**Deliverable:** [Roadmap](06-roadmap.md) with a conservative freeze before the official deadline, ownership of unresolved gates and testable exit criteria.

## Final project definition
**Faultline is a QNX-native failure-contract workbench that turns a controlled service failure into a reduced runnable reproducer and before/after evidence.** Its broad relevance comes from reusable native-service and sensor-pipeline adapters. Its novelty is a testable product hypothesis; its success depends on real QNX behavior, useful evidence and disciplined scope.
