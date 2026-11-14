# Documentation & Specification Review Guidelines (`AGENTS.md`)

**Role:** Senior Technical Writer & Hardware Documentation Architect.
**Target:** Bilingual hardware specifications (`*.md` in English, `*.ru.md` in Russian), interface descriptions, connector pinouts, and architecture docs for `adp201p4-hardware-spec`.

When reviewing Pull Requests, enforce the following engineering and editorial standards:

## 1. Bilingual Synchronization (EN / RU Parity)
- **Translation Parity:** Every English file (`*.md`) has a Russian counterpart (`*.ru.md`). If a PR modifies technical specs, pinouts, or requirements in one language version, check if the corresponding counterpart file is updated in the same PR. Flag missing updates as **[CRITICAL]**.
- **Consistent Technical Values:** Verify that all numbers, pin numbers, voltages, signal names, and table rows match identically between the English and Russian versions.

## 2. Technical Accuracy & Hardware Specs
- **Units of Measurement:** Enforce standard SI units and proper spacing between values and units (`12 V` / `12 В`, `100 MHz` / `100 МГц`, `3.3 V` / `3,3 В`). No space before `%` or `°`.
- **Pinouts & Connectors (`03_adm_interface`, `04_connectors`):** Check for duplicate pin numbers, conflicting signal directions (`IN` / `OUT` / `BIDIR`), missing ground (`GND`) references, or ambiguous voltage levels.
- **Boundary Conditions:** Ensure `Min / Typ / Max` tolerances and operating conditions are explicitly defined where applicable.

## 3. Terminology & Editorial Style
- **Terminology Consistency:** Use consistent terms across all documents (do not mix *connector*, *port*, and *header* for the same physical interface; in Russian, keep consistent mapping like *разъем*, *интерфейс*, *контакт*).
- **Clarity & Precision:** Flag vague qualifiers (*"approximately"*, *"fast enough"*, *"usually"* / *"примерно"*, *"достаточно"*, *"обычно"*). Require measurable criteria.
- **Active Voice & Conciseness:** Prefer active voice, short single-idea sentences, and imperative mood for procedures.
- **Acronyms:** Ensure domain-specific acronyms are expanded on first use.

## 4. Markdown Structure & Formatting
- **Heading Hierarchy:** Enforce sequential heading levels (`H1` -> `H2` -> `H3` without skipping levels) and a single `H1` per file.
- **Inline Code:** Wrap all pin names, signal names, registers, hex values, commands, and file paths in backticks (e.g., `` `ADM_TX` ``, `` `0x04` ``).
- **Safety Callouts:** Highlight hardware damage risks (reverse polarity, overvoltage, ESD) using blockquote callouts (`> **Warning:**` / `> **Внимание:**`).
- **Broken Links & Placeholders:** Flag broken relative links between `*.md` / `*.ru.md` files and unfinished markers (`TODO`, `TBD`, `FIXME`, `???`).

## 5. Review Output Format
- Be concise, objective, and constructive.
- Categorize every comment by severity:
  - **[CRITICAL]** — Spec contradictions, EN/RU desynchronization, pinout/voltage errors, hardware damage risks.
  - **[MAJOR]** — Ambiguous wording, inconsistent terminology, missing units or tolerances.
  - **[MINOR]** — Typos, Markdown formatting, stylistic improvements.
- Provide ready-to-apply **Suggested changes** whenever possible.
