# Validation Plan

*How to test this persona against real humans before relying on it for high-stakes decisions. Lightweight methods, ordered from cheapest to most expensive. Designed for a small team without a research budget; scale up the methods you have time for.*

---

## Why validate

A persona dossier is a *model* of a cohort, not the cohort itself. Even a careful, evidence-grounded dossier will:

- Compress real variation into legible subtypes.
- Reflect the author's reading of the cohort's culture, with the author's biases.
- Lag the moving present. Some claims here will be stale within 12–24 months.
- Be heavier on English-speaking Western voices than the global cohort warrants.

Validation is how you catch the drift before it costs you a launch, a community, or a community member's trust.

---

## Validation methods, in roughly increasing cost

### Method 1 — Internal sanity check

**Cost:** zero. **Time:** 1–2 hours per project.

Before a launch, a homepage, a README, or a community decision, have one team member load the relevant simulation card and walk through the artifact as if they were that persona. Have a second team member do the same with a different subtype.

Surface the predictions out loud:
- "Reading the homepage as a Protocol Cypherpunk, my first move is to click for the spec, and the link is in the footer. That's a problem."
- "Reading the README as Sovereign Computing, I notice there's no ARM build mentioned and the Docker image is on a third-party registry. Both are smells."

This is the cheapest possible check and catches the most common errors.

### Method 2 — Trusted-reviewer pre-read

**Cost:** the value of 1–3 hours of a trusted person's time. **Time:** a few days.

Identify 2–4 people in your own network who actually belong to this cohort. Send them the artifact (homepage draft, README, spec, threat-model doc, announcement) and ask for unfiltered reaction. Pay them or thank them seriously.

Specifically ask:
- "What's the first thing you notice?"
- "What's missing for you?"
- "What's a red flag?"
- "What would you click on first?"
- "Would you contribute to this? Why or why not?"

Compare their answers to what the persona predicted. Significant divergence is information.

### Method 3 — Structured asynchronous review

**Cost:** modest. **Time:** 1–2 weeks.

Recruit 5–10 reviewers across subtypes. Send them a short, structured questionnaire with the artifact attached. Ten minutes of their time, not an hour.

A useful questionnaire:

1. Which of the following best describes your relationship to this kind of project? (Subtype-mapping question; phrased to avoid leading.)
2. Without reading the homepage carefully, what is your immediate impression?
3. What's the *first* thing you'd want to verify before trusting this project?
4. What's missing from the homepage / README / spec that you'd expect?
5. If you were to contribute, what would your first action be? What would you need to see first?
6. Is there anything here that would make you stop engaging?
7. On a scale of 1–5: how likely are you to share this with a peer?
8. Free-text: anything else?

Mix subtypes deliberately. Compare the per-subtype answers to the per-subtype predictions in the dossier. Where they diverge, you have a calibration problem.

### Method 4 — Live interviews

**Cost:** higher. **Time:** 2–4 weeks for a small cohort.

Conduct 8–15 semi-structured interviews, distributed across subtypes. Aim for at least 2 representatives from each subtype you care about for the current project. 30–45 minutes each.

A short interview protocol:

- **Background (5 min):** What kinds of projects do you currently spend time on? How did you get into this space? What's your relationship to "cypherpunk" as a term — does it apply, half-apply, or not?
- **Worldview (10 min):** When you're evaluating a new privacy/decentralization/local-first project, what's your process? What signals make you trust it? Distrust it? Have you been burned recently?
- **Stimulus walkthrough (15 min):** Walk me through your reaction to [the homepage / README / spec / launch announcement]. Think out loud.
- **Contribution thinking (10 min):** What would have to be true for you to contribute? What would have to be true for you to keep contributing?
- **Open-ended (5 min):** Anything I should have asked but didn't?

Record (with consent). Transcribe. Code the answers for themes. Compare to the dossier.

This is the most expensive method but also the highest signal. The cohort is unusually willing to give serious feedback if asked seriously and not treated as a marketing target.

### Method 5 — Community observation

**Cost:** ongoing time. **Time:** continuous.

Be in the cohort's channels (Mastodon, Matrix, IRC, Hacker News, r/selfhosted, project-specific mailing lists, the relevant Discord rooms — yes, including them) as a participant or at minimum a reader. Read launch threads, criticism threads, postmortems, and "show HN" reactions.

Calibrate the dossier's predictions against what you see actually happen when other projects launch into this audience. Especially watch:
- What gets celebrated.
- What gets quietly skipped.
- What gets publicly criticized, and how.
- What gets defended, and who defends it.

A persona dossier should be tightened every 6 months with a half-day review against recent observations.

### Method 6 — Quantitative behavioral analysis

**Cost:** depends on your existing tooling. **Time:** ongoing.

If your own project is shipped, instrument it for behavioral signals that map to the dossier's predictions. Examples:

