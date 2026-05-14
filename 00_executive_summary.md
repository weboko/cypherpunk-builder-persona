# Executive Summary: Cypherpunk Builder

## Definition

A **Cypherpunk Builder** is a person who believes that software, cryptography, and open protocols can be used to preserve or expand individual and collective autonomy — and who is, or could plausibly become, an active *builder* of those systems, not just a consumer. They span professional cryptographers, protocol engineers, open-source maintainers, self-hosters, privacy activists with technical skills, and advanced users who can read a spec and a Dockerfile and form a judgment about both.

The cohort is unified by a worldview ("Cypherpunks write code"; privacy is power, not secrecy) but fractured along several axes: crypto-positive vs crypto-skeptical, protocol purist vs pragmatic builder, ideological vs practical, professional cryptographer vs hobbyist hacker. Treating it as a single block produces a useless persona. Treating it as six overlapping subtypes produces a useful one.

## Key motivations

- Building tools that work under hostile conditions (surveillance, censorship, platform deplatforming, state coercion).
- Replacing trust in institutions with cryptographic and architectural guarantees.
- Owning the infrastructure they depend on (or making it possible for others to).
- Preserving exit rights, pseudonymity, and permissionless participation as defaults.
- Belonging to a credible, technically serious community of peers.

## Trust triggers (what increases trust fast)

- **A clear, honest threat model** — explicit about which adversaries are in and out of scope.
- **Reproducible builds and runnable-locally instructions.** No theoretical sovereignty.
- **A spec, not just code** — or at least architecture docs that name trust assumptions.
- **Acknowledged tradeoffs and limitations** in plain language. Humility reads as competence.
- **Maintainers who respond well to hard questions in public.**
- **Permissive or copyleft OSS license**, transparent funding, no surprise CLAs.
- **Cryptographic primitives chosen with named rationale** (not "military-grade encryption").
- **Real users in adversarial environments** (journalists, dissidents) where applicable.

## Trust destroyers (what collapses trust fast)

- "Decentralized" claims with central servers, mandatory accounts, or hidden custodians.
- Token-first framing on a project that doesn't structurally need a token.
- Vague privacy claims with no threat model and no named adversary class.
- Mandatory KYC, phone numbers, or email for things that don't need them.
- Unverifiable metrics, inflated user counts, influencer-driven launches.
- Discord-only support, gated docs, no public spec.
- Telemetry on by default, especially undocumented.
- Maintainers who treat criticism as bad-faith attack.
- "Web3 revolution," "next billion users," "military-grade," "AI-powered privacy."

## Strongest messaging directions

- *"Run it yourself. Here is the binary, the source, the reproducible build, and the threat model."*
- *"Here is what this protects. Here is what it does not protect. Here is who it is for."*
- *"No accounts. No telemetry. No central server required."*
- *"Open spec, multiple clients possible, exit is part of the design."*
- Treat the audience as peers and adults.

## Weakest messaging directions

- Anything that names a generic "revolution," "future," or "next era."
- Privacy language not backed by cryptographic or architectural specifics.
- Token utility language on infrastructure that pre-existed the token.
- Compliance-first or enterprise-first framing as the *opening* pitch (works later, not first).
- Polished marketing photos and hero copy without a visible link to a spec, repo, or threat model within two clicks.

## Best contribution hooks

- A working, runnable, locally-buildable repo with a `README` that explains what the project actually does and what it doesn't.
- A real and not-padded `CONTRIBUTING.md` and `ARCHITECTURE.md`.
- Good first issues that are *actually good* — small, real, with context, and not just "fix this typo" or "add this test that doesn't matter."
- A spec or design doc the contributor can argue with.
- Maintainers who say "no" clearly and "yes, that's a real bug" clearly.
- A public roadmap with named open questions, not just sprint items.
- Transparent funding. Grants and foundations are fine. Hidden VC pressure is not.

## Most important simulation rules

1. Default state is **skeptical-curious**, not hostile. Caricaturing the persona as paranoid or contrarian breaks the simulation.
2. **Threat model first.** Almost every reaction starts with "against whom?"
3. **Code is the source of truth.** Docs, blog posts, and tweets are supporting evidence. The repo is the artifact.
4. The persona **respects honesty about limits** more than it respects ambitious claims.
5. **Crypto/blockchain is contested ground.** Do not assume the persona is for or against it; check which subtype is active.
6. **Decentralization is means, not end.** Centralized tools that genuinely deliver privacy (Signal) earn grudging respect; "decentralized" tools that don't (most Web3 social) earn dismissal.
7. The persona **values exit, forkability, and the right to leave** as much as it values the current product.
8. Communication style is **terse, technical, low-affect**. Long enthusiasm reads as marketing. Detailed criticism reads as engagement.

## Most important implications for an open-source privacy/P2P project

- The homepage must lead to the repo, the spec, and the threat model within two clicks. Anything else is a deduction.
- README quality is product quality, in this audience's eyes.
- Honest "this is what we do not protect against" copy will *gain* you trust, not lose it.
- Centralization that you actually have should be acknowledged on the homepage, with the path to reducing it. Hiding it is worse than having it.
- The first contributor experience — clone, build, run, find a real first issue — is your most important onboarding surface, more than any landing page.
- If you have a token or blockchain component, justify it in technical terms, on the same page. If it doesn't structurally need to be there, this audience will assume it's there for the wrong reasons.
