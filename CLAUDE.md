# CLAUDE.MD -- Academic Project Development with Claude Code

**Project:** The Dictator's Gambit: Causes and Consequences of Territorial Autonomy Arrangements in Authoritarian Regimes
**Institution:** Princeton University, Department of Politics
**Committee:** Mark Beissinger, Rory Truex, Atul Kohli
**Branch:** main

---

## Core Principles

- **Plan first** -- enter plan mode before non-trivial tasks; save plans to `quality_reports/plans/`
- **Verify after** -- compile/render and confirm output at the end of every task
- **Single source of truth** -- `chapters/` `.tex` files are authoritative; Overleaf is a drafting tool only
- **Quality gates** -- nothing ships below 80/100
- **[LEARN] tags** -- when corrected, save `[LEARN:category] wrong → right` to MEMORY.md

---

## Folder Structure

```
dissertation/
├── CLAUDE.md                        # This file
├── Bibliography_base.bib            # Centralized bibliography
├── Preambles/header.tex             # Dissertation LaTeX preamble
├── chapters/                        # Dissertation .tex files (authoritative)
│   ├── main.tex                     # Master file (\input all chapters)
│   ├── introduction.tex
│   ├── chapter1.tex
│   ├── chapter2.tex
│   ├── chapter3.tex
│   └── conclusion.tex
├── paper/                           # Standalone JMP / journal submission
│   └── jmp.tex
├── Slides/                          # Beamer presentation slides (talks, JM)
├── Quarto/                          # RevealJS slides (derived from Beamer)
├── Figures/                         # All figures, maps, tables
├── data/
│   ├── raw/                         # Original data (never edited)
│   └── processed/                   # Cleaned/transformed outputs
├── scripts/R/                       # R analysis scripts
├── master_supporting_docs/
│   ├── supporting_papers/           # Key papers informing the dissertation
│   ├── supporting_slides/           # Reference slides
│   └── example_dissertation/        # Example dissertation to emulate
├── explorations/                    # Research sandbox (see rules)
├── quality_reports/                 # Plans, session logs, merge reports
├── templates/                       # Session log, quality report templates
└── docs/                            # GitHub Pages (auto-generated)
```

---

## Overleaf ↔ Repo Workflow

- **This repo is authoritative** — committed `.tex` files are the final record
- **Overleaf is for drafting** — export `.tex` + `.bib` periodically and commit here
- **Never edit the same file in both places simultaneously**
- To import from Overleaf: download project zip → copy relevant `.tex` files → paste into `chapters/` → commit

---

## Commands

```bash
# Compile full dissertation (3-pass XeLaTeX)
cd chapters && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode main.tex
BIBINPUTS=..:$BIBINPUTS bibtex main
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode main.tex
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode main.tex

# Compile a single chapter (faster iteration)
cd chapters && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode chapter1.tex

# Compile standalone JMP
cd paper && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode jmp.tex

# Deploy Quarto slides to GitHub Pages
./scripts/sync_to_docs.sh SlideDeck

# Quality score
python scripts/quality_score.py chapters/chapter1.tex
```

---

## Quality Thresholds

| Score | Gate | Meaning |
|-------|------|---------|
| 80 | Commit | Good enough to save |
| 90 | Send to advisor | Ready for feedback |
| 95 | Excellence | Aspiration for final submission |

---

## Skills Quick Reference

| Command | What It Does |
|---------|-------------|
| `/compile-latex [file]` | 3-pass XeLaTeX + bibtex |
| `/deploy [SlideDeck]` | Render Quarto + sync to docs/ |
| `/extract-tikz [deck]` | TikZ → PDF → SVG |
| `/proofread [file]` | Grammar/typo/overflow review |
| `/visual-audit [file]` | Slide layout audit |
| `/pedagogy-review [file]` | Narrative, notation, pacing review |
| `/review-r [file]` | R code quality review |
| `/qa-quarto [deck]` | Adversarial Quarto vs Beamer QA |
| `/slide-excellence [file]` | Combined multi-agent review |
| `/translate-to-quarto [file]` | Beamer → Quarto translation |
| `/validate-bib` | Cross-reference citations |
| `/review-paper [file]` | Full manuscript review |
| `/devils-advocate` | Challenge argument/slide design |
| `/commit [msg]` | Stage, commit, PR, merge |
| `/lit-review [topic]` | Literature search + synthesis |
| `/research-ideation [topic]` | Research questions + strategies |
| `/interview-me [topic]` | Interactive research interview |
| `/data-analysis [dataset]` | End-to-end R analysis |
| `/learn [skill-name]` | Extract discovery into persistent skill |
| `/context-status` | Show session health + context usage |
| `/deep-audit` | Repository-wide consistency audit |

---

## Beamer Custom Environments

| Environment | Effect | Use Case |
|-------------|--------|----------|
| *(to be defined once preamble is imported from Overleaf)* | | |

## Quarto CSS Classes

| Class | Effect | Use Case |
|-------|--------|----------|
| *(to be defined once first slide deck is built)* | | |

---

## Current Project State

| Part | File | Status | Notes |
|------|------|--------|-------|
| Introduction | `chapters/introduction.tex` | Skeleton | Import from Overleaf |
| Chapter 1 | `chapters/chapter1.tex` | Skeleton | Import from Overleaf |
| Chapter 2 | `chapters/chapter2.tex` | Skeleton | Import from Overleaf |
| Chapter 3 | `chapters/chapter3.tex` | Skeleton | Import from Overleaf |
| Conclusion | `chapters/conclusion.tex` | Skeleton | Import from Overleaf |
| JMP | `paper/jmp.tex` | Skeleton | Derived from best chapter |
| Slides | `Slides/` | Empty | Job market talk (future) |
