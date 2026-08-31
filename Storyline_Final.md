# Dynamic Anchoring — Final Outline

Central claim the whole paper serves: **user preference and objective task performance for
AR anchoring techniques dissociate, and which one "wins" flips depending on whether the
task's dominant demand is motor/navigational or cognitive/environmental.** Four techniques
and two studies exist to demonstrate this claim cleanly, not as independent contributions.

---

## Title

Something that names the finding, not the system. Avoid "Four Anchoring Techniques for..."
Prefer a form like: *"When Stability Beats Access: A Cross-Context Study of Preference–
Performance Trade-offs in Mobile AR Anchoring."* (placeholder — refine once Abstract is final)

---

## Abstract (150–200 words)

1. One sentence: mobile AR anchoring is usually optimized for accessibility.
2. One sentence: we show accessibility and user preference are not the same target, and
   report which one should drive design under which conditions.
3. One sentence: method — 4 anchoring techniques (ScaleStable, PeriphGuide, AdaptiveLock,
   AdaptiveFlow), tested across two studies spanning a mobility-dominant individual task and
   a cognition-dominant collaborative task.
4. Two sentences: Study 1 — accessible techniques win on recall and attention time, but users
   still prefer the least accessible one (ScaleStable). Study 2 — under heavier cognitive/
   environmental load, ScaleStable wins on both preference *and* objective collaboration
   quality — the dissociation reverses.
5. One sentence: contribution — evidence that preference and performance require separate
   optimization targets, plus a compact framework for deciding which one to chase.
6. No "outperformed" language without qualification; no claim of new anchoring mechanisms.

---

## 1. Introduction

### 1.1 Opening (no dual-attention cliché)
Open directly on the tension: anchoring is normally judged by how accessible content is.
State plainly that accessibility and what users actually prefer can point in opposite
directions, and that this paper asks *when* they diverge and *why*, using anchoring as the
testbed.

### 1.2 The three traditional anchors (scoped precisely)
One paragraph. World-locked (stable, requires user movement to access), head-locked
(always accessible, occludes centrally), body-locked (accessible during movement, still
centrally occupies view). State their known trade-off exactly — stability vs. accessibility
vs. occlusion — without claiming they "fail" at mobile AR in general terms.

### 1.3 Why this diverges specifically in AR (motivating, not defensive)
Fold in the AR-specific reasoning as motivation, not rebuttal: physical stakes of inattention,
an unscripted/unpredictable environment, mutual occlusion between real and virtual content,
and fixed-focal-plane content over continuous-depth real-world (vergence-accommodation
mismatch). The point of this paragraph: these are the reasons accessibility and preference
can come apart in AR in a way they wouldn't in a fully virtual environment. One paragraph,
no more.

### 1.4 The gap
State plainly: prior work has proposed individual mechanisms for improving on
world/head/body-locking (scaling, peripheral placement, motion-triggered switching,
smoothing) but has not asked whether *users actually want* what improves their measurable
performance, nor whether the answer changes with task type. That absence is the gap.

### 1.5 Four design probes (not "four novel techniques")
One sentence each, exact parameters, no hedging verbs ("attempts to," "tries to"):
- **ScaleStable** — world-locked + distance-based angular scaling (constant apparent size,
  0.5–3.5 m operational range).
- **PeriphGuide** — head-locked but peripheral-clamped (±40°H/±30°V), not centered.
- **AdaptiveLock** — locomotion-state-triggered discrete toggle: body-locked while walking
  (>0.3 m/s), world-locked while stationary (>0.5 s still). [Confirm this is the final,
  correct direction before drafting — this was inconsistent across the ISMAR draft.]
- **AdaptiveFlow** — same toggle logic, ~2 s continuous interpolation instead of a discrete
  switch; triggers on fast walking (>1.5 m/s) OR head yaw (>150°/s), acting at different
  timescales (immediate vs. after 2 s smoothing).

### 1.6 Two studies, framed by dominant demand, not by "individual vs. collaborative"
Study 1: high mobility, moderate cognitive load, individual dual-task.
Study 2: moderate mobility, high cognitive/environmental load, collaborative sensemaking.
This framing is what licenses the cross-study claim later — the axis that matters is *load
type*, and task social structure (individual/collaborative) is a secondary feature, not the
independent variable.

### 1.7 Contribution statement (three items, dissociation first)
1. Evidence that preference and objective performance dissociate for anchoring choice, and
   that the direction of the dissociation depends on whether motor or cognitive/
   environmental demand dominates.
2. A two-study empirical comparison spanning both regimes, showing the pattern replicates
   rather than being a single-task artifact.
3. A compact, four-dimension design framework for deciding which target (accessibility vs.
   stability/preference) to optimize for, and how often to reconfigure.

---

## 2. Related Work

### 2.1 Reference-frame fundamentals
World/head/body-lock definitions, one paragraph, citing the standard sources.

