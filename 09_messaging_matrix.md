# Messaging Matrix

*Phrase-by-phrase guidance: what resonates, what repels, why, and how to improve it. Designed for use by a copy reviewer or a downstream agent evaluating marketing surfaces.*

Each row contains: the candidate phrase, the likely reaction, the subtypes most affected, the risk level, and a better version where possible. "Risk level" measures how much *trust damage* the phrase causes if it appears on a homepage, in a launch announcement, or in technical docs.

---

## Section 1 — Privacy and Security Claims

| Phrase | Likely reaction | Most-affected subtypes | Risk | Better version |
|---|---|---|---|---|
| "Military-grade encryption" | Instant credibility loss. The cohort knows this phrase is meaningless and signals technical illiteracy. | Protocol Cypherpunk, OSS Infra Hacker | **Severe** | "AES-256-GCM" / "ChaCha20-Poly1305" / "Signal Protocol" — name the actual primitive. |
| "Quantum-proof" / "Quantum-resistant" (no specifics) | Eye-roll. Asks: which primitive? Which parameter set? Did you do hybrid? | Protocol Cypherpunk | **High** | "Uses [primitive] from NIST PQC, hybrid with [classical primitive]." |
| "End-to-end encrypted" | Acceptable but insufficient on its own. Triggers: between whom and whom? What about metadata? | All technical subtypes | **Medium** | "End-to-end encrypted; the server cannot read message contents. We do see [list]." Be specific about what is and isn't protected. |
| "Privacy-first" | Reads as marketing unless the architecture is on the same page. | All | **Medium-High** | "Privacy-by-default: [specific architectural feature that delivers privacy]." |
| "We don't sell your data" | The floor, not the ceiling. Reads as defensive. | All | **Low-Medium** | "We don't collect [X], [Y], [Z]. Here is exactly what we store and where." |
| "Your privacy is our priority" | Slogan. The cohort assumes the opposite when they read this. | All | **High** | Just delete it. Show the architecture instead. |
| "Zero-knowledge" (used loosely) | Suspicion. Real ZK has specific technical meaning. | Protocol Cypherpunk, Crypto-Positive | **High** | If you mean ZK in the cryptographic sense, name the proof system. If you mean "we don't know your data," say that instead. |
| "Bank-grade security" | Bad. Banks have bad security. | Protocol Cypherpunk, OSS Infra Hacker | **Medium-High** | Name what you actually do. |
| "Audited" (without naming the auditor) | Distrust. Who? What scope? Is the report public? | Protocol Cypherpunk, Privacy Activist Builder | **Medium** | "Audited by [firm]. Full report: [link]. Findings and our responses: [link]." |
| "Trustless" | Mixed. Used correctly = good. Used loosely = bad. | All | **Medium** | If technically accurate (no trust in operator), use it and explain why. If not, don't. |
| "Anonymous" | Conflated with pseudonymous more often than not. | Protocol Cypherpunk, Privacy Activist Builder | **Medium-High** | If you mean unlinkable across sessions, say "anonymous." If you mean public-key identities, say "pseudonymous." |
| "We can't read your messages" | Sometimes true, sometimes not. The cohort will inspect the claim. | All technical subtypes | **Medium** | "Messages are encrypted with keys the server never sees. We can see: [metadata list]." |
| "GDPR-compliant" / "HIPAA-compliant" | The cohort doesn't care directly. Worth listing in a Compliance section, never as a privacy claim. | All | **Low** | Compliance is not privacy. Put it on the right page. |
| "We take privacy seriously" | The most overused phrase in tech. Reads as nothing. | All | **High** | Delete. Show the threat model instead. |

---

## Section 2 — Decentralization Claims

