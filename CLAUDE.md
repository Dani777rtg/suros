# SUROS — AI-assisted reverse engineering

Goal: document every function of SURÓS / PRORED (http://prored.suros.co/SUROS/Inicio.aspx), a web system for clinics and hospitals by SoftProject, so it can be rebuilt with the Shipwright plugin. This repo only documents; it does not build.

## Rules
- Observe only: never create, save, edit or delete anything in SUROS. It is production with real patient data.
- Never copy personal data (patients, staff, documents, phones) into these docs. Record field names, never values.
- Docs in Spanish (the client's language).

## Skills to use every session
- `graphify` — knowledge graph of `docs/` (`graphify-out/`); query it before reading many files.
- `caveman` — terse replies.
- `ponytail` — minimal code and docs, no speculative structure.
- `karpathy-guidelines` — state assumptions, ask when unclear, verifiable criteria.
- Models: Haiku/Sonnet subagents for screen exploration, Opus for synthesis. `/compact` between modules, `/clear` between unrelated tasks.

## Layout
- `docs/ingenieria-inversa.md` — the document: modules, functions, flows, rules, open questions.
- `docs/pantallas/` — raw per-screen extraction (fields, buttons, grids, dialogs).
