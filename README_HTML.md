# Enzymator HTML — Peptide Analysis Tool (Web Version)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
![Version](https://img.shields.io/badge/version-1.20-blue)
![Platform](https://img.shields.io/badge/platform-Web%20Browser-green)

## 🧬 Overview

**Enzymator HTML** is the standalone, browser-based version of the Enzymator proteomics tool. It requires **no installation**, no Python, and no server — simply open the `.html` file in any modern web browser and start analyzing peptide sequences from mass spectrometry data.

This version is specifically designed for studying **Matrix Metalloproteinases (MMPs)**, **ADAMTS proteins**, and other relevant proteins in the context of MALDI-TOF mass spectrometry.

---

## 📁 Files

| File | Description |
|------|-------------|
| `EnzymatorV1.10.html` | First HTML release of Enzymator |
| `EnzymatorV1.20.html` | Latest HTML release (recommended) |
| `enzymator_preloaded_data.js` | Preloaded protein sequence database (required) |

> ⚠️ **Important:** `enzymator_preloaded_data.js` must be in the **same folder** as the `.html` file for the tool to work correctly.

---

## 🚀 How to Use

### 1. Download

Download the following two files and place them in the **same folder**:
- `EnzymatorV1.20.html`
- `enzymator_preloaded_data.js`

### 2. Open in Browser

Double-click `EnzymatorV1.20.html` or open it with any modern browser (Chrome, Firefox, Edge, Safari).

> No installation, no internet connection required after download.

---

## 🔬 Features

### 1. Peptide Mass Search and Identification
- Automated peptide sequence matching against a comprehensive database
- Support for **54+ protein sequences** including:
  - Human MMPs (MMP1–28)
  - ADAMTS proteins (ADAMTS1–20)
  - Common contaminants (HSA, BSA, MSA)
  - Proteases (Chymotrypsin, Trypsin)
  - Interleukin-1 (IL-1)

### 2. Chemical Labeling Support
- **Ahx** (Aminohexanoic acid + CHCA): +284.126092 Da
- **Amb** (4-Aminomethylbenzoic acid + CHCA): +304.095792 Da
- **Unlabeled** peptide analysis

### 3. Enzymatic Digestion Analysis
- **Chymotrypsin**: cleaves after F, Y, W, M, L, H
- **Trypsin**: cleaves after K, R
- **Combined digestion**: both enzymes simultaneously
- Missed cleavage calculation and filtering

### 4. MS/MS Analysis
- Theoretical fragmentation pattern generation
- Support for b, y, a, immonium ions and internal fragments
- Loss/addition series (H₂O, NH₃, CO)
- Fragment matching and scoring

### 5. Pro-domain Analysis
- Automatic detection of peptides originating from protein pro-domains
- Pre-defined pro-domain boundaries for major MMPs
- Configurable inclusion/exclusion

### 6. Filtering Options
- Adjustable mass tolerance (default: 0.5 Da)
- Max missed cleavages setting (default: 3)
- Overlapping peptide detection

### 7. Data Export
- Export results to Excel (`.xlsx`)
- Statistical summaries (enzyme occurrences, overlapping peptides)

---

## 📋 Basic Workflow

1. **Enter MALDI peaks** — input m/z values separated by spaces
   ```
   Example: 1234.567 1456.789 1678.901
   ```
2. **Select digestion type** — Chymotrypsin, Trypsin, or both
3. **Choose proteins** — select from MMPs, ADAMTS, contaminants, etc.
4. **Set parameters** — mass tolerance, missed cleavages, pro-domain inclusion
5. **Select labeling** — AmbCHCA, AhxCHCA, or None
6. **Click Search** — results appear in the table below
7. **Export** — download results as Excel file

---

## 💡 Tips & Best Practices

- **MALDI-TOF**: use a mass tolerance of 0.1–0.5 Da
- Always include **contaminant proteins** (HSA, BSA) to filter background signals
- Use **custom sequence** input for novel or non-listed proteins
- For labeling experiments, always verify the correct labeling type is selected

---

## 🔄 Differences from Python Version

| Feature | Python Version | HTML Version |
|---------|---------------|-------------|
| Installation | pip + Python 3.6+ | None |
| GUI | Tkinter desktop app | Web browser |
| SoustractorV2 | ✅ | ❌ |
| Peak extraction from Excel | ✅ | ❌ |
| MS/MS Analysis | ✅ | ✅ |
| Portability | OS-dependent | Any device with a browser |

---

## 🛠️ Troubleshooting

**Tool doesn't load / database missing**
→ Make sure `enzymator_preloaded_data.js` is in the **same folder** as the HTML file.

**No matches found**
→ Check mass tolerance, labeling type, and enzyme selection.

**Export not working**
→ Allow pop-ups and file downloads in your browser settings.

**Slow on large datasets**
→ Reduce the number of selected proteins or narrow your mass range.

---

## 📬 Contact & Support

Developed for analytical chemistry and mass spectrometry research, focused on protease analysis and peptide characterization.

📧 **Contact:** ugo.pasco@outlook.com

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 🗂️ Version History

| Version | Date | Notes |
|---------|------|-------|
| V1.00 | 09/2025 | Initial Python release |
| V1.10 | 2025 | First HTML version |
| V1.20 | 2026 | Latest HTML version (current) |