- What does your GitHub Insights / contributor graph look like? Are PR reviewers distributed or bottlenecked? Are issues triaged?
- Where do contributors come from — discovery sources, geographies, referral platforms?
- Where do contributors *leave* — what was the last interaction before they stopped?
- Where do users come from? What's the share of self-hosted vs hosted use?
- How does the issue tracker handle hostile reports? Constructive ones?

Map the data against the persona's predictions. A persona that predicts "contributors will leave if PRs sit unreviewed" should be testable against "did contributors leave when their PRs sat unreviewed?"

### Method 7 — Hostile review

**Cost:** the value of paying a credible external critic. **Time:** 1–2 weeks.

Identify a person known to be critical of projects in your space — someone whose blog or social presence regularly punctures hype. Ask them, in good faith, to tear the artifact apart. Pay them; do not retaliate; do not respond defensively when the review comes back.

This is the most uncomfortable validation method and often the most useful. The cohort's blogosphere does this work for free for many projects; soliciting it deliberately, before launch, lets you fix problems instead of being embarrassed by them publicly.

---

## What to look for in validation results

### Signs the persona is calibrated for your case

- Real reviewers' predictions match the simulation card's predictions on >70% of the artifact's surfaces.
- The objections real reviewers raise are predicted by the dossier.
- The features they praise are the features the dossier predicts will land.

### Signs the persona is mis-calibrated for your case

- Real reviewers consistently surface a concern the dossier doesn't mention. (Add it.)
- Real reviewers consistently dismiss a concern the dossier emphasizes. (Downgrade it.)
- Subtypes are reacting differently than the dossier predicts. (Maybe a subtype boundary is wrong, or your audience skews more heavily to one than expected.)
- Real reviewers cluster around a worldview the dossier doesn't have a card for. (Possibly a new or sub-subtype.)

### Signs the persona is reasonable in general but wrong for *this project*

- Real reviewers like things the dossier predicts they won't (or vice versa) for project-specific reasons.
- The project sits at the intersection of two or three subtypes in a way the dossier compresses too much.

In this case, the dossier is fine; you just need to weight the cards differently for this project.

---

## What to do with validation results

1. **Update the dossier.** Concretely: edit `01_main_dossier.md`. Add a dated note to the relevant section. Update the simulation cards where their predictions failed. Keep the original claim visible (don't silently overwrite — leave a note about what was updated and why).
2. **Update the messaging matrix.** When real reviewers react differently to a phrase than predicted, update `09_messaging_matrix.md`.
3. **Update the contribution matrix.** When real contributors' onboarding paths look different from the predicted ones, update `10_contribution_matrix.md`.
4. **Update the bibliography.** When validation surfaces sources or community discussions the dossier missed, add them.
5. **Cite the validation in your simulation prompts.** A downstream agent should know which predictions in the dossier have been tested and which haven't.

---

## Specific validation focuses to prioritize

Of all the claims in this dossier, the following are most worth validating against real humans first, because they are most consequential and most likely to be miscalibrated:

1. **Subtype membership thresholds.** Is the boundary between OSS Infrastructure Hacker and Sovereign Computing as clean as the dossier suggests, or is there a single broader subtype that the dossier should merge?
2. **Crypto-Positive heterogeneity.** Is this really one subtype, or is it three (Bitcoin-only, privacy-coin-focused, ZK/Ethereum-focused)?
3. **The Privacy Activist Builder subtype.** Does this subtype exist as a *builder* category, or is it more often a *user* category with a small technical core? The dossier may be over-weighting it.
4. **The relationship between Crypto-Skeptical Decentralist and the local-first community.** Are they really overlapping, or is the dossier merging two adjacent communities that should be kept separate?
5. **The relative size of subtypes.** The dossier's weighting (Sovereign Computing and OSS Infrastructure Hacker as the largest, Protocol Cypherpunk as the smallest) is interpretive. Sample-based validation should sharpen this.
6. **Whether "Web3" vocabulary really is a deal-breaker as severe as the dossier claims.** The dossier is confident here, but the confidence is partly based on Hacker News culture, which is more skeptical than other channels.
7. **Generational drift.** The dossier may be over-anchored on the 2013–2020 wave of builders. The 2022+ wave (AI/cloud-centralization-motivated, on-device-AI-focused, post-Web3-disillusionment) may behave differently.

---

## Frequency

- **Per-project quick check:** Method 1 every time. Method 2 for important launches.
- **Per-quarter:** Method 5 (community observation) as continuous practice.
- **Per-year:** Methods 3 and 4 once, with a meaningful sample. Update the dossier.
- **Per-major-decision:** Method 7 for high-stakes launches and positioning shifts.

---

## A note on validation honesty

Validation is most valuable when you're willing to be wrong and to update accordingly. The most common failure mode is to seek validation, get unwelcome results, and absorb only the comfortable parts. The persona system is most useful if it is *willing to be revised*, not protected.

If a validation pass surfaces a fundamental mismatch — for example, that the audience for your project is *not* primarily the Cypherpunk Builder cohort at all — that result is more valuable than any reassurance the dossier could provide. Use the dossier as a tool, not as identity.
