# Study 1 — Finalized Storyline

Study 1 is the first half of the paper's central claim: under a **mobility-dominant**
context, accessibility drives objective performance but not preference. It sets up the
tension Study 2 resolves by reversing. This version folds in the design-logic corrections
(reference-frame taxonomy, corrected FoV values, the AdaptiveLock/AdaptiveFlow threshold
rationale) and locks in the two decisions that were previously open.

**Decisions finalized**: no baseline condition; N=16; gaze measurement upgraded to
depth-based AOI classification.

---

## RQ1
How does anchoring technique affect objective performance and subjective preference under
high mobility, moderate cognitive demand — and do the two dissociate?

---

## Method

**Design**: 4 techniques (ScaleStable, PeriphGuide, AdaptiveLock, AdaptiveFlow) × 2
environments (Open Space, Room-to-Room) = 8 conditions per participant, single session.
Technique order and environment order both fully counterbalanced via an 8-condition Williams
design — N=16 gives exactly 2 participants per sequence, fully balanced.

**Introduce techniques using the reference-frame taxonomy** (Design_Logic_Corrected.md §0),
then immediately drop into precise per-technique parameters — the taxonomy organizes the
introduction, it doesn't replace the specifics:
- **ScaleStable** — environment-referenced (world-locked), 0.5–3.5 m operational range,
  continuous scale adjustment for constant angular size.
- **PeriphGuide** — user-referenced, head-referenced, offset clamped **±21.5°H** (vertical
  value pending the same correction — resolve before finalizing for submission).
- **AdaptiveLock** — environment-referenced ↔ body-referenced, binary threshold at 0.3 m/s,
  discrete switch, world-locked stationary / body-locked moving.
- **AdaptiveFlow** — body-referenced ↔ environment-referenced, graded threshold at 1.5 m/s
  (or fast yaw >150°/s), ~2 s continuous interpolation.

**State the threshold-placement rationale explicitly in this section** (from
Design_Logic_Corrected.md §B): AdaptiveLock's threshold answers a binary question (moving at
all, yes/no); AdaptiveFlow's answers a graded one (motion disruptive enough to justify a
costly transition). A shared threshold would collapse one technique toward the other's
behavior across the 0.3–1.5 m/s range where most of the waypoint task actually happens —
state this prospectively, from each technique's design purpose, not as a post-hoc defense
of the data.

**Tasks**: waypoint navigation (mobility) concurrent with slide-deck memory encoding
(cognitive), 12-item immediate recall per condition — unchanged from the ISMAR version.

**Measures**: interface attention ratio, immediate recall accuracy, temporal availability,
NASA-TLX, SUS, preference ranking.

**Gaze measurement (upgraded)**: AOI classification via gaze-ray intersection against the
HoloLens spatial mesh compared to the fixed panel-distance plane — the nearer intersection
along the ray determines the classification (panel vs. environment), replacing pure
bounding-box intersection. This resolves the "looking through the semi-transparent panel"
ambiguity R1 raised structurally, rather than only bounding it with a post-hoc sensitivity
check. State the method precisely in Measures; keep the sensitivity-check argument
(≤10% misclassification doesn't change significant contrasts) as a secondary robustness note
rather than the primary defense.

**Session**: 8 conditions × ~16 min (task + recall + questionnaires + break) ≈ 128 min, plus
setup/calibration/practice (~20–30 min) and a mid-session break (~30 min) ≈ **2.5–3 hours
total** — shorter than the original 3–4.5 hour, 12-condition design; state this explicitly as
a structural response to the fatigue concern, not a footnote.

---

## Results (ordering is the argument)

1. **Lead with the dissociation**: ScaleStable worse on recall and interface attention time,
   *and* still tops SUS and preference-ranking votes alongside AdaptiveLock. State this
   contrast as the headline of Results, first paragraph — not an "interestingly" aside after
   the main effects.

2. **Explain AdaptiveLock vs. AdaptiveFlow differences using the threshold-placement logic**,
   not just "one is discrete, one is continuous." If AdaptiveFlow shows more gaze
   transitions, longer time-in-transition, or higher workload than AdaptiveLock, tie it
   explicitly to the mechanism: AdaptiveFlow's threshold sits further out on the speed axis
   and its transitions take ~2 s, so it spends more of the session in transit or in an
   accessible mode that AdaptiveLock exits sooner via a discrete snap. Connect data to
   mechanism here — don't just report the contrast as a technique-level curiosity.

3. **Performance mechanism** (accessibility → recall/attention) — the explanatory step, not
   the headline. Report main effects (F, p, η²) here.

4. **Robustness**: 95% CIs on all key contrasts, Friedman non-parametric check, trial-order
   mixed-effects null result (reported plainly as a fatigue check).

5. Workload: report whether technique shows an effect at this load level — in the ISMAR
   draft it didn't (environment drove workload, not technique); if this replicates, note it
   plainly as the setup for Study 2, where workload *does* start showing technique effects
   once cognitive load increases.

---

## Discussion

End on the real open question, stated directly: if users prefer low-interference stability
even when it measurably costs them performance under *moderate* mobility-dominant load, what
happens as cognitive/environmental load increases instead — does that preference get
reinforced, or does performance catch up to it? That question is why Study 2 exists — not
"let's also test a collaborative task for breadth."

---

## What this locks in for the rest of the paper

- Method §3 (Design Space) must carry the reference-frame taxonomy language and the
  threshold-placement rationale in full — both are referenced here but belong there first.
- Limitations §9 should note the two-environment scope and the depth-based gaze method's
  own residual ambiguity (it resolves the transparency issue but still can't distinguish two
  overlapping real-world objects at similar depth — a much narrower, more defensible
  residual limitation than the original bounding-box ambiguity).
- No baseline condition means the paper's defense against "how much do these improve over
  traditional anchoring" continues to rest on the pilot study plus the softened
  "outperformed" language already planned in the Introduction/Abstract — this wasn't
  strengthened by this round of decisions, so that softening still needs to happen exactly as
  previously planned.
