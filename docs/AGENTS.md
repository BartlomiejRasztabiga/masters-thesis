# Repository Guidelines

## Project Structure & Module Organization
- `main.tex` is the entry point; it assembles chapter files from `tex/` and pulls bibliographic data from `bibliografia.bib`.
- `src/` contains the WUT thesis class (`wut-thesis.cls`) and language-specific assets under `pl/` and `en/`.
- `tex/` holds chapter content (prefixed with numeric ordering); keep new sections in this folder to retain compilation order.
- `build/` and `_minted/` are generated; PDFs land in `build/pdfs/` or as `main.pdf` in the repo root after quick builds.
- `test/` stores Jinja templates and expected outputs for rendering and PDF text comparisons.
- `THESIS_NOTES.md` tracks the current chapter plan and TODOs; update alongside content changes.

## Build, Test, and Development Commands
- Install tooling: `pip install -r requirements.txt` plus system LaTeX with `latexmk`, `pdflatex`, `lualatex`, and `pygmentize` (for `minted`).
- Fast PDF: `scons quick` (produces `main.pdf`).
- Full variants: `scons all` or `scons pdf`/`scons lua` (writes to `build/pdfs/`).
- Clean artifacts: `scons clean`.
- Generate/update test fixtures: `scons generate_tests` then `scons update_refs_local` (or `scons update_refs_docker` for a clean Docker toolchain).
- Single PDF check: `scons test_pdf pdf=build/pdfs/pdflatex.pdf ref=test/pol/eiti/EngineerThesis_pdflatex.txt`.

## Coding Style & Naming Conventions
- LaTeX sources use 4-space indentation and English macro names from `src/wut-thesis.cls`; avoid tabs and trailing whitespace.
- Name new chapter files `tex/<number>-<topic>.tex` (e.g., `tex/6-system-paas.tex`) and include via `\input{...}` in `main.tex`.
- Prefer descriptive command/macros names; keep user-facing content bilingual only when the thesis language requires it.
- Do not edit generated files in `build/` or `_minted/`; commit only source `.tex`, `.bib`, and class/template updates.

## Testing Guidelines
- Regenerate `.textest` fixtures when language/faculty options change via `scons generate_tests`.
- Compare PDFs against references with `scons test_pdf`; update refs only when intentional layout/text changes occur.
- Keep new examples compilable with both `pdflatex` and `lualatex` (watch for packages that differ between engines).

## Commit & Pull Request Guidelines
- Use concise, imperative commit titles in English (e.g., `Add MEiL English thesis example`); limit subject to ~72 characters.
- In PRs, describe scope, commands run, and whether reference texts were updated; attach or link resulting `main.pdf` when visuals change.
- Cross-reference related issues and note any engine-specific caveats (pdflatex vs. lualatex) or new runtime dependencies.
