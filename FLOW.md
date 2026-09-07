# FLOW

Data moves through the Fabric only when actualized by a specific process; until then, paths are latent — possible but not real.

---

## Inference Vivification Flow (actualized)

Raw inference text enters; a scored, categorized semantic unit exits — the Fabric grows one node.

- Raw text arrives via STDIN or argument → `vivify.py`
- Left-semantic pass: Claude API extracts 8-12 keyword clumps capturing felt meaning, not surface words
- **Tension node — structural**: the inference is placed in `inferences/unclustered/` — the Fabric has not yet decided where it belongs
- `keyword_graph.py` accumulates co-occurrence edges across all inferences — graph grows with corpus
- `categorize.py` reads graph seeds (left keywords only) → builds emergent 2-3 layer category tree → assigns `category_paths`
- **Tension node — conflict**: `right_pass.py` runs a digital/structural pass; keywords describe the same inference analytically, not semantically
- `tension_score.py` measures left/right divergence — `1.0 - (shared / total unique)` — scores the gap between analog meaning and digital structure
- **Tension node — resolution**: `beneficial_signals()` surfaces inferences where divergence exceeds threshold — these are intervention candidates
- Phase 5 `prediction_output()` shapes the result as a navigational signal, not a conclusion

---

## Secret Storage Flow (actualized)

A secret enters encrypted by the client; the server strips routing layers and stores a human-readable JSON file.

- Secret created on client → `vivify.py` + `secrecy.py` (PBKDF2/Fernet, client-side)
- `freeze.py` serializes payload to base64 JSON for IP transit
- SSH tunnel carries payload to phone (star topology hub)
- `server.py` (Flask, Android/Termux) receives → strips name + app-name layers → recreates directory path
- JSON stored at `db/{username}/{app_name}/secret.json` — filesystem is the database
- Blobs separated; raw sensitive material never stored unencrypted

---

## Tension Nodes (cross-flow)

Tension is structural pressure pointing toward the next evolution — four types, each visible in the flow.

- **Structural** — the unclustered drop point in vivify: inference exists but Fabric hasn't autovivified to place it; graph must accumulate before categorization is possible
- **Conflict** — left/right divergence measured by `tension_score.py`: analog human meaning pulling against digital structural description; score near 1.0 means the system is under maximum interpretive pressure
- **Functional** — rules in `pillars/CLAUDE.md` and `pillars/doc_standard_v1.json`: constraints that resist certain flows (no external taxonomies, no schema-first design, no concluding statements in exploratory sections)
- **Resolution** — `beneficial_signals()` and Phase 5 output: the pull toward beneficial outcome; what the system is oriented toward, not what it has achieved

---

## What Isn't (unactualized)

These paths exist as structural pressure — latent in the Fabric, not yet actualized.

- **Typed tension JSON**: `tension_score.py` outputs a float; the typed shape `{type, magnitude, between, resolution_vector}` is specified but not yet in the code
- **Normalization standard**: conflict inputs enter raw — no standard yet for stripping proper nouns, collapsing entities to typed roles, offsetting dates; data contaminates before it vivifies
- **Cloudflare Workers runtime**: the Fabric is described in terms of Worker isolates and Durable Objects but runs locally in Python; the translation is unactualized
- **Animal Crossing instantiation**: same underlying model, different population (elders, children) — the instantiation doesn't exist; only the shared model does
- **Reify feedback loop**: `reify.py` holds two inferences in synthesis simultaneously but doesn't write back to the graph or update `category_paths`; synthesis is terminal, not recursive
- **Cross-inference autovivification**: the moment a Flow decides the Fabric needs a new branch is not yet explicit — it happens by corpus accumulation, not by a triggered decision
- **`right_pass.py --all` duplication**: inferences appear across multiple category paths when run in bulk — bug, not feature
- **Secret Server ↔ vivify-inferences connection**: the two flows are independent; no path yet from a vivified inference into the secret storage layer

---

<!-- llm: claude-sonnet-4-6 | 2026-05-07 | repos/pillars/FLOW.md | created — flow view of actualized and unactualized paths, tension nodes by type -->
