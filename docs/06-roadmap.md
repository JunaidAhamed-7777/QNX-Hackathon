# Faultline build roadmap
Planning baseline: 4 November 2026. **No implementation is claimed complete.**

Submission deadline: **16 December 2026, 00:30 IST** ([official rules](https://qnx.devpost.com/rules)). Target an internal submission-ready freeze on **12 December**, leaving several days for defects and upload problems. Dates below are planning targets, not commitments made to an organizer or proof of feasibility.

## Delivery principle
Finish a convincing vertical slice before widening scope. A strong one-workload tool with a real reproducer is better than an incomplete collection of domain demos. All execution stays on an authorized cloud arrangement; no user's laptop is assumed available.

## Phase 0 — License, environment and proof of execution
**Target:** first 2–3 working days after setup approvals, preferably November 4–7.

Tasks:
- Review issued noncommercial SDK license and obtain required consent.
- Confirm the selected cloud runtime/image use is permitted.
- Establish a documented supported host route and sufficient resources.
- Install only authorized official dependencies.
- Boot a headless QNX 8 target.
- Cross-compile/run hello-world, then a two-process request/reply example.
- Retrieve logs and record exact toolchain/guest versions.

**Exit gate:** repeatable commands and actual QNX output from this cloud workflow, with no secrets or proprietary artifacts committed.

**If blocked:** do not spend days polishing UI. Continue schemas, documentation and host unit tests while resolving the gate. If no permitted practical target route exists, explicitly reassess a host tool with genuine QNX evidence. Do not substitute a simulated target and imply native validation.

## Phase 1 — One honest failure and one correct fix
**Target:** November 8–12, contingent on Phase 0.

Tasks:
- Implement a tiny native IPC fixture with clearly labeled naive and corrected modes.
- Reproduce a cancellation/unblock scenario based on installed-version semantics.
- Record request, session and event identifiers in a single target clock domain.
- Bound every run and ensure cleanup of owned processes.
- Define terminal-outcome and cancellation contracts.
- Run repeated baseline/corrected trials and preserve outputs.

**Exit gate:** the baseline violates a named contract; the corrected version passes the same controlled scenario in declared trials; hung/partial runs are INCONCLUSIVE or explicit failures.

**Cut rule:** if this fixture is not reliable, simplify before adding the cart pipeline, resource manager or tracing.

## Phase 2 — Reusable scenario engine and evidence bundle
**Target:** November 13–18.

Tasks:
- Implement versioned scenario validation and a documented action allowlist.
- Add bounded receive/reply delay and owned-process termination cases.
- Produce manifest, raw events, contract results and readable static report.
- Make CLI runs independent of a browser.
- Add corrupt/missing/duplicate/out-of-order event tests.
- Separate generator seed from scheduler nondeterminism.
- Document exact replay commands and target requirements.

**Exit gate:** a fresh run produces complete machine-readable evidence; a partial run cannot produce false PASS; reports can be read offline.

## Phase 3 — The differentiator: reduced reproducible failures
**Target:** November 19–24.

Tasks:
- Implement a simple bounded event-removal reducer.
- Preserve original scenario, reduction candidates, repeats and outcomes.
- Require the same violation to reproduce before accepting a reduction.
- Display original/reduced sequences and reproducibility statistics.
- Export a source-linked runnable bundle.
- Compare baseline and corrected builds under the same retained scenario.

**Exit gate:** at least one longer deliberately constructed failure sequence is reduced without losing its recorded violation. Trial logs demonstrate the reduction; there is no unsupported “globally minimal” claim.

**Fallback:** if arbitrary reduction is too flaky, support a documented bounded scenario family rather than pretending universality.

## Phase 4 — Product clarity and natural breadth
**Target:** November 25–December 1.

Tasks:
- Build a compact React/TypeScript evidence viewer only after CLI output is stable.
- Make expected/observed/violated/inconclusive states obvious.
- Show provenance, event IDs and raw evidence alongside explanation.
- Add a synthetic sensor/controller workload using the same scenario engine if feasible.
- Demonstrate stale-session rejection with a simple 2D explanatory view, not a large simulator.
- Evaluate optional QNX resource-manager adapter.
- Recheck competitors and revise novelty language.

**Exit gate:** one engine supports the native-service demonstration and, if included, a second workload without parallel bespoke infrastructure.

**Cut rule:** remove the second workload if it delays reproducibility, tutorial or final validation. Low-level depth plus developer-tool value remains a legitimate broad story.

## Phase 5 — QNX evidence, tutorial and independent reproduction
**Target:** December 2–7.

Tasks:
- Add supported kernel-trace correlation only if privileges/configuration are verified and it adds evidence.
- Do not make HAM or tracing mandatory unless installed-version support is proven.
- Write the codelab from clean setup to failing contract to corrected experiment.
- Include prerequisites, expected outputs, troubleshooting and limitations.
- Have an independent reviewer reproduce the experiment from repository instructions.
- Inventory dependencies and choose a suitable open-source license.
- Audit the public repository for proprietary files, credentials and misleading claims.

**Exit gate:** a clean reviewer can run the core experiment; documentation and screenshots match actual behavior; source ownership and dependencies are documented.

## Phase 6 — Submission package and freeze
**Target:** December 8–12.

Tasks:
- Re-read current event rules and verify primary category and allowed bonus choices.
- Record a truthful public demonstration under three minutes.
- Show actual QNX target evidence, baseline violation, reducer trials and corrected outcome.
- Finalize project description: problem, differentiation, QNX-specific implementation, scope, limitations and future work.
- Verify public source, license, README, tutorial and video links.
- Use exact versions and commands, not “works on my machine.”
- Prepare final form answers without inventing performance, novelty or safety claims.
- Obtain required user/legal approvals before final submission where needed.

**Exit gate:** complete evaluator-ready package, links verified from outside the working checkout, and no critical reproducibility defects.

## Phase 7 — Buffer and verified submission
**Target:** December 13–15; official cutoff December 16 at 00:30 IST.

Use the buffer for defects and upload issues, not new scope. Verify submission receipt and final entry contents; distinguish saved draft from submitted entry. Record final repository commit, video URL, submitted category and timestamp. Do not assume a welcome email proves project submission.

## Acceptance checklist
### Functional
- [ ] Real QNX 8 code executes.
- [ ] Baseline and corrected fixture behavior is demonstrated.
- [ ] Three controlled fault cases and explicit contracts are supported.
- [ ] CLI and report work without the UI.
- [ ] At least one reduced reproducer is preserved with trial evidence.
- [ ] Partial evidence yields INCONCLUSIVE, not false PASS.
- [ ] Cleanup is bounded and restricted to run-owned processes.

### Evidence and distribution
- [ ] Manifest includes versions, target configuration, revision and assumptions.
- [ ] Host and target clocks are not misleadingly conflated.
- [ ] Emulated timing limitations are stated.
- [ ] Public source excludes proprietary SDKs/images and secrets.
- [ ] Dependency/license inventory exists.
- [ ] Independent clean reproduction is documented.

### Judging package
- [ ] One clear primary category is selected.
- [ ] Novelty is stated as a substantiated differentiator, not “first ever.”
- [ ] Broad applicability comes from the shared engine.
- [ ] Codelab is independently useful.
- [ ] Video is public and under three minutes.
- [ ] All links and final submission state are verified.

## Implementation boundary
This roadmap authorizes no purchases, new credentials, license acceptance or security changes by itself. The present assignment was research and planning. Begin implementation only under applicable user authorization and required setup approvals. Keep ongoing unrelated OSS contribution work separate so this project does not consume or duplicate its rotation.
