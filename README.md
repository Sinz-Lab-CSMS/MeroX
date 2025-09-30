# MeroX & StavroX

**Cross-linking Mass Spectrometry Analysis Software**

MeroX and StavroX are comprehensive software tools for identifying cross-links of peptides in complex mixtures using mass spectrometry analysis. As of version 2.0, MeroX includes all StavroX functionality, providing a unified platform for cross-link identification and analysis. StavroX identifies all kinds of cross-linked peptides (including DSS, BS³, disulfides, zero-length cross-linkers), while MeroX specializes in identifying cross-links from MS-cleavable cross-linkers (CID-cleavable). Both software solutions utilize advanced algorithms for automated assignment and scoring of cross-linked products in protein structural analysis.

## Documentation

📚 **Full documentation will be available soon on this repository.**

For now, comprehensive materials including tutorials, user guides and FAQ are available at:
**[https://www.stavrox.com/](https://www.stavrox.com/)**

## System Requirements

### Java Version Requirements

- **Versions 2014-2018**: Requires Java ≥8
- **Version 2024**: Requires Java ≥21

Please ensure you have the appropriate Java version installed before running the software.

## Key Features

- Identification of protein cross-links from mass spectrometry data
- Support for MS-cleavable cross-linkers
- Advanced scoring algorithms with FDR control
- Graphical user interface for data visualization
- Multi-threading support for improved performance
- Support for multiple file formats including mzML

## Visualization and Analysis Tools

### XLDataGraph
Results from MeroX can be visualized and analyzed using the **XLDataGraph** Python library:
- **Repository**: [https://github.com/a-helix/XLDataGraph](https://github.com/a-helix/XLDataGraph)
- **Features**: Circos protein interaction plots, Venn diagrams, Gephi network exports, ChimeraX integration, structural predictions
- **File Support**: Direct import of MeroX `.zhrm` files with domain annotations, FASTA sequences, and structural data

### xVis Web Server
Cross-link data can also be visualized using **xVis** for schematic visualization and interpretation of crosslink-derived spatial restraints. The web server displays crosslinks in clear schematic representations including circular, bar, and network diagrams with interactive features for topological and functional interpretation.

## Issues and Support

Found a bug or have a feature request? Please submit issues to:
**[https://github.com/Sinz-Lab-CSMS/MeroX/issues](https://github.com/Sinz-Lab-CSMS/MeroX/issues)**

## License

This software is distributed under a freeware license. See the LICENSE file for details.

## Citation

If you use MeroX/StavroX in your research, please cite the appropriate publications:

- [(1) Götze et al. Automated Assignment of MS/MS Cleavable Cross-Links in Protein 3D-Structure Analysis. J Am Soc Mass Spectrom. 2014 Sep; ePub ahead of print.](http://www.ncbi.nlm.nih.gov/pubmed/25261217)

- [(2) Götze et al. StavroX--a software for analyzing crosslinked products in protein interaction studies. J Am Soc Mass Spectrom. 2012 Jan;23(1):76-87.](http://www.ncbi.nlm.nih.gov/pubmed/22038510)

- [(3) Müller et al. Cleavable Cross-Linker for Protein Structure Analysis: Reliable Identification of Cross-Linking Products by Tandem MS. Anal Chem. 2010 Aug;82(16):6958-6968.](http://www.ncbi.nlm.nih.gov/pubmed/20704385)

- [(4) Grimm et al. xVis: a web server for the schematic visualization and interpretation of crosslink-derived spatial restraints. Nucleic Acid Res. 2015 Jul;43(W1):W362-9.](http://www.ncbi.nlm.nih.gov/pubmed/25956653)

- [(5) Iacobucci and Götze et al. A cross-linking/mass spectrometry workflow based on MS-cleavable cross-linkers and the MeroX software for studying protein structures and protein-protein interactions. Nat Protoc. 2018 Dec;13(12):2864-2889.](https://www.ncbi.nlm.nih.gov/pubmed/30382245)

---

*This repository is currently under construction. Complete documentation and source code will be available soon.*
