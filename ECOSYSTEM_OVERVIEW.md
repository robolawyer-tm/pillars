# Ecosystem Overview

This system predicts beneficial resolution paths from conflict data through functional models that self-evolve via inference accumulation and researcher-grounded operator refinement — explicitly excluding adversarial determination.

**The non-schema is the philosophy expressed in infrastructure.** Autovivification (structure emerges from co-occurrence, never imposed) is the same move as the left pass (meaning emerges from felt sense, never from predefined taxonomy) is the same move as the anti-status-quo position (outcomes emerge from the conflict itself, not from institutional determination). These are not three things that rhyme — they are the same refusal operating at three layers of the stack simultaneously: data architecture, LLM prompt design, and social/political framing. A schema-first approach would be the status quo baked into the code.

**Beneficial means constructive, not adversarial.** Courts, legal outcomes, and institutional adjudication are excluded as targets even when that material enters as conflict data. The project positions against status quo adversarial structures; the research filter selects only frameworks oriented toward constructive resolution (collaborating, compromising, accommodating) and excludes frameworks that normalize win/lose determination or institutional authority over individuals. "Agreeable researchers" means researchers who model constructive dynamics: Austin, Searle, Grice, Douglas, Granovetter, Glasl, Durkheim, Bandura — not legal theorists or court process models.

---

## Conceptual layer — `pillars/`

The theory, schemas, and standards that all other repos implement.

- `logos/` — operator schemas only, no code: `logos_schema_v01.json` (functional, 7 dimensions), `logos_social_v01.json` (structural, Dunbar layers), `logos_combined_v01.json`

  **Logos as the bridge between left and right.** The logos schema is not an invented taxonomy — it describes evolved human organizational logic: how people speak to produce effects (Austin, Searle), how conversation maintains coherence (Grice), how groups structure authority and social distance (Douglas grid/group, Dunbar layers). Because logos captures what human society already does, both the left pass (felt meaning, organic social logic) and the right pass (structural, digital) are reaching toward the same substrate from different angles. The left pass arrives as semantic weight in natural language — "evolved logic as logos." The right pass arrives as structural coordinates. Logos is what makes them commensurate. LLMs trained on human text already carry implicit logos knowledge; the schema makes that knowledge explicit and navigable, which is why this framework improves LLM comprehension of human organization rather than just indexing it.
- `FABRIC.md` / `FABRIC.json` — the five FABRIC components: vivify, payload, secrecy, freeze, server
- `FLOW.md` — pipeline connections: how FABRIC components chain; actualized vs. latent flows
- `WRITING_IN_REVERSE.md` — constructivist inquiry model: final learning first; the halting criterion shared with the co-occurrence graph and AI round-robin
- `doc_standard_v1.json` — one defining sentence + bullets; governs all documentation
- `capture/inbox.md` — intake for new ideas; written during /wrapup
- `MULTI_MODEL_CONVERGENCE.md` — multi-model round-robin; intermediate embedding accumulation

---

## Inference pipeline — `vivify-inferences/` (canonical)

The active development repo. Processes raw text into operator-tagged JSON and regenerates prose from coordinates.

### Core pipeline (four passes)

| Script | Pass | What it does |
|---|---|---|
| `vivify.py` | 1 — left semantic | LLM extracts 8–12 concept-level keywords + clumps from felt meaning |
| `right_pass.py` | 2 — right structural | Attaches fixed structural keywords describing the pipeline; normalizes synonyms |
| `categorize.py` | 3 — emergent filing | Co-occurrence graph → seed keywords → category paths; moves inference files into directories |
| `tension_score.py` | 4 — divergence | `1 - (shared / total)`; high tension = felt meaning resists structural capture |
| `fabric.py` | runner | Chains all four passes in sequence |

### Inverse pass

| Script | What it does |
|---|---|
| `reify.py` | Reconstructs prose from coordinates (left_keywords, clumps, category_paths, tension_score). Three modes: single / synthesize / voice. Voice mode speaks for an entire category — this is the public output text. All LLM calls use `claude -p --no-session-persistence` subprocess. |

