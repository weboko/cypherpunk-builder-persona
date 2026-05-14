# Contribution Matrix

*For each subtype: what kind of contribution they can make, what conditions they need first, the best first task to offer them, and what makes them disengage. Designed for use by a community/DX lead or a downstream agent evaluating contributor strategy.*

---

## How to read this matrix

Each subtype contributes differently. Treating "contributor" as one undifferentiated category causes projects to (a) build onboarding flows that only serve one kind of person, and (b) miss out on the contributions other subtypes are uniquely good at.

The columns:

- **What they can contribute:** the kinds of work this subtype produces well.
- **What they need first:** the project prerequisites that must exist before this subtype will start.
- **Best first task:** a concrete, low-friction starting point.
- **What loses them:** the most common reason a project that *could* have attracted them doesn't.
- **Retention risk:** the most common reason they leave after starting.

---

## Section 1 — The Matrix

### Protocol Cypherpunk

| Field | Detail |
|---|---|
| **What they can contribute** | Protocol design, spec authorship, cryptographic review, formal verification, threat-model refinement, primitive selection, security audits, academic-paper-quality writeups, IETF/CFRG/RFC engagement, careful reduction proofs, attack research, post-quantum migration planning. |
| **What they need first** | A real spec or design doc to argue with. A real threat model to critique. Maintainers who can engage at protocol depth. A clear answer to "who is reviewing this?" Some indication that contribution will be taken seriously beyond cosmetic PRs. |
| **Best first task** | A targeted review request: "Here is the threat model. Here are the open questions. Please critique." Or a request to review a specific primitive choice. Or a co-authorship invitation on a spec draft. |
| **What loses them** | Marketing-led launches; custom cryptography without rationale; absent threat model; vague "we're decentralized" claims; team that confuses competence with rank. |
| **Retention risk** | They leave when their protocol input is ignored in favor of marketing pressure; when the project drifts toward a token launch; when the maintainer team turns over without succession; when the project starts shipping rushed security-critical code under launch deadlines. |

### Open-Source Infrastructure Hacker

| Field | Detail |
|---|---|
| **What they can contribute** | Code, in volume. Tests. CI work. Documentation. Issue triage. Dependency upgrades. Bug fixes. Refactors. Build-system improvements. Reproducible-build setup. Package maintenance (apt, AUR, Nix, Homebrew). Linter fixes. Architecture documentation. Performance work. |
| **What they need first** | A clean repo. A README that explains what the project does and how to run it. A real `CONTRIBUTING.md` and `ARCHITECTURE.md`. Real first issues. Active maintainers. A defined PR review cadence. A non-hostile review tone. |
| **Best first task** | A real "good first issue" that fixes a real bug a real user reported, ideally with reproduction steps and a pointer to the right code area. Not a typo fix. Reviewer assigned in advance. |
| **What loses them** | Closed-core projects pretending to be open source; broken build instructions; dead-on-arrival repos with marketing sites; PRs that sit unreviewed for months; CLAs assigning copyright; relicensing histories; a Discord-only community. |
| **Retention risk** | They leave when reviews stall; when maintainers ship features they (the contributor) had explicitly objected to; when the project gets acquired or relicensed; when burnout becomes visible; when their work isn't acknowledged in releases. |

### Privacy Activist Builder

| Field | Detail |
|---|---|
| **What they can contribute** | Field testing with real at-risk users. User research with marginalized or hostile-environment users. Translations (and *maintained* translations). Accessibility work. Onboarding flows for non-technical users. Documentation in multiple languages, including the warnings. UX critique grounded in specific user populations. Relationships to civil-society organizations. Field deployment expertise. |
| **What they need first** | A threat model that names real user populations. Evidence the project takes UX seriously beyond technical users. A commitment to maintaining translations (not just one-time crowdsourcing). A code of conduct that's real, not theatrical. Maintainers who treat real-world deployment as core engineering, not as a "nice to have." |
| **Best first task** | A user research partnership with a named civil-society org; or a localization tranche tied to a specific user community; or a documentation review focused on threat-model communication to non-technical users; or a SECURITY.md review focused on disclosure paths usable by activists. |
| **What loses them** | Generic "privacy for everyone" framing; UX that assumes Western, English-speaking, low-threat users; translations that get added then abandoned; maintainers who don't understand the real-world stakes; ignoring or downplaying disclosures that affect at-risk users. |
| **Retention risk** | They leave when the project drifts toward consumer / "modern teams" framing; when at-risk-user concerns are deprioritized; when funding model becomes incompatible with the protection claims; when a serious incident is mishandled. |

### Crypto-Positive Cypherpunk

