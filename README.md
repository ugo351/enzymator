## License

This project is licensed under the MIT License - see the LICENSE.txt file for details.

# Enzymator V1.00 - Peptide Analysis Tool

## Overview

Enzymator V1.00 is a comprehensive Python application for analyzing peptide sequences from mass spectrometry data, specifically designed for studying Matrix Metalloproteinases (MMPs), ADAMTS proteins, and other proteolytic enzymes. The tool provides automated peptide identification, mass spectral analysis, and MS/MS fragmentation analysis capabilities.

## Features

### 1. **Peptide Mass Search and Identification**
- Automated peptide sequence matching against a comprehensive database
- Support for 54 different protein sequences including:
  - Human MMPs (MMP1-28)
  - ADAMTS proteins (ADAMTS1-20)
  - Common contaminants (HSA, BSA, MSA)
  - Proteases (Chymotrypsin, Trypsin)
  - Interleukin-1 (IL1)

### 2. **Chemical Labeling Support**
- **Ahx (Aminohexanoic acid + alpha cyano-4-hydroxycinamic acid)** labeling: 284.126092 Da
- **Amb (4-Aminomethylbenzoic acid + alpha cyano-4-hydroxycinamic acid)** labeling: 304.095792 Da  
- **Unlabeled** peptide analysis
- Automatic mass adjustment based on labeling type

### 3. **Enzymatic Digestion Analysis**
- **Chymotrypsin**: Cleaves after F, Y, W, M, L, H
- **Trypsin**: Cleaves after K, R
- **Combined digestion**: Both enzymes simultaneously
- Missed cleavage calculation and filtering

### 4. **Spectral Processing Tools**

#### SoustractorV2 Feature
- Subtracts spectra (CHCA matrix from CHCE matrix)
- Automated peak detection and grouping
- Isotope pattern recognition
- Excel export with organized results

#### Peak Extraction
- Import m/z values from Excel files
- Automatic column detection and data cleaning

### 5. **MS/MS Analysis**
- Theoretical fragmentation pattern generation
- Support for b, y, a, immonium ions and internal fragments
- Loss and addition series (H₂O, NH₃, CO)
- Fragment matching with experimental spectra
- Scoring system based on matched ions
- Lysine labeling consideration in fragmentation

### 6. **Pro-domain Analysis**
- Automatic detection of peptides originating from protein pro-domains
- Configurable inclusion/exclusion of pro-domain fragments
- Pre-defined pro-domain boundaries for major MMPs

### 7. **Filtering Options**
- Mass tolerance adjustment (default: 0.5 Da)
- Maximum missed cleavages (default: 3)
- Sequence validation rules
- Overlapping peptide detection

### 8. **Data Export and Visualization**
- Excel export 
- Statistical summaries (enzyme occurrence, overlapping peptides)
- Spectral plotting with peak annotation
- Comprehensive result tables

## System Requirements

### Required Python Libraries
```python
tkinter          # GUI framework (usually included with Python)
pandas           # Data manipulation
matplotlib       # Plotting
threading        # Multi-threading support
re               # Regular expressions
os               # Operating system interface
collections      # Specialized data structures
functools        # Functional programming tools
dataclasses      # Data classes
typing           # Type hints
```

### Installation
```bash
pip install pandas matplotlib
```

Note: `tkinter` is typically included with Python installations.

## How to Run

### 1. **Starting the Application**
```bash
python enzymatorV1.00.py
```

### 2. **Basic Peptide Search**

1. **Enter MALDI peaks**: Input m/z values in the "Pic(s) MALDI" field, separated by spaces
   ```
   Example: 1234.567 1456.789 1678.901
   ```

2. **Select digestion type**: Check Chymotrypsin, Trypsin, or both

3. **Choose protein sequences**: Select from the organized panels:
   - **Main MMPs**: Most commonly studied MMPs
   - **Contaminants**: HSA, BSA, MSA, etc.
   - **ADAMTS**: All ADAMTS proteins
   - **Other MMPs**: Additional MMP variants

4. **Set parameters**:
   - **Mass tolerance**: Allowed deviation (default: 0.5 Da)
   - **Max missed cleavages**: Maximum allowed (default: 3)
   - **Include pro-domain**: Check/uncheck as needed

5. **Select labeling type**: AmbCHCA, AhxCHCA, or None

6. **Click "Search"** to start analysis

### 3. **Using SoustractorV2**

1. Click **"SoustractorV2"** button
2. Select **CHCA matrix file** (TXT format)
3. Select **CHCE matrix file** (TXT format)
4. Processing window will show progress
5. Choose output Excel file location
6. Results automatically open in Excel

