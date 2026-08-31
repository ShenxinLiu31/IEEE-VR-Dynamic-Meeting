# Study 1 — Reconstructed Storyline

Study 1 is the first half of the paper's central claim: under a **mobility-dominant**
context, accessibility drives objective performance but not preference. It sets up the
tension Study 2 resolves by reversing. Everything below folds in the design-logic
corrections (reference-frame taxonomy, corrected FoV values, the AdaptiveLock/AdaptiveFlow
threshold rationale) so Study 1 no longer reads as a set of patched-over issues — each fix
now has an argumentative job.

---

## Two open decisions this storyline is built to accommodate

These aren't resolved yet; the structure below works either way, but the choice changes
what Results §4.3 can claim.

1. **Baseline**: add a body-locked baseline condition, or not (discussed previously —
   world-locked was rejected as a baseline candidate because its result is near-certain and
   it reopens the constant-angular-size confound; body-locked survived both objections).
   If added: N=20, 5 conditions × 2 environments = 10 per participant, consider splitting
   across two sessions. If not added: N=16, 4 × 2 = 8 conditions, single session.
2. **Gaze measurement**: keep the bounding-box + sensitivity-check approach, or upgrade to
   depth-based AOI classification using HoloLens spatial mesh (only relevant if Study 1 data
   is being recollected anyway, which it is, given the environment redesign).

Recommendation if resources allow: do both — add the body-locked baseline, and switch to
depth-based gaze classification, since you're already rebuilding data collection and the
marginal cost of both is much lower now than fixing either after the fact.

---

## RQ1a (primary)
How does anchoring technique affect objective performance and subjective preference under
high mobility, moderate cognitive demand — and do the two dissociate?

## RQ1b (only if baseline is added — this is new, and worth adding)
Does locomotion-triggered reference-frame switching (AdaptiveLock, AdaptiveFlow) improve
measurably over a static body-locked baseline, or does simply staying accessible the whole
session perform just as well?

**Why RQ1b matters beyond completeness**: this is the empirical answer to R2's "novelty is
incremental" concern — not a reframing move, an actual test. If AdaptiveLock beats plain
body-locked on any measure (workload, temporal availability, spatial-consistency ratings),
that's direct evidence the switching mechanism earns its added complexity, not just a design
rationale asserted in §3. If it doesn't beat plain body-locked, that's still worth reporting
honestly — it would mean the paper's design contribution is more about the trade-off *space*
than about AdaptiveLock specifically, which is consistent with the reframed R2-language
contribution statement already adopted (empirical/design contribution over new mechanisms).
Either outcome is informative; only the absence of the comparison is a problem.

---

## Method

**Design**: 4 techniques (ScaleStable, PeriphGuide, AdaptiveLock, AdaptiveFlow) [+ 1
body-locked baseline, if adopted] × 2 environments (Open Space, Room-to-Room). Technique
order and environment order both fully counterbalanced — 8-condition Williams design (4
techniques × 2 environments) or the equivalent 10-condition version with baseline included.

**Introduce techniques using the reference-frame taxonomy** (from Design_Logic_Corrected.md
§0), then immediately drop into precise per-technique parameters — don't let the taxonomy
substitute for specifics:
- ScaleStable — environment-referenced (world-locked), 0.5–3.5 m operational range.
- PeriphGuide — user-referenced, head-referenced, offset clamped **±21.5°H** (and vertical,
  once confirmed — see open item in Design_Logic_Corrected.md).
- AdaptiveLock — environment-referenced ↔ body-referenced, binary threshold at 0.3 m/s,
  discrete switch.
- AdaptiveFlow — body-referenced ↔ environment-referenced, graded threshold at 1.5 m/s (or
  fast yaw), ~2 s continuous interpolation.
- [Baseline, if adopted] — plain body-referenced, static for the full condition, same
  angular parameters as AdaptiveLock/AdaptiveFlow's accessible mode (0.85 m,
  ±30°H/±20°V pending the same FoV correction applied to PeriphGuide).

**State the threshold-placement rationale here, not just in this planning doc** (pulled
directly from Design_Logic_Corrected.md §B): AdaptiveLock's threshold answers a binary
question (moving at all, yes/no); AdaptiveFlow's answers a graded one (motion disruptive
enough to justify a costly transition). A shared threshold would collapse one technique
toward the other's behavior in the exact speed range Study 1's waypoint task lives in —
state this prospectively, from design purpose, not as a post-hoc defense.

**Tasks**: waypoint navigation (mobility) concurrent with slide-deck memory encoding
(cognitive), 12-item immediate recall per condition — unchanged.

**Measures**: interface attention ratio, immediate recall accuracy, temporal availability,
NASA-TLX, SUS, preference ranking. If depth-based gaze classification is adopted, state the
method precisely (gaze-ray intersection with spatial mesh vs. fixed panel plane, nearer
intersection wins) instead of relying solely on the bounding-box + sensitivity-check
argument.

---

## Results (ordering is the argument)

1. **Lead with the dissociation** (unchanged from Storyline_Final.md): ScaleStable worse on
   recall/attention, better on preference/SUS. This is the headline of Study 1, stated in
   the first paragraph of Results.

2. **[If baseline added] Report the switching-vs-static comparison as its own explicit
   subsection**, not folded into the four-technique comparison. This is the RQ1b payoff —
   give it the same visibility as the dissociation finding, since it's doing real
   argumentative work (novelty defense), not just filling in a gap.

3. **Explain AdaptiveLock vs. AdaptiveFlow differences using the threshold-placement logic,
   not just as "one is discrete, one is continuous."** If AdaptiveFlow shows more gaze
   transitions or higher workload than AdaptiveLock, tie it explicitly to the fact that
   AdaptiveFlow's threshold sits further out and its transitions are longer — connect the
   mechanism (§B) to the data, don't just report the contrast.

4. **Performance mechanism** (accessibility → recall) as before — this is now explicitly the
   secondary point, not the headline.

5. **Robustness**: CIs, Friedman check, trial-order null result — unchanged.

---

## Discussion

Two forward-pointing questions instead of one:
1. The existing one: if preference favors stability even when it costs performance under
   moderate load, does that reverse as cognitive/environmental load increases? → motivates
   Study 2.
2. **New, if baseline included**: if switching earned its complexity over static
   accessibility in a mobility-dominant context, does that advantage hold, shrink, or
   disappear once cognitive load dominates instead? → gives Study 2 a second thread to
   report on (does AdaptiveLock/Flow's edge over a body-locked baseline persist under
   collaborative load), strengthening the cross-study synthesis in §6 beyond the
   preference/performance reversal alone.

---

## What this changes about the paper's overall spine

The central claim (preference/performance dissociation, reversing with context) stays
exactly as in Storyline_Final.md — nothing here replaces that. What's new is that Study 1
now also directly demonstrates, with data, the novelty-reframing argument R2 asked for
("empirical/design contribution, not new mechanisms") instead of only asserting it in the
Introduction. That argument used to live entirely in prose; RQ1b gives it a result.
