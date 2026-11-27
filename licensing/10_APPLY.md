# Licensing — where each part lands

Every public repo gets a LICENSE file and a short COPYRIGHT.md naming which paths fall under AGPL, which under CC BY, and which are excluded.

- Status 2026-11-27: APPLIED and pushed to vivify-operators, robolawyer-tm.github.io, pillars, star-bridge, claude-shareable-config, payload-vivify; dist_files pushed after android_home.tgz was taken out of its unpushed history (file kept local, gitignored); holder robolawyer-tm (John's choice)
- Not licensed, made PRIVATE 2026-11-27 instead: perl-depth-system and payload-persist (both held private files)
- File pattern per repo: LICENSE (AGPL-3.0 full text), LICENSES/CC-BY-4.0.txt (full text), COPYRIGHT.md (path map + exclusions + "© robolawyer-tm, all rights reserved beyond these grants")
- vivify-operators: code AGPL; docs and inferences/ CC BY; raw_text fields of inferences/field/*.json and quoted case text in experiments/ excluded as third-party
- vivify-operators, open question for John: strip raw_text from future versions of the five field inferences (history keeps the old copies unless rewritten, which needs a force-push)
- pillars: mostly writing, so CC BY; scripts and code AGPL; capture/inbox.md is CC BY like the rest
- robolawyer-tm.github.io: site code AGPL, posts and pages CC BY; footer replaced by a plain notice of the split (wording John's)
- star-bridge, payload-vivify, claude-shareable-config: AGPL; their docs CC BY
- dist_files: CC BY for the text; android_home.tgz (star-bridge save) kept local and gitignored
- secret-server: unchanged, public domain
- lescc-hackathon: a fork of dssg-nyc's repo, which has no licence; not ours to license; left as is
- Private repos (sys_adm, organization, star-bridge-private, private-field-family): no licence; they stay private
- discovery.jsonld and llms.txt: add a license field (CC BY 4.0 URL) for the public inference domains, never for private
- CONTRIBUTING.md in vivify-operators (the one repo likely to draw pull requests): "contributions need a signed CLA first"
- Order: footer and LICENSE files first (cheap, removes the contradiction), then COPYRIGHT.md maps, then the jsonld field, then the raw_text decision
- Blocking for pairfam tables only: the GESIS contract documents; nothing else waits on them
- Found while checking, not licensing: dist_files holds android_home.tgz (a star-bridge save); taken out of the never-pushed history before dist_files was first pushed

<!-- llm: claude-opus-5-5 | 2026-11-27 | pillars/licensing/10_APPLY.md | created: per-repo application plan for the licensing split -->
<!-- llm: claude-opus-5-5 | 2026-11-27 | pillars/licensing/10_APPLY.md | status: applied to vivify-operators and the site -->
<!-- llm: claude-opus-5-5 | 2026-11-27 | pillars/licensing/10_APPLY.md | status: applied to remaining public repos; two repos made private -->
