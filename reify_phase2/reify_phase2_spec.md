# Reify Phase Two: Technical Specification

*Predictive layer — precedent-based prospective readings from the inferential store. Companion to `vivify-abstraction.md` §8. Intended for Claude Code ingestion into pillars.*

---

## Governing Constraint (read before implementing anything)

Schema pressure will concentrate here. The predictive layer consumes **only** membrane output (Logos coordinates); it has **no write path** to filing, vivification, or the fabric tree. Enforce this in code, not convention:

- Prediction modules import from the coordinate layer only. No imports from filing/promotion code.
- No prediction function receives raw account text.
- Any proposal to "normalize accounts for better matching" is rejected by design. Matching quality improves by growing the precedent base, never by reshaping inputs.

---

## 1. New Container: the Restoration Vector

Sibling to `inf_*.json`. Trajectory, not snapshot.

**File:** `res_<id>.json` — lives beside the account's inference container; indexed, but the human-walkable path is authoritative for reading.

```json
{
  "res_id": "res_00347",
  "account_ref": "inf_00347",
  "scale": "person",
  "signature_initial": {
    "authority": "sovereign",
    "resonance": "illusion",
    "...": "remaining six dimensions"
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
    "authority": "accountable",
    "resonance": "aligned",
    "...": "..."
  },
  "tension_delta": {
    "structural": -0.7,
    "conflict": -0.9,
    "functional": -0.2,
    "resolution": +0.8
  },
  "outcome": "restored | partial | unresolved",
  "_src": ["ostrom", "dunbar"]
}
```

Rules:
- `signature_*` fields hold coordinate values in Logos vocabulary. They are copied from the membrane, never computed here.
- `outcome: unresolved` vectors file under `unresolved/` (honest-latency sibling of `unclustered/`). Never coerced to `partial`.
- `resolution/` fabric paths autovivify only when a vector with `outcome: restored` is promoted. The vector does not create fabric structure directly — it is offered to the normal categorize→promote flow.

---

## 2. Scale Field (blocking dependency — implement first)

Add to the logos coordinate schema, all containers:

```json
"scale": "person | dyad | group | institution | culture"
```

- Required on every new `inf_*.json` and `res_*.json`.
- Backfill pass over existing corpus: assign where unambiguous, else `"scale": null` and file the account's coordinates as scale-pending (honest latency applies to metadata too).
- Cross-scale matching rule: a precedent at scale S is a **direct precedent** only for new accounts at scale S. At any other scale it is emitted as `cross_scale_analogy` with mandatory flag — a weak hypothesis, rendered differently (see §5).

---

## 3. Right-Side Intervention Ontology

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
- Effect evaluation happens exclusively in Logos coordinates (`tension_delta`, terminal signature). No intervention type carries a "success rate" attribute; efficacy lives in the vectors, contextualized by signature and scale.

Membrane contract: intervention types cross into a `res_*.json` only inside `intervention_trace`. Nothing in the fabric tree, filing vocabulary, or coordinate space may reference an intervention type.

---

## 4. Matching: the Precedent Reader (new operator)

A reusable interpretive mechanism in `vivify-operators/`, derived from the store per the operator pattern. Working name: `resonate` (or `precedent` if the overload with the resonance axis is too costly — decide in docs before code).

Pipeline (read-only against the store):

1. **Input:** coordinate signature + scale of a new high-tension account.
2. **Neighbor search:** distance over the eight dimensions within same-scale vectors. Distance metric is per-dimension and ordinal where the lineage supports it — but the metric is machinery and its output is never shown as a number to the human reader.
3. **Partition:** direct precedents (same scale) / cross-scale analogies (flagged) / none.
4. **Compose:** emit a **prospective reading** — a second-order composition in Logos vocabulary describing candidate coordinate movements, e.g. `resonance: illusion → aligned`, each movement anchored to its precedent vectors by `res_id`.
5. **No-neighbor case:** emit honest latency — "the field cannot yet read a path here" — and file the query itself as demand signal for corpus growth. Never extrapolate.

Recursion hook: when new vectors are promoted, the precedent reader's neighbor index rebuilds as part of the existing corpus re-read. Self-evolution = the reachable-delta map refining, nothing more exotic.

---

## 5. Output Structure: the Prospective Rendering

Reify-phase output. Logos as communication: the grammar of the rendering **is** coordinate movement.

```json
{
  "rendering": "prospective",
  "account_ref": "inf_00512",
  "scale": "institution",
  "field_state": {
    "pressure": ["authority", "resonance"],
    "blockage": ["secrecy"],
    "openings": [
      {
        "movement": { "resonance": ["illusion", "aligned"] },
        "precedents": ["res_00347", "res_00389", "res_00401"],
        "standing": "direct",
        "reading": "accounts with this signature moved toward restoration when authority rebalanced and resonance realigned"
      },
      {
        "movement": { "authority": ["sovereign", "accountable"] },
        "precedents": ["res_00122"],
        "standing": "cross_scale_analogy",
        "scale_of_precedent": "group",
        "reading": "a weak hypothesis carried across scale; read the precedent before acting"
      }
    ]
  },
  "human_gate": true
}
```

Rendering rules:
- **Never a probability, score, or ranking number in human-facing output.** Openings are ordered by precedent standing (direct before analogy) and precedent count — ordering is presentation, not verdict.
- Every opening links to walkable precedent nodes. The reader can leave the rendering and read the actual restored accounts. Inspectability is the substitute for confidence intervals.
- `human_gate: true` is structural and permanent on prospective renderings: the system points, the human decides. There is no auto-apply path from rendering to intervention.
- Visual layer (field of pressure / blockage / openings) consumes this JSON; the JSON is the contract, the visual is presentation.

---

## 6. The Closed Loop

1. Prospective rendering issued → human operator selects and enacts an intervention (right side).
2. Intervention trace recorded against the account.
3. On observed outcome: coordinates re-read (normal flow), terminal signature captured, `res_*.json` written with honest `outcome`.
4. Vector offered to categorize→promote. `restored` may grow `resolution/` paths; `unresolved` files under `unresolved/`.
5. Corpus re-read fires; precedent index rebuilds; operators refine.

Failure handling is the integrity test of the whole phase: an `unresolved` vector is a first-class citizen of the store. If reporting pressure ever pushes toward reclassifying failures, the precedent base rots and prediction silently degrades into wishcasting.

---

## 7. Build Order

1. **Scale field** in logos schema + backfill pass (everything depends on it).
2. **`res_*.json` container** + `unresolved/` path + promotion wiring.
3. **Intervention ontology** (right side, typed, versioned).
4. **Precedent reader operator** (read-only, same-scale matching first; cross-scale analogy second).
5. **Prospective rendering** JSON contract, then visual field on top.
6. Loop closure: outcome capture → vector promotion → index rebuild.

Each step is independently useful; none requires the later ones to justify itself. Step 1–2 alone upgrade the store from case library toward functional model.
