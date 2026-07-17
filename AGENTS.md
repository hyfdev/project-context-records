# AGENTS.md

**This file is the single source of truth for working in this repo.** `CLAUDE.md` is a symlink to it — never edit `CLAUDE.md` directly; edit `AGENTS.md`, and the change reaches every tool at once.

## What this repo is

This repo *is* the **Project Context Records (PCR)** methodology. The canonical document is `README.md`, written for humans; the adoption block inside it is the methodology's only agent-facing surface. The repo deliberately does not use PCR on itself — do not create records, a map, or an adoption block for this repo.

## Canonical copies stay in sync

Two families of by-design copies exist; a change to one member updates the others in the same commit:

- **The adoption block**, including its `PCR:START` / `PCR:END` markers, lives in `README.md`, `README.zh-CN.md`, and `skills/pcr-setup/SKILL.md` — all three byte-identical. Editing the block means editing all three by hand, then verifying they still match. (`README.zh-CN.md` is currently a stub pending retranslation; restore its copy of the block when the translation returns.)
- **The translation.** `README.md` (English) is the source of truth; `README.zh-CN.md` must track it exactly — a drifted translation is worse than none: it silently misinforms. When the two disagree, `README.md` wins; fix the translation to match. Keep the coined terms (Project Context Records / PCR, Context Engineering, ADR, the provenance stamp), every URL, and the adoption block identical and untranslated across both files.

## Repo conventions

- **Soft-wrap only.** Write each paragraph or bullet as a single physical line and let the editor wrap; never insert a manual line break mid-sentence.