| Field | Detail |
|---|---|
| **What they can contribute** | Protocol-level cryptographic work, ZK circuit design and review, MPC protocol contributions, smart-contract review, formal-methods application, on-chain instrumentation, treasury-management feedback, sober ecosystem connections that don't read as marketing. They write good papers and good specs. They also know who to talk to. |
| **What they need first** | A protocol with cryptographic substance. A clear funding model (foundation, treasury, grant — not VC-driven launch pressure). A token rationale that is technical (or, ideally, no token). Awareness of regulatory context (post-Tornado-Cash). Maintainers who can talk at protocol depth. |
| **Best first task** | A targeted protocol review; co-authorship on a spec or design doc; security review of a specific component; grant-funded research on an open problem in the project; bridge to a relevant academic group. |
| **What loses them** | Token-first framing; premine and insider allocation surfacing late; VC funding overhanging the protocol direction; the project becoming "the next thing on [chain]" rather than a contribution to cryptographic infrastructure. |
| **Retention risk** | They leave when the project gets captured by token-price incentives; when speed-of-launch wins over security review; when the project starts marketing in ways that contradict its technical claims; when regulators put pressure that the project mishandles. |

### Crypto-Skeptical Decentralist

| Field | Detail |
|---|---|
| **What they can contribute** | Federated and P2P architecture work. ActivityPub, Matrix, libp2p, Hypercore, IPFS (without Filecoin), Nostr (with caveats), local-first / CRDT work. Critical blog posts that clarify what real decentralization is (a public-good in the discourse). Connection to the fediverse and to local-first communities. Strong opinions about license choice and supply-chain hygiene. |
| **What they need first** | A project that is not in the Web3 space, or one that very clearly distances itself from it. A funding model that doesn't depend on a token. Architecture grounded in federation, P2P, or local-first. A maintainer team whose vocabulary doesn't borrow from crypto marketing. |
| **Best first task** | A contribution to a federated or P2P feature; a maintenance role on a non-crypto decentralization protocol; a writeup explaining what the project does without the Web3 framing some marketer added. |
| **What loses them** | Any token; any blockchain; any Web3 vocabulary; community that bridges to crypto Twitter; ambassador programs; airdrop launches; NFT side projects. |
| **Retention risk** | They leave the moment a token is announced; they leave when the language drifts toward Web3; they leave when the funding source starts to look like it'll demand financialization. |

### Sovereign Computing / Self-Hosting Builder

| Field | Detail |
|---|---|
| **What they can contribute** | Docker Compose files, Helm charts, Nix flakes, Ansible roles, packaging for popular distros, ARM builds, deployment documentation, reverse-proxy configs, backup-and-restore documentation, monitoring integration (Prometheus, Grafana), update-path testing. They will write better deployment docs than your team has time to. |
| **What they need first** | A binary that runs; a container image that runs; a Compose file that works; ARM support, or at least an obvious path to it; sane defaults; a clear license; multi-user features in the free/self-host tier (not gated behind an enterprise tier). |
| **Best first task** | "Send us your Compose file and we'll merge it into the official examples." "Add a Helm chart." "Add ARM build to CI." "Improve the backup-and-restore docs." "Document Caddy reverse-proxy config." |
| **What loses them** | Cloud-first / cloud-only deployment; mandatory cloud account for self-host; phoning home; absurd resource requirements; SSO-as-enterprise-tier; "source-available" mislabeled as open source; "self-host coming soon" forever. |
| **Retention risk** | They leave when the project decides to "focus on the cloud product"; when self-host features are quietly removed; when telemetry is added without consent; when an enterprise tier eats the features they need; when the maintainer becomes hostile to operational questions. |

---

## Section 2 — Contributor Funnel Stages

Useful for instrumenting the contributor experience. Each stage has its own losses.

### Stage 1 — Discovery

The contributor finds the project. Typical paths:
- Hacker News / Lobsters / Mastodon post.
- GitHub trending or a search result.
- Recommendation from a respected maintainer.
- Conference talk or technical writeup.
- A mailing-list announcement.

**Highest-loss problems at this stage:** the project is invisible to the cohort's discovery channels (no HN presence, no Mastodon posts from real humans, no maintainer-driven writeups). Or the project's discovery surface is dominated by marketing rather than substance.

### Stage 2 — First impression

The contributor lands on the homepage and the repo. They are deciding whether to spend the next twenty minutes.

**Highest-loss problems at this stage:** marketing-heavy homepage; hidden repo; no clear "what is this"; mandatory email or signup walls; "schedule a demo" CTAs.

### Stage 3 — Technical evaluation

The contributor reads the README, scans the repo, and looks at recent activity.

**Highest-loss problems at this stage:** broken build instructions; dead repo; missing `ARCHITECTURE.md`; PRs that have sat unreviewed; closed-core hidden away.

### Stage 4 — First-run

The contributor tries to clone, build, and run the project.

**Highest-loss problems at this stage:** failed `make`; failed `docker compose up`; missing dependencies; out-of-date instructions; mandatory cloud account; broken demo.

