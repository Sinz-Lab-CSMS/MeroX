# MeroX & StavroX

**Cross-linking Mass Spectrometry Analysis Software**

MeroX and StavroX are comprehensive software tools for identifying cross-links of peptides in complex mixtures using mass spectrometry analysis. As of version 2.0, MeroX includes all StavroX functionality, providing a unified platform for cross-link identification and analysis. StavroX identifies all kinds of cross-linked peptides (including DSS, BS³, disulfides, zero-length cross-linkers), while MeroX specializes in identifying cross-links from MS-cleavable cross-linkers (CID-cleavable). Both software solutions utilize advanced algorithms for automated assignment and scoring of cross-linked products in protein structural analysis.

## Table of Contents

- [System Requirements](#system-requirements)
- [Key Features](#key-features)
- [Workflow Overview](#workflow-overview)
- [Getting Started](#getting-started)
- [Input File Formats](#input-file-formats)
- [Configuration and Settings](#configuration-and-settings)
- [Command Line Usage](#command-line-usage)
- [Graphical User Interface](#graphical-user-interface)
- [Visualization and Analysis Tools](#visualization-and-analysis-tools)
- [Issues and Support](#issues-and-support)
- [Citation](#citation)
- [License](#license)

## System Requirements

### Java Version Requirements

- **Versions 2014-2018**: Requires Java 8
- **Version 2024**: Requires Java 21
- **Version 2025**: Requires Java 25

Please ensure you have the appropriate Java version installed before running the software.

## Key Features

- Identification of protein cross-links from mass spectrometry data
- Support for MS-cleavable cross-linkers with automated assignment
- Advanced scoring algorithms with FDR (False Discovery Rate) control
- Support for multiple cross-linker types (DSS, BS³, disulfides, zero-length, MS-cleavable)
- Comprehensive modification handling (static and variable)
- Multiple protease support with customizable cleavage rules
- Graphical user interface for data visualization and analysis
- Multi-threading support for improved performance
- Command-line interface for batch processing and automation
- Support for multiple MS file formats (MGF, mzXML, mzML, PKL)
- Decoy database analysis for statistical validation
- Network plot generation for protein interaction visualization

## Workflow Overview

MeroX/StavroX follows a systematic workflow for cross-link identification:

1. **Data Input**: The software requires two essential files:
   - **MS Data File**: Contains precursor information and MS/MS spectra (MGF, mzXML, mzML, or PKL format)
   - **FASTA File**: Contains protein sequences used in the cross-linking experiment

2. **Configuration**: Configure analysis parameters including:
   - Protease specifications and cleavage rules
   - Possible modifications (static and variable)
   - Cross-linker chemistry and properties
   - Mass spectrometry technical parameters

3. **Analysis**: From the protein sequences and experimental setup, the software:
   - Calculates all theoretically possible peptides
   - Compares combinations of peptides to precursor masses
   - Identifies potential cross-linked products

4. **Scoring**: Identified hits are scored by:
   - Comparing theoretical fragmentation patterns to MS/MS spectra
   - Applying statistical validation (FDR calculation)
   - Ranking results by confidence

5. **Visualization**: Results are presented through:
   - Interactive main analysis window
   - Detailed spectrum views with fragment annotation
   - Network plots showing protein interactions
   - Exportable reports and data files

## Getting Started

### Quick Start

1. **Launch the software**: Execute via command line `java -jar MeroX_2025.jar`
2. **Load Files**:
   - Click "Load Fasta" to import your protein sequence file
   - Click "Load MS-File" to import your mass spectrometry data
3. **Configure Settings**: Adjust analysis parameters to match your experimental setup (see [Configuration and Settings](#configuration-and-settings))
4. **Start Analysis**: Begin the cross-link identification process
5. **Review Results**: Examine identified cross-links in the analysis windows

## Input File Formats

### FASTA Files (.fasta, .fas, .txt)

FASTA files contain protein sequences in standard one-letter amino acid code.

**Format Structure**:
```
>Protein_Name_1
SEQUENCE
>Protein_Name_2
SEQUENCE
```

**Important Notes**:
- Each protein entry starts with `>` followed by the protein name
- Sequence follows on the next line(s)
- Modified amino acids use a user-defined one-letter code (e.g., "M" for methionine, "m" for oxidized methionine)
- The software automatically adds terminal brackets:
  - Protein N-terminus: `{` (H atom)
  - Protein C-terminus: `}` (OH group)
  - Peptide N-terminus: `[` (H atom)
  - Peptide C-terminus: `]` (OH group)

**Recommended Source**: Download FASTA files from [UniProt](http://www.uniprot.org) for optimal header information compatibility.

### MGF Files (Mascot Generic Format)

MGF files contain MS/MS spectra with precursor information.

**Data Extracted by MeroX/StavroX**:
- m/z value of precursor
- Charge state
- Scan number
- Retention time
- MS/MS spectrum (fragment ions and intensities)

See the [MASCOT MGF format specification](http://www.matrixscience.com/help/data_file_help.html#GEN) for detailed format information.

### mzXML Files

Open file format for mass spectrometric data developed at the Seattle Proteome Center.

**Features**:
- Comprehensive metadata storage
- Hierarchical structure for MS/MS experiments
- Standard format supported by most MS software tools

**Conversion**: Raw data from mass spectrometers can be converted to mzXML using tools like [MSConvert](http://proteowizard.sourceforge.net/tools.shtml) or [ReadW](http://sourceforge.net/projects/sashimi/).

### mzML Files

Newer open standard for mass spectrometry data developed by the HUPO Proteomics Standards Initiative.

**Advantages**:
- XML-based structure
- Improved metadata handling
- Better controlled vocabulary integration

### PKL Files

Simple peak list format containing precursor and fragment information.

## Configuration and Settings

### Quick Setup

MeroX provides a Quick Setup feature for common experimental configurations:
- Pre-configured settings for popular cross-linkers
- Standard protease profiles (Trypsin, Lys-C, Glu-C, etc.)
- Common modification sets
- Recommended mass tolerances for different instrument types

### Amino Acids

Define amino acid properties and modifications:
- Standard amino acid masses
- Custom one-letter codes for modified residues
- Terminal modifications (N-terminal acetylation, C-terminal amidation)
- Element composition for each amino acid

### Protease Sites

Configure enzymatic cleavage rules:
- **Specificity**: Define cleavage sites (e.g., Trypsin cleaves after K and R)
- **Missed Cleavages**: Set maximum number of allowed missed cleavages
- **Exceptions**: Specify inhibitory conditions (e.g., Trypsin does not cleave before P)
- **Multiple Proteases**: Combine different protease specificities

**Common Proteases**:
- Trypsin: Cleaves C-terminal to K and R (except before P)
- Lys-C: Cleaves C-terminal to K
- Glu-C: Cleaves C-terminal to D and E
- Chymotrypsin: Cleaves C-terminal to F, W, Y, L

### Modifications

Define static and variable modifications:

**Static Modifications**: Applied to all instances of specified amino acids
- Example: Carbamidomethylation of cysteine (C → C+57.021 Da)

**Variable Modifications**: Considered as possible but not required
- Example: Oxidation of methionine (M → M+15.995 Da)
- Maximum number of variable modifications per peptide can be limited

**Common Modifications**:
- Oxidation (M): +15.995 Da
- Carbamidomethylation (C): +57.021 Da
- Phosphorylation (S, T, Y): +79.966 Da
- Acetylation (N-terminus, K): +42.011 Da
- Deamidation (N, Q): +0.984 Da

### Cross-Linker Configuration

Define cross-linker chemistry and properties:

**Parameters**:
- **Reactive Groups**: Amino acids that can be linked (e.g., K, protein N-terminus)
- **Linker Mass**: Molecular mass added by the cross-linker
- **Spacer Length**: Physical distance constraint for modeling
- **MS-Cleavable Properties**: For MeroX, define cleavage products and fragment masses
- **Dead-End/Mono-Link**: Hydrolyzed or quenched cross-linker forms

**Common Cross-Linkers**:
- DSS (Disuccinimidyl suberate): Lysine-lysine, 138.068 Da
- BS³ (Bis[sulfosuccinimidyl] suberate): Lysine-lysine, 138.068 Da
- EDC (1-Ethyl-3-[3-dimethylaminopropyl]carbodiimide): Zero-length cross-linker
- DSSO (Disuccinimidyl sulfoxide): MS-cleavable, multiple fragment signatures

### Mass Comparison Tolerances

Set mass accuracy parameters for your instrument:

**Precursor Tolerance**: Mass deviation allowed for precursor matching
- High-resolution: ±5-10 ppm
- Low-resolution: ±0.5-1.0 Da

**Fragment Tolerance**: Mass deviation for MS/MS fragment matching
- High-resolution: ±10-20 ppm
- Low-resolution: ±0.5-1.0 Da

**Recommendation**: Use ppm for high-resolution instruments (Orbitrap, FTICR) and Da for low-resolution instruments (ion traps, older TOF).

### Analysis Modes

Configure search strategies:

**Search Types**:
- Cross-links between different peptides
- Cross-links within the same peptide (loop-links)
- Mono-links (dead-end modifications)
- Unmodified peptides (for background assessment)

**Computational Options**:
- Multi-threading: Enable parallel processing for faster analysis
- Memory allocation: Adjust RAM usage for large datasets
- Candidate filtering: Set pre-scoring filters to reduce search space

### FDR & Scoring

Configure statistical validation:

**False Discovery Rate (FDR)**:
- Decoy database strategy (reverse, shuffle, or hybrid)
- Target-decoy discrimination
- FDR threshold (typically 1% or 5%)

**Scoring Parameters**:
- Fragment ion types to consider (b, y, a, x, c, z ions)
- Intensity weighting
- Minimum number of matched fragments
- Score cutoff thresholds

### Visualization Settings

Customize graphical output:

**Spectrum View**:
- Fragment ion color coding
- Intensity normalization
- Theoretical vs. observed peak alignment
- Annotation density

**Network Plots**:
- Layout algorithms
- Node size and color schemes
- Edge thickness (based on number of cross-links or confidence)
- Label display options

### Composition and Elements

Define custom elements or isotopic compositions for specialized experiments:
- Non-standard isotope labeling
- Custom chemical modifications
- Elemental composition constraints

## Command Line Usage

MeroX/StavroX supports command-line execution for automation and batch processing.

### Basic Syntax

```
bash
java -jar MeroX_2025.jar [options] <ms-file> <fasta-file> <settings-file> <result-file> [log-file]
```

### Command Line Options

| Option | Description |
|--------|-------------|
| `-D` | Decoy analysis only (no target database search) |
| `-M` | Disable multi-threading |
| `-L` | Do not write log file |
| `-l` | Write log output to command prompt |

### Usage Examples

**Open Settings Window**:
```
bash
java -jar MeroX_2025.jar file.ssf
```

**Open Saved Results**:
```
bash
java -jar MeroX_2025.jar file.zhrm
```

**Run Analysis (basic)**:
```
bash
java -jar MeroX_2025.jar data.mgf proteins.fasta settings.mxf results.zhrm
```

**Run Analysis with Log**:
```
bash
java -jar MeroX_2025.jar data.mgf proteins.fasta settings.mxf results.zhrm analysis.log
```

**Run Analysis with Console Output**:
```
bash
java -jar MeroX_2025.jar data.mgf proteins.fasta settings.mxf results.zhrm -l
```

**Single-threaded Decoy Analysis**:
```
bash
java -jar MeroX_2025.jar -D -M data.mgf proteins.fasta settings.mxf results.zhrm analysis.log
```

### Batch Processing

For high-throughput analysis, create batch scripts to process multiple datasets:

**Windows Batch Example**:
```
batch
@echo off
for %%f in (*.mgf) do (
    java -jar MeroX_2025.jar %%f proteins.fasta settings.mxf %%~nf.zhrm %%~nf.log
)
```

**Linux/Mac Shell Example**:
```
bash
#!/bin/bash
for file in *.mgf; do
    java -jar MeroX_2025.jar "$file" proteins.fasta settings.mxf "${file%.mgf}.zhrm" "${file%.mgf}.log"
done
```

## Graphical User Interface

### Start Window

The initial window for loading data and configuring analysis:
- **Load MS Data**: Import mass spectrometry data
- **Load Settings**: Access configuration dialogs
- **Load Target Fasta**: Import protein sequence database
- **Select Result File**: Specify result file path
- **Start Analysis**: Begin cross-link identification

### Main Analysis Window

Primary interface for reviewing results:

**Features**:
- Cross-link list with sortable columns (score, FDR, proteins)
- Filtering options (by score, FDR, protein, peptide length)
- Export functions (CSV, Excel, text reports)
- Network view access
- Detail view for individual cross-links

**Information Displayed**:
- Protein pairs involved in cross-link
- Peptide sequences with modification indicators
- Cross-link positions in protein sequences
- Score and statistical confidence
- Spectrum match quality metrics

### Detail Window

In-depth view of individual cross-link identifications:

**Spectrum View**:
- Annotated MS/MS spectrum with matched fragments
- Theoretical peak predictions
- Fragment ion coverage display
- Mass error visualization

**Cross-Link Information**:
- Peptide sequences with cleavage sites highlighted
- Modification locations
- Cross-link connectivity diagram
- Alternative explanations (if any)

**Quality Metrics**:
- Number of matched fragments
- Sequence coverage
- Mass accuracy statistics
- Score components breakdown

### Decoy Analysis Window

Visualization of target-decoy discrimination:

**FDR Plots**:
- Score distribution for target and decoy hits
- FDR as a function of score threshold
- Histogram of score differences

**Statistics**:
- Total targets and decoys identified
- FDR at various score cutoffs
- Estimated false positives

### Network Plots

Visual representation of protein interaction networks:

**Features**:
- Nodes represent proteins
- Edges represent cross-links
- Interactive manipulation (zoom, pan, rearrange)
- Export to image formats or Gephi
- Integration with structural modeling tools

**Display Options**:
- Color coding by protein type, domain, or confidence
- Edge thickness proportional to cross-link count
- Labels for protein names or IDs

## Visualization and Analysis Tools

### XLDataGraph

Results from MeroX can be visualized and analyzed using the **XLDataGraph** Python library:

- **Repository**: [https://github.com/a-helix/XLDataGraph](https://github.com/a-helix/XLDataGraph)
- **PyPi**: [https://pypi.org/project/xldg/](https://pypi.org/project/xldg/)
- **Features**:
  - Circos protein interaction plots
  - Venn diagrams for comparing datasets
  - Gephi network exports for advanced network analysis
  - ChimeraX integration for 3D structural visualization
  - Structural predictions and distance validation
- **File Support**: Direct import of MeroX `.zhrm` files with domain annotations, FASTA sequences, and structural data

### xVis Web Server

Cross-link data can also be visualized using **xVis** for schematic visualization and interpretation of crosslink-derived spatial restraints.

- **URL**: Referenced in citation (4)
- **Features**:
  - Clear schematic representations
  - Circular, bar, and network diagrams
  - Interactive features for topological analysis
  - Functional interpretation tools
  - Web-based access (no installation required)

## Documentation

📚 **Full documentation will be available soon on this repository.**

For now, comprehensive materials including tutorials, detailed user guides, and FAQ are available at:
**[https://www.stavrox.com/](https://www.stavrox.com/)**

### Additional Resources

- **Quick User Guide**: [https://www.stavrox.com/qug.htm](https://www.stavrox.com/qug.htm)
- **Detailed Help**: [https://www.stavrox.com/help.htm](https://www.stavrox.com/help.htm)
- **FAQ**: [https://www.stavrox.com/faq.htm](https://www.stavrox.com/faq.htm)

## Issues and Support

### Reporting Issues

Found a bug, have a feature request, or need help with setup or troubleshooting?  
Please submit your issues here:  
**[MeroX GitHub Issues](https://github.com/Sinz-Lab-CSMS/MeroX/issues)**

### Contact Developer

For setup assistance, troubleshooting, or bug reports:
- **GitHub**: https://github.com/Sinz-Lab-CSMS/MeroX/issues

## License

This software is distributed under a freeware license. See the LICENSE file for details.

## Citation

If you use MeroX/StavroX in your research, please cite the appropriate publications:

1. **[Götze et al. (2014)](http://www.ncbi.nlm.nih.gov/pubmed/25261217)** - Automated Assignment of MS/MS Cleavable Cross-Links in Protein 3D-Structure Analysis. *J Am Soc Mass Spectrom.* 2014 Sep; ePub ahead of print.

2. **[Götze et al. (2012)](http://www.ncbi.nlm.nih.gov/pubmed/22038510)** - StavroX--a software for analyzing crosslinked products in protein interaction studies. *J Am Soc Mass Spectrom.* 2012 Jan;23(1):76-87.

3. **[Müller et al. (2010)](http://www.ncbi.nlm.nih.gov/pubmed/20704385)** - Cleavable Cross-Linker for Protein Structure Analysis: Reliable Identification of Cross-Linking Products by Tandem MS. *Anal Chem.* 2010 Aug;82(16):6958-6968.

4. **[Grimm et al. (2015)](http://www.ncbi.nlm.nih.gov/pubmed/25956653)** - xVis: a web server for the schematic visualization and interpretation of crosslink-derived spatial restraints. *Nucleic Acid Res.* 2015 Jul;43(W1):W362-9.

5. **[Iacobucci and Götze et al. (2018)](https://www.ncbi.nlm.nih.gov/pubmed/30382245)** - A cross-linking/mass spectrometry workflow based on MS-cleavable cross-linkers and the MeroX software for studying protein structures and protein-protein interactions. *Nat Protoc.* 2018 Dec;13(12):2864-2889.

## Acknowledgments

**Developed by**: Michael Götze, Oleksandr Sorokin

**Logo Design**: Rebekka Balogh

---

*This repository is currently under construction. Complete documentation and source code will be available soon.*
