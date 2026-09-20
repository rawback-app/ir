# ir — agent guide

Rawback's investor-relations repo: the seed-round pitch deck, published
bilingually (EN / 中文) as both ready-to-send PDFs and web decks. It is a
content repo — no build system, no dependencies, no CI, nothing to run. It has
no code dependency on the other Rawback repos.

## Commands

None. There is nothing to install, build, test or deploy. The HTML is authored
by hand and committed; distribution is GitHub itself (the PDFs render inline)
plus "download the repo and open `index.html`".

To regenerate a PDF: open `en/index.html` or `zh/index.html` in a browser and
print to PDF at 1920×1080 landscape.

## Layout

| Path | What |
|---|---|
| `README.md` / `README.zh-CN.md` | The public front door, and the repo's main artifact |
| `Rawback-Investor-Deck-EN.pdf` / `-ZH.pdf` | Ready-to-send decks |
| `en/`, `zh/` | `index.html` — the built single-file deck — plus `preview.png`, `overview.jpg` |
| `src/en/project/`, `src/zh/project/` | `deck.json` + `slides/*.html` — the 13 slide sources |
| `assets/` | Founder photographs the decks reference as `../assets/*.jpg` |

## Conventions

- **Slides are edited in `src/<lang>/project/slides/*.html`**, never in
  `en|zh/index.html`. Those two files are the built bundle: 13 fixed 1920×1080
  `<section>` frames concatenated with one inline `<style>` block.
- `src/<lang>/project/deck.json` fixes slide order via its `order` array, and
  names the `cover` and the four `sections`. Adding or reordering a slide means
  updating `deck.json` too.
- The decks are **single-file, not self-contained**: `index.html` loads
  Newsreader + Manrope from `fonts.googleapis.com` and references
  `../assets/*.jpg`. Keep the `assets/` folder alongside.

## Validation

There is no test suite. Before committing, open both `en/index.html` and
`zh/index.html` in a browser and confirm all 13 frames render with their
photographs.

## Gotchas

- **Edit EN and ZH as a pair.** The two READMEs are kept in lockstep — every
  heading currently sits on the same line number in both files, and every figure
  matches (shipped-photo count, MCP server count, the four price points, the four
  storage/credit tiers, slide count, date). A change to one that skips the other
  is the failure mode this repo is most prone to.
- Every number in the READMEs also appears in the slides and the PDFs. Changing a
  figure means changing it in six places: two READMEs, two slide sets, two PDFs.
- The PDFs are committed binaries. Re-export both when the slides change, or they
  silently disagree with the web decks.

## Commit & PR

Conventional Commits with scope, e.g. `docs(ir): update seed-round figures`,
`feat(deck): add competitive-landscape slide`.
