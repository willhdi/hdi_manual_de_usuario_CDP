# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

This is a **documentation repository**, not a software project — there is no build, lint, or test tooling. It holds the user manual and training materials for the **Colombia Data Program (CDP)**, HDI Seguros' Amazon Redshift analytics data warehouse. Content is in Spanish.

## Document map and editing workflow

- **`CDP-MANUAL-DE-USUARIO.md`** — the canonical, editable source of the manual. It is organized in 9 numbered sections (see its table of contents) covering: what the CDP is, its medallion-architecture layers, the star-schema data model (`dim_`/`fact_` tables, surrogate keys, `current_record_flag`), how to request Redshift access (DATAHUB ticket), DBeaver connection setup per environment, sandbox rules, and best practices.
- **`CDP_Manual_de_Usuario.docx`** — the distributable Word version of the same manual. **These two files are updated together in the same commit** (see git history: every content change touches both `.md` and `.docx`). When asked to update the manual, edit the Markdown first for the authoritative text, then regenerate/update the `.docx` to match — do not let them drift.
- **`CDP-MANUAL-DE-USUARIO.md` has a "Control de versiones" table near the top** (version, description, author, date) — bump it when making substantive content changes, matching the style of existing rows.
- **`ADP-Manual de Usuario_v2.1 5.pdf`** — the legacy Liberty-era "Andes Data Program" manual (28/11/2023) that the CDP manual was originally based on/adapted from. Treat as a historical reference, not something to edit.
- **`Capacitacioncdp.md`** — raw, largely unedited meeting transcript of the CDP training session (09/07/2026). Treat as a primary-source transcript (speaker-labeled, informal), not prose to clean up casually.
- **`RESUMEN-CAPACITACION-CDP.md`** — a plain-language explainer distilled from the transcript above, written for someone who has never worked with the CDP (inline 🟡 callouts define jargon). This same content is embedded verbatim as the Anexo (section 9) of `CDP-MANUAL-DE-USUARIO.md` — if one is updated, check whether the other needs the same update.
- **`Template final Diccionario de datos.xlsx`** — data dictionary template referenced by the manual's "Soporte y documentación" section (the live dictionary itself lives in Confluence).

## Domain context worth knowing when editing content

- CDP = successor to ADP after a Liberty-era multi-country split; now Colombia-only. Backing store is Amazon Redshift on AWS, refreshed nightly (service cuts during the load window), analytical only — not real-time/transactional, and not to be conflated with the legacy SQL Data Warehouse.
- Data model is a star schema: `dim_*` (dimensions) and `fact_`/`fac_` (facts) tables joined via surrogate keys (SK). A recurring, load-bearing rule repeated throughout the docs: **never hardcode SK values** in queries/code — join on them only, since they shift over time.
- `current_record_flag = 1` is the convention for "latest valid record" across both fact and dimension tables.
- Access is requested via a DATAHUB Jira Service Management ticket; the manual documents each form field and includes a filled-out example — keep that example internally consistent if the form or roles change (current CDP role options: `cdp_bus_users_basic`, `cdp_bi_users`, and their `_dev` equivalents).
- Connection tool is DBeaver (Redshift JDBC driver), with separate host endpoints per environment (Prod/Non Prod/Dev) but shared port (`9519`) and database (`adp_dwh`) — documented in section 5 of the manual.

## Conventions

- Keep new/edited Markdown content in Spanish, consistent with the existing tone (direct, instructional, HDI-internal terminology).
- Don't commit files containing plaintext credentials (the manual itself explicitly warns against hardcoding credentials/keys in developed code — apply the same standard to this repo).
