# slide-workflow

A Claude skill that transforms messy documents — meeting transcripts, multi-meeting dumps, experiment/data reports, papers, financial statements — into **presentation-ready, design-quality slides**.

Unlike typical "one-click slide generators," this skill **thinks through the content first and verifies the numbers**, then hands off to visual production:

1. **Distill + Inventory** — reports document scope, tags every section with a destination (on-slides / reserve area / handle separately), **intercepts sensitive data (names / salaries / non-compete clauses / personal info) into the reserve area**, then **stops and waits for your confirmation**.
2. **Style Specification** — translates "make it look designed" into concrete hex codes, fonts, and layouts; choose from the built-in library of 34 styles, or use "show me options first."
3. **Generate** — single HTML file, fixed 16:9 stage, no improvising.
4. **Chart Verification** — all charts drawn from raw data with actual calculations; **re-computes every statistic the document claims before drawing**, catches numerical errors in the source, flags discrepancies without guessing or inventing.
5. **Visual QA** — expected vs. actual, screenshot-by-screenshot review, only the specified pages get touched.
6. **Retrospective Packaging** — saves the entire workflow as a reusable SOP.

Design philosophy in one line: **AI produces, humans decide.** Three decisions always stay with you: what leaves the reserve area, how to handle chart discrepancies, and visual sign-off.

## Installation

- **Cowork / Claude Desktop**: Click **Save skill** on the skill card — installs to `~/.claude/skills/slide-workflow/`.
- **Manual**: Copy the entire `slide-workflow/` folder into `~/.claude/skills/`.

Once installed, just drop a file and say "turn this into slides" or "make a presentation from this report" — the skill triggers automatically.

## File Structure

```
slide-workflow/
├── SKILL.md                      # Main workflow (6 steps)
├── references/
│   ├── prompts.md                # 6 ready-to-paste prompt templates
│   ├── chart-integrity.md        # Chart data verification rules (real math, no fabrication, no accusations)
│   └── visual-craft.md           # Visual craft (rhythm, CJK type sizes, image ratios, pre-check, QA, handoff)
├── bold-template-pack/           # 34 style design specs (see Acknowledgements below)
├── CREDITS.md                    # Third-party attribution and licenses
├── LICENSE                       # MIT license for original work
└── README.md
```

## Chaining with Other Deck Skills (Optional)

This skill is the **content + data brain**. The generation step can hand off to a skill specialized in visual production:

- **guizang-ppt-skill** — depth-focused: 2 refined styles (editorial magazine / Swiss International Typographic Style) + a verification script.
- **frontend-slides** — breadth-focused: 30+ styles + fixed 16:9 stage + PPTX import + deploy URL / PDF export.

See `references/visual-craft.md` §10 for guidance on which to use.

## Acknowledgements

- The **original work** in this project (workflow, `references/`, `SKILL.md`) is released under the **MIT License** — see [`LICENSE`](LICENSE).
- `bold-template-pack/` (34 style design specs) is from **[frontend-slides](https://github.com/zarazhangrui/frontend-slides)** by **Zara Zhang**, MIT License — see [`bold-template-pack/LICENSE`](bold-template-pack/LICENSE). The upstream source of these design systems is **[`zarazhangrui/beautiful-html-templates`](https://github.com/zarazhangrui/beautiful-html-templates)**.
- Full third-party attribution and compliance notes: [`CREDITS.md`](CREDITS.md).