| Phrase | Likely reaction | Most-affected subtypes | Risk | Better version |
|---|---|---|---|---|
| "Decentralized" (with single operator on AWS) | Severe credibility loss. "Decentralized in name only." | All | **Severe** | "Federated, currently with three operators." Or "Centralized today, with a documented path to federation." Be honest. |
| "Permissionless" | Acceptable when technically accurate. | Crypto-Positive, OSS Infra Hacker | **Low** | Make sure it actually is — no allowlists, no KYC chokepoints. |
| "Trustless" (in P2P contexts) | Sometimes accurate. Often hyperbole. | All technical subtypes | **Medium** | Specify what trust is and isn't required. |
| "Censorship-resistant" | Asks: against whom? With what mechanisms? | Privacy Activist Builder, Protocol Cypherpunk | **Medium** | "Multiple ingress paths; no single jurisdiction or operator can take this down. Specifically: [list]." |
| "User-owned" / "You own your data" | Resonates if backed up by exportability and self-hosting. | Sovereign Computing, Crypto-Skeptical Decentralist | **Low** | Pair with: "Export to [standard format] any time. Self-hostable. No vendor lock-in." |
| "Self-sovereign" | Worn-out crypto-adjacent term. Use with care. | Crypto-Positive (mixed), Crypto-Skeptical (negative) | **Medium-High** | "Self-custodial" if you mean keys. "User-owned" if you mean data. Be specific. |
| "Federated" | Strong positive signal if accurate. | Crypto-Skeptical, Privacy Activist Builder | **Low** | If the protocol is genuinely federated (multiple independent operators), say so and name a few. |
| "P2P" | Strong positive signal if accurate. | Crypto-Skeptical, OSS Infra Hacker, Sovereign Computing | **Low** | Be specific about how — DHT? Direct? Mesh? With a coordinator? |
| "On-chain" | For Crypto-Positive: neutral, depending on context. For Crypto-Skeptical: deal-breaker. | All | **High** for Crypto-Skeptical reach | Only use when accurate. Justify why on-chain is necessary. |
| "Web3" | Crypto-Skeptical: instant rejection. Crypto-Positive: also winces, increasingly. OSS Infra Hacker: skepticism. | All except some Crypto-Positive | **Severe** for most cohort reach | Delete the word. Describe what you actually do. |
| "Web3-native" | Same as above, worse. | All except some Crypto-Positive | **Severe** | Same. |
| "Decentralized X (instead of centralized Y)" | Asks: how, structurally? | All | **Medium** | "X is run across [n] independent operators in [jurisdictions]. No operator can read your data because [mechanism]." |

---

## Section 3 — Token, Blockchain, and Crypto Vocabulary

| Phrase | Likely reaction | Most-affected subtypes | Risk | Better version |
|---|---|---|---|---|
| "Powered by blockchain" | Bad across the board. | All | **Severe** | If you genuinely need a blockchain, explain why on the same page. Otherwise delete. |
| "Built on Ethereum" / "Built on Solana" / etc. | Crypto-Positive: contextual. Crypto-Skeptical: closes tab. | All except crypto-aware subtypes | **High** for reach | Name the role the chain plays specifically. |
| "Buy our token" | Crypto-Skeptical exits immediately. Crypto-Positive looks at premine and tokenomics. | All | **Severe** | If the token has a technical role, explain it. If it's funding, find a foundation or grant route instead. |
| "Tokenized X" | Distrust. The cohort assumes financialization of something that didn't need it. | All | **Severe** | If you mean "represented on-chain," say that specifically and explain why. |
| "DAO governance" | Skepticism. Often marketing. | All | **High** | Describe the governance structure plainly. "Governed by [foundation board]" is fine if accurate. |
| "Airdrop" | Strong negative for Crypto-Skeptical; mixed for Crypto-Positive. | All | **High** for reach | Avoid as a customer-acquisition strategy if you want broad cohort reach. |
| "DeFi" | Crypto-Positive: contextual. Crypto-Skeptical: dismissive. | All | **High** for reach outside crypto-positive | Describe what the protocol does specifically. |
| "NFT" | Almost universally negative reaction at this point. | All | **Severe** | If your use of NFTs is genuinely interesting (identity, access, attestation), avoid the word and explain the function. |
| "Smart contract" | OSS Infra Hacker: skepticism. Protocol Cypherpunk: neutral. Crypto-Positive: contextual. | All | **Medium-High** | "On-chain program" / "contract on [chain]" — and explain what it does. |
| "Gas" / "gas fees" | Acceptable inside the crypto-positive frame. Sounds alien outside it. | All | **Medium** outside crypto-positive | If your audience includes non-crypto people, translate. |
| "No premine, fair launch" (when true) | Strong positive for Crypto-Positive. | Crypto-Positive | **Low (positive)** | Say it. Back it up with the genesis details. |
| "Token utility" | Almost always reads as rationalization. | All | **High** | If the token has a real technical role, describe the role. Don't lead with the word "utility." |

