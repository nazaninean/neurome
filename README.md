# Neurome

**Agentic scientific imaging data analysis — powered by AI.**

Neurome accepts raw scientific data files, automatically detects the format, reasons about what analyses are appropriate, executes real Python code, returns a structured scientific report, and grounds findings in published literature from PubMed — all in one step.

No pipeline configuration. No manual preprocessing. No algorithm selection. The AI figures it out.

---

## What it does

Drop in any raw scientific file. Neurome will:

1. **Inspect** the file — detect format, structure, dimensions, data types
2. **Reason** about what analyses make sense for this specific data
3. **Execute** real Python code using domain-appropriate scientific libraries
4. **Interpret** the results in plain scientific language
5. **Ground** findings in published literature — searches PubMed and Semantic Scholar automatically, retrieves relevant papers, and compares your results against existing research
6. **Generate a report** — downloadable as PDF, viewable onsite
7. **Answer** follow-up questions in a chat interface

---

## Supported formats

| Domain | Formats |
|---|---|
| Neuroimaging | NIfTI (`.nii`, `.nii.gz`), DICOM (`.dcm`) |
| Electrophysiology | EDF (`.edf`, `.bdf`), MNE FIF (`.fif`) |
| Genomics | FASTQ (`.fastq`, `.fq`), FASTA (`.fa`, `.fasta`), VCF (`.vcf`) |
| Multi-omics | HDF5 (`.h5`, `.hdf5`), AnnData (`.h5ad`) |
| Tabular | CSV, TSV |

---

## Features

- **Agentic analysis** — Claude reasons about your data and decides what to do, rather than following fixed rules
- **Literature grounding** — after every analysis, automatically searches PubMed and Semantic Scholar and writes a literature context section comparing findings to published research
- **Structured reports** — results shown as clean scientific reports with summary, key findings, methods, and literature context. Downloadable as PDF.
- **Persistent projects** — analyses saved in your browser. Reports and sidebar update automatically as you run more.
- **Follow-up chat** — ask questions about your results after the analysis completes

---

## Architecture

```
neurome.html         ← Frontend (single file, no build step)
agent_backend.py     ← Python backend (file inspection, code execution, Claude API, literature search)
```

The frontend is a single HTML file — no build step, no dependencies. Open it in any browser.

The backend is a FastAPI server that:
- Inspects uploaded files using scientific Python libraries
- Sends metadata to Claude AI, which reasons about the data and writes analysis code
- Executes the generated code in a safe namespace
- Forces a final written interpretation after all code runs
- Searches PubMed and Semantic Scholar for relevant papers
- Asks Claude to compare findings against retrieved abstracts
- Returns everything to the frontend

---

## Getting started

### Requirements
- Python 3.9+
- An Anthropic API key — get one at [console.anthropic.com](https://console.anthropic.com)

### Install

```bash
pip3 install -r requirements.txt
```

### Run

```bash
ANTHROPIC_API_KEY=your_key_here python3 agent_backend.py
```

Then open `neurome.html` in your browser. The sidebar will show **Backend: Ready**.

Enter your Anthropic API key via the **API Key** button in the top right, drop a file, and click **Start analysis**.

---

## Stack

- **Reasoning** — [Claude AI](https://anthropic.com) (claude-sonnet-4-6)
- **Backend** — [FastAPI](https://fastapi.tiangolo.com) + [uvicorn](https://www.uvicorn.org)
- **Literature** — [PubMed E-utilities API](https://www.ncbi.nlm.nih.gov/books/NBK25501/) + [Semantic Scholar API](https://www.semanticscholar.org/product/api) (both free, no key required)
- **Neuroimaging** — [nibabel](https://nipy.org/nibabel/), [nilearn](https://nilearn.github.io), [MNE-Python](https://mne.tools)
- **Genomics** — [biopython](https://biopython.org), [h5py](https://www.h5py.org)
- **ML** — [scikit-learn](https://scikit-learn.org), [scipy](https://scipy.org)
- **Frontend** — Vanilla HTML/CSS/JS, zero dependencies

---

## Project structure

```
neurome/
├── neurome.html         # Frontend — open this in your browser
├── agent_backend.py     # Python backend — run this first
├── requirements.txt     # Python dependencies
└── README.md
```