### Session capture tools

| Script | What it does |
|---|---|
| `session_to_chat.py` | col-b terminal → styled HTML chat + clean markdown |
| `session_extract.py` | Clean markdown → 3–8 prose inferences → vivify (plain extraction) |
| `session_extract_op.py` | Same, but operator-aware: logos schema vocabulary in prompt → operator-calibrated keywords |
| `jsonl_to_md.py` | Claude Code `.jsonl` session → LLM-friendly markdown (783KB → 57KB) |
| `inf_to_md.py` | Inference dir → single markdown doc for LLM search or comparison |

### Inference store domains

```
inferences/
├── autovivification/       ← public: meta-synthesis, multi-model convergence
│   ├── analogical_religion/
│   ├── agentic_self_evolution/
│   └── ...
├── private/                ← real conflict material; not distributed
├── claude_code_sessions/   ← session domain; operator-calibrated; isolated from logos graph
│   └── unclustered/        ← 9 inferences (2026-06-11); needs right_pass/categorize/tension_score
└── unclustered/
```

### All LLM calls

All scripts use `claude -p --no-session-persistence` subprocess. No API key, no `anthropic` package required.

---

## Operators layer — `vivify-operators/`

Contains the logos operator suite not yet integrated into `vivify-inferences/`.

- `logos_operator.py` — runs all 8 logos dimensions in sequence on one inference; writes `inference["logos"]`
- `conflict_operator.py` — reads completed logos coordinates; outputs `inference["conflict"]`: schema, behavior, terrain, window, escalation_phase
- Individual dimension operators: `act_type_operator.py`, `authority_operator.py`, `cooperative_operator.py`, `resonance_operator.py`, `social_field_operator.py`, `structural_operator.py`, `transmission_operator.py`, `utility_operator.py`
- `logos_narrative.py` — reads tagged inference → one plain-English sentence (rename pending: → `logos_plain_read.py`)

**Conflict styles as plain_read vocabulary (candidate):** Five response modes from conflict resolution research — competing, avoiding, accommodating, compromising, collaborating — are candidate labels for the constructive output layer. When `reify --voice` or `plain_read` points toward a restoration path, these modes give it a vocabulary: "this terrain calls for accommodating" is more actionable than a coordinate set. Not yet implemented; planned as a labeling target for the plain_read output pass.

### ⚠ Split issue (unresolved, 2026-06-12)

`vivify-operators/` duplicates all FABRIC pipeline scripts (`vivify.py`, `reify.py`, `right_pass.py`, `categorize.py`, `fabric.py`, `tension_score.py`, `lib/`, `config/`) and has its own inference store (identical to `vivify-inferences/` minus `claude_code_sessions/`). The duplicate scripts are behind: `vivify-operators/reify.py` still uses `anthropic.Anthropic()`; `vivify-inferences/reify.py` has the subprocess fix.

**Canonical repo is `vivify-inferences/`.** The operators from `vivify-operators/` need to be integrated into `vivify-inferences/` as part of the major pivot cleanup.

---

## Storage — `secret-server/`

Phone-based encrypted JSON vault running on Android/Termux via Flask.

- `web_server.py` — Flask app serving the vivify interface; stores encrypted payloads
- `main.py` — entry point
- `db/` — encrypted JSON payloads on device filesystem
- Two-layer auth: login password (UI access) + secret password (browser-side encryption key, never sent to server)
- FABRIC components implemented: vivify (interface), secrecy (browser encryption), payload (packaging), server (storage)

---

## Network — `star-bridge/`

Turns an Android device into a persistent SSH/SSHFS hub (star topology).

- `ssh_admin_connection.py` — laptop client; auto-detects USB/Bluetooth path; establishes SSH tunnels + SSHFS mount; self-heals
- `hub_manager.py` — Android orchestrator; manages `sshd`, `auth-server`, `web-server` lifecycle; handles wake-locks
- `auth-server/auth_server.py` — authentication server running on the hub alongside secret-server
- Status: parked pending second Android phone (star topology needs two nodes)

