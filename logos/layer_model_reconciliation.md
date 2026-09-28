# Layer Model Reconciliation

Three files define the social layer axis, two agree exactly, and the third is a differently-shaped object that was forked rather than reconciled.

- `logos_combined_v01.json#structural.axes.scale` is canonical: `self, dyad, small_group, local_network, institution, global`.
- `structural_operator.py:23` `VALID_SCALES` holds the same six values and its comment cites combined as the canonical source.
- `logos_social_v01.json` holds seven sized layers: `person(1), intimate(5), sympathy_group(15), village(150), culture(500), religion(null), society(1500)`.
- Combined calls its layers "coordinate points, not social labels" and gives scale six positions alongside six sibling axes — density, persistence, authority, transmission, memory_channel, language_mode.
- Social calls its layers containers: each carries signify coordinates, a first-class `operators` reference, and an `_inferences` array for accumulating evidence.
- The fork is therefore structural before it is nominal — one file makes a layer a coordinate, the other makes it a container.
- Four rungs correspond without dispute: `person`/`self`, `sympathy_group`/`small_group`, `village`/`local_network`, and the ordering from self outward.
- `intimate(5)` and `dyad(2)` occupy the same rung at different sizes, which is an unreconciled numeric discrepancy, not a disagreement about what the rung is.
- Dunbar's 50 layer appears in neither file, so both ladders skip a documented rung of the series they cite.
- `religion` is agreed non-dimensional by both files: social records `size: null` with the note "no size bound — crosses Dunbar frame", and structural_operator lists it among cross-cutting overlays.
- `culture(500)` and `society(1500)` are the genuine conflict: sized layers in social, cross-cutting overlays in structural_operator's prompt.
- `family` exists only in structural_operator, as an overlay spanning self through small_group, and has no entry in the social schema.
- Social stakes a falsifiable claim at `culture`: "phase transition — cooperative.status flips to violated, resonance becomes illusion; status quo operator begins here".
- Social stakes a second at `society`: "status quo operator fully operational here — archive transmission, sovereign authority, cooperative violated".
- Those two notes make the culture-versus-overlay question empirical rather than editorial, because they predict where reading behaviour changes on the ladder.
- The field cannot currently test either claim: all three canonical field tellings read `institution`, so no case spans the 150-to-500 boundary where the predicted transition sits.
- `cross_scale.py` consumes the combined/operator six and never reads the social seven, so the store's link structure rests entirely on the canonical axis.
- The social schema's `_inferences` arrays are empty at all seven layers and no code writes to them, so the container model has never been exercised.
- Reconciling the four agreed rungs changes no stored coordinate, because the operator already writes only canonical values and coerces anything else to null.
- Changing `intimate` to 2 or `dyad` to 5 would alter the instrument and require re-reading the field, so it is deferred rather than settled here.
- Deciding culture and society requires cases selected to span the 500 boundary, which is corpus work gated on the unjudged blind round-trip in `experiments/round_trip/`.
- This document records the mapping so the two models stop drifting silently; it resolves nothing that needs evidence.

## Mapping

| social schema | size | canonical axis | status |
|---|---|---|---|
| person | 1 | self | agreed |
| intimate | 5 | dyad | same rung, size differs (2 vs 5) |
| — | 50 | — | Dunbar rung absent from both |
| sympathy_group | 15 | small_group | agreed |
| village | 150 | local_network | agreed |
| culture | 500 | *overlay in operator* | OPEN — layer or overlay |
| religion | null | *overlay in operator* | agreed non-dimensional |
| society | 1500 | *overlay in operator* | OPEN — layer or overlay |
| — | — | institution | form-named, unsized, no social counterpart |
| — | — | global | form-named, unsized, no social counterpart |
| — | — | family | overlay in operator only, absent from social |

<!-- llm: claude-opus-5 | 2026-09-28 | repos/pillars/logos/layer_model_reconciliation.md | created — records the mapping between logos_combined_v01#structural (canonical six), structural_operator.py VALID_SCALES and logos_social_v01's seven sized layers; documents agreement, the intimate/dyad size discrepancy and the open culture/society layer-or-overlay question; decides nothing requiring evidence -->