---

## Section 4 — Open-Source and Repo Signals

| Phrase | Likely reaction | Most-affected subtypes | Risk | Better version |
|---|---|---|---|---|
| "Open source" (with closed clients) | Severe trust loss. | OSS Infra Hacker | **Severe** | Be specific: "Core protocol open source under [SPDX ID]. Client is currently closed." If the client is closed, the cohort wants to know the path to open. |
| "Source-available" | Acceptable if honest about not being OSI-approved. Bad if marketed as "open source." | OSS Infra Hacker | **High** if mislabeled | "Source-available under [license name]; not OSI-approved." Honesty preserves trust. |
| "MIT licensed" / "Apache-2.0" / "GPL-3.0" / "AGPL-3.0" | Trust signal if the license badge is real. | OSS Infra Hacker, Sovereign Computing | **Low (positive)** | Just say it. Use the SPDX identifier in the README and a real LICENSE file. |
| "Star us on GitHub!" (popup) | Distrust. Vanity-metrics signal. | OSS Infra Hacker | **Medium-High** | Remove. |
| "Powered by [VC logos]" | Negative across cohort. Worse for Crypto-Skeptical. | All | **High** | Move to an "Investors" or "Backers" page; don't lead with logos. |
| "Foundation-funded" / "Donation-funded" / "Grant-funded" | Positive signal. | All | **Low (positive)** | Be specific about funding sources, including amounts and durations. |
| "Free forever for self-hosters" | Strong positive if credible. | Sovereign Computing | **Low (positive)** | Pair with a feature comparison that shows the self-host isn't crippled. |
| "Cloud-first, self-host coming soon" | Distrust. "Coming soon" usually means "never with parity." | Sovereign Computing | **Severe** | Either ship self-host as a first-class option, or be honest that this isn't a self-host project. |
| "Enterprise tier with SSO" (when SSO is the only path to multi-user) | "SSO tax" — actively disliked. | Sovereign Computing | **High** | Include basic SSO in the open tier. Charge for support, scale, advanced features — not for security basics. |
| "Reproducible builds" (when real) | Strong positive. | Protocol Cypherpunk, OSS Infra Hacker | **Low (positive)** | Document how to reproduce. Provide attestation. |
| "Telemetry off by default" | Strong positive. | All | **Low (positive)** | Pair with: "No telemetry at all in offline mode." If there is any telemetry, document exactly what data and where. |
| "We collect anonymized usage data" | Distrust. The cohort knows anonymized data is rarely actually anonymous. | All | **High** | Don't collect it. Or make it strictly opt-in with full disclosure. |

---

## Section 5 — Community, Onboarding, and Tone

