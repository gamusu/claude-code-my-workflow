# Plan: Dissertation Workflow Configuration

**Status:** COMPLETED
**Date:** 2026-04-16
**Session log:** quality_reports/session_logs/2026-04-16_dissertation-setup.md

---

## Context

The repo was forked from `pedrohcgs/claude-code-my-workflow` and contains only template infrastructure — all CLAUDE.md placeholders are unfilled, no dissertation content exists yet. The user has scattered materials (Overleaf LaTeX + Word/notes) for a monograph dissertation at Princeton, and needs the repo configured as a structured completion environment before any chapter work begins.

This plan covers **configuration only** — it does not touch dissertation content.

---

## Dissertation Facts (for filling placeholders)

| Field | Value |
|-------|-------|
| Title | "The Dictator's Gambit: Causes and Consequences of Territorial Autonomy Arrangements in Authoritarian Regimes" |
| Field | Comparative Politics |
| Institution | Princeton University, Department of Politics |
| Committee | Mark Beissinger, Rory Truex, Atul Kohli |
| Format | Monograph (book-style): Intro + 3 chapters + Conclusion |
| Stats | R (primary) |
| LaTeX editor | Overleaf (primary) + this repo |
| Deliverables | Dissertation paper (LaTeX), JMP, Beamer slides, R analysis |

---

## Folder Structure (new)

The template uses `Slides/` for Beamer lectures. This repo is repurposed for a dissertation:

```
dissertation/
├── CLAUDE.md                    ← updated (this plan)
├── Bibliography_base.bib        ← centralized .bib (import from Overleaf)
├── Preambles/
│   └── header.tex               ← dissertation preamble (Princeton style)
├── chapters/                    ← NEW: dissertation .tex files (authoritative)
│   ├── main.tex                 ← master file (\input all chapters)
│   ├── introduction.tex
│   ├── chapter1.tex
│   ├── chapter2.tex
│   ├── chapter3.tex
│   └── conclusion.tex
├── paper/                       ← NEW: standalone JMP / journal submission
│   └── jmp.tex
├── Slides/                      ← Beamer presentation (seminar, job market)
├── Quarto/                      ← RevealJS slides (derived from Beamer)
├── Figures/                     ← all figures, maps, tables
├── data/                        ← NEW: raw/ and processed/ data
│   ├── raw/
│   └── processed/
├── scripts/
│   └── R/                       ← R analysis scripts
├── master_supporting_docs/
│   ├── supporting_papers/       ← key papers (already exists)
│   ├── supporting_slides/       ← (already exists)
│   └── example_dissertation/    ← NEW: example dissertation to emulate
├── explorations/                ← research sandbox
├── quality_reports/             ← plans, session logs, specs
└── docs/                        ← GitHub Pages (auto-generated)
```

---

## Changes to Make

### 1. Update CLAUDE.md

Fill in all `[BRACKETED PLACEHOLDER]` fields:

- **Project name:** The Dictator's Gambit
- **Institution:** Princeton University, Department of Politics
- **Branch:** main
- **Folder structure:** Replace lecture-centric table with dissertation structure above
- **Commands:** Replace `LectureN.tex` pattern with dissertation compilation commands
- **Current Project State table:** Replace lecture rows with chapter rows (Intro, Ch1, Ch2, Ch3, Conclusion)
- **Beamer/Quarto tables:** Leave as placeholder — fill in once preamble is established

### 2. Create dissertation directory scaffold

Create empty placeholder `.tex` files in `chapters/`:
- `main.tex` — master file with standard `\input{}` structure + Princeton formatting notes
- `introduction.tex`, `chapter1.tex`, `chapter2.tex`, `chapter3.tex`, `conclusion.tex` — each with a minimal skeleton (title comment only; user will populate from Overleaf)

Create `paper/jmp.tex` — skeleton for standalone JMP.

Create `data/raw/.gitkeep` and `data/processed/.gitkeep`.

Create `master_supporting_docs/example_dissertation/` directory.

### 3. Update CLAUDE.md commands section

Replace lecture-specific commands with dissertation-specific ones:

```bash
# Compile dissertation (3-pass XeLaTeX)
cd chapters && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode main.tex
BIBINPUTS=..:$BIBINPUTS bibtex main
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode main.tex
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode main.tex

# Compile single chapter (faster iteration)
cd chapters && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode chapter1.tex

# Compile JMP
cd paper && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode jmp.tex
```

### 4. Save user + project memories

Write memory files:
- `memory/user_profile.md` — Princeton comparative politics PhD, committee, field
- `memory/project_dissertation.md` — title, structure, deliverables, Overleaf workflow

Update `MEMORY.md` index.

### 5. Document Overleaf bridging strategy (in CLAUDE.md)

Add a short section explaining:
- This repo is the **authoritative source** for committed/final work
- Overleaf is for drafting; periodically export `.tex` + `.bib` from Overleaf and commit here
- Never edit the same file in both places simultaneously

---

## What This Plan Does NOT Do

- Does not write any dissertation content
- Does not import or transcribe Overleaf files (user does that manually or in next session)
- Does not set up R scripts or data pipelines (separate session)
- Does not create the Princeton LaTeX preamble (needs user's Overleaf preamble)

---

## Verification Steps

1. `CLAUDE.md` — no `[BRACKETED]` placeholders remain
2. `chapters/` directory exists with 6 skeleton `.tex` files
3. `paper/jmp.tex` exists
4. `data/raw/` and `data/processed/` directories exist
5. `master_supporting_docs/example_dissertation/` exists
6. Memory files written and MEMORY.md index updated
7. All changes committed via `/commit`

---

## Next Session Roadmap (after this plan)

1. **Content import:** User uploads example dissertation + key papers to `master_supporting_docs/`; exports Overleaf `.tex` files to `chapters/`
2. **Chapter-by-chapter review:** Go through intro, Ch1, Ch2, Ch3, Conclusion in sequence
3. **Formal theory session:** Use `/interview-me` to formalize identification strategy and model
4. **R analysis session:** Use `/data-analysis` to build empirical pipeline
5. **Slides session:** Use `/create-lecture` for job market talk
