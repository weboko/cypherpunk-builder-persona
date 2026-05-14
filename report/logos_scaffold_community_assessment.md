# Community-Involvement Assessment: `logos-co/scaffold`

*A persona-driven review of [github.com/logos-co/scaffold](https://github.com/logos-co/scaffold) using the Cypherpunk Builder dossier in this repository. Findings are aggregated from five independent simulated readings — Open-Source Infrastructure Hacker, Crypto-Skeptical Decentralist, Protocol Cypherpunk, Crypto-Positive Cypherpunk, and Sovereign Computing self-hoster — and filtered down to the changes that materially move adoption, contribution, and trust.*

*Repository state at the time of review: v0.1.1 (Apr 2026), 67 commits, 6 stars, 10 forks, 20 open issues, 16 open PRs, 86 closed PRs, dual MIT/Apache-2.0, no CLA, no telemetry.*

---

## 1. Summary in one paragraph

`logos-scaffold` is a **technically clean Rust CLI**. Dual MIT/Apache-2.0, no CLA, no telemetry, sober dependency list, an unusually mature `CONTRIBUTING.md`, an ADR file, a FURPS doc, and a 23-scenario `DOGFOODING.md` runbook. The persona cohort respects all of that. What it currently *fails* to do is communicate **what LEZ is, who LEZ is for, what trust assumptions LEZ makes, and what the relationship is between the scaffold, the Logos ecosystem, and any future token or governance event**. Every persona — including the friendly ones — closed the tab earlier than they had to, for reasons that are fixable with prose, two or three doc files, a `flake.nix`, and a handful of issue labels. None of the reasons are reasons of code quality.

The gap is not "build a community." The gap is **let the community recognize itself when it walks in.**

---

## 2. Where the personas converged

Across five independently simulated readings, the same handful of findings surfaced regardless of which persona did the walking. These are the high-confidence findings.

### Convergence 1 — The README assumes you already drank from logos.co

Every persona, in their own words:

- **OSS Infra Hacker:** *"the README assumes I've already drunk from logos.co. I went to logos.co; it says 'social movement and decentralized technology stack.' that phrase makes my eye twitch."*
- **Protocol Cypherpunk:** *"The string 'LEZ' expands to 'Logos Execution Zone' and is never further defined… no IACR ePrint reference, no IETF/CFRG draft, no peer-reviewed paper, no named cryptographer."*
- **Crypto-Skeptical Decentralist:** *"there is no story in this repo about why a chain — that conversation lives on logos.co, not here."*
- **Crypto-Positive Cypherpunk:** *"no link to a spec or even a design note, no mention of which risc0 release is pinned, no reproducible-build story for the guest image (which is the entire trust root)."*
- **Sovereign Computing:** Implicit — the tool's purpose was inferred from `wallet topup` and `program_id`, not stated.

A first-contact tool that requires off-site context to be understood is the **single largest leak in the contributor funnel** (per `10_contribution_matrix.md` §"Stage 2 — First impression").

### Convergence 2 — Issue tracker contradicts the CONTRIBUTING.md priority

`CONTRIBUTING.md` says priority goes to "active builders" and "contributors with documented user demand," with generic cleanups deprioritized and a hard 3-PR-per-7-days cap on non-org members. That framing is **defensible and even welcome** to the OSS Infra Hacker — but it requires the issue tracker to expose which substantive bugs are approachable. Today, **zero issues are labeled `good first issue` or `help wanted`**, even though 8–10 of the 20 open issues are genuinely scoped, reproducible, and ideal entry-level work (e.g. `#161` summary-line bug, `#44` duplicated path constant, `#101` panic on missing indexer).

> *"CONTRIBUTING says 'we want substantive contributors,' issue tracker provides zero signal about which substantive bug is approachable. that's the friction point."* — OSS Infra Hacker

This is the **highest ROI fix in the entire review.** Cost: a maintainer-hour. Effect: every drive-by visitor who currently bounces sees a path in.

### Convergence 3 — `SECURITY.md` is mislabeled

The current `SECURITY.md` is a **dev-wallet hygiene note** ("don't commit `.scaffold/wallet`, deterministic password is dev-only, no telemetry"). All five personas flagged this. The Protocol Cypherpunk most sharply: *"it is mislabeled: it is not a security model."* There is no disclosure address, no PGP/age key, no SLA, and no statement of adversary classes for the system the scaffold deploys against.

For a tool that scaffolds projects whose output is a cryptographic commitment (`program_id` = risc0 image ID), this is a credibility gap with cypherpunks of every flavor.

### Convergence 4 — The "Anchor on Solana" comparison sets the wrong frame

The README's `LEZ Framework` section compares the developer experience to **Anchor on Solana**. The Crypto-Skeptical Decentralist named this as *"the one phrase in an otherwise sober README that hard-codes the repo's identity as 'alt-L1 SDK' in my head before I've read the architecture."* The Crypto-Positive Cypherpunk independently inferred *"this is Anchor-for-our-chain"* from the same line. The Protocol Cypherpunk read it as confirmation that LEZ is being positioned as a product, not a protocol.

One line, three different negative reads. The line is true at the structural level — both projects are Rust SDKs for deploying on-chain programs — but **Solana carries a heavy 2021–2023 reputational payload** in the broader OSS/decentralization community. Even the friendly readers winced. Better-framed analogues exist (`forge`, `anchor` *and* `hardhat` in shape; Cargo for project layout) and could be placed in `ADR.md` instead of the user-facing README.

### Convergence 5 — Flake outputs are referenced but the repo isn't a flake

`FURPS.md` and `DOGFOODING.md` reference `.#lgx-portable` and AppImage staging — Nix-flake idioms. There is **no `flake.nix` in the scaffold repo root**. Both the Sovereign Computing self-hoster and the OSS Infra Hacker flagged this. From the dossier: *"A project that uses Nix or has a `flake.nix`: instant credibility bump."* (`04_subtype_oss_infrastructure_hacker.md` §"Project-Category Reactions"). Today the scaffold gets *credit-by-association* with Nix without paying the trust dividend a real flake would unlock.

### Convergence 6 — The funding / token posture is undisclosed

Three of five personas (Crypto-Positive, Crypto-Skeptical, Protocol) independently asked for an explicit statement on funding and token plans. The scaffold doesn't mention a token — neither does logos.co's homepage — but the **institutional context (IFT, parent to Status, which ran an ICO and holds SNT)** makes "no statement" read as "assume token until disclosed." A single paragraph in the README or a `FUNDING.md`, even just *"Logos infrastructure is funded by IFT; there is no LEZ token planned; if that changes, the governance process is X"*, would convert this from a yellow flag to a green one.

### Convergence 7 — The single-sequencer assumption is silent

The scaffold's `localnet reset`, `sequencer_service`, and "deploys to the sequencer" language imply a single-sequencer architecture. **Optimism, Arbitrum, Aztec, and Scroll all started this way and were not scandalized for it** — but they said so, and they published a roadmap. The scaffold says neither. Both crypto-adjacent personas flagged this as "fine for testnet, red if undocumented."

---

## 3. Where the personas diverged — and what to do about it

Divergences are useful: they tell you the audience boundary the project is currently straddling.

### Divergence A — The 3-PR-per-7-days cap

- **OSS Infra Hacker:** *"defensible-but-watching. 16 open PRs and 86 closed suggests they do merge external work. I'd test it."*
- **Crypto-Skeptical:** Approving — read it as *"this is a working tool, not a portfolio piece."*
- **Protocol Cypherpunk:** Did not weigh in (not their lens).
- **Sovereign Computing:** Did not weigh in.

**Verdict:** The rule itself is fine and even welcome. **What's missing is documentation of the exception path.** Where does the Action live? How do you appeal? Does a draft PR count? Does a doc-only PR count? Org members are exempt — when does an external contributor become eligible? A short `CONTRIBUTING.md` subsection (10–15 lines) closes this entirely.

### Divergence B — Is this a tool for the homelab or the dev laptop?

- **Sovereign Computing:** *"Today: laptop-only … there's no path from `scaffold dev` to `systemctl status logos-localnet`. That gap is where I lose interest as a self-hoster."*
- All other personas: assumed dev-laptop only and didn't probe further.

**Verdict:** The scaffold is, today, a developer ergonomic. That's a defensible scope. **But a one-paragraph "Running a persistent devnet" section** in the README (even as "not officially supported yet, here's the rough recipe") would (a) capture the self-hosting wing of the cohort as future contributors of Compose files / Nix modules / systemd units, and (b) provide a roadmap surface for the operationalization work that will eventually be required anyway.

### Divergence C — Who from outside Logos should be invited in?

- **Crypto-Positive Cypherpunk** named specific natural constituencies: risc0 / SP1 / Jolt (zkVM); PSE, Aztec, Penumbra, Aleo (privacy/circuits); Espresso, Astria, Radius (sequencing); Cashu / Fedimint / Ark (Bitcoin-side digital cash).
- **Crypto-Skeptical Decentralist** named the *opposite* set as the audience they wished the project would respect more visibly: Matrix, Mastodon, ActivityPub, libp2p (no chain), Hypercore, Ink & Switch local-first.

**Verdict:** These two audiences are not the same. Logos has to choose how heavily to court each. The **scaffold-as-doorway** strategy can serve both: by making it possible to read the scaffold without buying the chain frame (changes 1, 4, 8 below), the project can keep optionality with the decentralization wing while still serving its core zkVM-app-dev audience.

---

## 4. The recommended changes, prioritized by impact and cost

Each change is annotated with: which personas it unlocks, cost in maintainer-time, and the trust mechanism from the dossier it activates.

### Tier 1 — Do this week. High impact, low cost.

**1.1 Add a "What is LEZ, in 90 seconds" section at the very top of the README.**
- Two paragraphs + one ASCII or Mermaid diagram. Five boxes: `lgs CLI → risc0 guest build → image ID → sequencer submit → indexer query`.
- State explicitly: substrate is risc0 zkVM, pinned version X, what the sequencer is, what `program_id` commits to (a SHA-256 of the ELF image — *not* a soundness statement), what's in scope and out of scope for this tool.
- Unlocks: **all five personas.** This is the single most-cited gap.
- Mechanism: `00_executive_summary.md` §"Most important implications" — *"The homepage must lead to the repo, the spec, and the threat model within two clicks."*
- Cost: 1–2 hours.

**1.2 Label 8–10 of the existing open issues with `good first issue` and `help wanted`.**
- Candidates flagged by the personas as real and approachable: `#44` (duplicated path constants), `#161` (sequencer line summary), `#101` (panic when indexer unreachable), `#69` (missing fields on HashType), `#70` (`run_hello_world` not working).
- Add a "pointer to the right code area" comment on each, per `10_contribution_matrix.md` §"Open-Source Infrastructure Hacker / Best first task."
- Unlocks: **OSS Infra Hacker.** Highest single-fix ROI in the entire review.
- Cost: 1 maintainer-hour.

**1.3 Cut the "Anchor on Solana" comparison from the user-facing README.**
- Move it to `ADR.md` if a comparison is wanted internally. Replace in the README with: *"Project layout is Cargo-shaped: `methods/` for guest programs, `client/` for host code, `scaffold.toml` for module config."*
- Unlocks: **Crypto-Skeptical Decentralist** (no longer auto-rejects). **Crypto-Positive** (no longer reads as alt-L1 SDK). **Protocol Cypherpunk** (no longer cues "product not protocol").
- Cost: 5 minutes.

**1.4 Rename `SECURITY.md` to `SECURITY-DEV.md` (or `WALLET-SECURITY.md`) and create a real `SECURITY.md`.**
- Real `SECURITY.md` to contain: disclosure address, PGP/age key, response SLA, in-scope and out-of-scope adversary classes for the scaffold itself, link to LEZ protocol threat model (or a tracking issue if not yet written).
- Unlocks: **Protocol Cypherpunk, Privacy Activist Builder, OSS Infra Hacker.**
- Cost: 2–3 hours.

**1.5 Add a one-sentence funding statement in the README.**
- *"`logos-scaffold` is developed inside Logos, an IFT-funded project. There is no LEZ token. If that changes, the governance process is published at &lt;link&gt;."* Only ship the third clause if it's true.
- Unlocks: **Crypto-Skeptical** (defuses the institutional-pattern-match). **Crypto-Positive** (turns yellow flag to green).
- Cost: 30 minutes, plus internal sign-off.

### Tier 2 — Do this month. High impact, medium cost.

**2.1 Write `ARCHITECTURE.md` — not the existing `ADR.md`, a new file.**
- Data-flow diagram + 1–2 paragraphs per box: CLI → local risc0 build → image ID → wallet → sequencer submit → indexer → state read. Trust boundaries marked. Threat model named.
- Unlocks: **OSS Infra Hacker** (it's in their inspect-first list). **Protocol Cypherpunk** (gives them something concrete to argue with).
- Cost: 1 day.

**2.2 Ship a real `flake.nix` at the repo root.**
- `packages.default = scaffold`, `apps.default`, `devShell` with the toolchain pinned. Bonus: `packages.docker` for an OCI image.
- This is the single highest-credibility deployment-artifact change available for this audience.
- Unlocks: **OSS Infra Hacker, Sovereign Computing, Protocol Cypherpunk.**
- Mechanism: `04_subtype_oss_infrastructure_hacker.md` §"A project that uses Nix or has a `flake.nix`: instant credibility bump."
- Cost: 1–2 days.

**2.3 Add a "Running a persistent devnet" section + `contrib/compose/docker-compose.yml`.**
- Sequencer + deterministic wallet + healthcheck on `:3040/health`. Position as "informal recipe, roadmap link &lt;here&gt; for first-class support."
- Unlocks: **Sovereign Computing** as a future contributor base.
- Cost: 1–2 days.

**2.4 Document the PR rate-limit Action and its appeal path in `CONTRIBUTING.md`.**
- Where the rule is enforced, what counts (drafts? docs?), how to request an exception, when an external contributor becomes eligible for an exception.
- Unlocks: **OSS Infra Hacker** (turns "watching" into "trust").
- Cost: 30 minutes.

**2.5 Add a `PROTOCOL.md` (or "For protocol reviewers" section in README) linking out to:**
- LEZ spec (or tracking issue if WIP).
- risc0 version pin and release-notes link.
- Sequencer design doc / decentralization roadmap.
- Any IACR / IETF / audit artifacts (or "none yet, scope TBD").
- Unlocks: **Protocol Cypherpunk, Crypto-Positive.**
- Cost: 4 hours (mostly inventory and linking).

### Tier 3 — Do this quarter. Strategic.

**3.1 Multi-arch release binaries.**
- `linux/amd64`, `linux/arm64`, `darwin/arm64`. Static or musl. Pi 5 and ARM cloud nodes.
- Unlocks: **Sovereign Computing** (and a quiet credibility bump everywhere else).
- Cost: 1–2 days of CI work.

**3.2 Replace `lsof | grep` PID detection with a state-directory + PID file.**
- `--state-dir` flag defaulting to `$XDG_STATE_HOME/scaffold/`. CI matrix on Ubuntu, Debian, Fedora, Alpine, NixOS.
- Unlocks: portability headroom that the Sovereign Computing persona names as a hard blocker today.
- Cost: 2–3 days.

**3.3 `lgs doctor --json` for machine-readable health output.**
- Telegraf / Prometheus textfile collector / homelab monitoring can scrape it. Doesn't change the dev-tool focus, just adds an output mode.
- Cost: 1 day.

**3.4 Pin and surface the risc0 version in `scaffold.toml` and in `doctor` output.**
- Plus a `lgs spec` (or `lgs doctor --protocol`) subcommand that prints: pinned LEZ commit, pinned risc0 version, pinned spel commit, link to spec, link to threat model, link to audit reports. Version skew is a soundness-relevant fact, not a packaging detail.
- Unlocks: **Protocol Cypherpunk, Crypto-Positive.**
- Cost: 1 day.

**3.5 `REVIEWERS.md` naming the engineers / cryptographers reviewing LEZ.**
- Named accountability is the cheapest trust signal a project can produce. If none yet, say so explicitly and invite candidates.
- Cost: editorial; institutional sign-off may be the gating factor.

### Tier 4 — Worth doing but not load-bearing

- CHANGELOG.md per release, with breaking-change call-outs. Signed release tags.
- `CODE_OF_CONDUCT.md` (linked Contributor Covenant or similar, real enforcement path).
- Move primary technical discussion to a public, searchable channel (mailing list, Discourse, or Matrix/IRC) and demote Discord if it exists. Per `04_subtype_oss_infrastructure_hacker.md`: *"Discord as the only support channel: actively hostile to long-term maintenance."*
- A `WHY-A-CHAIN.md` (Crypto-Skeptical's specific request). Higher cost because it's a real-stakes editorial document, but it converts the most-hostile fraction of the audience.

---

## 5. The single most-cited bridge

If only one thing changes after this review, change this:

> **The top of the README must answer, in 90 seconds and without leaving the page: (a) what LEZ is, (b) what the scaffold does, (c) what trust assumptions it inherits, and (d) whether there is a token.**

Every persona, friendly and hostile, asked for this. Nothing else moves the cohort the same amount per maintainer-hour.

---

## 6. What the scaffold is currently optimized for, and what it would unlock if shifted

**Currently optimized for:** application developers who are already inside the Logos worldview, plus Rust+zk engineers who can decode `program_id = risc0 image ID` on sight without further context. For that audience, the tool is excellent.

**What a shifted version unlocks:**
- The OSS Infrastructure Hacker cohort, which is the *largest contributor pool* in the broader cypherpunk-builder population (per `00_executive_summary.md`). They will not invest in a project whose README they can't read in five minutes.
- The Crypto-Skeptical Decentralist cohort, which is the *most hostile* by default — but also the *warmest* once they recognize a clean Rust infra tool that isn't asking them to buy a token. This cohort, won over, becomes an unusually loud advocate ("federated, no chain, well-engineered, look at this") and a strong reputational moat against the conflation with the speculative wing.
- The Protocol Cypherpunk cohort, who will not contribute code in volume but will deliver the *peer-review and named-reviewer trust signals* that the project's institutional positioning currently lacks.
- The Sovereign Computing cohort, who will, when invited, contribute the `flake.nix`, the Compose files, the systemd units, the ARM CI, and the Prometheus integration that the maintainers do not have time to write.

The conversion mechanism in every case is **prose + a few small structural changes**, not protocol re-architecture or strategic repositioning. Most of this report's recommendations fit in a single sprint.

---

# Part II — Social-content directions for these personas

*Per the brief, the second deliverable: what kind of social content might make sense for the cypherpunk-builder audience, applied to Logos / scaffold specifically.*

The Cypherpunk Builder cohort treats most "social content" with suspicion (see `09_messaging_matrix.md` §"Trust destroyers"). They detect campaigns. They detect ambassador programs. They detect "join our community" CTAs and they close the tab. This section names what they *do* engage with, by channel and content type, plus a concrete list of post candidates Logos could produce starting next week.

## 7. Channel map

Different subtypes live in different channels. Don't try to reach all of them in one feed.

| Channel | Primary audience | What works | What dies on contact |
|---|---|---|---|
| **Hacker News** | OSS Infra Hacker, Sovereign Computing, Crypto-Skeptical (selectively) | Show-HN with a working binary, a real README, and a maintainer in the comments. Long-form postmortems. "I rewrote X in Rust because Y" pieces. | "We're launching a token." "Our community of 50,000 builders." "Decentralized [thing that doesn't need decentralizing]." |
| **Lobsters** | OSS Infra Hacker, Protocol Cypherpunk | Same as HN, slightly more technical floor. Self-submission norms matter; don't astroturf. | Marketing. Anything resembling a press release. |
| **Mastodon (fediverse)** | Crypto-Skeptical Decentralist, Privacy Activist Builder, OSS Infra Hacker | Quiet, ongoing build updates from real maintainer accounts. Threads about specific design decisions with screenshots/code. Federation/local-first energy. | Crossposted Twitter copy. Hashtag chains. Anything tonally crypto. The fediverse instantly down-ranks Web3 vocabulary; this is enforced socially, not algorithmically. |
| **Twitter / X** | Crypto-Positive Cypherpunk (some), almost nobody else from this cohort | Protocol-research threads with citations. Calm replies in long technical discussions. | Pump posts. "🚀" anything. Anything that touches token price. The OSS / decentralization wing actively *avoids* this channel now. |
| **Nostr** | Crypto-Positive Cypherpunk (Bitcoin-adjacent specifically) | Protocol-level posts. Bitcoin-aligned audience, modest reach but high signal. | Same caveats as Twitter for the non-Bitcoin-aligned subtypes. |
| **Reddit (r/rust, r/selfhosted, r/cryptography, r/privacy)** | OSS Infra Hacker (r/rust), Sovereign Computing (r/selfhosted), Protocol Cypherpunk (r/cryptography), Privacy Activist Builder (r/privacy) | Honest write-ups by real maintainers. AMAs. Bug-hunt updates. | Mod-blockable patterns: drive-by promo, throwaway accounts, "I built X — feedback?" with no actual technical content. |
| **Mailing lists / IETF / IRTF-CFRG / IACR** | Protocol Cypherpunk exclusively | Drafts. Reviews. Specs. Errata. | Anything else. |
| **YouTube / podcasts (self-hosted, BSDNow, Rustacean Station, Bitcoin Audible, ZK Podcast)** | All subtypes, partitioned | Long-form maintainer interviews. Architecture deep-dives. Postmortems. | Promo segments, sponsored reads that sound like ads. |
| **Conference talks (RustConf, FOSDEM, Real World Crypto, zkSummit, Devcon)** | Partitioned by subtype | Talks that ship — meaning, the repo is real and live the day of the talk. | Vaporware decks. |

## 8. Content types that work, applied to Logos / scaffold

These are post / piece ideas that are tonally appropriate for the cohort and concretely producible from the current repo state.

### Type A — The "engineering postmortem / design note"

Cohort takes this seriously. Examples for Logos:

- **"Why we pinned risc0 version X for LEZ — and what we learned about prover RAM."** Lobsters / HN / fediverse / r/rust. Names a primitive, names a tradeoff, treats the reader as a peer.
- **"`lgs run` collapses build → IDL → localnet → deploy. Here's the failure-mode taxonomy we built around it."** Engineering blog + r/rust. Real bugs from the open issue tracker, traced through.
- **"How `program_id` is derived in scaffold, and why image-hash ≠ soundness."** Protocol Cypherpunk audience. Pre-empts the "is `program_id` your security claim?" question.
- **"Replacing `lsof | grep` with a state directory: lessons from porting localnet to Alpine."** Sovereign Computing audience. r/selfhosted, r/rust, fediverse.
- **"Dual MIT/Apache-2.0, no CLA, no telemetry: the three license decisions in scaffold and the reasons for each."** Cypherpunk cohort universally. Short, plain, no manifesto language.

### Type B — The "spec-and-threat-model release post"

When the LEZ spec and threat model ship (a Tier 2 recommendation above):

- **"LEZ threat model, v0.1: in scope, out of scope, and the adversary classes we name."** IACR ePrint cross-post (if it merits one), CFRG / IRTF mailing lists (where relevant), HN, Lobsters.
- **"The single-sequencer decision in LEZ testnet, and the path to decentralized sequencing."** Pre-empts the most-cited yellow flag in this report. Audience: Protocol Cypherpunk + Crypto-Positive.
- **Public RFC threads** ("comment by date X, named reviewers welcome") on specific protocol decisions. Per `03_subtype_protocol_cypherpunk.md`: *"Open peer review in public channels (mailing lists, security workshops)"* is a top trust trigger.

### Type C — The "contributor portrait / maintainer voice"

The cohort respects **named maintainers writing in their own voice** more than it respects any institutional account.

- A periodic "scaffold maintainer notes" on the fediverse from real engineering accounts (not a `@logos` corporate handle). Build status, what got fixed this week, what's blocking, what they're learning. Honest. Dry.
- Maintainer AMAs on r/selfhosted, r/rust, or Matrix/IRC office hours. Per `08_subtype_sovereign_computing.md` §"Trust triggers": *"A maintainer that runs r/selfhosted-style AMAs occasionally."*
- A `MAINTAINERS.md` and `REVIEWERS.md` with real names, real PGP keys, real handles. Then those handles post.

### Type D — The "show-HN that doesn't lie"

When the next milestone ships (e.g. a Tier 2 release that includes `flake.nix`, the new `SECURITY.md`, the README rewrite):

- *"Show HN: logos-scaffold — Rust CLI for risc0 guest programs on a zk execution zone (single-binary, no telemetry, MIT/Apache)"*
- Maintainer in the comments. Tells the truth about what works and what doesn't. Names the sequencer-is-single fact. Names the funding source.
- Per `00_executive_summary.md` §"Strongest messaging directions": *"Here is what this protects. Here is what it does not protect. Here is who it is for."*

### Type E — The "comparison piece" (handle with care)

Comparisons are a strong content type but a high-risk one — get the comparison wrong and you alienate one of the two sides.

- **Safe comparison:** "scaffold vs. Foundry vs. Anchor vs. Hardhat: a developer-ergonomics matrix." Concrete, neutral, focuses on shape.
- **Unsafe comparison:** "Why LEZ is better than [chain X]." Reads as marketing. Closed instantly.
- **Useful comparison for Crypto-Skeptical:** "What LEZ does that signed objects + Waku + Codex can't, and what it can't do that they can." Honest exchange-of-value framing. This is, specifically, the piece that converts the Crypto-Skeptical Decentralist from default-reject to default-curious.

### Type F — The "long-form architecture walkthrough"

Per `04_subtype_oss_infrastructure_hacker.md`: *"A protocol with a reference implementation: you'll run it. You'll write about it. If it's good, you'll send PRs."* The OSS Infra Hacker cohort *writes about* the projects they like. Provide enough material to write with:

- Hour-long YouTube / blog walkthrough by a maintainer: clone, build, run, deploy a counter, inspect `program_id`, read the threat model, point at the open issues. No b-roll, no music, screen recording and a terminal.
- Live-build streams (sparingly — once a month, not weekly).

## 9. What to avoid

Drawn from `09_messaging_matrix.md`. Apply to all Logos surfaces, not just scaffold.

- **"Social movement"** as the headline frame on logos.co's landing page is the single biggest tonal friction with the OSS/decentralization wing. The Crypto-Skeptical persona named it explicitly. **Recommendation:** keep the movement framing for activist audiences, but ensure the *first* link from the GitHub README does *not* land on the movement page — it should land on a technical overview.
- **"Circles" / "203 active contributors / 33 local chapters"** as a metric. This pattern-matches to ambassador programs (per `07_subtype_crypto_skeptical.md` §"Trust destroyers": *"Ambassador program"*). Even if the Circles are genuinely civic-tech reading groups, the *framing* needs to be obviously not-an-ambassador-program.
- **Anything resembling token speculation.** Even neutral language ("our economic design," "treasury management") triggers the speculative-wing pattern-match. Until and unless there is a real token disclosure, the safer posture is: don't talk about tokens at all in scaffold-adjacent channels.
- **"The future of [X]"** framing. Per the messaging matrix: *"Describe the present."*
- **Influencer / KOL launches.** This audience treats endorsement-driven discovery as a trust *destroyer*, not builder.

## 10. A concrete six-week social-content sprint

For a single maintainer-writer pairing, achievable from current repo state:

| Week | Piece | Channel | Persona |
|---|---|---|---|
| 1 | "What is LEZ in 90 seconds" (also goes in the README) | Personal Mastodon / fediverse + dev.to or maintainer blog | All |
| 2 | "Why no telemetry, why dual license, why no CLA" | HN show-HN + r/rust | OSS Infra Hacker, Crypto-Skeptical |
| 3 | "Replacing `lsof | grep`: a state-directory port for local devnets" | r/rust + r/selfhosted + fediverse | Sovereign Computing |
| 4 | "How `program_id` is derived, and what it does and doesn't promise" | Lobsters + ZK Podcast pitch + fediverse | Protocol Cypherpunk, Crypto-Positive |
| 5 | "What we learned writing 23 dogfooding scenarios — testing dev tools as a user, not as a developer" | HN + r/rust + dev.to | OSS Infra Hacker |
| 6 | First "scaffold maintainer notes" (recurring biweekly thereafter) | Maintainer Mastodon account + repo Discussions | All |

None of these require a CMS, none require paid promotion, none require token rhetoric, and all of them are pieces the cohort actively wants to read.

---

## Appendix A — Raw persona excerpts (one quote each, for reviewer recall)

- **OSS Infra Hacker:** *"biggest red flag: README assumes you're already inside the Logos worldview. for a bootstrapping CLI, that is exactly backwards — scaffolding tools are first-contact surfaces. biggest green flag: DOGFOODING.md plus the shape of the open issues. people are using this thing on purpose."*

- **Crypto-Skeptical Decentralist:** *"as a Rust CLI, this is clean. If someone handed me this file tree with the word 'Logos' scrubbed out, I would not flinch. … The single thing I'd remove first: the Anchor-on-Solana comparison."*

- **Protocol Cypherpunk:** *"scaffold itself is competently engineered Rust tooling — well-scoped, ADRs present, no telemetry, dual-licensed, no CLA. I have no complaint with the CLI. My complaint is that the system it bootstraps is, from this vantage, a black box wearing a friendly Anchor-shaped hat."*

- **Crypto-Positive Cypherpunk:** *"Net: tool is clean, org-level signaling is thin, easily fixable. I'd revisit on v0.2 if the README grows a spec link, a sequencer paragraph, and a funding sentence."*

- **Sovereign Computing self-hoster:** *"telemetry-off, MIT/Apache, no CLA, honest about Unix-only — that's four green flags before breakfast. Not my tool today. Could be in two releases."*

---

## Appendix B — Method note

This assessment was produced by:

1. Reading the persona dossier in this repository (`00_executive_summary.md` through `10_contribution_matrix.md`).
2. Inspecting the public state of `logos-co/scaffold` (README, CONTRIBUTING.md, SECURITY.md, ADR.md, FURPS.md, DOGFOODING.md, Cargo.toml, issues, PRs, releases, org context via logos.co).
3. Running five independent persona simulations as subagents (OSS Infra Hacker, Crypto-Skeptical Decentralist, Protocol Cypherpunk, Crypto-Positive Cypherpunk, Sovereign Computing self-hoster). Each subagent was loaded only with its own persona dossier and the public-state facts above, and asked to produce a 400–900-word reaction in the persona's voice.
4. Synthesizing convergences (where multiple personas independently flagged the same finding) and divergences (where audiences split). Convergences became the recommended changes; divergences became audience-positioning notes.

The intent of the persona-simulation step is to surface findings that a single neutral analyst would not — specifically, the gap between *what the project says* and *what cohort members hear when they read it*. The five simulations broadly agreed on the diagnoses, which raises confidence that the recommendations are not artifacts of any one persona's bias.

Findings flagged by only a single persona are reported as such (see §3 "Divergences") and weighted accordingly in the prioritization.
