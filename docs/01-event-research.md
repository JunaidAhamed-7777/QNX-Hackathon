# Event research and decision constraints
Research snapshot: 4 November 2026. This is a planning document, not legal advice or a claim of completed implementation.

## Confirmed entry status
The participant has confirmed QNX Global Hackathon registration. A subsequent authenticated QNX message confirmed activation of the separate myQNX account. These do not establish SDK license acceptance, a downloaded toolchain, target-image rights, or a working runtime. No project submission is recorded for this repository.

## Dates and eligibility
The [official rules](https://qnx.devpost.com/rules) set the submission deadline to **15 December 2026 at 2:00 p.m. Eastern**, equivalent to **16 December at 00:30 IST**. The development window began 2 November. New projects or substantial improvements made during the window can qualify. Preserve a dated work history and identify any pre-existing dependencies rather than presenting old work as newly created.

The rules require entrants to be at least 18. India is not listed among the excluded locations in the rules reviewed; the participant's stated age of 20 appears eligible. Recheck the live rules before submission. Other eligibility exclusions and team requirements still apply. The event is free to enter; this does not imply free cloud execution or unrestricted software licensing.

## The prize strategy
The [rules, particularly sections 4, 6 and 8](https://qnx.devpost.com/rules), require **one primary submission category**. A project may receive at most one Overall prize, one Bonus prize, and Community Choice. It cannot accumulate the five category prizes, combine Grand Prize with another Overall prize, or collect both $3,500 bonuses.

The largest listed cash combination for one submission is $10,000 Grand Prize + one $3,500 bonus = $13,500. This is a rules-based ceiling, not an expected return or prediction. The supplied prize list is preserved in [initial.md](initial.md).

**Recommended entry:** Developer Tooling & Host Tools. Demonstrate naturally reusable low-level, robotics and mobility applications of the same engine. A strong QNX-specific mechanism and an independently useful codelab provide two possible bonus routes, but only one can be awarded. A reusable source repository is not automatically an Open-Source Contribution & Ports entry.

Registration counts seen on the event page were roughly 310–318 during research. These count registered participants, not completed projects or competing teams; cached pages differed. Do not infer easy odds.

## Submission requirements that shape the product
The [event overview](https://qnx.devpost.com/) and [resources](https://qnx.devpost.com/resources) allow real QNX 8 applications/components and host tools supporting QNX 8 development. Host software must do something meaningful for QNX; branding a generic web dashboard is not sufficient.

Plan for:
- Public source with a detectable open-source license, subject to ownership and dependency checks.
- Exact QNX version, toolchain, target configuration and reproducible build/run instructions.
- A working implementation and observable QNX integration.
- English documentation, or the required translation.
- A public demonstration video **under three minutes**.
- Honest attribution of dependencies and pre-existing work.
- A new submission repository for an OSS-port entry, containing the porting work and referencing upstream rather than passing off upstream fork/history as the submission.

Judging weighs implementation, design/coherence, impact and innovation equally. The documentation and demo must make each visible. No award or judging eligibility can be guaranteed.

## AI-assisted work
No explicit AI coding-assistance prohibition or disclosure requirement was found in the reviewed contest rules. That is not a blanket guarantee that any AI use is permissible: follow licenses, originality requirements, third-party rules, and any updated organizer instructions. Answer application questions truthfully. Do not interpret the phrase “Innovation & AI Creativity” as permission to misrepresent authorship or results.

The selected project does not require an LLM to operate. Avoid an AI-generated diagnosis that claims more certainty than the recorded evidence.

## License and execution gates
The [QNX Everywhere introduction](https://www.qnx.com/developers/docs/qnxeverywhere/introduction.html) describes a free **noncommercial** SDP path involving a myQNX account, license deployment, QNX Software Center and SDK installation. No license was accepted by this research task.

The published [noncommercial license](https://www.qnx.com/download/download/51624/BB_QNX_Development_License_Non-Commercial_License_Class_v7_2025-12-10.pdf), including Exhibit A, allows licensed cloud development tools but imposes restrictions on QNX-provided Cloud Target System Images and derivatives. Whether a locally built QEMU/QSTI image on the selected cloud host falls under that particular restriction is **unresolved**. Do not assume either a blanket cloud ban or blanket permission.

Before installing or running QNX:
1. Review the actual license issued to the participant and obtain required acceptance.
2. Establish that the chosen host/runtime arrangement is permitted.
3. Confirm host compatibility and usable resources.
4. Prove real cross-compilation and target execution.
5. Keep SDK files, license material, credentials and proprietary target images out of this public repository unless redistribution rights are separately verified.

The official [QEMU route](https://www.qnx.com/developers/docs/qnxeverywhere/com.qnx.doc.target_images/topic/qsti_qemu/about.html) documents Ubuntu 22.04/24.04. The current cloud host was Debian 13 during inspection, without qcc, QEMU or an exposed KVM device. Its ability to execute the QNX demo is **not proven**. This is a feasibility gate, not a reason to simulate Linux execution and call it QNX.

## Evidence policy
Use three explicit labels throughout the project:
- **Verified:** supported by a source or a reproducible run.
- **Hypothesis:** a design or novelty proposition awaiting tests.
- **Unverified:** a dependency, permission or capability not yet established.

Do not publish medical-safety, certification, universal determinism or physical hard-real-time guarantees. An emulated demonstration can show functional behavior and observed latencies, not bounds under all hardware conditions.
