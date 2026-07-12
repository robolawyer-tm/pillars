# Reify Phase Two: Technical Specification — r1 (reconciled against live repos)

*Revision of [reify_phase2_spec.md](reify_phase2_spec.md) incorporating [review_2026_07_11.md](review_2026_07_11.md). Changes from r0 are marked ⟲. The governing philosophy is unchanged: analogical not statistical, trajectory not state, inspectability over confidence, honor failure.*

---

## Governing Constraint (read before implementing anything)

Schema pressure will concentrate here. The predictive layer consumes **only** membrane output (Logos coordinates); it has **no write path** to filing, vivification, or the fabric tree. Enforce this in code, not convention:

- Prediction modules import from the coordinate layer only. No imports from filing/promotion code.
- ⟲ Enforced by test: `tests/test_membrane.py` asserts the prediction module's import list contains no filing/promotion modules and that no prediction function signature accepts `raw_text`. The flat repo root makes convention the only wall; the test is the wall.
- No prediction function receives raw account text.
- Any proposal to "normalize accounts for better matching" is rejected by design. Matching quality improves by growing the precedent base, never by reshaping inputs.

⟲ Precedent for this constraint working: the 2026-07-10 contamination fix (operators commit `3944ecf`) — machinery vocabulary had colonized the emergent tree; the fix confined filing to left keywords. Same membrane, same discipline, already proven once.

---

## 1. New Container: the Restoration Vector

Sibling to `inf_*.json`. Trajectory, not snapshot.

**File:** ⟲ `res_<8-hex>.json` (hash id, matching the `inf_285ae7ab` convention — not sequential). Lives beside the account's inference container; indexed, but the human-walkable path is authoritative for reading.

```json
{
  "res_id": "res_9f3c21ab",
  "account_ref": "inf_285ae7ab",
  "scale": "institution",
  "signature_initial": {
    "act_type": "assertive",
    "cooperative": "honored",
    "transmission": "archive",
    "resonance": "illusion",
    "authority": "sovereign",
    "utility": "narrative",
    "social_field": {"grid": 0.85, "group": 0.3, "quadrant": "hierarchical"},
    "structural": {"layer": "institution", "scale": "institution"}
  },
  "intervention_trace": [
    {
      "type": "legal.remedy.exoneration_motion",
      "actor": "human_operator",
      "ts": "...",
      "notes_ref": "optional pointer, never inline prose"
    }
  ],
  "signature_terminal": {
    "resonance": "harmony",
    "...": "remaining dimensions re-read after outcome"
  },
  "delta": {
    "movements": { "resonance": ["illusion", "harmony"] },
    "tension_score": -0.42
  },
  "outcome": "restored | partial | unresolved",
  "_src": ["ostrom", "dunbar"]
}
```

Rules:
- `signature_*` fields hold coordinate values in Logos vocabulary. They are copied from the membrane (a normal logos re-read), never computed here.
- ⟲ **`delta` replaces r0's `tension_delta`.** The four tension types (structural/conflict/functional/resolution) are architectural node types, not per-account measurables — functional tension is "rules in CLAUDE.md," not a number an account carries. The delta is therefore: (a) `movements` — per-dimension coordinate changes over the eight logos dimensions, each expressible and enum-validated; (b) `tension_score` — the scalar left/right divergence delta, already measured by the pipeline. If typed per-account tension is ever actualized (it is listed unactualized in pillars/FLOW.md), the delta can grow — by deliberate schema change at the membrane, not by example drift.
- ⟲ **Terminal vocabulary decision:** terminal signatures reuse the existing enums (`resonance: illusion → harmony` is expressible today). Where restoration has no honest existing value (e.g. restored authority — current enum `sovereign|tribal|occult`), the enum grows by a deliberate, versioned addition to `config/coordinates.json`, reviewed as a membrane change. `logos_fused` validation stays authoritative; no value enters via a `res_` file first.
- `outcome: unresolved` vectors file under `unresolved/` (honest-latency sibling of `unclustered/`). Never coerced to `partial`.
- `resolution/` fabric paths autovivify only when a vector with `outcome: restored` is promoted. The vector does not create fabric structure directly — it is offered to the normal categorize→promote flow. ⟲ That flow now exists as code: `promote.py` (both repos, 2026-07-10); `unresolved/` reuses its empty-paths holding-pen pattern.