| Phrase | Likely reaction | Most-affected subtypes | Risk | Better version |
|---|---|---|---|---|
| "Join our Discord" (as primary community link) | OSS Infra Hacker, Crypto-Skeptical: distrust. Search-hostile, platform-dependent. | OSS Infra Hacker, Crypto-Skeptical | **Medium-High** | Add Matrix, mailing list, IRC, or forum as the primary technical channel. Discord can exist as a secondary. |
| "Schedule a demo" (CTA on a homepage) | OSS Infra Hacker closes the tab. | OSS Infra Hacker, Sovereign Computing | **High** | "Try it locally: `docker compose up`. Demo video: [link]." |
| "Request access" | Worse than "schedule a demo." | All | **High** | Public access. If gated for capacity reasons, explain the reason and the timeline. |
| "Talk to sales" | This signals you're not for this audience. | OSS Infra Hacker, Sovereign Computing | **High** | OK if you have an enterprise tier, but never the *only* path. |
| "Sign up to get started" | Frustration. The cohort wants to *use* before signing up. | All | **High** | "Run locally without signing up." Make signup optional for as long as possible. |
| "Get started in seconds" (cloud signup) | Marketing language. | All | **Medium-High** | "Local install in 30 seconds: [command]." |
| "Try it for free" (with credit card) | Distrust. | All | **High** | "Free, no credit card required, optional account." |
| "Modern teams use [project]" | This signals the audience is teams, not individuals or the cohort. | OSS Infra Hacker, Sovereign Computing | **Medium-High** | Address the actual use case. |
| "Built by ex-Google / ex-Meta engineers" | Mixed. Some respect; some skepticism. | All | **Low-Medium** | If you want to use it, name the people, not the brand. |
| "The future of [X]" | Eye-roll. | All | **Medium-High** | Describe the present. |
| "Revolutionary" | The most overused word in tech. | All | **High** | Delete. |
| "Reinventing [X]" | Reads as marketing. | All | **Medium** | Describe specifically what you do that's different. |
| "Next-generation" | Generic. Means nothing. | All | **Medium** | Specify. |
| "Powered by AI" | Suspicion. "AI" near privacy is a red flag absent specifics. | Privacy Activist Builder, all | **High** for privacy projects | "Uses [specific model] running [on-device / on our servers]; the data flow is: [description]." |
| "Trusted by [company logos]" | Mild distrust. Logo theater. | OSS Infra Hacker | **Low-Medium** | Show real users where consent exists. Don't seed logos. |
| "Number 1 [category] tool" | Distrust. Unverifiable. | All | **Medium** | Delete. Let users say it instead. |
| "Hundreds of thousands of users" | Suspicion. Inflated metrics are normal. | All | **Medium** | Specific numbers with methodology, or no numbers. |

---

## Section 6 — Threat Model and Limits

| Phrase | Likely reaction | Most-affected subtypes | Risk | Better version |
|---|---|---|---|---|
| "Here is our threat model" (on the homepage) | Very strong positive signal. | All | **Low (positive)** | Just do this. It is the single highest-leverage homepage element for this audience. |
| "What this does not protect against: [list]" | Very strong positive signal. | All | **Low (positive)** | Honesty about limits *increases* trust, contrary to most marketing instinct. |
| "Compromised endpoint / device security is out of scope" | Strong positive — sober adversary scoping. | Protocol Cypherpunk, Privacy Activist Builder | **Low (positive)** | Be this specific everywhere. |
| "We protect [user class] against [adversary class]" | Strongest positive form. | Privacy Activist Builder, Protocol Cypherpunk | **Low (positive)** | E.g., "We protect journalists against ISP-level observation of who they communicate with." Specificity wins. |
| "Protected against all adversaries" | The cohort will laugh. No system is. | Protocol Cypherpunk | **Severe** | Replace with specific scope. |
| "What happens if you're served a warrant" (answered honestly) | Strong positive. | Privacy Activist Builder, all | **Low (positive)** | Address this directly. "We have / don't have the following data. We have published / not published a transparency report. We have / have not received and complied with subpoenas." |

---

## Section 7 — Replacement Patterns

Common ways to upgrade copy without losing the marketing point.

