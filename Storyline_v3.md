# Dynamic Anchoring — Storyline v3 (independent judgment, not reviewer-compliance)

v2 was organized as "section → which reviewer complaint this answers." That produces a
paper shaped like a rebuttal letter. This version is organized around what I think is
actually the strongest, most defensible scientific claim in this work, and treats reviewer
feedback as a checklist of *risks to avoid*, not as the paper's spine. Where a reviewer's
suggestion is just good methodology, I kept it — not because they said it, but because it's
correct on its own terms. Where a suggestion was really about defending against one
reviewer's specific (and sometimes idiosyncratic) reading, I cut it or folded it in so it
doesn't read as defensive.

---

## The one claim the paper should be built around

**Users' stated preference and their objective task performance point in different
directions, and which one "wins" is determined by what kind of processing load the task
places on them — not by how mobile they are.**

This is the actual finding worth publishing. Everything else (four techniques, two studies,
design guidelines) exists to demonstrate this claim cleanly. If a reader remembers one thing
from this paper, it should be this, not "we built four anchoring techniques."

Why this is objectively strong, independent of any reviewer:
- It's counterintuitive (better performance did not win preference — twice, in two very
  different task types), which is what makes a finding worth a paper rather than a systems
  demo.
- It has direct design consequences: it tells you that optimizing for the metric you can
  measure (accuracy, attention time) can produce an interface people actively don't want to
  use, which is a real and generalizable risk in any adaptive-interface design, not just AR
  anchoring.
- It's falsifiable and was actually tested twice under different conditions, which is what
  makes it a finding rather than an anecdote.

Everything below is in service of stating this claim as cleanly and confidently as possible.

---

## 1. Introduction

**Do not open on "mobile AR is hard because dual attention."** Every anchoring paper opens
this way; it signals "incremental systems paper" before the reader gets to the actual
contribution. Open on the tension instead:

> Anchoring techniques are usually evaluated by how well they let users access digital
> content. This paper asks a different question: when accessibility and user preference
> disagree, which one should drive design — and does the answer change with context?

Then, in order:
1. One paragraph on the three traditional anchors and their known trade-off (stability vs.
   accessibility vs. occlusion) — scoped precisely, no overclaiming that they "fail" at
   mobile AR generally.
2. **Cut the standalone "why AR not VR" rebuttal paragraph from v2.** It read as defensive
   because it was written to answer a specific complaint. Instead, fold the actual
   distinction (physical stakes, unscripted environment, mutual occlusion) into the *problem
   motivation* paragraph as the reason accessibility/preference can diverge in AR specifically
   — i.e., use it to set up the paper's real claim, not to pre-empt an objection. Same content,
   different job: motivating, not defensive.
3. State plainly that the four techniques are design probes built from established
   mechanisms (scaling, peripheral clamping, motion-triggered switching, smooth
   interpolation), used to sample the accessibility–interference space — not pitched as
   inventions. This isn't a concession to R2; it's just an accurate description, and accurate
   descriptions read as more confident than inflated ones.
4. Contribution statement, three items, but reordered so the dissociation finding leads:
   (1) preference and performance dissociate, and the direction of the dissociation flips
   with task context; (2) a two-study empirical comparison across mobility-dominant and
   cognition-dominant contexts, showing this isn't a one-off; (3) a compact design framework
   for when to optimize for which.

---

## 2. Related Work

**Job, stated independent of R1:** a reader cannot evaluate whether "preference and
performance dissociate" is new without knowing what's already known about anchoring
adaptation. This is not citation-padding for review — it's the actual epistemic function of
related work.

Keep the five works (Lindlbauer, Lu, Pfeuffer, Jannat, Satkowski, path-anchoring), but frame
each one by what it *predicts* about this paper's finding, not by "how it's different":
- Lindlbauer's context-aware adaptation predicts stability should track task complexity —
  consistent with this paper's Study 2, worth saying so plainly rather than defensively
  distinguishing.
- Jannat's body-anchoring is the nearest neighbor; if their data shows a similar
  preference-performance split, that's corroboration worth citing directly, not a threat to
  novelty — genuinely useful cross-study synthesis reads as generous, not competitive.
  (Someone needs to actually check this before drafting — if Jannat doesn't report
  preference alongside performance, say that gap is exactly why this paper's contribution
  matters.)
- Lu's glanceable/on-demand AR is a genuinely different bet (user-initiated vs.
  system-driven access) — name it as the natural alternative design this paper didn't test,
  not as a threat to be distinguished from.
- Path-anchoring and AdaptiveLock: resolve this once, cleanly, as a definitional note in §3
  rather than in Related Work — it's a mechanism question, not a literature-positioning
  question.

---

## 3. Design Space & Techniques

