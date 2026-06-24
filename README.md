# Variant Cartographer

A single-file, browser-based tool that maps every **pathogenic / likely-pathogenic** ClinVar variant onto a protein, alongside its domain architecture, exon structure, and any custom mutations you add. Type a human gene symbol and it draws a publication-style lollipop + density figure on the fly.

**Live site:** `https://tinyurl.com/variant-cartographer`

---

## What it does

- **Pulls live data** for any human gene from three public sources — no database to maintain:
  - **ClinVar** (NCBI E-utilities) — pathogenic / likely-pathogenic variants, by aggregate VCV classification
  - **UniProt** (reviewed human entry) — protein length and domain/feature architecture
  - **Ensembl** (canonical transcript) — exon / intron / UTR structure and genomic coordinates
- **Protein variant map** — a lollipop of variants colored by functional class (frameshift, nonsense, splice, missense, etc.), stacked by residue, over the domain track, with a sliding-window truncating-vs-missense density panel.
- **Exon track (aligned)** — coding sequence mapped onto the residue axis, so you can read which exon each variant falls in.
- **Detailed gene model** — a separate box drawing the full exon/intron/UTR structure in genomic coordinates (with a *to-scale* toggle), independent of the protein axis. Shows reference assembly and the gene's chromosomal start/stop.
- **Custom mutations** — add your own variants by residue position, type, and label; multiple supported. A *highlight* mode grays out the ClinVar variants so your variants of interest stand out.
- **Themes** — light/dark mode and six accent palettes, with an accent-matched page background.
- **Exports** — download the protein map and the gene model each as **SVG** (vector) or **PNG**; the full variant table as **CSV**; and a multi-sheet **Excel workbook** (`.xlsx`) containing a **Summary** (breakdown by classification, review-star level, variant type, and functional class), a full **P-LP Variants** sheet (with GRCh38 + GRCh37 coordinates, stars, last-evaluated date, residue, etc.), and an **Excluded (non-P/LP)** sheet documenting records the broad ClinVar search captured but that are not aggregate P/LP.

## How it works

Everything runs **client-side in your browser**. There is no server and nothing is uploaded — the page fetches directly from the public APIs, so requests come from your own machine. Results are cached in your browser (`localStorage`) for 24 hours, so redrawing a gene makes no new calls.

## Usage notes

- **Gene symbol** — use the official HGNC symbol (e.g. `TP53`, `CFTR`, `SLC25A13`).
- **Structure features are lazy** — the exon track and gene model only query Ensembl when you enable them.
- **NCBI API key (optional)** — under *Advanced*, you can paste your **own** free NCBI API key to raise the rate limit from ~3 to 10 requests/second. The key is stored only in your browser. **Do not** commit a personal key into the page source.
- **Positions** — missense/nonsense/frameshift positions come from HGVS `p.` notation; splice/intronic variants are placed at an approximate residue (cDNA ÷ 3) and flagged. Whole-gene CNVs are counted but not plotted.
- **Coordinates** — the gene model reports the reference assembly (e.g. GRCh38) and the gene's chromosomal span; the diagram is drawn over the canonical transcript.

## Deploying on GitHub Pages

1. Create a **public** repository and upload these three files (`index.html`, `README.md`, `LICENSE`).
2. Go to **Settings → Pages**.
3. Under *Build and deployment*, set **Source** = *Deploy from a branch*, **Branch** = `main`, folder = `/ (root)`, then **Save**.
4. After ~1–2 minutes your site is live at `https://YOUR-USERNAME.github.io/REPO-NAME/`.

To update, commit a new `index.html` (or re-upload via the web UI); the site refreshes within a minute or two.

## Limitations / disclaimer

Exploratory and visualization tool only — **not for clinical use**. ClinVar updates weekly, so counts will drift over time. Classifications reflect ClinVar's aggregate germline classification at every review (star) level; filter or verify against the primary record for higher-confidence use.

## Data sources

- NCBI ClinVar — https://www.ncbi.nlm.nih.gov/clinvar/
- UniProt — https://www.uniprot.org/
- Ensembl — https://www.ensembl.org/

---

Copyright © 2026 Nguyen Thanh Phuong. All rights reserved. See `LICENSE`.
