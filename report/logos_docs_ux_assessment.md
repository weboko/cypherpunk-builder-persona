# UX Assessment: `logos-co/logos-docs`

*A persona-driven UX investigation of [github.com/logos-co/logos-docs](https://github.com/logos-co/logos-docs) using the Cypherpunk Builder dossier in this repository. Findings are aggregated from four independent simulated readings — Protocol Cypherpunk, OSS Infrastructure Hacker, Crypto-Skeptical Decentralist, and Sovereign Computing self-hoster — and filtered to the changes that materially move adoption, contribution, and trust.*

*Repository state at the time of review: 45 open issues, 14 open PRs, 107 closed PRs, MIT license (Institute of Free Technology, 2025), 5 docs subfolders with content (apps, blockchain, connect, storage, plus the contributing scaffolding), Messaging marked "We're working on the content" and **excluded from this review per instructions to skip software that is not public-ready**. Active commits Mar–May 2026.*

*Software in scope for this review:*
- *Logos Blockchain node (CLI quickstart; binary tarball install)*
- *Logos Execution Zone (LEZ) wallet CLI + sequencer (build-from-source quickstart, transfer tutorials, custom-token tutorial, AMM sample app)*
- *Logos Storage (linked out to `logos-storage-docs.netlify.app`; not authored in this repo)*
- *AnonComms Mixnet demo (chat-UI + Waku + mixnet via `nix run '.'`)*
- *Logos App (linked out to `github.com/logos-co/logos-app`; build instructions not in this repo)*
- *The docs workflow itself: `CONTRIBUTING.md`, the `journeys.logos.co` sidecar app, templates, writing rules, labels, the Red Team.*

---

## 1. Summary in one paragraph

`logos-co/logos-docs` is a docs repository in the middle of an organizational consolidation — three previously separate projects (Nomos, Codex, Waku) being unified as Logos Blockchain, Logos Storage, and Logos Messaging. The contributing workflow is unusually grown-up for a project this early: a six-phase board, a state-machine sidecar app at `journeys.logos.co`, an SME-and-Red-Team quality ladder, an `area:*`/`quality:*`/`type:*`/`status:*` label taxonomy, an explicit MIT license with no CLA, and honest "early draft" disclaimers on every journey. All four personas registered this as a *real* docs operation, not a marketing site cosplaying as one. The repository earns first-pass trust as institutional infrastructure work. What it does not yet earn — for any of the four subtypes — is *substantive* trust as a source of truth about the software it documents. The reasons are convergent: **no threat model anywhere in the repo**; eleven 0-byte README files including the ones `CONTRIBUTING.md` points at as the source of writing rules and templates; a published "journey" (`anoncomms`) still in raw R&D doc-packet shape; an identical "this may not run as written" disclaimer on every page; a single sample app whose subject is an AMM; a `wget`-the-binary install path with no checksums or signatures; and a half-finished rename leaking the previous codename `NSSA` into a user-facing environment variable. None of these are fatal. All of them are cheap to fix relative to their impact on trust. The cohort would update significantly on a small number of targeted changes: a `SECURITY.md` per module, the writing-rules file actually written, signed and checksummed release artifacts, and the anoncomms journey rewritten as a journey rather than as the intake template it currently is.

---

## 2. Where the personas converged

These findings appeared independently in three or four of the four readings.

### Convergence 1 — There is no threat model

**Personas: all four (loudest from Protocol Cypherpunk and Crypto-Skeptical).**

There is no `SECURITY.md`, no `THREAT_MODEL.md`, no `docs/security/` subtree, no "What this does not protect against" page anywhere in the repository. The README claims "privacy is built in from the ground up" (`README.md:15`); the blockchain quickstart claims "private validator identity via local leadership election with ZKPs"; the LEZ docs introduce ZK proofs, nullifiers, and viewing keys. None of these are tied to a named adversary class.

The closest the repo gets is a single-line `Security / safety notes: None` in the AnonComms doc (`discover-nodes-and-send-messages-via-the-anoncomms-mixnet-demo-app.md:133`) — for a mixnet, whose entire purpose is anonymity. The Protocol Cypherpunk read it as the most damaging line in the repo: *"`None` is not a threat model; it's a placeholder."*

This is the single highest-leverage gap in the entire docs surface. Every other finding below is secondary to this one. From `02_simulation_card_general.md`: the cohort's evaluation order is *threat model → architecture → implementation → community → governance → marketing*. The repo currently has nothing for the cohort to read at step 1.

### Convergence 2 — Eleven 0-byte README files, including two referenced from `CONTRIBUTING.md`

**Personas: Protocol Cypherpunk, OSS Infrastructure Hacker.**

Inventory verified by `wc -c`:

```
0 /tmp/logos-docs/docs/README.md
0 /tmp/logos-docs/docs/apps/README.md
0 /tmp/logos-docs/docs/blockchain/README.md
0 /tmp/logos-docs/docs/connect/README.md
0 /tmp/logos-docs/docs/core/README.md
0 /tmp/logos-docs/docs/messaging/README.md
0 /tmp/logos-docs/docs/storage/README.md
0 /tmp/logos-docs/docs/_shared/README.md
0 /tmp/logos-docs/resources/writing-rules/README.md
0 /tmp/logos-docs/resources/templates/README.md
0 /tmp/logos-docs/.github/pull_request_template.md
```

`CONTRIBUTING.md` links to two of these (`resources/writing-rules/README.md` and `resources/templates/README.md`) as the source of writing rules and the source of canonical templates. Both targets are empty. Issue #246 ("Empty docs/**/README.md files — keep, populate, or delete?") shows the team is aware. As the OSS Infra Hacker put it: *"the documentation equivalent of a 404 inside your own onboarding flow."*

The `.github/pull_request_template.md` being 0 bytes is independently noted as the cheapest of all fixes — five lines of yaml/markdown is twenty minutes — and the failure to ship it is a strong signal of priorities, not capacity.

### Convergence 3 — `CONTRIBUTING.md` describes five canonical templates; the repo contains zero

**Personas: Protocol Cypherpunk, OSS Infrastructure Hacker.**

`CONTRIBUTING.md` declares five canonical templates (Quickstart, Procedure, Concept, Reference, Troubleshooting), describes them in detail, and explicitly states using one is "mandatory before writing." The `resources/templates/` directory contains exactly two markdown files: `doc-packet.md` (an R&D *intake* form, not a writer's template) and `doc-fix-or-request.md` (an issue template).

A literal unresolved comment in `CONTRIBUTING.md:15` acknowledges this: `<!-- TODO: Add final templates links once all resources are committed. -->`. From the OSS Infra Hacker's notes: *"the contributing guide tells me to read the rules; the rules file does not exist. ... The honest move would be a banner in `CONTRIBUTING.md`: 'Templates not yet committed. Until then, mirror an existing journey — see X.' That's not there."*

The gap between described process and shipped artifact is the single most credibility-damaging structural problem in the repo. The workflow described is sophisticated and forward-looking; the artifacts described are mostly aspirational. A first-time external contributor cannot follow `CONTRIBUTING.md` because the files it points at are blank.

### Convergence 4 — The AnonComms journey is the doc-packet template, not a journey

**Personas: Protocol Cypherpunk, OSS Infrastructure Hacker.** (Crypto-Skeptical and Sovereign Computing didn't flag the structural problem because they were reading the content.)

`/docs/connect/anoncomms/journeys/discover-nodes-and-send-messages-via-the-anoncomms-mixnet-demo-app.md` is structured `A. Outcome + value` / `B. Scope + ownership` / `C. Runnable happy path` / `D. Configuration` / `E. Hardware requirements` / `F. Verify + troubleshoot` / `G. Limits for v0.1` / `H. References`. That is verbatim the doc-packet template's headings (`resources/templates/doc-packet.md`).

This is the workflow described in `CONTRIBUTING.md` failing visibly. The R&D handoff happened; the Docs-team transformation into a Quickstart or Procedure structure did not. From the OSS Infra Hacker: *"As an evaluator I now know the workflow has a non-zero failure-to-transform rate, and the failure mode is visible to readers."* From the Protocol Cypherpunk: *"the doc that introduces me to your anonymity story is literally a labelled draft of an R&D handoff form. Of all surfaces to publish in raw intake form, the mixnet one is the worst choice."*

Worth noting: the Crypto-Skeptical persona, reading the same doc for *content*, identified it as **the strongest artifact in the repo for the decentralization-minded subtype** — a real mixnet demo with libp2p + capability discovery + `nix run '.'`, no chain, no token, real spec links. The page that is most credible for the most skeptical audience is also the page that is structurally the most broken. That's a high-stakes fix.

### Convergence 5 — The "early draft" disclaimer epidemic

**Personas: all four.**

Every single journey opens with a near-identical IMPORTANT block:

> "This page is an early draft and may be incomplete or incorrect. Expect changes, missing prerequisites, and commands that might not work in your setup. We are actively working to complete and verify this content."

The LEZ wallet quickstart varies it slightly to *"may not have been run end-to-end as written"* — which the OSS Infra Hacker noted is actually worse: it admits the team has not run their own Quickstart end-to-end, *and ships it anyway*.

How the personas read it:

- **Protocol Cypherpunk:** Honest-but-procedural. The `quality:stub` / `quality:unverified` / `quality:sme-verified` / `quality:verified` ladder in `CONTRIBUTING.md` is the right shape, but applying identical boilerplate uniformly across pages means the taxonomy isn't doing work yet.
- **OSS Infra Hacker:** *"identical boilerplate across N pages is one of two things — (a) somebody got told by legal/comms to add an admonition and ran a sed across the directory, or (b) the docs are being shipped to hit a milestone before the underlying software is stable. Either way: the maintainers know the docs aren't reliable, ship them anyway, and put the risk on the reader."*
- **Sovereign Computing:** *"honesty doesn't paper over the gaps."*
- **Crypto-Skeptical:** Did not flag explicitly but reads the pattern as part of the project's general "shipping ahead of readiness" posture.

All four agreed that the right fix is to **replace the prose disclaimer with a visible quality badge** that maps to the existing `quality:*` taxonomy. Same information, less learned-helplessness, upgradeable per-doc as Red Team verification completes.

### Convergence 6 — Naming friction and the half-finished rename

**Personas: all four.**

In a single clone-build-run, a reader has to hold the following naming systems simultaneously:

- Three GitHub orgs: `logos-co` (docs), `logos-blockchain` (chain code), `logos-messaging` (some specs).
- The Notion workspace `nomos-tech/` — still using the old project name — hosts the hardware requirements page that the blockchain quickstart links to (`docs/blockchain/quickstart-guide-for-the-logos-blockchain-node.md:29`).
- Three brand renames in progress: Nomos → Logos Blockchain, Codex → Logos Storage, Waku → Logos Messaging.
- The user-facing environment variable `NSSA_WALLET_HOME_DIR` and the home directory `~/.nssa/wallet/storage.json`. **`NSSA` is never expanded anywhere in the user-facing docs.** It is a leaked internal codename.
- The wallet quickstart even calls out a bug in its own help text about this variable (`quickstart-for-the-logos-execution-zone-wallet.md:200`).
- Distinct config-dir conventions on the same host: `~/.nssa/wallet` vs. `~/.logos-blockchain-circuits`.
- Three press-vs-spec subdomains: `press.logos.co` (the README's main outbound link for architecture concepts), `lip.logos.co/ift-ts/raw/...` (the actual specs, only linked from one journey), `testnet.blockchain.logos.co` (faucet + explorer).
- Internal product names with overlapping abbreviations: LEZ (Logos Execution Zone), LEE (Logos Execution Environment), LP (LibP2P Peer *and* Liquidity Provider).

`README.md:76` acknowledges the rebrand explicitly: *"Legacy names may still appear in repositories and specifications, but going forward the Logos-first names will be used across our docs."* That is the right honesty, and worth points. **What is missing is a single name-translation table** that maps old → new → repo URL → planned-sunset-date. The Protocol Cypherpunk read the `NSSA` leak as diagnostic: *"a freshly renamed product still leaking the previous code-name through environment variables is the kind of thing that means the rename happened in marketing before it happened in engineering."*

### Convergence 7 — Reproducibility, checksums, and signed releases are absent

**Personas: Protocol Cypherpunk, OSS Infrastructure Hacker, Sovereign Computing.**

The blockchain quickstart asks the reader to `wget` a tarball from `github.com/logos-blockchain/logos-blockchain/releases/...`. The LEZ wallet quickstart asks the reader to pipe-curl-to-shell *twice* (`sh.rustup.rs`, `risczero.com/install`) and to run `./scripts/setup-logos-blockchain-circuits.sh` which fetches another tarball. Nowhere is there:

- A `sha256sums.txt` next to a release.
- A GPG / minisign / cosign signature.
- A reproducible-build statement.
- A "verify your tarball before running it" snippet.
- A `flake.nix` or `Dockerfile` in the LEZ or blockchain repos.

This intersects with **Convergence 1 (threat model)** in a damaging way: the `~/.logos-blockchain-circuits` archive contains the *ZK circuits* whose correctness is the entire trust root for private execution. The Protocol Cypherpunk's read: *"a ZK system whose circuits are downloaded as opaque blobs from a GitHub release with no verification instructions and no reproducibility story is a system that cannot be trusted, regardless of the underlying math."*

The Sovereign Computing persona's read: *"the whole pitch of a privacy-preserving Proof-of-Stake chain rests on operator key handling, and the install instructions are 'download this binary off the internet and run it.'"*

The AnonComms demo, by contrast, ships with `nix run '.'`. The contrast is jarring and tells the reader that **someone in this org knows how to ship binaries properly**, which makes the absence of equivalent rigor in the LEZ and blockchain quickstarts read as a choice or a capacity issue, not an oversight.

### Convergence 8 — `press.logos.co` is substituted for specs

**Personas: Protocol Cypherpunk, Crypto-Skeptical.**

The README's architecture paragraph and the blockchain quickstart both link to `press.logos.co/article/why-proposer-anonymity` for both Cryptarchia and Blend. **The same URL twice, for two different primitives.** No paper, no IACR ePrint, no IETF/CFRG draft, no named cryptographer.

The AnonComms doc gets this right: it links `lip.logos.co/ift-ts/raw/extended-kad-disco.html`, `lip.logos.co/ift-ts/raw/mix.html`, and `github.com/logos-messaging/specs/blob/master/standards/core/mix.md`. Real specs, with URLs. These are the strongest links in the entire docs repo and they are buried in section H of one journey. They should be in the README architecture section.

Protocol Cypherpunk's read: *"A press article is not a spec."* Crypto-Skeptical's read: *"Replace the `press.logos.co/article/why-proposer-anonymity` link in the blockchain quickstart with a link to the actual Cryptarchia paper or spec. The `lip.logos.co` links in the AnonComms doc set the right standard; the blockchain doc should match it."*

### Convergence 9 — The README's headline framing overshoots what the docs deliver

**Personas: all four.**

The README leads with *"Logos is a modular technology stack for building local-first, decentralised applications"* (`README.md:5`) and the **Linux distribution analogy** (`README.md:7`). Within twenty lines the reader has been introduced to AMMs, "native tokens," staking keys (later), a faucet (later), and a Piñata branding callout.

Each persona's mismatch was different but pointed in the same direction:

- **Crypto-Skeptical:** "Local-first" means Hypercore / automerge / Ink & Switch, not "a UTXO chain plus zones plus a sequencer plus circuits plus a faucet plus an LP-token tutorial." The phrase is doing work it can't pay for.
- **Sovereign Computing:** The README explicitly markets *"the headless Logos Node ... ideal for validators, infrastructure operators, or backend services"* — but no headless-Node journey exists in the docs. The same file that promises the artifact also fails to deliver a table-of-contents entry for it.
- **Protocol Cypherpunk:** *"the README runs straight into a Linux-distribution analogy before naming a single primitive. That's the wrong order for this audience."*
- **OSS Infra Hacker:** *"The first thing the repo does is send me off the repo."* (After the analogy, the README routes to `logos.co`, the Logos App build instructions on a different repo, the Storage docs on a Netlify site, the chain repo on a different GitHub org, and Notion. Five domains and two orgs in five minutes.)

The composite finding: **the README is structured for a reader who already knows what Logos is. The docs root assumes the marketing site.** A self-contained README that names the threat model, names the architecture, links to specs (not press posts), and stands alone is what each subtype's evaluation method demands.

---

## 3. Where the personas diverged — and what to do about it

Divergences are useful: they show where the audience boundary the project is straddling actually lives.

### Divergence A — The AMM sample-app tutorial

- **Crypto-Skeptical:** Strongly negative. *"They picked an AMM. Not a private group chat. Not a censorship-resistant publishing tool. ... That is the crypto-native UX pattern par excellence."* Reads it as diagnostic of whose mental model shaped the prioritization (people who came up through DeFi).
- **Protocol Cypherpunk:** Notes the AMM tutorial indirectly via the `wallet token` and `wallet amm` primitives; treats it as a vehicle for exercising the LEZ programming model, not as suspicious in itself. Wants to see the Aleo/Zexe-lineage spec referenced.
- **OSS Infra Hacker:** Indifferent — the AMM tutorial is one of many docs; not their primary concern.
- **Sovereign Computing:** Indifferent — outside their use case.

**Verdict:** The AMM tutorial can live in the docs. **Where it sits is the problem.** Today it is one of four LEZ wallet-section bullets in the README, and the only bullet under "sample apps." A non-DeFi-native reader who lands on it as the *canonical* example of "what you do with LEZ" rebuckets the project as a DeFi project. A second sample app — a private credential, a private auction, a metadata-resistant payment to a journalist, or an anonymous attestation — placed *alongside* the AMM would let the same docs serve both audiences without forcing a re-write of the AMM page. Cost: one new journey. Effect: substantial widening of who recognizes themselves in the docs.

### Divergence B — Private Proof of Stake (PPoS / Cryptarchia)

- **Crypto-Skeptical:** Reads PoS as token-economic gating; concedes private validator identity is a substantive cryptographic contribution; nets out at *"the cryptography is interesting; the role it's deployed in is the part I'm skeptical of."*
- **Protocol Cypherpunk:** Wants the paper. The press-post substitution is unacceptable. The construction itself sounds plausible but cannot be evaluated without the spec.
- **Sovereign Computing:** Tolerant — runs Ethereum validators, accepts PoS, finds proposer anonymity intellectually interesting.
- **OSS Infra Hacker:** No strong view.

**Verdict:** PoS is going to lose the Crypto-Skeptical subtype regardless of presentation; nothing the docs say can make a Proof-of-Stake design appeal to a reader whose null hypothesis is "money should not be a credential." **The fixable problems are the *presentation* problems**: link to the Cryptarchia paper, not the press article; name the proving system (RISC Zero, STARK-based, FRI) on the architecture page; describe the leadership-election circuit with enough specificity that a Protocol Cypherpunk can evaluate the soundness claim.

The Crypto-Skeptical reader can be retained for the *mixnet and storage layers* if those are visibly separable from the chain. See Recommendation 5 below.

### Divergence C — The `journeys.logos.co` sidecar app

- **OSS Infra Hacker:** Sharp, mixed. *"As engineering: someone built a sidecar workflow app to keep GitHub issues consistent with a hand-rolled state machine. That's an honest response to GitHub Projects being weak."* But: *"The 'Fix Labels' button exists because the state machine drifts often enough that a manual reconciliation button was worth shipping ... This is a kanban for an internal team. The external contributor is bolted on."*
- **Protocol Cypherpunk:** Process-first culture, artifact-thin so far. Forward-looking infrastructure.
- **Other two:** Did not weigh in.

**Verdict:** The sidecar app is real engineering work and worth respect. **The fixable problem is that none of its state — the `status:*` labels, the `blocked-by:*` labels, the milestones — is meaningfully actionable for an external contributor.** A short `CONTRIBUTING.md` subsection titled "What the labels mean for *you* if you're outside the project" would help. Right now read-access to a kanban you have no agency in is spectator mode.

### Divergence D — The Linux-distribution analogy

- **Crypto-Skeptical:** *"The analogy is doing the rhetorical lifting of 'we're plumbing, like Linux is plumbing' while the actual default profile puts a chain in the base distribution. ... If I'm reaching for the Linux analogy, the chain should be `apt install logos-chain` — clearly optional, clearly one tool among many."*
- **Sovereign Computing:** Reads it neutrally — "modular stack, swap modules in and out, fine."
- **OSS Infra Hacker:** Mildly skeptical — *"Either you understand Linux and you don't need the analogy, or you don't and the analogy is doing none of the work."*
- **Protocol Cypherpunk:** Wants primitives, not metaphors. Reads the analogy as marketing.

**Verdict:** Two of four read the analogy as overreaching, one reads it as neutral, one wants it gone. Three changes would resolve most of the friction without losing the framing:

1. Rephrase as "modular *like* Linux is modular" — keep the architecture point, drop the "you already know how this works" assertion.
2. Or commit to the analogy by **removing the chain from the default profile** and shipping it as one optional module among many.
3. Or replace the analogy with a one-sentence direct statement of what Logos is.

Option 3 is cheapest. Option 2 is the strongest move with this audience but is a real product decision, not a docs decision.

---

## 4. Software-specific findings

### Logos Blockchain node (the most important file in the repo for the Sovereign Computing persona)

The blockchain quickstart (`docs/blockchain/quickstart-guide-for-the-logos-blockchain-node.md`) is the operator-facing entry point. Two persona reactions of note:

- **Sovereign Computing:** *"The ARM-native tarball and the explicit Raspberry Pi 5 mention are the single biggest reason I kept reading."* This is a real green flag from the homelab audience. Worth preserving and surfacing.
- **Same persona, harder:** The "Known limitations" section states that *"If the node is restarted while bootstrapping, it does not save sync progress and will restart from the beginning,"* combined with a stated 12-to-24-hour bootstrap. *"A home lab box gets restarted. ... Twenty-four hours of sync wiped because of a power blip is not a 'limitation,' it is a non-starter for unattended operation."*

Other findings from this file:

- **No systemd unit, no Compose file, no documented service supervision.** The README markets "headless Logos Node" but the quickstart's runtime model is "open a terminal and run the binary." This is the single largest "promise vs. delivery" gap in the repo.
- **Hardware requirements live in Notion.** `https://www.notion.so/nomos-tech/Hardware-Requirements-1fd261aa09df81a4a52be19e90b60891` — a Notion URL, on the *old project* workspace name, linked from a public docs page that claims to be the source of truth.
- **Bandwidth requirements are listed as "No specific requirements"** for a global libp2p+QUIC chain node. Read by the persona as "not measured."
- **Network port discovery is implicit.** The node uses `8080` (HTTP API) and `3000`-`3003` UDP (libp2p QUIC). The LEZ sequencer uses `3040`. The AnonComms demo uses TCP `60000`. There is no "Ports and network" reference page in the repo. For a multi-tenant homelab, this is felt.
- **No backup story for `user_config.yaml`.** The file holds the staking keys. The doc does not say "back this up before exposing this node to a network." Single-paragraph fix, very high-leverage.
- **Single bootstrap-peer IP block (`65.109.51.37`, a Hetzner address) for four ports.** Censorship-resistance discussion that doesn't appear: a single AS hosting the bootstrap nodes is itself a centralization concern worth one sentence.

### Logos Execution Zone (LEZ) wallet quickstart and tutorials

The LEZ wallet quickstart (`quickstart-for-the-logos-execution-zone-wallet.md`) is the second most-read file by the personas. Findings:

- **The `NSSA_*` leak** discussed under Convergence 6. Wallet env var and home dir use a project codename never expanded user-facing. The quickstart even documents a bug in the binary's help text about this variable. The honest move is acknowledged; the underlying naming inconsistency is not yet fixed.
- **Build-from-source is the only documented path.** `cargo install --path wallet --force` after cloning two repos and running `setup-logos-blockchain-circuits.sh`. No prebuilt LEZ wallet binary. No Docker image. No Nix flake. Acceptable for an alpha; not aligned with the README's "Linux distribution" framing.
- **Two `curl | sh` installs in the quickstart** (`sh.rustup.rs`, `risczero.com/install`). For a project that markets privacy and trust-minimization as core values, this is a category error. Even a parenthetical "you can verify the rustup signature with X" would help.
- **The "circuits required even for public transactions" admission** (`quickstart-for-the-logos-execution-zone-wallet.md:122`): *"the current `wallet` build still requires these files to be present locally"* even for the public-only Quickstart flow. Honest, and a yellow flag — the public/private split at the build level is less clean than the architecture description suggests.
- **The viewing-key / nullifier-key vocabulary is Sapling/Orchard lineage.** Say so. Cite Zcash. Don't make the reader infer the cryptographic family from a CLI flag (`--to-npk` / `--to-vpk`).
- **The LEZ sequencer is a centralization point.** The wallet posts to `localhost:3040` in the quickstart, but in production a sequencer is a real role with real metadata visibility. The architecture-level discussion of "what does the sequencer learn, and what does that mean for the privacy claim" is absent.

### LEZ AMM sample-app tutorial

Discussed at length under Divergence A. The AMM tutorial reads cleanly as a Uniswap-V2 walkthrough. Line 19 acknowledges fee support is on the roadmap. The Crypto-Skeptical persona's verdict: it is the canonical "what to do with LEZ" example in a slot that, structurally, broadcasts whose hands shaped the prioritization. The fix is not to remove it; the fix is to ensure it is **not the only sample app** and not the headline example.

### AnonComms / Mixnet demo

The strongest content artifact in the repo for the Crypto-Skeptical and Protocol-Cypherpunk subtypes. Real `lip.logos.co` spec links, `nix run '.'` install, libp2p + capability discovery + mixnet, no chain in the call path. Also the most structurally broken artifact: published in raw doc-packet shape (`A. / B. / C. / D. ...`) rather than as a Quickstart or Procedure. The single most credibility-leveraging fix in the entire repo is to **rewrite this as a journey** using the LEZ wallet quickstart's structure as the template.

Specific gaps in the AnonComms doc beyond the structural one:

- *"Security / safety notes: None"* (line 133) for a mixnet demo. The word "None" should be replaced with at minimum a statement of out-of-scope adversaries (global passive observer, sybil attack, intersection attack over time, cover-traffic absence).
- TCP port `60000` for discovery; "improved if reachable externally even behind a NAT." A self-hoster wants to run a relay; the doc does not let them. A second journey — "Run a mix relay on a server" — would unlock the strongest single contributor funnel for the cohort.
- Known failure: orphaned `logos_host` processes requiring `pkill -f logos_host`. A process supervisor would fix this. None is suggested.

### Logos Storage

Documentation lives at `logos-storage-docs.netlify.app` and is not authored in this repo. The repo links to two tutorials there. **The OSS Infra Hacker noted the off-site hosting as a leak** — a docs repo that links out to a Netlify site for one of its three foundational modules is, in form, a portal page. This is not a fatal critique; it is a noted inconsistency. If the storage docs cannot be moved into this repo, a one-paragraph synopsis ("What Logos Storage is, what it isn't, what its trust assumptions are") at `docs/storage/README.md` (currently 0 bytes) would close the gap without requiring a migration.

### Logos App

External — lives at `github.com/logos-co/logos-app`. Build instructions not in this repo. As above for Storage: the empty `docs/apps/README.md` could carry a one-paragraph intro plus a link.

### Messaging

**Excluded from this review per the original instruction to skip software not public-ready.** README explicitly states "We're working on the content." The personas did not evaluate Messaging content. Note however that `docs/messaging/README.md` is a 0-byte file alongside the others in Convergence 2; the cohort would expect a placeholder note ("In progress; planned for 2026Qx; tracked at #XX") rather than an empty file.

---

## 5. The recommended changes, prioritized by impact and cost

Each change is annotated with: which personas it unlocks, cost in maintainer-time, and the trust mechanism from the dossier it activates.

### Tier 1 — Do this week. Cheap, high-leverage.

**1. Write `SECURITY.md`, even as a v0.** *(All four personas. Cost: a senior engineer-day. Activates trust trigger "A clear, honest threat model — explicit about which adversaries are in and out of scope" — `00_executive_summary.md`.)*

One page. Name the modules (Blockchain, Storage, Mixnet, LEZ wallet). For each, list:

- In-scope adversaries (passive network observer, active attacker on libp2p, malicious validator subset, malicious sequencer, malicious prover, ...).
- Out-of-scope adversaries (compromised endpoint, OS-level malware, supply-chain on the rustup install, global passive observer until cover traffic ships, ...).
- Known metadata leaks (sequencer-level metadata, libp2p peer-id correlation, on-chain-commitment timing, ...).
- Disclosure address with a PGP or age key.

This single change moves the repo from "claims privacy" to "specifies what privacy means here." Without it, every other crypto claim reads as marketing.

**2. Fill in `resources/templates/README.md` and `resources/writing-rules/README.md`, or remove the links to them from `CONTRIBUTING.md`.** *(Protocol Cypherpunk + OSS Infra Hacker. Cost: half a tech-writer-day to ship a v0 of each, twenty minutes to remove the links. Activates "real and not-padded `CONTRIBUTING.md` and `ARCHITECTURE.md`" — `00_executive_summary.md`.)*

Pick one. The current state — `CONTRIBUTING.md` references "writing rules" and "canonical templates" that point to 0-byte files — is the single most credibility-damaging artifact for the cohort. If the full rules aren't ready, ship a v0 page that says: *"Until the full rules ship, mirror `docs/apps/wallet/journeys/quickstart-for-the-logos-execution-zone-wallet.md`. See `<linked PR>` for the rules in progress."* Resolve the `<!-- TODO -->` in `CONTRIBUTING.md:15` as part of this PR.

**3. Write `.github/pull_request_template.md`.** *(OSS Infra Hacker. Cost: 20 minutes.)*

Five lines: linked issue, what changed, did you run the linters, target quality level, doc type. Zero bytes today.

**4. Convert the AnonComms doc from doc-packet (`A. / B. / C. / D. ...`) to a Quickstart structure.** *(Protocol Cypherpunk + OSS Infra Hacker; benefits Crypto-Skeptical by surfacing the strongest content. Cost: half a tech-writer-day.)*

Mirror the LEZ wallet quickstart's frontmatter and `## Step 1 / ## Step 2` structure. Keep all the existing content (it's good). Replace "Security / safety notes: None" with at minimum "Out of scope: global passive adversary; sybil resistance; cover traffic — see [link to mixnet threat model section of `SECURITY.md`]." This is the page the project's most skeptical audiences will judge it by; right now it is structurally an intake form.

**5. Add `sha256sums.txt` and a signing-key statement to every release in `logos-blockchain/logos-blockchain` and `logos-blockchain/logos-execution-zone`, and add a "verify the tarball" snippet to the quickstarts.** *(Protocol Cypherpunk + OSS Infra Hacker + Sovereign Computing. Cost: an hour of CI work plus a paragraph in each quickstart.)*

Trust trigger: "Reproducible builds and runnable-locally instructions. No theoretical sovereignty." Without checksums or signatures, the install paths fail the most basic test the cohort applies to any binary it is asked to run on its own machine.

### Tier 2 — Do this month. Higher-impact, more work.

**6. Replace the "early draft" boilerplate disclaimer with a visible quality badge.** *(All four personas. Cost: a half-day for design + a search-and-replace.)*

Render the existing `quality:*` taxonomy at the top of each journey as a one-line badge: *"Quality: unverified — no SME has confirmed this page"* with a link to a one-paragraph explainer. This converts learned-helplessness boilerplate into an upgradeable signal. As Red Team verification completes, badges flip to `sme-verified` and `verified`. The cohort respects this kind of visible, incremental rigor.

**7. Move "Hardware Requirements" out of `notion.so/nomos-tech/` into this repo, and add a "Ports and network" reference page.** *(Sovereign Computing + Protocol Cypherpunk. Cost: half a tech-writer-day.)*

The Notion link is doubly bad: a public docs page sending readers to a gated SaaS *on the old project's workspace name*. Pull the content into `docs/blockchain/reference/hardware.md` (or equivalent). Add a second reference page enumerating every TCP/UDP port the full stack opens. Multi-tenant homelab readers need this.

**8. Ship a `systemd/logos-blockchain-node.service` and a `docker-compose.yml` for the node** (either in the release artifact or in a sibling `logos-blockchain/deploy` repo), linked from the blockchain quickstart. *(Sovereign Computing. Cost: a few days of an SRE.)*

`Restart=on-failure`, `StateDirectory=logos`, `User=logos`, `ProtectSystem=strict`. This is the single change that converts the node from "a thing you run on a laptop" to "a thing you run on infrastructure" — i.e., closes the gap between the README's headline ("ideal for validators, infrastructure operators, or backend services") and the quickstart's reality (`./logos-blockchain-node user_config.yaml` in a terminal).

**9. Fix the "no resume on bootstrap restart" known limitation, or document a sync-state snapshot workaround.** *(Sovereign Computing. Cost: an engineering effort or a documented workaround.)*

Until this is fixed, the 12-to-24-hour bootstrap makes unattended operation impossible on commodity home networks. A documented "here's how to snapshot a synced node and seed others" workaround is acceptable in the interim.

**10. Write a one-paragraph backup callout in every quickstart.** *(Sovereign Computing. Cost: an hour.)*

Which files are sensitive (`user_config.yaml`, `~/.nssa/wallet/storage.json`), where they live, what `restic` / `borg` should target, what happens if they are lost. Three sentences per page. Single most-cost-effective fix in the entire repo and currently absent.

**11. Replace `press.logos.co` links in the README and blockchain quickstart with `lip.logos.co` and paper / spec links.** *(Protocol Cypherpunk + Crypto-Skeptical. Cost: an hour, plus whatever effort is needed if some specs aren't published yet.)*

If a primitive doesn't have a spec yet, write a stub page in this repo titled "Cryptarchia spec (in progress)" with the assumptions, the cryptographic family (e.g., "STARK-based ZK using RISC Zero, FRI-based, post-quantum-curious"), the proving system parameters, and the open questions. The cohort respects a clearly marked work-in-progress spec more than a press post used as a spec substitute.

### Tier 3 — Do this quarter. Strategic moves.

**12. Ship a single name-translation table** mapping Nomos / Codex / Waku / NSSA / `nomos-tech/` → their Logos-era counterparts, with planned sunset dates. *(All four. Cost: a half-day.)* Place it in `docs/reference/naming-migration.md` and link from the README.

**13. Fix the `NSSA_*` leak in the wallet binary itself.** *(All four. Cost: an engineering effort.)* Rename to `LOGOS_WALLET_HOME_DIR` and `~/.logos/wallet/`. The doc-level acknowledgment is honest but does not substitute for the engineering fix.

**14. Add a non-DeFi sample-app journey to LEZ.** *(Crypto-Skeptical primarily; benefits the wider cohort.)* A private credential proof, a private auction, a private vote, or a metadata-resistant payment to a journalist. The AMM tutorial stays; this sits alongside it. The slot says: *we know who the privacy-preserving execution model is for, and it isn't only DeFi.*

**15. Write a one-page "Why a chain is in the stack" passage.** *(Crypto-Skeptical; benefits Protocol Cypherpunk.)* Named cryptographic and economic guarantees that the chain provides and that a Hypercore log, a CRDT, a federated ledger, or libp2p pubsub cannot. **Acceptable answer: "The chain serves the financial-primitive use case; the messaging, storage, and mixnet modules do not depend on it."** That admission would convert the framing problem from a credibility leak into a clarification.

**16. Disclose the funding and token situation explicitly.** *(Crypto-Skeptical primarily.)* One of:
- "There is no Logos token. The project is funded by IFT grants. The testnet 'native tokens' are non-economic units and will not be sold." Or:
- A sober token-plan disclosure: allocations, vesting, the launch posture, the IFT-Status-treasury relationship.

Silence on this question is currently doing the work of the worst-case disclosure for the cohort. Either explicit posture is better than the current ambiguity.

**17. Add an external-contributor promotion path to `CONTRIBUTING.md`.** *(OSS Infra Hacker.)* Right now the wall is hard: external contributors get "fix or improve existing docs"; "write new docs" is gated to core contributors. Document a named route — three reviewed fixes earns a Red Team trial; an SME nomination process for external experts — even if the bar is high. The current wall is undocumented and looks impassable.

---

## 6. What the personas would actually trust

Each subtype wrote a "what would convert me" section. Synthesized into a single ranked list, the trust ladder is:

1. **A `SECURITY.md` per module that names adversaries.** All four agree. Without this nothing else matters.
2. **Specs over press posts.** Cryptarchia paper, Bedrock DA design, LEE proof-statement, Blend mixnet construction. Currently the strongest set of links in the docs is in section H of the AnonComms journey; that pattern should be the rule, not the exception.
3. **Signed, checksummed, reproducible release artifacts** for the blockchain node and the LEZ wallet — ideally with a `flake.nix`. The AnonComms team demonstrates the team can do this when it chooses to.
4. **A `quality:verified` end-to-end journey on at least one module**, with the disclaimer removed because Red Team verification actually completed. The cohort wants to see the ladder doing work, not just being described.
5. **The five canonical templates and the writing rules actually shipped**, so the described contribution workflow becomes a real one. Resolves the largest "described process vs. lived process" gap in the repo.
6. **A self-hosted operator path** — systemd unit, Compose file, NixOS module, documented backup-and-recovery — that delivers on the README's "headless Logos Node" promise.
7. **A clear "why a chain" passage** that admits the chain is load-bearing only for the financial-primitive class of use cases. This single passage would buy back the largest amount of credibility with the Crypto-Skeptical wing without compromising the project's positioning with the crypto-positive one.

---

## 7. What the project is doing right

A persona-driven review oriented around findings tends to read negative. To be clear about what survives this review intact:

- **The MIT license, IFT copyright, and absence of a CLA.** No copyright-assignment ceremony. Forkability preserved on paper.
- **The honest "consolidation in progress" disclaimer in the README**, which acknowledges the rename and the legacy-name drift before the reader has to discover it.
- **The contributing workflow's *shape*.** A six-phase board, an SME-plus-Red-Team verification ladder, an `area:*`/`quality:*`/`type:*`/`status:*` taxonomy, and a state-machine sidecar app is more than most projects ten times this size bother with. The artifacts are not shipped yet; the *shape* is right.
- **The Raspberry Pi 5 / aarch64 support** in the blockchain node release artifacts. Reads as a green flag from the homelab audience that this project is taking ARM seriously, not as an afterthought.
- **The AnonComms demo content.** Real spec links to `lip.logos.co`, `nix run '.'` install, libp2p + capability discovery + mixnet, no chain in the call path. The strongest content artifact in the repo. *Structurally* broken (it's a raw doc-packet) but content-good. Fix the structure and surface it.
- **Honest "Known limitations" sections** at the bottom of the blockchain and AnonComms journeys. The cohort respects this kind of admission far more than it respects a polished page that has been quietly broken.
- **The "consolidation under one Logos identity" move itself** — unifying Nomos / Codex / Waku into Logos Blockchain / Storage / Messaging. Long-term this is the right organizational move and the README's framing of it is sober.
- **The Logos Journeys app's auto-managed state machine.** Most projects don't bother. The fact that it exists at all is a credibility marker for the docs operation as a real engineering function.

---

## 8. A note on what was excluded

Per the original instruction, **Messaging was excluded** because the README explicitly marks it as "We're working on the content." Note that `docs/messaging/README.md` is a 0-byte file (part of Convergence 2 above). A minimum placeholder note ("Logos Messaging documentation is in progress. Tracked at #XX. Planned for testnet vX.Y.") at this location would close a confusing gap for readers who arrive at the messaging tree expecting at least a status statement.

External-hosted Storage docs at `logos-storage-docs.netlify.app` were not audited line-by-line; they were assessed only as structural artifacts (an off-site link from the docs repo for one of three foundational modules). The same applies to the Logos App build instructions in `github.com/logos-co/logos-app`. A future review pass focused on those surfaces would be a useful complement to this one.

---

## 9. Closing read

`logos-co/logos-docs` is an institutional docs operation in mid-build, with an organizational consolidation in flight, a sophisticated workflow described, and a small handful of strong content artifacts (the AnonComms demo, the blockchain quickstart's "Known limitations" section, the LEZ wallet's honest admission about its own help-text bug). It earns first-pass institutional credibility from every subtype in the Cypherpunk Builder cohort.

What it does not yet earn — for any subtype — is *substantive* credibility about the software it documents. The reasons converge:

- No threat model, anywhere.
- A described workflow whose load-bearing artifacts (writing rules, canonical templates) are 0-byte files.
- An identical disclaimer on every journey doing the work of a per-doc quality badge.
- Install instructions that fail the most basic verifiability test the cohort applies.
- A "journey" that is still in raw R&D intake-form shape, on the exact module (mixnet / AnonComms) where the most skeptical audience would judge the project hardest.
- A rename that has happened in marketing but not yet in engineering (`NSSA_WALLET_HOME_DIR`, `~/.nssa/wallet/`).
- Spec-substitution by press posts.

None of these are unfixable. Most are cheap. The Tier 1 changes above — a `SECURITY.md` v0, the writing-rules file, the PR template, the AnonComms structural rewrite, and checksums — collectively close more than half of the cohort's objections, and none of them require new engineering. They require somebody on the Docs team and an SME from each module to spend a focused week.

The gap to substantive trust is not a content-volume gap. It is a **specificity gap** (claims without specs), a **verifiability gap** (binaries without checksums), and a **process-vs-artifact gap** (described workflow without shipped artifacts). The repo is closer to closing these than it appears, because the *shape* of the operation is right. The next ship cycle will tell.
