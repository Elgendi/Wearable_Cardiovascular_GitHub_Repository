# Wearable cardiovascular accuracy must account for unobserved time

Data, analysis code, figures and LaTeX sources accompanying the manuscript.

## Reproduce the analyses

Tested with Python 3.12.14. From the repository root:

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python code/run_all.py
```

On Windows, activate with `.venv\Scripts\activate` instead. After dependencies are installed, the analysis runs offline from included data and extracted feature tables. It verifies AFDB input hashes, performs numerical checks and regenerates Figures 2–5, supplementary Figure S1 and analysis tables. Figure 1 is supplied original artwork and is preserved unchanged. `tested_environment.json` and `Validation_record.json` document the previously tested analysis environment and validation.

## Re-extract features from original PPG signals

Original PPG waveforms (approximately 438 MB) are hosted by PhysioNet and are not bundled here. Network access is required for download:

```bash
python code/download_ppg.py --raw-dir raw_ppg
python code/ppg_extract.py --raw-dir raw_ppg
python code/run_all.py
```

Source URLs, publisher checksums, protocols and feature provenance are in `source_data/`.

## Contents

| Path | Contents |
| --- | --- |
| `code/` | Analysis, downloads, feature extraction and numerical checks |
| `source_data/` | Attributed inputs, extracted features, protocols and results |
| `figures/` | Main and supplementary figures, including original Figure 1 |
| `tables/` | Generated LaTeX tables |
| `reference_assets/` | Original artwork used by the reproduction scripts |
| `manuscript/main.tex` | Main manuscript entry point for pdfLaTeX |
| `manuscript/supplement.tex` | Supplementary information |
| `requirements.txt` | Exact versions of principal Python dependencies |

## Compile the manuscript

Upload the contents of `manuscript/` as an Overleaf project and choose `main.tex` as the main document, using pdfLaTeX. The figures and bibliography needed for compilation are included in that folder. Locally, from `manuscript/`, run `latexmk -pdf main.tex`. Compile `supplement.tex` separately for supplementary information. Analysis scripts regenerate the root figures and tables; copy those outputs into `manuscript/figures/` and `manuscript/tables/` before recompiling after an analysis change.

## Evidence and interpretation

The measured PPG analysis uses recorded signals with offline quality gates. The AFDB analysis uses recorded rhythm timings with imposed observation schedules. Clinical tables contain published summaries. The worked status record and mask examples are constructed examples. These evidence types must remain distinct; the analyses do not establish commercial-device clinical validation or prospective clinical benefit.

See `source_data/README.md` for the evidence map and `source_data/PPG_DATA_DICTIONARY.md` for the PPG fields.

## Attribution and licensing

Third-party data retain their source licenses. PPG-derived database content is supplied under ODbL v1.0; see `source_data/PPG_ATTRIBUTION.md` and `source_data/PPG_SOURCE_LICENSE.txt`. AFDB attribution and its license reference are in `source_data/afdb/ATTRIBUTION.md`. A separate open-source license for author-created code and artwork has not been assigned in this package; dataset licenses do not grant rights to those materials.

## Citation

The accompanying manuscript is not represented here as an accepted or published article. `CITATION.cff` provides its title and authors without a fabricated publication DOI or release identifier. Please also cite the original datasets when using their data.
