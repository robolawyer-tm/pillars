# CLAUDE.md — robolawyer-tm / Vivify

> Read this first. Everything else is detail.

---

## What this is

A local-first, privacy-preserving system for capturing and structuring LLM inferences into a semantic database. The goal is to develop semantics that work with conflict data — predicting beneficial outcomes from functional models, dynamically, privately, (preferably) on local hardware.

The human (semantic/analogical) conception drives everything. Code follows structure. Structure follows meaning.

---

## The core duality

- **Left (Semantic):** Analogical, logos-based — language, emotion, felt meaning. LLMs participate here through analogical synthesis. This is the human side.
- **Right (Digital):** Analytical — code, filesystem, pattern detection. Supports the left; never reduces it.

Output is always analogical. Synthesis happens from thesis without antithesis (not Hegelian). The right side serves the left.

---

## FABRIC — the components

The symbolic building blocks of the system:

- **vivify** — create vivified (Perl-equiv hash-of-hashes) objects in JSON. Much LLM intelligence involved here: keyword extraction, semantic categorization, emergent structure.
- **payload** — create payload object to send to server device
- **secrecy** — encrypt for payload and for stored secrets
- **freeze** — serialize payload object to send over IP
- **server** — strip first 2-3 layers to create directories, recreate JSON, remove blobs, give links

---

## FLOW — how FABRIC connects

**Secret-server storage flow:**
```
secret creation (vivify + secrecy)
  → payload (send, includes freeze)
  → IP
  → payload (receive)
  → server (formats and stores data)
```

**Inference vivification flow (primary build target):**
```
raw inference text
  → left-LLM semantic pass (8-12 keyword clumps, felt meaning)
  → keyword co-occurrence graph (local only)
  → emergent categories (3-4 layers, no external taxonomies)
  → autovivified filesystem + JSON structure
  → right-digital pass (structural keywords, analytics)
  → tension score (left/right divergence → beneficial outcome signal)
```

---

## Code style

- **Shell-first** at the high level — keep processes visible as shell commands
- **Python** for executables and libraries — scripts easily wrapped into shell commands
- **pipx** for wrapping Python code as shell-accessible commands
- No opaque formats. No external taxonomies. All structure emerges from data.
- **Naming convention**: hyphens for project/repo names (`vivify-inferences`, `star-bridge`), underscores for files, directories, and executables (`vivify_core.py`, `extract_keywords`, `inferences/`)
- **Python — app-level (public-facing, FABRIC components)**: Standard Python module structure — FABRIC component names as module names (`vivify.py`, `secrecy.py`, `freeze.py`, `server.py`), every module standalone via `if __name__ == '__main__':` with usage code. No pipx. Readable by anyone.
- **Python — housekeeping (local admin)**: pipx-wrapped via a shell script in `sys_adm/`. Use `shell_template_pipx`. Not for public repos.
- **STDIN**: All housekeeping executables accept data on standard input. Python uses `fileinput.input()` — reads file args OR STDIN transparently (Perl `<>` equivalent). Shell uses pipe-detect: `if [ -p /dev/stdin ]; then while IFS= read -r line; do ...; done; fi`
- Shell scripts use the appropriate template from `~/repos/sys_adm/`:
  - `shell_template` — general scripts (header, `usage()`, `realpath`, `items[]` loop)
  - `shell_template_exec` — library/executable hybrids (`parse_args()`, `process_item()`, `main()`, `BASH_SOURCE` guard, sourceable)
  - `shell_template_pipx` — thin wrappers delegating to a pipx-installed Python command

---

## What already exists

- `CLAUDE_CODE_BOOTSTRAP.md` — full pipeline spec, vivification rules, build order (Phases 1-4)
- `FABRIC_and_FLOW` — conceptual sketch of components and flows
- `FABRIC.md` / `FABRIC.json` — FABRIC structure in markdown and JSON form
- `secret-server` repo — working Flask app on Android/Termux, autovivification storage, SSH/SSHFS
- `star-bridge` repo — SSH admin connection manager

## What needs building

`vivify/` — the inference pipeline (does not exist yet). See `CLAUDE_CODE_BOOTSTRAP.md` §3 and §9 for full spec and build order.

---

## Documentation standard

All documentation follows a single defining sentence followed by up to 25 supporting bullets that expand without repetition. Full schema: `pillars/doc_standard_v1.json`

- Defining sentence: one direct claim, active voice, 25 words max, no vague qualifiers
- Bullets: each expands a distinct angle — evidence, example, or constraint — 15 words avg
- Forbidden: multiple claim sentences, bullets that restate the opener, nested bullets, concluding statements in exploratory sections

---

## LLM signing standard

Every LLM-edited file gets a footer line recording the model, date, path, and change.

- Format: `# llm: model-id | YYYY-MM-DD | full/path/from/repos | what changed`
- Use `<!-- llm: ... -->` for HTML/markdown files
- Full path from `~/repos/` — never filename alone
- One line per edit session at the bottom of the file
- A scan script can aggregate all footers across the codebase on demand

---

## Housekeeping rules

- **Before editing any existing file**, back it up first: `backit ~/repos/<project>/<file>`
- Backups mirror path structure under `~/backups/` — outside all repos, safe from git commands
- AI must not run destructive git commands (`reset`, `clean`, `checkout .`, `force-push`) without explicit user confirmation
- **Never delete or overwrite any script or file** without explicit user confirmation — run `backit` first, then ask
- New shell scripts start from `~/repos/sys_adm/shell_template`
- `sys_adm` repo is the source for scripts deployed to `~/bin`

---

## Non-negotiables

1. Local-first — zero cloud dependencies
2. Privacy-preserving — all data stays local, SSH tunnels for transport
3. No external taxonomies — all structure emerges from the data
4. Analogical orientation — output serves human emotion and empathy
5. Filesystem transparency — no opaque formats, human-readable JSON
6. Python 3 + shell-first — see code style above
7. Structure first — define target file layout before writing any process code

---

## Reference documents (all in `~/repos/pillars/`)

| File | Purpose |
|------|---------|
| `CLAUDE_CODE_BOOTSTRAP.md` | Full pipeline spec, rules, build order — read this second |
| `FABRIC_and_FLOW` | Living conceptual sketch — FABRIC components + FLOW pipelines |
| `DESIGN_PHILOSOPHY.md` | Hardware/Android edge layer (separate from LLM-semantic thesis) |
| `TECHNICAL_AUDIT_SUMMARY.md` | Current state of secret-server + vivify pillars |
| `Semantic_edge_manifesto.md` | Secret-server README / feature list |
| `PILLARS_SUMMARY.md` | Full architectural vision |
| `MULTI_MODEL_CONVERGENCE.md` | Multi-model round-robin convergence via accumulated embeddings |
| `WRITING_IN_REVERSE.md` | Writing in reverse methodology — constructivist inquiry model, connections to AI convergence |

<!-- llm: claude-sonnet-4-6 | 2026-04-13 | repos/pillars/CLAUDE.md | added documentation standard, LLM signing standard (in-file footer approach) -->
<!-- llm: claude-sonnet-4-6 | 2026-04-14 | repos/pillars/CLAUDE.md | updated code style with 3 shell templates, added non-removal directive -->
<!-- llm: claude-sonnet-4-6 | 2026-04-14 | repos/pillars/CLAUDE.md | added naming convention, two Python standards (app-level vs housekeeping/pipx) -->
<!-- llm: claude-sonnet-4-6 | 2026-04-27 | repos/pillars/CLAUDE.md | updated documentation standard bullet count from 3-6 to up to 25 -->
