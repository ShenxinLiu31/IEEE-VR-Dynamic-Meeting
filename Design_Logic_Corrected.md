# Design Logic of the Four Anchoring Techniques — Corrected

Mechanistic decomposition of ScaleStable, PeriphGuide, AdaptiveLock, and AdaptiveFlow,
updated per implementation verification. This document describes implementation only — no
context, no performance claim. Evidence is reported separately in Studies 1–2.

---

## A. Two structural questions, four techniques

**Q1** — Does the panel commit to one reference frame for the entire session, or does it
change reference frame in response to the user's real-time motion state?

### Single, fixed reference frame

**Q2** — What property is fixed or constrained to compensate for that frame's structural
weakness?

**ScaleStable** — *world-locked*
- **Weakness**: accessibility degrades with viewing distance/angle.
- **Compensates via**: continuous scale adjustment — constant angular (retinal) size.
- Operational range 0.5–3.5 m · continuous user-facing rotation · Move/Rotate Lerp = 0.1.

**PeriphGuide** — *head-locked*
- **Weakness**: persistent occlusion of central vision.
- **Compensates via**: fixed angular offset, clamped to the periphery of the FoV.
- Render distance 0.8–1.0 m · offset clamped **±21.5°H** / ~~±30°V~~ **[see FoV flag below]** ·
  reorients if outside bounds.

> **Correction applied**: horizontal clamp changed from ±40°H to **±21.5°H**, matching the
> HoloLens 2's actual horizontal FoV (43°H total ÷ 2). ±40°H was nearly double the device's
> real horizontal field and is very likely the exact source of R3's "not actually peripheral"
> critique — a reviewer who checks HoloLens 2 specs against the stated number would catch this
> immediately.

> **⚠ Unresolved — flagging, not silently fixing**: you only asked me to correct the
> horizontal value, but the same error class applies to two more numbers that weren't in
> scope for this edit:
> 1. **PeriphGuide's vertical clamp (±30°V)** — HoloLens 2's vertical FoV is ~29° total,
>    i.e. **±14.5°V** from center. ±30°V is more than double the real vertical field, same
>    problem as the horizontal one just fixed. Left as-is in this draft pending your
>    confirmation, but a reviewer checking one number will very likely check the other.
> 2. **AdaptiveLock's walking-state clamp (±30°H/±20°V)** — ±30°H also exceeds the real
>    ±21.5°H horizontal boundary. Same category of error, different technique. If you fix
>    PeriphGuide's numbers and leave AdaptiveLock's inconsistent, a careful reviewer who
>    verifies one will likely verify the other and find the same problem still standing.
>
> Recommend resolving both before this is finalized for submission — say the word and I'll
> apply the same correction pattern to these two.

### Reference frame switches with motion state

**Q2′** — Both techniques share the same three-tier motion classifier (stationary <0.3 m/s ·
slow–moderate 0.3–1.5 m/s · fast >1.5 m/s, or head yaw >150°/s). Where is the switch
threshold placed on this shared scale, and how is the transition executed?

**AdaptiveLock** — *world ↔ body-locked*
- **Threshold at**: stationary ↔ moving boundary (0.3 m/s) — a binary distinction.
- **Executed as**: discrete, instantaneous reassignment.
- World-locked when stationary >0.5 s (within 1 m radius) · **body-locked** while moving
  (0.85 m, ±30°H/±20°V — flagged above for the same FoV correction).

**AdaptiveFlow** — *body ↔ world-locked*
- **Threshold at**: slow–moderate ↔ fast boundary (1.5 m/s or fast yaw) — a graded
  distinction.
- **Executed as**: continuous ~2 s interpolation.
- **Body-locked** below threshold (0.85 m) · temporarily world-locked above threshold ·
  low-pass filter α ≈ 0.6–0.8, eases back as motion subsides.

