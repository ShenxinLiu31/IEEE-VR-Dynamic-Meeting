# Dynamic Anchoring — Full Storyline (v2, post-ISMAR revision logic)

This is the narrative skeleton, not final prose. Every section states (a) the argumentative
job it does, (b) what it must contain, (c) how it hands off to the next section. It incorporates
every decision made in the ISMAR rebuttal + revision discussion: 2 environments, RQs not
hypotheses, contribution reframed as empirical/design, related work integrated inline,
AR-vs-VR motivation upfront, 4 orthogonal design guidelines.

---

## 1. Introduction

**Job:** get to "why anchoring, why now, why not solved" in three moves, then state the
contribution as empirical/design work, not new mechanisms.

1. **Hook (1 paragraph).** Mobile AR requires simultaneous processing of physical and
   digital information while the user's relationship to both is constantly changing. State
   this as a *design* problem, not a phenomenon: where should content live when the user's
   mobility state keeps changing the cost of every placement?

2. **Why AR is not VR (new — directly answers R3).** One paragraph, not an aside. AR
   differs from VR in ways that make anchoring a live, unsolved problem specifically here:
   physical stakes (real hazards on inattention), unscripted environments (can't pre-script
   the world), mutual occlusion (content and world compete for the same visual space), and
   depth conflict (fixed-focal-plane content over continuous-depth real world worsens
   vergence-accommodation mismatch). This paragraph exists so an IEEE VR reviewer with a
   3DUI/VR background cannot dismiss the premise in one sentence.

3. **The three traditional anchors and why they're each incomplete (short).** World/head/
   body-locked, one sentence each, framed as *specific, known* trade-offs (stability vs.
   accessibility vs. central occlusion) — not as a strawman to be knocked down, since R2
   will read "traditional anchors are insufficient" as an under-cited overclaim if not scoped
   precisely.

