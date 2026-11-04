# Risks, open questions and decision log
Snapshot: 4 November 2026. Update this document as evidence changes.

## Decisions
| Decision | Reason | Reconsider when |
| --- | --- | --- |
| Select Faultline | Strong reusable output and software-only demonstration potential | Runtime gate fails or competitor review eliminates the differentiation |
| Primary category: Developer Tooling & Host Tools | Product is a developer workbench; other domains are workloads | Official category guidance or completed implementation changes fit |
| Real QNX native fixture before UI | Prevent a generic dashboard with superficial integration | Never waive real integration; only change the form of the host tool |
| IPC cancellation first | Small, documented, QNX-specific behavior | Target experiment reveals it is unreliable or uninformative |
| Stale-session cart scenario second | Makes cross-domain impact understandable | Core is late; then omit it |
| Application events before kernel tracing | Lower privilege/setup dependency | Core reliable and trace access verified |
| Reduction with trial history | Differentiation without claiming deterministic scheduling | It cannot reliably preserve the original violation |
| No LLM in control/evidence loop | Avoid unnecessary uncertainty and unverifiable explanations | A separate grounded optional feature has clear measured benefit |
| Cloud-only work | Participant's explicit direction | Only participant may authorize another environment |

## Risk register
| Risk | Impact | Early signal | Mitigation / decision gate |
| --- | --- | --- | --- |
| License scope unclear for chosen cloud runtime | Cannot execute target legally | Issued license/runtime class unresolved | Review actual terms and obtain required acceptance before use; do not assume free means unrestricted |
| Host not supported or insufficient resources | No usable QNX execution | Current host Debian; no SDK/QEMU/KVM established | Gate 0 compatibility/boot proof, headless route, no hardware purchase assumed |
| A timeout fixture hangs indefinitely | Unreliable demo and wasted sessions | Cleanup fails after injected fault | Parent watchdog, run-owned processes, total deadline and failure artifact |
| Nondeterminism defeats minimization | Misleading reduced reproducer | Reduction only fails sporadically | Repeatability threshold, full trial log, label non-reproduced/inconclusive |
| Instrumentation changes behavior | Evidence does not reflect baseline | Tracing materially changes latency/outcomes | Compare trace on/off; record overhead and configuration |
| Existing tools already solve proposed gap | Weak novelty | Existing runnable-contract/reducer workflow found | Compare actual workflows, strengthen adapter/reproducer value or pivot |
| Overbroad domain scope | Incomplete core | More time on animation than native tests | One hero fixture; one optional second workload |
| Unsafe or exaggerated claims | Credibility and eligibility risk | “Certified,” “guaranteed,” “first ever” language | Evidence review and explicit limits |
| Proprietary redistribution | License breach | SDK/image files enter repository | Ignore rules, precommit/manual review, publish original source only |
| Dependency and license problems | Public repository cannot be evaluated | Missing licenses or incompatible dependencies | Inventory and license review early |
| Late video/tutorial | Strong code but poor judging evidence | No recorded dry-run by freeze | Dedicated submission milestone and buffer |
| Changed event rules | Wrong category or deliverables | Official update differs from snapshot | Recheck before final submission |

## Unresolved questions
1. Which actual noncommercial license is deployed to the activated myQNX account?
2. Is the intended QEMU/QSTI cloud arrangement allowed by that license and provider?
3. Can an authorized cloud runtime boot and execute SDP 8-built binaries with usable resources?
4. Which exact installed SDK version and target components support the chosen experiment?
5. Can the baseline cancellation violation be reproduced consistently and cleaned up safely?
6. What minimum event evidence is sufficient without privileged kernel tracing?
7. Does an existing open tool already provide the full experiment/reducer/reproducer workflow for QNX?
8. Will organizer updates clarify AI-assistance policy or host-tool evaluation requirements?
9. Which open-source license should be selected after ownership/dependency review?
10. Does the completed product justify a second workload without weakening the core?

The plan does not require the participant to answer these all now. Resolve through authorized research and engineering; ask only for permissions or decisions that cannot be inferred.

## Status checklist
- [x] Participant confirmed event registration.
- [x] Public repository created; supplied prize brief preserved.
- [x] Official rules and primary technical documentation reviewed.
- [x] Eight concepts compared across three passes.
- [x] One concept selected and refined through five passes.
- [x] Roadmap and validation gates documented.
- [ ] SDK license accepted/deployed and cloud runtime scope verified.
- [ ] QNX toolchain installed.
- [ ] Real QNX target booted and first native program run.
- [ ] Baseline/fixed experiment validated.
- [ ] Project implemented and independently reproduced.
- [ ] Submission prepared, approved as needed and verified.

## Source notes
The license discussion is a conservative interpretation of the published document, not legal advice. The relevant [license PDF](https://www.qnx.com/download/download/51624/BB_QNX_Development_License_Non-Commercial_License_Class_v7_2025-12-10.pdf) distinguishes cloud development tools from specified Cloud Target System Images. Applicability to the final arrangement must be established rather than guessed.
