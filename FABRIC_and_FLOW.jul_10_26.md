# FABRIC and FLOW — what the process is meant to do

The system turns raw human accounts into an emergent, navigable structure of meaning, measuring where machine description pulls away from human meaning so intervention lands where it helps.

- Input is a real human account — a case, a session, a conflict — not a data record
- No taxonomy exists before the data: every category is grown from the accounts themselves
- The output serves human emotion and empathy — coordinates for understanding, not conclusions
- Everything stays local, human-readable JSON on a filesystem a person can walk
- Tension — the gap between felt meaning and structural description — is the system's core signal

---

## FABRIC — the structure meaning grows into

The Fabric is an autovivified tree of JSON files: one account per file, filed two levels deep under categories the corpus itself produced.

```
                            THE FABRIC (generalized)

   <domain>/                        chosen by the human — the only imposed layer
   │
   ├── unclustered/                 the holding pen — exists, but unplaced
   │     inf_x.json                 an account the corpus hasn't yet made room for
   │
   ├── <seed>/                      grown: a high-degree keyword the corpus produced
   │     └── <sub>/                 grown: a strong neighbor of that seed
   │           inf_y.json           filed: the account lives at a meaningful address
   │
   └── index.json                   the tree as metadata — regenerable, never authoritative

   one inference file (always additive — base fields are never altered):
   ┌─────────────────────────────────────────────────────────────┐
   │ raw_text          the human account, verbatim               │
   │ left_keywords     what it MEANS   (analog, felt, per-account)│
   │ right_keywords    what the SYSTEM did (digital, identical)  │
   │ category_paths    where meaning says it belongs             │
   │ tension_score     how far the two readings pulled apart     │
   │ logos             its coordinates in communicative space    │
   │ conflict          second-order reading built on logos       │
   └─────────────────────────────────────────────────────────────┘
```

- The directory path is for humans; the index is for programs — same truth, two readers
- `unclustered/` is honest latency: nothing is force-filed before the corpus can place it
- A category address like `dna_exoneration/delayed_justice` is itself a reading of the account
- Autovivification (the original FABRIC idea): structure appears at the moment content needs it, never before

---

## FLOW — the process meaning moves through

An account enters as text and exits as a filed, scored, coordinate-tagged node; each pass exists to answer one human question.

```
                         THE FLOW (generalized)

   a human account (raw text)
        │
   ┌────▼─────────────┐   MEANT TO: hear what the account means
   │ 1  LEFT PASS     │   semantic keywords — felt meaning, not surface words
   │    (analog)      │   → account saved to unclustered/ (placed later, honestly)
   └────┬─────────────┘
   ┌────▼─────────────┐   MEANT TO: record what the machine did with it
   │ 2  RIGHT PASS    │   structural keywords — identical on every account,
   │    (digital)     │   they describe the pipeline, never the person
   └────┬─────────────┘
   ┌────▼─────────────┐   MEANT TO: let categories grow out of the corpus
   │ 3  CATEGORIZE    │   co-occurrence graph over LEFT keywords only →
   │    (emergence)   │   seed/sub tree → category_paths (metadata first)
   └────┬─────────────┘
   ┌────▼─────────────┐   MEANT TO: make the decided placement real
   │ 3b PROMOTE       │   categorized accounts move to <seed>/<sub>/ on disk;
   │    (actualization)│  unplaced accounts stay in the holding pen
   └────┬─────────────┘
   ┌────▼─────────────┐   MEANT TO: measure the analog/digital gap
   │ 4  TENSION       │   1.0 − shared/total across left vs right —
   │    (the signal)  │   high tension = machine description missed the meaning
   └────┬─────────────┘
        ▼
   filed, scored account — a node the Fabric can navigate to
```

- The two vocabularies never mix roles: meaning files things, machinery only measures against it
- Categorize decides, promote enacts — deciding and doing are separate acts, so each stays inspectable
- The corpus is the categorizer: every new account re-reads the whole corpus, so the tree can reshape as understanding grows
- High-tension accounts are surfaced as intervention candidates — the flow points at where help is needed, it does not conclude

---

## The operator overlay — coordinates for empathy

Filed accounts gain logos coordinates: eight answers to eight human questions, then a second-order conflict reading composed from those answers.

```
   filed account
        │
   ┌────▼──────────────────────────────────────────────────────┐
   │ LOGOS (one fused pass — 8 dimensions, each a human question)│
   │                                                             │
   │  act_type      what kind of move is this?                   │
   │  cooperative   is it playing fair?                          │
   │  transmission  how does it travel?                          │
   │  resonance     does the surface match what's underneath?    │
   │  authority     who authorized it?                           │
   │  utility       what is it for?                              │
   │  social_field  how tight is the social grid around it?      │
   │  structural    where in social life does it live?           │
   └────┬──────────────────────────────────────────────────────┘
   ┌────▼──────────────────────────────────────────────────────┐
   │ CONFLICT (second-order — reads the coordinates, not the text)│
   │  schema · behavior · terrain · window · escalation phase    │
   │  the operators compose: readings built on readings          │
   └─────────────────────────────────────────────────────────────┘
```

- Each dimension cites its theorist lineage — the coordinates are grounded, not invented
- Resonance is the empathy axis: surface story vs underlying truth held as one coordinate
- Composition is the point: once coordinates exist, higher-order readings need only the coordinates

---

## Worked example — one account through the whole flow

The Josiah Sutton case (wrongful conviction, DNA exoneration) entered as raw text and exited as a located, readable node.

- Left pass heard: `wrongful_conviction`, `dna_exoneration`, `forensic_fabrication`, `custodial_years_lost`
- Categorize grew seeds from the case's own vocabulary; promote files it under `dna_exoneration/`
- Logos placed it: authority `sovereign`, resonance `illusion` — lawful surface, manufactured certainty underneath
- Conflict composed the coordinates: `entangled` schema, `suppression` behavior — the reading a person needs to know where help was owed

<!-- llm: claude-opus-4-8 | 2026-07-10 | repos/pillars/FABRIC_and_FLOW.jul_10_26.md | created — repo structure + FABRIC pipeline flow diagram documenting the new promote.py stage -->
<!-- llm: claude-fable-5 | 2026-07-10 | repos/pillars/FABRIC_and_FLOW.jul_10_26.md | rewritten — generalized FABRIC (structure) and FLOW (process) explanation replacing session-specific changelog -->
<!-- llm: claude-fable-5 | 2026-07-10 | repos/pillars/FABRIC_and_FLOW.jul_10_26.md | rewritten purpose-first — what the process is MEANT to do; generalized structure/flow/operator diagrams, two-vocabulary principle from the contamination fix, Sutton worked example -->