### 4. **Peak Extraction from Excel**

1. Click **"Extract"** button
2. Select Excel file containing m/z data
3. Tool automatically detects m/z column
4. Values populate in the MALDI field

### 5. **MS/MS Analysis**

1. Perform initial peptide search
2. Click **"MS/MS Analysis"** button
3. Select Excel file with MS/MS spectra
4. Choose output location for results
5. Analysis matches theoretical fragments with experimental data

### 6. **Custom Sequence Analysis**

1. Click **"Custom sequence"**
2. Enter your protein sequence (single-letter amino acid codes)
3. Check **"Use"** to include in analysis

## Input File Formats

### TXT Files (for SoustractorV2)
Works with Mass Spectrum extract from FlexAnalysis, require Mass list of CHCA spectrum and CHCE spectrum
```
m/z      Intensity
1000.5   12345.6
1001.5   23456.7
1002.5   34567.8
```

### Excel Files (for peak extraction)
- Column A should contain m/z values
- Starting from row 3 (if no headers)
- Or any column labeled "m/z"

### MS/MS Excel Files
Works with Mass List to excel from FlexAnalysis files. Several mass list can be handle as long as they are on the same file in different sheets
- Each sheet represents one spectrum
- Cell A1 should contain precursor mass in format: "...1234.567.LIFT..."
- Data starts from row 4
- Columns: m/z (A) and Intensity (C)

## Output Files

### Main Results Excel File
Contains multiple sheets:
- **Main results**: Peptide matches with all details
- **Enzyme statistics**: Occurrence counts
- **Overlapping peptides**: Analysis of redundant sequences

### SoustractorV2 Output
- **Grouped peaks**: After background subtraction
- **Top 50 peaks**: Most intense signals
- **Isotope A only**: Monoisotopic peaks

### MS/MS Analysis Output
- **Fragment matches**: Theoretical vs experimental
- **Scoring results**: Match quality assessment
- **Detailed annotations**: Ion series identification

## Understanding the Results

### Result Columns
- **MALDI peaks**: Input m/z value
- **Protein**: Source protein
- **Sequence**: Peptide sequence with preceding amino acid
- **Position**: Location in protein sequence
- **Masses**: Calculated mass
- **Gap**: Mass deviation from target
- **MissClivage**: Number of missed cleavages
- **Pro-Domain?**: Whether peptide is from pro-domain

### Statistics Section
- **Analysis time**: Processing duration
- **Combinations tested**: Search space coverage
- **Enzyme occurrences**: Hit distribution
- **Overlapping peptides**: Redundant sequences detected

## Tips and Best Practices

### Mass Accuracy
- Use appropriate mass tolerance based on your instrument
- MALDI-TOF: typically 0.1-0.5 Da
- High-resolution MS: 0.01-0.05 Da


### Protein Selection
- Start with main MMPs for targeted analysis
- Include contaminants to identify background signals
- Use custom sequences for novel proteins

### MS/MS Analysis
- Requires good quality fragmentation spectra
- Works best with peptides containing lysine residues (for labeling analysis)
- Fragment tolerance can be adjusted  (default: 0.5 Da)

## Troubleshooting

### Common Issues

1. **"No matches found"**
   - Check mass tolerance settings
   - Verify correct labeling type
   - Ensure appropriate enzyme selection

2. **Excel export errors**
   - Close any open Excel files
   - Check file permissions
   - Ensure sufficient disk space

3. **Slow performance**
   - Reduce number of selected proteins
   - Decrease mass tolerance slightly
   - Close unnecessary applications

4. **Import errors**
   - Verify file formats match specifications
   - Check for non-numeric data in m/z columns
   - Ensure proper file encoding (UTF-8)

### Memory Optimization
- The tool pre-computes peptide indices for fast searching
- Large protein sets may require more RAM
- Consider analyzing in batches for very large datasets

## Advanced Features

### Custom Sequence Support
- Add your own protein sequences
- Useful for novel proteins or variants
- Supports standard single-letter amino acid codes

### Pro-domain Analysis
- Pre-defined boundaries for major MMPs
- Useful for studying zymogen activation
- Can be toggled on/off per analysis

### Spectral Visualization
- Built-in plotting capabilities
- Peak annotation at 10% threshold
- Supports both raw and processed spectra

## Version Information

**Current Version**: V1.00 
**Last Updated**: 09/2025  
**Compatibility**: Python 3.6+

## Contact and Support

This tool was developed for analytical chemistry and mass spectrometry research, particularly focused on protease analysis and peptide characterization in biochemical studies. It is working with Bruker Flexanalysis export formats.

For technical support or feature requests, contact ugo.pasco@outlook.com .

