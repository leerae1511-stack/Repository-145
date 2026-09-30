# Tool Pocket Generator V145

## Provenance
- Rebuilt directly from the supplied `Tool_Pocket_Generator_V139_FINAL(1).zip`.
- V140–V144 were intentionally not used as the source. This is a controlled restart from V139, the requested baseline.

## Exactly what changed
- **Add point placement only:** when Add point is active, the tap is projected onto the sampled profile line before the point is inserted.
- The projection uses `sampled()` with the current Straight/Curve modes, matching the curve interpretation used by the profile drawing logic.
- The inserted point remains a new Straight point and the existing insertion/renumbering flow is retained.
- Version labels/output markers identify this rebuild as V145. The saved-tools storage key is retained for compatibility.

## Problem addressed
A tap used to insert a point at the raw canvas tap coordinates, rather than snapping it to the displayed outline. On curved sections this could leave the new point away from the visible profile.

## Process / order
1. Start from V139.
2. Add one helper to find the nearest location on the displayed sampled outline.
3. Change only the Add point pointer handler to insert at that projected location.
4. Preserve the existing point insertion index logic, point mode default, undo, autosave, and downstream geometry workflow.

## Not changed
- Finger reliefs (FRs)
- Existing profile points, coordinates, numbering, and Straight/Curve modes
- Insert point button behaviour
- Dimensions, physical-grid workflow, Geometry Check, STL generation, or JSON structure apart from the app version value
- Other controls and layout

## Retest instructions
1. Open the V145 page and load/create the same profile used for the previous test.
2. Activate **Add point**.
3. Tap near a straight section of the visible outline. The new Straight point should appear on the line.
4. Undo, activate Add point again, and tap near a curved section. The new Straight point should appear on the displayed curve.
5. Check that existing points and the rest of the profile have not moved unexpectedly.
6. Report the result; Safari/iPad behaviour has not been verified by this build process.

## Verification
- ZIP integrity checked.
- Source-level checks confirm the new helper is called from the Add point handler.
- No claim is made that the interactive behaviour has been tested in iPad Safari.