4. **The gap (this is the novelty reframe — R2's core ask).** State explicitly: individual
   anchoring mechanisms (scaling, peripheral placement, motion-based switching, smooth
   interpolation) all build on prior work. What's missing from the literature is *evidence for
   when each strategy is right* — a cross-context empirical comparison, not a new mechanism.
   Say this in the Introduction, not just in a rebuttal letter, so no reviewer has to infer it.

5. **Four design probes, named as probes.** ScaleStable, PeriphGuide, AdaptiveLock,
   AdaptiveFlow — each gets one sentence stating its *specific* mechanism (not "world-locked"
   generically): ScaleStable = world-locking + constant-angular-size scaling; PeriphGuide =
   head-locked but peripheral-clamped, not centered; AdaptiveLock = locomotion-state-triggered
   discrete toggle (walking→body-locked, stationary→world-locked — corrected direction);
   AdaptiveFlow = same toggle logic but ~2s continuous interpolation instead of a discrete
   switch.

6. **Two studies, stated as testing different regions of the context space, not as
   "individual vs. collaborative" alone.** Study 1: high mobility, moderate cognitive load,
   individual. Study 2: moderate mobility, high cognitive load, collaborative. This framing
   is what lets §8 later argue the *reversal* between studies is a context effect, not a
   study-artifact.

7. **Contribution statement, three items, in R2's language:**
   (1) cross-context empirical comparison showing anchoring preference is not fixed but
   context-dependent; (2) identification of a preference–performance dissociation
   (ScaleStable: worse recall, higher preference) as a design-relevant finding in its own
   right, not a confound; (3) a four-dimension design framework (§9) derived from where the
   reversal does and doesn't hold.

**Hands off to:** Related Work, which must justify why these four specific mechanisms are
non-obvious combinations of known ideas.

---

## 2. Related Work

**Job:** stop being a list. Every cited work must connect to a specific technique or a
specific finding — R1's exact complaint was that §2.3 "stops at a shallow description... before
circling back to multi-user collaboration."

**§2.3 Anchoring Techniques (expand, this is the central-topic subsection R1 flagged):**
- World/head/body-lock baseline definitions (kept from before).
- **Path-anchoring [27]** — move here from wherever else it's cited. Directly compare to
  AdaptiveLock: both are locomotion-state-triggered, but articulate the difference (or
  rename AdaptiveLock if there isn't one — R1 explicitly requires this resolved, not sidestepped).
- **Lindlbauer 2019 (Context-Aware MR, UIST)** — context-aware *adaptation* precedent;
  differentiate: Lindlbauer adapts layout/complexity to context, this paper adapts *reference
  frame* to locomotion state specifically.
- **Lu 2023 (Glanceable AR, SUI)** — on-demand/glanceable access as an alternative solution
  to the accessibility problem; note where PeriphGuide's always-on peripheral approach makes
  a different bet than glanceable's on-demand approach, and flag this contrast as material
  for §9 Limitations (Chang et al. on-demand hiding — same thread, R1 also names this).
- **Pfeuffer 2021 (ARtention, C&G)** — gaze-adaptive UI design space; position this paper's
  motion-adaptive design space as the complementary axis (motion state vs. gaze state).
- **Jannat 2025 (Body-Anchored AR, ISMAR)** — most directly comparable prior body-anchoring
  work; this is the one comparison a reviewer will check first, so it needs a real paragraph,
  not a citation.
- **Satkowski 2022 (Above & Below, ISMAR)** — content placement in underused FoV regions;
  relevant contrast for PeriphGuide's peripheral-clamping logic.

**Handoff:** by the end of §2.3, the reader should already expect the paper's contribution
to be comparative/empirical, because every technique has just been shown to sit on an
existing axis — the Introduction's novelty framing (item 4 above) is now earned, not asserted.

---

## 3. Design Space & Technique Descriptions

**Job:** make the trade-off framework precise enough that Study 1/2 results read as tests of
stated predictions, not post-hoc narrative.

- State the trade-off axes precisely: field-of-view interference vs. digital accessibility,
  modulated by mobility state. Keep this — it survived review essentially intact and R2 called
  it the strongest contribution.
- **Separate panel size from panel location explicitly** (this is the rebuttal's answer to
  R3's FoV complaint — put it in the paper, not just the rebuttal letter). One paragraph:
  angular size is held constant across all four techniques (cite the specific values); *where*
  content sits is the independent variable, because that's literally what "anchoring" means.
  This single paragraph pre-empts the single most repeated R3 objection.
- Technique descriptions, each with exact parameters (not "peripheral," but "±40°H/±30°V"):
  this is the "replace vague claims with concrete measurements" fix R1 asked for.
- **AdaptiveFlow trigger condition, stated once, precisely:** walking >1.5 m/s OR head yaw
  >150°/s, acting at different timescales (immediate vs. after 2s smoothing). This was
  R1's specific confusion point — get it right here so it doesn't need re-explaining later.
- Smoothing note: all four techniques use temporal smoothing (Lerp=0.1) — state this here so
  R3-style "did you consider smoothing" objections are foreclosed structurally, not just
  rebutted reactively.

**Handoff:** the reader now has a precise, falsifiable framework. Study 1 tests it under one
context; Study 2 tests it under another.

---

## 4. Study 1 — Individual mobility + moderate cognitive load

**Job:** show accessibility dominates when mobility is high and environmental processing is
simple. Set up the tension (preference ≠ performance) that Study 2 will resolve differently.

- **RQ1** (not H1–H3): How does anchoring technique accessibility affect performance and
  experience under high mobility, moderate cognitive demand?
- **Method:** 12 participants, 4 techniques × **2 environments** (Open Space, Room-to-Room —
  drop Narrow Corridor). Both technique order and environment order counterbalanced
  (8-condition Williams design, or independently counterbalanced Latin squares — pick per the
  earlier design discussion). State session length explicitly and note it is shorter than the
  original 3-environment design — this is a direct, structural answer to the fatigue critique,
  not a defensive footnote.
- **Results, organized around the argument, not around measures:**
  1. Accessibility → performance: ScaleStable impairs recall and interface attention time
     relative to the other three (numbers as before).
  2. Accessibility → preference is NOT the same story: despite worse recall, ScaleStable and
     AdaptiveLock top both SUS and preference rankings. **State this tension explicitly as the
     first appearance of the preference–performance dissociation** — don't bury it in a later
     "interestingly" aside. This is the thread Study 2 will pull on.
  3. Robustness: report 95% CIs, Friedman check, and the trial-order mixed-effects result
     (β=−0.078, p=.449) showing fatigue didn't drive the technique effect — put this in
     Results, not just the rebuttal.
- **Discussion (§4.4):** end on an explicit, stated question, not an implied one: *if
  accessibility wins on performance but not preference even here, what happens when
  environmental/cognitive load — not mobility — dominates?* That question is Study 2.

---

## 5. Study 2 — Collaborative sensemaking + high cognitive load

**Job:** show the reversal, and explain *why* it's a reversal (environmental processing cost
of interference outweighing accessibility benefit), not just report that it happened.

- **RQ2:** How does the accessibility–stability trade-off manifest when AR must support
  sustained environmental processing and collaborative cognition?
- **Method:** 12 dyads, same 4 techniques, single task environment (this study was never a
  3-environment design — no change needed here, just confirm this stays as-is).
- **Results, again organized around the argument:**
  1. ScaleStable wins on collaboration quality and spatial consistency, *despite* lowest
     interface attention (25.32% vs. 40%+ for PeriphGuide/AdaptiveFlow) — state the paradox
     up front: less access, better outcome.
  2. Workload data now *does* show technique effects (unlike Study 1): AdaptiveFlow's
     continuous transitions cost more than AdaptiveLock's discrete ones under load. This is
     the mechanism, not just a second finding — cognitive disruption from switching, invisible
     under Study 1's lighter load, becomes visible here.
  3. Qualitative quotes carry the "why": predictability/shared reference language for
     ScaleStable, "chasing it with my eyes" for AdaptiveFlow.
- **Discussion (§5.4):** name the reversal explicitly and tie it back to Study 1's unresolved
  tension: the preference for stability wasn't noise in Study 1, it was a preview — Study 2 is
  the context where that preference and performance finally align, because interference costs
  now dominate over accessibility gains.

---

## 6. Cross-Study Synthesis (§6 or fold into General Discussion opening)

**Job:** state the single sentence the whole paper is building to, then generalize it into a
framework — this is where R2's "strongest contribution" pays off and where R1's "engage with
related work" gets executed, not promised.

- **The one sentence:** optimal anchoring is not a property of a technique, it's a property of
  a (technique, context) pair — and the context axis that matters is *what kind of processing
  load dominates*, not motion state alone.
- Explicitly connect to related work here, not in a separate literature-review-shaped
  paragraph:
  - vs. **Lindlbauer**: this paper's adaptation trigger is locomotion state; Lindlbauer's is
    task/interface complexity — state where the two would agree and disagree given this
    paper's data.
  - vs. **Jannat**: compare body-anchoring findings directly — does this paper's
    preference–performance dissociation appear in Jannat's data too, or contradict it?
  - vs. **Lu's glanceable AR**: glanceable (on-demand) is a third strategy this paper didn't
    test — flag as the natural next comparison, sets up part of Limitations.
- State the preference–performance dissociation as a **standalone finding**, not a footnote:
  users will accept a measurable performance cost to reduce visual interference. This is the
  rebuttal to R3's core complaint (that ScaleStable's preference implies poor implementation
  of the others) — the paper doesn't need to argue this defensively anymore if it's framed
  here as the point, not an anomaly.

---

## 7. Design Guidelines (§9, four orthogonal dimensions — replaces the old five)

**Job:** guidelines that don't restate each other. Replace the old 5-item list entirely.

1. **Which demand dominates** — mobility-dominant tasks favor accessibility-preserving
   anchoring (Study 1 pattern); cognitive/environmental-dominant tasks favor
   stability-preserving anchoring (Study 2 pattern, the reversal).
2. **How often to reconfigure** — static / discrete-switch / continuous-interpolation, with
   the finding that continuous costs more under cognitive load than discrete.
3. **What to optimize for** — perceived interference vs. objective accessibility; state that
   these are not the same target and picking one can cost the other (this is where the
   dissociation finding becomes actionable design guidance, not just an observation).
4. **Who controls access** — system-driven (adaptive) vs. user-initiated (glanceable/on-demand,
   tying back to Lu 2023 in Related Work) — explicitly flagged as untested by this paper,
   which motivates Limitations/Future Work.

---

## 8. Limitations

Short list, each tied to something already fixed or explicitly scoped, not vague hedging:
- Environment reduced to 2 (Open Space, Room-to-Room) for full counterbalancing — state this
  as a design choice, not an apology; note the dropped Narrow Corridor condition explicitly so
  no one assumes it was silently discarded post-hoc without explanation.
- HoloLens 2 FoV — acknowledge, tie to the panel-size-vs-location distinction already made in
  §3 so it reads as "known and controlled for," not "overlooked."
- N=12 (Study 1) / 12 dyads (Study 2) — standard for the field, CIs reported, note Study 2's
  N=24 as corroborating evidence.
- Gaze-through-transparent-panel ambiguity — state the ≤10% sensitivity check result.
- On-demand/glanceable anchoring untested — explicit pointer to Lu 2023, sets up Future Work.

---

## 9. Conclusion

One paragraph. Anchoring choice should be driven by which processing demand dominates, not by
motion state alone or by which technique maximizes any single metric in isolation. The
preference–performance dissociation means designers must choose which one they're optimizing
for and say so — there is no anchoring strategy that wins on both simultaneously across all
contexts, and pretending otherwise is the mistake this paper's two studies were designed to
expose.

---

## What changed vs. the ISMAR version, at a glance

| Element | ISMAR version | This version |
|---|---|---|
| Environments (Study 1) | 3, fixed order, uncounterbalanced | 2, fully counterbalanced |
| Novelty framing | "four new techniques" | "four design probes testing a trade-off space" |
| AdaptiveLock description | Contradicted itself (§5.1.2 vs §6.4) | Single corrected definition, stated once |
| Hypotheses | H1–H6 | RQ1, RQ2 |
| Related Work §2.3 | Thin, circles back to collaboration | Five works integrated with explicit contrasts |
| General Discussion | No engagement with prior work | Explicit compare/contrast with Lindlbauer, Jannat, Lu |
| Design Guidelines | 5 overlapping items | 4 orthogonal dimensions |
| Preference–performance gap | Reported, not framed | Named as a standalone contribution, threaded from §4 through §6 |
| AR vs. VR distinction | Absent / 1 sentence in rebuttal only | Full paragraph in Introduction |