---

## 2. Scale (⟲ rewritten — substantially already built)

r0 treated scale as an unbuilt blocking dependency. In the live repos:

- `logos.structural` **already carries** `scale` and `layer` per inference (Sutton: `scale: institution`), emitted by `structural_operator.py` / `logos_fused.py`.
- `cross_scale.py` (vivify-operators) **already consumes it**: `scale = structural.scale or structural.layer`, builds Psi–Phi–Omega coordinate fingerprints, and surfaces cross-scale isomorphic pairs — r0's `cross_scale_analogy` concept, running today.

Remaining work, in order:

1. **Enum unification.** r0 proposed `person | dyad | group | institution | culture`; the structural layer vocabulary already in use is `self | dyad | small_group | local_network | institution | global`. **Use the existing vocabulary** — one scale language across `inf_*`, `res_*`, and cross_scale. Do not introduce a parallel enum. (Mapping for r0 readers: person→self, group→small_group, culture→global.)
2. **Require on containers.** `scale` is required on every new `res_*.json`, copied from the account's `logos.structural.scale`.
3. **Backfill = a structural_operator pass** over inferences lacking `logos.structural`, not a new mechanism. Where the operator cannot assign confidently, `"scale": null` — scale-pending, honest latency applies to metadata too.
4. Cross-scale matching rule (unchanged from r0): a precedent at scale S is a **direct precedent** only at scale S; at any other scale it is emitted as `cross_scale_analogy` with mandatory flag — a weak hypothesis, rendered differently (§5).

---

## 3. Right-Side Intervention Ontology (unchanged in substance)

The one place a fixed schema is correct. Typed, versioned, boring on purpose.

```
intervention/
  legal.remedy.*        (exoneration_motion, appeal, settlement, ...)
  cognitive.cbt.*       (reframing, exposure_protocol, ...)
  procedural.*          (record_correction, review_mandate, ...)
  relational.*          (mediation_session, facilitated_dialogue, ...)
```

- Namespaced dotted types; extension by adding leaves, never by loosening the grammar.
- An intervention record is a **trace of what was done** — machinery vocabulary, right-side only.
- Effect evaluation happens exclusively in Logos coordinates (`delta`, terminal signature). No intervention type carries a "success rate" attribute; efficacy lives in the vectors, contextualized by signature and scale.
- Membrane contract: intervention types cross into a `res_*.json` only inside `intervention_trace`. Nothing in the fabric tree, filing vocabulary, or coordinate space may reference an intervention type.
- ⟲ File as `config/interventions.json` beside `config/coordinates.json` — both are membrane schemas, versioned the same way.

---

## 4. Matching: the Precedent Reader

⟲ **Name decided: `precedent_operator.py`.** r0's alternative `resonate` is rejected by the abstraction's own terminology discipline — the empathy axis must not be overloaded.

⟲ **Build on `cross_scale.py`, do not start fresh.** Its Psi (resonance + cooperative), Omega (banded tension), and dynamic (conflict schema/behavior/terrain) fingerprint is the signature representation; its store-walk and pair-surfacing are the neighbor mechanics. The precedent reader extends it from *pairs of accounts* to *account → restoration vectors*.

Pipeline (read-only against the store):

1. **Input:** coordinate signature + scale of a new high-tension account.
2. **Neighbor search:** distance over the eight dimensions within same-scale vectors. Distance metric is per-dimension and ordinal where the lineage supports it — but the metric is machinery and its output is never shown as a number to the human reader.
3. **Partition:** direct precedents (same scale) / cross-scale analogies (flagged, via the existing cross_scale channel) / none.
4. **Compose:** emit a **prospective reading** — a second-order composition in Logos vocabulary describing candidate coordinate movements, e.g. `resonance: illusion → harmony`, each movement anchored to its precedent vectors by `res_id`.
5. **No-neighbor case:** emit honest latency — "the field cannot yet read a path here" — and file the query itself as demand signal for corpus growth. Never extrapolate.