| Original instinct | What to say instead | Why |
|---|---|---|
| "Privacy-first messaging" | "End-to-end encrypted; the server stores [list]. Threat model: [link]." | Show the architecture. |
| "Decentralized social network" | "Federated social network running on [N] independent servers. Run your own." | Be specific about the architecture. |
| "Take back your data" | "Export your data in [format] any time. Self-host the server. Permissive license." | Show, don't slogan. |
| "Trust no one" | "Verifiable: signed releases, reproducible builds, open source." | Trust-replaced-by-verification is the cohort's preferred frame. |
| "Built by privacy advocates" | "Maintained by [named people]; funded by [foundation / grants]." | Named beats branded. |
| "The Web3 way" | Delete. Describe the actual mechanism. | "Web3" loses you most of the cohort. |
| "Future-proof your stack" | "Open formats; self-hostable; long-term maintained; no lock-in." | Concrete. |
| "Powered by zero-knowledge proofs" | "Uses [Halo2 / Groth16 / PLONK / etc.] to prove [specific statement] without revealing [specific data]." | Specific cryptography reads as competent. |
| "Military-grade security" | "Uses ChaCha20-Poly1305 for transport, X25519 for key agreement, Argon2id for password hashing." | Concrete primitives. |
| "Trusted by leading companies" | Drop the framing entirely. Or use case studies with named users (with consent). | Logo wall fails for this audience. |

---

## Section 8 — Subtype-Specific Tone Patterns

### Maximally resonant register (use for *all* subtypes)

- Specific.
- Honest about limits.
- Past tense for what's shipped; future tense only for things you're certain of.
- Names the user being protected and the adversary being protected against.
- Links to the repo and the spec within two clicks.
- Treats the reader as a peer.

### Distinctly resonant register, by subtype

- **Protocol Cypherpunk:** cites primitives, names assumptions, links to specs.
- **OSS Infrastructure Hacker:** shows the install command, names the license, links to recent commits.
- **Privacy Activist Builder:** names user populations, names adversary classes, mentions field testing.
- **Crypto-Positive:** describes cryptographic substrate; addresses tokenomics directly on the same page; engages with credible-neutrality and Tornado-Cash-style cases honestly.
- **Crypto-Skeptical:** explicitly states "no token, no blockchain" when true; describes federation or P2P architecture.
- **Sovereign Computing:** leads with deployment commands, system requirements, ARM support, backup story.

### Distinctly *repelling* register, by subtype

- **Protocol Cypherpunk:** marketing language, vague security claims, custom crypto without rationale.
- **OSS Infrastructure Hacker:** vanity metrics, demo-request walls, closed-core "open source."
- **Privacy Activist Builder:** generic "privacy for everyone," AI-near-privacy without specifics, untested-in-field claims.
- **Crypto-Positive:** premine and insider allocation, vague tokenomics, opt-in privacy.
- **Crypto-Skeptical:** any token, any blockchain, any Web3 vocabulary.
- **Sovereign Computing:** "cloud-first," "schedule a demo," "enterprise tier with SSO."

---

## Section 9 — Quick Decision Heuristics

For a copy reviewer in a hurry, the following heuristics catch >80% of phrasing problems:

1. **If the phrase could appear on a SaaS landing page unchanged, replace it.**
2. **If the phrase makes a security claim without naming what's protected and against whom, replace it.**
3. **If the phrase uses a buzzword borrowed from the Web3 marketing ecosystem, replace it unless the project is squarely in that ecosystem.**
4. **If the phrase asks for trust without offering verification, replace it.**
5. **If the phrase hides centralization that exists in the architecture, replace it.**
6. **If the phrase promises something the code cannot deliver, replace it.**
7. **If the phrase reads as performative (uses cypherpunk imagery without substance), delete it.**
8. **If the phrase is generic (could describe any project in the category), replace it with something specific.**

---

## Use notes

- This matrix is opinionated. A project for a different audience may legitimately use phrases listed here as "high-risk." The matrix is calibrated to the Cypherpunk Builder cohort specifically.
- Risk levels assume the phrase appears in primary marketing surfaces (homepage, GitHub README, launch announcement). In a buried docs page or a deep-dive blog post, tolerance is higher.
- Run any homepage and any launch announcement through this matrix before publishing. Use the messaging-by-subtype subsection of `01_main_dossier.md` for further depth.