This is one of the two most consequential stages. A failed first-run loses ~80% of potential contributors who got this far.

### Stage 5 — First issue / first contribution

The contributor opens an issue or sends a PR.

**Highest-loss problems at this stage:** no real "good first issues"; issues with no context; reviewer never assigned; maintainer responds in days/weeks/never; review tone is hostile or pedantic.

This is the *other* most consequential stage. A great first-contribution experience converts an evaluator into a long-term contributor.

### Stage 6 — Sustained contribution

The contributor returns for a second, third, tenth contribution.

**Highest-loss problems at this stage:** the project drifts in direction; the contributor's previous work is undone without explanation; CLA terms change; a relicensing event; the project is acquired; the contributor isn't named in releases.

### Stage 7 — Promotion to maintainer

The contributor takes on more responsibility. Eventually, ideally, becomes a maintainer.

**Highest-loss problems at this stage:** opaque promotion paths; "founder bottleneck" where one person blocks all decisions; absent succession planning; maintainer burnout that the project does not address.

---

## Section 3 — Cross-Subtype Patterns

### What every subtype needs

- A real repo, with real activity.
- A real license, with no surprises.
- A real maintainer team that responds.
- A real artifact (binary, package, container) the contributor can run.

### What attracts multiple subtypes simultaneously

- **Reproducible builds.** Attracts Protocol Cypherpunk, OSS Infra Hacker, Sovereign Computing.
- **A real threat model on the homepage.** Attracts Protocol Cypherpunk, Privacy Activist Builder, Crypto-Positive.
- **Federation or P2P architecture without a chain.** Attracts Crypto-Skeptical Decentralist, Sovereign Computing, OSS Infra Hacker.
- **ARM support + Docker Compose + permissive license.** Attracts Sovereign Computing, OSS Infra Hacker, Crypto-Skeptical.
- **Honest acknowledgment of current centralization and a path to reducing it.** Attracts everyone except the most maximalist Crypto-Skeptical.

### What repels multiple subtypes simultaneously

- **Tokens.** Repels everyone except Crypto-Positive, and even there only conditionally.
- **Web3 vocabulary.** Repels every subtype except some of Crypto-Positive.
- **Closed-core "open source."** Repels OSS Infra Hacker and Sovereign Computing especially; the others notice and downgrade trust.
- **Discord-only community.** Repels OSS Infra Hacker, Crypto-Skeptical, Sovereign Computing, Privacy Activist Builder.
- **Mandatory cloud account for self-host.** Repels Sovereign Computing entirely and others significantly.
- **"Schedule a demo" as the only access path.** Repels all technical subtypes.

---

## Section 4 — Hiring and Paid Contribution

A few subtypes will work on a project full-time if compensated, and the project's behavior here matters.

### What attracts paid contribution

- A foundation-backed funding model with multi-year stability.
- Grants from credible programs (NLnet, OTF, Sovereign Tech Fund, EU NGI, Bitcoin-related grant programs, Ethereum Foundation PSE for the Crypto-Positive wing).
- A track record of treating contractors as full members of the project.
- Honest pay (above industry-discount "we're a non-profit so we underpay").
- The ability to keep working on the project after the engagement ends.
- No assignment of copyright to a single corporate entity.

### What repels paid contribution

- VC-style "we'll pay below market for equity" deals on what was an open-source project.
- Contracts that demand IP assignment beyond the work being done.
- Pressure to ship security-critical work to launch deadlines.
- The project's funding model creating obvious conflicts of interest.

---

## Section 5 — Recovery: Bringing Back a Contributor

When a contributor disengages, the most common recovery paths are:

1. **Address the specific reason they left.** If they cited an unmerged PR, merge it (or explain why not). If they cited a relicensing, address the relicensing publicly.
2. **Invite them to weigh in on a decision.** A real consult, not a survey.
3. **Acknowledge them publicly when their past work helps a new feature.**
4. **Ask for help on a specific problem they were uniquely suited for.**

What does *not* work: generic outreach, marketing emails, "we miss you" messaging, asking them to do free work for a now-commercial product they used to contribute to.

---

## Section 6 — A Note on Pseudonymous Contribution

This cohort respects pseudonymous contribution. Many of its most respected figures contribute under pseudonyms with long, verifiable track records. Projects that demand legal-name attribution as a default lose contribution from this cohort. Projects that demand it for security reasons (e.g., supply-chain audit requirements) should explain why, scope the requirement narrowly, and offer pseudonymous-friendly alternatives where possible (signed-with-a-published-key contribution, etc.).

The cohort distinguishes pseudonymous contribution (legitimate, normal, central to the tradition) from anonymous contribution (legitimate but harder to evaluate at the trust level needed for maintainership). Trust accrues to *consistent identities*, even if those identities are not legal names.