> **Correction applied (both techniques)**: the accessible/moving-state reference frame is
> confirmed **body-locked**, not head-locked. Removed the "confirm body- vs head-locked" flag
> from both entries and from the figure caption. This should be cross-checked once against
> §5.1.2 and the Fig. 1 captions in the manuscript to make sure every mention agrees — this is
> exactly the category of error (one section says one thing, another section says the
> opposite) that already cost you an "undeniable error" citation from two reviewers on
> AdaptiveLock once before; worth a full-text search for "head-locked" near "AdaptiveLock" or
> "AdaptiveFlow" before submission, not just fixing this one document.

---

## B. Why AdaptiveLock and AdaptiveFlow do *not* share a threshold — and why that's correct

| Speed | AdaptiveLock | AdaptiveFlow |
|---|---|---|
| Stationary (0–0.3 m/s) | world-locked | body-locked |
| Slow–moderate (0.3–1.5 m/s) | body-locked | body-locked |
| Fast (>1.5 m/s or fast yaw) | body-locked | world-locked (temp.) |

The two techniques agree only in the middle band (0.3–1.5 m/s) — both accessible. At the two
extremes they diverge, and **this divergence is deliberate, not an oversight**:

- **AdaptiveLock's threshold answers a binary design question**: is the user moving at all?
  Any nonzero movement should get accessible (body-locked) content — there is no principled
  reason to withhold accessibility during moderate walking, since the whole point of the
  technique is immediate response to the stationary/moving distinction.
- **AdaptiveFlow's threshold answers a different design question**: at what point does motion
  become disruptive enough that a body-locked panel becomes hard to track, justifying the cost
  of a ~2 s transition? That point is *fast* motion specifically, not any motion — a
  continuous interpolation triggered too early (e.g., at 0.3 m/s) would keep the panel in
  transit for most of a normal walking bout, since sustained walking speed routinely exceeds
  0.3 m/s. The panel would rarely settle into either mode, undermining exactly the behavior
  AdaptiveFlow is designed to test.

**Aligning the two thresholds breaks one of the two techniques regardless of which direction
you align them:**
- Lowering AdaptiveFlow's threshold to 0.3 m/s puts it in near-continuous transition during
  ordinary walking — neither stable nor reliably accessible, likely depressing its recall
  performance for reasons unrelated to "transition style," the variable actually under test.
- Raising AdaptiveLock's threshold to 1.5 m/s makes it world-locked through the entire
  moderate-walking range — which is where most of Study 1's waypoint-navigation task actually
  happens — collapsing AdaptiveLock's behavior toward plain world-locked for most of the
  session and undermining the very recall advantage that supports the paper's central
  dissociation finding (AdaptiveLock: good recall, high preference).

**Framing note for the manuscript**: state this design rationale prospectively, from each
technique's stated purpose (binary vs. graded transition), not retrospectively from the
results. Do not write "we kept thresholds different because aligning them hurt performance" —
that reads as data-driven post-hoc justification. Write it as: each technique's threshold
placement follows directly from the specific design question it answers; a shared threshold
would eliminate the behavior each technique was built to test. This paragraph needs to appear
in §3 (Design Space) or Study 1 Discussion — right now it exists only in this analysis, not
in any manuscript draft.

---

## Summary of changes in this pass

| Item | Status |
|---|---|
| PeriphGuide horizontal clamp ±40°H → ±21.5°H | ✅ Fixed |
| PeriphGuide vertical clamp ±30°V | ⚠ Flagged, not fixed — same error class, needs your confirmation |
| AdaptiveLock clamp ±30°H/±20°V | ⚠ Flagged, not fixed — same error class, needs your confirmation |
| Body- vs head-locked ambiguity (AdaptiveLock/AdaptiveFlow) | ✅ Confirmed body-locked, flags removed |
| Threshold misalignment (AdaptiveLock 0.3 m/s vs. AdaptiveFlow 1.5 m/s) | ✅ Kept as-is; design rationale written out in §B above — must be moved into the actual manuscript, not left in this standalone doc |