---

## Housekeeping — `sys_adm/`

Local admin scripts. Source of truth for all scripts deployed to `~/bin/`.

| Script | Purpose |
|---|---|
| `backit` | Mirrors file to `~/backups/` before any edit |
| `publish_repos` | rsync to Namecheap (wholesystemsmodel.org) + generates llms.txt |
| `desktop_backup` | USB drive backup (ext4, inference_1/inference_2) |
| `shell_template` | Base template for new shell scripts |
| `shell_template_exec` | Template for library/executable hybrids |
| `shell_template_pipx` | Template for pipx-wrapped Python scripts |

**Gap (parked):** No automated deploy step from `sys_adm/` to `~/bin/`. Scripts updated in `sys_adm/` diverge silently from what runs. Planned: git-diff-based deploy in `/wrapup`.

---

## Distribution — `robolawyer-tm.github.io/`

GitHub Pages blog. Public output layer for the project.

- `_posts/` — blog posts in markdown; JSON-LD auto-generated per post via `_layouts/post.html`
- `llms.txt` / `llms-full.txt` — LLM agent entry points (runtime), mirrored to wholesystemsmodel.org
- `index.html` — project entry page; needs intent-first restructure (pending)
- Distributed via `publish_repos` (rsync) + `git push` in `/wrapup`

---

## Data flow

```
raw conflict/session text
    │
    ▼
vivify.py (left semantic pass) ──────────────────────────────┐
    │                                                         │
    ▼                                                         │
right_pass.py (structural pass)                               │
    │                                                         │
    ▼                                                         │
categorize.py (co-occurrence → category dirs)                 │
    │                                                         │
    ▼                                                         │
tension_score.py (left/right divergence)                      │
    │                                                         │
    ▼                                                         │
inf_*.json in inferences/<domain>/                            │
    │                                                         │
    ├──▶ logos_operator.py → inference["logos"] coordinates   │
    │        │                                                 │
    │        ▼                                                 │
    │    conflict_operator.py → inference["conflict"]          │
    │                                                          │
    └──▶ reify.py --voice <category>  ◀────────────────────────┘
              │
              ▼
         public output text
              │
              ▼
    robolawyer-tm.github.io (blog)
    wholesystemsmodel.org (via publish_repos)
```

---

## What is not yet connected

- Logos operators (`vivify-operators/`) not yet called from `vivify-inferences/` pipeline
- `claude_code_sessions` domain: `right_pass`, `tension_score`, `categorize` not yet run
- `secret-server` not yet receiving vivify output (FABRIC payload/freeze/server chain not wired)
- `star-bridge` parked pending second Android phone

<!-- llm: claude-sonnet-4-6 | 2026-06-12 | repos/pillars/ECOSYSTEM_OVERVIEW.md | created — full ecosystem map: pillars, vivify-inferences, vivify-operators, secret-server, star-bridge, sys_adm, distribution layer; two-repo split issue documented -->
<!-- llm: claude-sonnet-4-6 | 2026-06-12 | repos/pillars/ECOSYSTEM_OVERVIEW.md | added conflict phenomenology model framing to intro; added conflict styles (competing/avoiding/accommodating/compromising/collaborating) as candidate plain_read vocabulary -->
<!-- llm: claude-sonnet-4-6 | 2026-06-12 | repos/pillars/ECOSYSTEM_OVERVIEW.md | updated defining sentence: self-evolving functional models, researcher-grounded; added adversarial exclusion — courts/legal outcomes explicitly excluded as targets; beneficial criterion defined -->
<!-- llm: claude-sonnet-4-6 | 2026-06-12 | repos/pillars/ECOSYSTEM_OVERVIEW.md | added non-schema/left-pass/anti-status-quo isomorphism — same refusal at three stack layers -->
<!-- llm: claude-sonnet-4-6 | 2026-06-12 | repos/pillars/ECOSYSTEM_OVERVIEW.md | added logos-as-bridge note — evolved human organizational logic as commensurate substrate for left and right passes; LLM comprehension claim -->