Recursion hook: when new vectors are promoted, the precedent reader's neighbor index rebuilds as part of the existing corpus re-read. Self-evolution = the reachable-delta map refining, nothing more exotic.

---

## 5. Output Structure: the Prospective Rendering

Reify-phase output. Logos as communication: the grammar of the rendering **is** coordinate movement. ⟲ All movement values must be enum-valid per `config/coordinates.json` — the rendering inherits membrane validation; examples updated accordingly.

```json
{
  "rendering": "prospective",
  "account_ref": "inf_285ae7ab",
  "scale": "institution",
  "field_state": {
    "pressure": ["authority", "resonance"],
    "blockage": ["transmission"],
    "openings": [
      {
        "movement": { "resonance": ["illusion", "harmony"] },
        "precedents": ["res_9f3c21ab", "res_44a1c0de"],
        "standing": "direct",
        "reading": "accounts with this signature moved toward restoration when authority rebalanced and resonance realigned"
      },
      {
        "movement": { "authority": ["sovereign", "tribal"] },
        "precedents": ["res_b2276e01"],
        "standing": "cross_scale_analogy",
        "scale_of_precedent": "small_group",
        "reading": "a weak hypothesis carried across scale; read the precedent before acting"
      }
    ]
  },
  "human_gate": true
}
```

Rendering rules (unchanged from r0):
- **Never a probability, score, or ranking number in human-facing output.** Openings are ordered by precedent standing (direct before analogy) and precedent count — ordering is presentation, not verdict.
- Every opening links to walkable precedent nodes. Inspectability is the substitute for confidence intervals.
- `human_gate: true` is structural and permanent on prospective renderings: the system points, the human decides. No auto-apply path from rendering to intervention.
- Visual layer consumes this JSON; the JSON is the contract, the visual is presentation.

---

## 6. The Closed Loop (unchanged from r0, grounded)

1. Prospective rendering issued → human operator selects and enacts an intervention (right side).
2. Intervention trace recorded against the account.
3. On observed outcome: coordinates re-read (normal logos flow), terminal signature captured, `res_*.json` written with honest `outcome`.
4. Vector offered to categorize→promote (⟲ `promote.py`, live). `restored` may grow `resolution/` paths; `unresolved` files under `unresolved/`.
5. Corpus re-read fires; precedent index rebuilds; operators refine.

Failure handling is the integrity test of the whole phase: an `unresolved` vector is a first-class citizen of the store. If reporting pressure ever pushes toward reclassifying failures, the precedent base rots and prediction silently degrades into wishcasting.

---

## 7. Build Order (⟲ revised for what already exists)

1. **Scale unification + backfill** — adopt the existing structural vocabulary; run structural_operator over untagged corpus; `null` where unconfident. (Mostly an operator run, not new code.)
2. **`res_*.json` container** + `unresolved/` path + promotion wiring (reuses `promote.py`).
3. **Intervention ontology** — `config/interventions.json`, typed, versioned.
4. **`precedent_operator.py`** — extend `cross_scale.py`: same-scale matching first, cross-scale analogy channel second. Plus `tests/test_membrane.py` (import wall).
5. **Prospective rendering** JSON contract, then visual field on top.
6. Loop closure: outcome capture → vector promotion → index rebuild.

Each step is independently useful; none requires the later ones to justify itself. ⟲ Step 1 is smaller than r0 assumed; steps 1–2 together still upgrade the store from case library toward functional model.

<!-- llm: claude-fable-5 | 2026-07-11 | repos/pillars/reify_phase2/reify_phase2_spec_r1.md | created — reconciled revision of reify_phase2_spec.md: delta replaces typed tension_delta, terminal-enum protocol, scale section rewritten against live logos.structural + cross_scale.py, precedent_operator naming, hash ids, membrane test, build order regrounded -->