### 2.2 Context-aware and adaptive AR interfaces
- **Lindlbauer 2019 (Context-Aware MR, UIST)** — adapts layout/complexity to task context.
  State what it would predict about this paper's Study 2 result, and whether the data agrees.
- **Pfeuffer 2021 (ARtention, C&G)** — gaze-adaptive design space; complementary axis
  (gaze state vs. motion state as the adaptation trigger).

### 2.3 Anchoring techniques (the central-topic subsection — must not be thin)
- **Path-anchoring [ref]** — closest mechanism-level neighbor to AdaptiveLock. Resolve the
  relationship explicitly here: same locomotion-triggering logic or not, and if similar
  enough, state why AdaptiveLock is still a distinct point in the design space (discrete
  toggle vs. path-following) or rename it if it isn't.
- **Jannat 2025 (Body-Anchored AR, ISMAR)** — nearest empirical neighbor. Check specifically
  whether their data reports preference alongside performance; if yes, compare directly
  (agreement = corroboration, disagreement = interesting boundary condition); if no, state
  that gap as part of this paper's contribution.
- **Satkowski 2022 (Above & Below, ISMAR)** — underused-FoV placement; relevant contrast for
  PeriphGuide's peripheral-clamping logic.

### 2.4 On-demand / glanceable access
- **Lu 2023 (Glanceable AR, SUI)** and **Chang et al. [on-demand hiding]** — user-initiated
  access as the alternative to this paper's system-driven adaptation. Name explicitly as the
  design axis this paper does not test (ties to Limitations and Design Guideline #4).

---

## 3. Design Space & Technique Implementation

### 3.1 The trade-off framework
Two axes: field-of-view interference (how much digital content competes with/occludes
environmental processing) and information accessibility (how easily content can be reached
across mobility states). State plainly that traditional anchors each pick a fixed point on
this space; the four probes sample other points, including motion-adaptive ones.

### 3.2 Separating panel size from panel location
One explicit paragraph: angular size is held constant across all four techniques (state exact
values/ranges); *where* content sits relative to the user is the manipulated variable, because
that is the definition of anchoring. State this positively as the logic of the design, not as
a response to an anticipated objection.

### 3.3 Technique specifications
Table or itemized list with exact parameters for each of the four techniques (angular extent,
distance range, trigger thresholds, smoothing constants). All four techniques use temporal
smoothing (Lerp = 0.1) — state once here.

### 3.4 Implementation
HoloLens 2 + Unity, spatial anchors, motion thresholds (stationary <0.3 m/s, slow 0.3–1.5 m/s,
fast >1.5 m/s).

---

## 4. Study 1 — Mobility-Dominant Context

### 4.1 Research question
RQ1: When mobility demand is high and cognitive demand is moderate, how do anchoring
techniques compare on objective performance versus subjective preference?

### 4.2 Method
- **Participants**: 12 (report demographics).
- **Design**: 4 techniques × 2 environments (Open Space, Room-to-Room). Technique order and
  environment order both fully counterbalanced (state the specific scheme — e.g., 8-condition
  Williams design or independently counterbalanced Latin squares). Report resulting session
  length and note it is shorter than a 3-environment design would require.
- **Tasks**: waypoint navigation (mobility) concurrent with slide-deck memory encoding
  (cognitive), immediate 12-item recall test per condition.
- **Measures**: interface attention ratio, immediate recall accuracy, temporal availability,
  NASA-TLX, SUS, preference ranking.

### 4.3 Results (ordered around the claim)
1. **Lead with the dissociation.** ScaleStable significantly impairs recall (numbers) and
   draws less interface attention (numbers) than the other three — *and* still tops SUS and
   preference-ranking votes alongside AdaptiveLock. State this contrast as the headline
   result, in the first paragraph of Results, not as a later aside.
2. **Then the performance mechanism.** Report the recall and attention-ratio main effects
   (F, p, η²) as the explanation for *why* accessibility helps objectively.
3. **Robustness**: 95% CIs on all key contrasts; Friedman test as a non-parametric check;
   trial-order mixed-effects null result (reported plainly as a fatigue check, not flagged
   defensively).
4. Workload: no technique effect — note this plainly; it means accessibility differences
   didn't cost users measurable cognitive burden at this load level (important setup for
   Study 2, where this changes).

### 4.4 Discussion
State the real open question this raises: if users prefer low-interference stability even
when it measurably costs them performance under *moderate* load, what happens as cognitive/
environmental load increases — does preference get reinforced, or does performance catch up
to it? That question, not "let's test collaboration for breadth," is why Study 2 exists.

---

## 5. Study 2 — Cognition-Dominant Context

### 5.1 Research question
RQ2: When environmental processing and collaborative cognitive load dominate over mobility
demand, does the same dissociation hold, reverse, or disappear?

### 5.2 Method
- **Participants**: 12 dyads (24 total, report demographics), none from Study 1.
- **Task**: collaborative murder-mystery sensemaking; AR wearer navigates between two
  physical evidence stations (3.2 m apart) while synthesizing digital profiles with a remote
  partner. Five equivalent scripts control learning effects.