Keep from v2: precise parameters instead of vague adjectives, the panel-size-vs-location
distinction, the corrected AdaptiveLock direction, the precise AdaptiveFlow trigger. These are
kept because precise, falsifiable descriptions are just better writing — not because a
reviewer asked for them. State them once, correctly, with no hedging language ("attempts to,"
"tries to") — the vague framing in the draft (e.g., "AdaptiveLock tries to provide optimal
positioning") undersells results that were actually clean.

Cut: any sentence whose only job is pre-empting a specific critique (e.g., defensively
explaining why FoV differs by design before anyone has objected). State the design rationale
positively instead — "location is the manipulated variable; size is held constant" — and let
it stand on its own logic.

---

## 4. Study 1 — mobility-dominant context

Same method as v2 (2 environments, full counterbalancing, RQ not H) — kept because these are
just correct methodological choices (confounds are real regardless of who flagged them), not
because of reviewer pressure.

**Results narrative, reordered around the paper's actual claim:**
1. Lead with the dissociation, not with the performance result. ScaleStable is worse on
   recall and attention time *and* still wins preference and SUS. State this as the headline
   finding of Study 1, not as an "interestingly" aside buried after the main effects.
2. Then explain the performance side (accessibility drives recall) as the mechanism, not the
   headline.
3. Robustness checks (CIs, Friedman, trial-order null result) belong here as ordinary good
   practice — reported plainly, not flagged as "responding to a concern."

**Discussion:** end by asking the real question the finding raises — if people prefer
low-interference stability even when it costs them measurable performance under moderate
load, does that preference get stronger or weaker as cognitive load increases? That's the
actual scientific motivation for Study 2 — not "let's also test a collaborative task for
breadth."

---

## 5. Study 2 — cognition-dominant context

**Results narrative:** lead with the fact that the dissociation *reverses direction* —
ScaleStable now wins on both preference and the objective collaboration-quality measure,
despite lowest interface attention. This is the second data point that makes the claim a
pattern rather than a one-off: preference tracked stability in both studies, but performance
flipped to agree with preference once cognitive/environmental load became the dominant
demand instead of mobility.

State the mechanism plainly: interference has a cost that scales with how much sustained
attention the environment/task demands, and that cost was invisible under Study 1's
lighter cognitive load. This is a real, general claim about attention economics, not a
narrow AR finding — say it at that level of generality once, clearly.

---

## 6. Cross-Study Synthesis

One paragraph stating the general principle, independent of anchoring specifically:

> When task demands are dominated by motor/navigational load, accessibility is worth its
> interference cost. When task demands are dominated by sustained cognitive/environmental
> processing, interference cost dominates and stability wins — even against users' own
> objective performance in the first context. Preference tracks the second pattern in both
> studies; performance only catches up to preference once cognitive load is high enough.

This sentence is the paper. Everything else is evidence for it.

Related-work integration goes here, but as *genuine engagement* — where this paper's finding
sharpens, contradicts, or extends Lindlbauer/Jannat/Lu — not as an obligatory paragraph
proving "we read the literature."

---

## 7. Design Guidelines

Keep the four orthogonal dimensions from v2 (they're just better organized than the original
five, independent of who flagged the redundancy) — but derive them explicitly from the
dissociation finding rather than presenting them as a generic checklist:

1. **Diagnose which load dominates** — this determines whether to optimize for accessibility
   or stability at all.
2. **Match reconfiguration frequency to load** — continuous adaptation is fine under light
   load, costly under heavy load (Study 2's AdaptiveFlow result).
3. **Decide explicitly which metric you're designing for** — accessibility and preference are
   not proxies for each other; picking one without saying so is a design error, not a neutral
   choice.
4. **Consider who initiates access** — system-driven vs. user-initiated (Lu's glanceable
   model) is untested here and worth flagging as the open question.

---

## 8. Limitations

Keep only limitations that are real (2-environment scope, HoloLens FoV, N, gaze-through
ambiguity) — state them as scope, not apology. Cut any limitation whose only purpose is
answering a specific reviewer objection nobody else will raise (e.g., don't spend a full
paragraph rebutting a smoothing critique that's already foreclosed by stating the design
correctly in §3).

---

## 9. Conclusion

One paragraph. The finding that should travel beyond this paper is that user preference and
objective performance are separable design targets whose relationship flips with cognitive
context — designers who chase one metric without checking the other risk building interfaces
that perform well and get rejected, or feel good and quietly fail their users. Anchoring is
the testbed here; the claim is broader than anchoring.

---

## What actually changed from v2, and why

| v2 | v3 | Why |
|---|---|---|
| Organized by "which reviewer objection this section answers" | Organized around one central claim (preference/performance dissociation + reversal) | A paper should have a spine independent of any specific critique |
| "Why AR not VR" as a standalone rebuttal paragraph | Same content, refolded into problem motivation | Same facts, not defensive framing |
| Four techniques introduced modestly *because R2 said so* | Four techniques introduced modestly *because that's what they are* | Accuracy, not concession |
| Dissociation finding reported as "interestingly, despite..." | Dissociation finding is the headline of both studies' results | It's the actual contribution — lead with it |
| Design guidelines presented as a fixed checklist | Design guidelines derived explicitly from the dissociation finding | Guidelines should follow from the claim, not sit beside it |
| Heavy defensive framing around FoV/smoothing | Stated once, correctly, in §3; no rebuttal-shaped paragraphs elsewhere | Confidence reads better than defense |