- **Design**: same 4 techniques, single task environment, counterbalanced technique order.
- **Measures**: interface attention ratio, communicative focus ratio, perceived attention
  allocation, NASA-TLX, perceived collaboration quality, preference ranking, qualitative
  interviews.

### 5.3 Results (ordered around the claim)
1. **Lead with the reversal.** ScaleStable wins on perceived collaboration quality
   (numbers) *and* spatial consistency/temporal availability, *despite* lowest interface
   attention ratio (numbers) of all four techniques. State explicitly: this is the same
   direction as Study 1's preference result, but now performance (collaboration quality)
   agrees with it instead of contradicting it.
2. **Cognitive cost becomes visible.** Unlike Study 1, workload now shows a technique effect:
   AdaptiveFlow's continuous transitions cost more than AdaptiveLock's discrete ones (numbers).
   State the mechanism: switching overhead that was invisible under Study 1's lighter load
   becomes measurable once collaborative reasoning raises baseline cognitive demand.
3. Qualitative evidence: quotes on predictability/shared reference for ScaleStable
   ("always knew where it was," "stayed aligned on the document"); quotes on disruption for
   AdaptiveFlow ("chasing it with my eyes"); PeriphGuide's persistent interference
   ("always in my way").

### 5.4 Discussion
State the reversal explicitly and connect back to Study 1: the preference for stability
wasn't noise — it was consistent across both studies. What changed is whether *objective*
performance agreed with it. Interference has a real cost, and that cost scales with how much
sustained attention the environment/task already demands.

---

## 6. Cross-Study Synthesis (opens General Discussion)

### 6.1 The general principle
State once, cleanly, at a level of generality beyond anchoring:

> When task demand is dominated by motor/navigational load, accessibility is worth its
> interference cost, and objective performance tracks accessibility. When task demand is
> dominated by sustained cognitive/environmental processing, interference cost dominates,
> and both preference and objective performance shift toward stability. User preference
> favored stability in both regimes; performance only caught up to it once cognitive load
> was high enough.

### 6.2 Engagement with related work (genuine, not obligatory)
- Compare directly against Lindlbauer's context-aware adaptation: does this paper's
  load-type axis subsume, extend, or conflict with Lindlbauer's complexity-based adaptation
  trigger?
- Compare directly against Jannat's body-anchoring results (per the check flagged in §2.3).
- Name Lu's glanceable/on-demand model as an untested third design axis (user-initiated vs.
  system-driven access) — sets up Design Guideline #4 and Limitations.

### 6.3 Why this matters beyond AR anchoring
One paragraph, stated generally: any adaptive interface that is tuned to a measurable
performance metric risks producing something users actively don't want, if the metric and
the user's actual cost function (visual interference, predictability, cognitive overhead)
are not the same thing. Anchoring is the testbed; the risk is general to adaptive-interface
design.

---

## 7. Design Guidelines

Four orthogonal dimensions, each derived explicitly from the dissociation finding above
(not presented as a generic checklist):

1. **Diagnose which load dominates before choosing an optimization target.**
   Motor/navigational load → optimize for accessibility. Cognitive/environmental load →
   optimize for stability/interference minimization.
2. **Match reconfiguration frequency to load level.** Continuous adaptation (AdaptiveFlow-
   style) is affordable under light cognitive load; under heavy load, discrete or static
   positioning costs less (Study 2's workload result).
3. **State explicitly which metric you are designing for.** Accessibility, objective
   performance, and user preference are three different targets that do not always move
   together — treating one as a proxy for the others is the design error this paper's data
   argues against.
4. **Consider who initiates access.** System-driven adaptation (this paper's four
   techniques) vs. user-initiated/glanceable access (Lu 2023) is an open design axis not
   tested here — flag explicitly as future work.

---

## 8. Limitations

State each as scope, not apology:
- Two environments (Open Space, Room-to-Room), chosen to permit full order counterbalancing;
  state explicitly why a third (narrow corridor) was dropped rather than leaving it
  unaddressed.
- HoloLens 2 FoV — acknowledge, tie back to §3.2's size/location distinction so it reads as
  accounted for, not overlooked.
- N=12 (Study 1) / 12 dyads (Study 2) — standard for within-subjects HCI/AR work; CIs
  reported throughout; Study 2's N=24 as corroborating scale.
- Gaze-through-transparent-panel measurement ambiguity — report the sensitivity check
  (≤10% misclassification does not change significant contrasts).
- On-demand/glanceable anchoring untested — explicit pointer to future work building on Lu
  2023.

---

## 9. Conclusion

One paragraph. The finding that should outlive this specific paper: user preference and
objective performance are separable design targets, and their relationship is not fixed —
it flips depending on what kind of demand a task places on the user. Designers who optimize
only for what they can measure risk building interfaces that perform well and get rejected,
or that feel good and quietly underperform. Anchoring in mobile AR is the testbed here; the
claim is broader than anchoring, and broader than AR.
