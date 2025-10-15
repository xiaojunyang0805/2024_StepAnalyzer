# StepAnalyzer

**Quantitative analysis software for current-blockade particle-impact electrochemistry**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)

## Overview

StepAnalyzer is a comprehensive analysis tool for electrochemical step signals from particle collisions on ultramicroelectrodes (UMEs). It automates the detection, fitting, and quantification of current steps caused by insulating particles (e.g., polystyrene beads) impacting disk or ring electrodes.

### Key Features

- **Standalone Windows Application** - No Python installation required
- **Interactive GUI** - Modern PyQt5 interface with real-time visualization
- **Automated Analysis** - Intelligent step detection and sigmoid curve fitting
- **Quality Control** - Interactive review with adjustable quality thresholds
- **Batch Processing** - Process multiple files with combined statistical analysis
- **Professional Reporting** - Excel exports with histogram and Gaussian fitting
- **Configuration Presets** - Pre-configured for low-noise and high-noise setups

## Quick Start

### For Windows Users (No Python Required)

1. Download the latest release from the [Releases](https://github.com/xiaojunyang0805/2024_StepAnalyzer/releases) page
2. Extract the `StepAnalyzer_v3.zip` file
3. Double-click `StepAnalyzer.exe`
4. Start analyzing your data!

See `StepAnalyzer_v3/Quick_Start.txt` for detailed instructions.


**Note:** The `Script/` folder contains development code and is not included in public releases.

## Features

### Interactive Analysis

- **4-Panel Visualization**: Overview, filtered signal, step detail, and histogram
- **Real-time Detection**: Immediate feedback as you adjust parameters
- **Quality Review**: Interactive filtering with R², SNR, and confidence sliders
- **Step Navigation**: Click-to-select or browse through detected steps

### Batch Processing

- Process multiple data files simultaneously
- Automatic parameter optimization per file
- Combined statistical analysis across all files
- Professional Excel reports with:
  - Individual file statistics
  - Overall summary
  - Histogram with Gaussian fitting
  - Side-by-side comparison

### Export Formats

- **Excel**: Multi-sheet reports with statistics and visualizations
- **CSV**: Simple text format for further analysis
- **JSON**: Structured data for programmatic access

## System Requirements

### Standalone Application
- Windows 10 or higher (64-bit)
- 4 GB RAM minimum (8 GB recommended)
- 500 MB free disk space
- Display: 1920×1080 or higher recommended

### Python Version (Developers)
- Python 3.10 or higher
- Required packages listed in `requirements.txt`

## Documentation

- **User Guide**: See `StepAnalyzer_v3/README.md`
- **Quick Start**: See `StepAnalyzer_v3/Quick_Start.txt`
- **Example Data**: Available in `TestData/` folder
- **Scientific Paper**: See `SciPaper/` folder

## Citation

If you use this software in your research, please cite:

**Moazzenzade, T.; Walstra, T.; Yang, X.; Huskens, J.; Lemay, S. G.**
"Ring Ultramicroelectrodes for Current-Blockade Particle-Impact Electrochemistry"
*Anal. Chem.* **2022**, 94, 10168–10174.
DOI: [10.1021/acs.analchem.2c01503](https://doi.org/10.1021/acs.analchem.2c01503)

## License

This project is licensed under the MIT License - see the [LICENSE](StepAnalyzer_v3/LICENSE) file for details.

## Version

**Current Release**: v3.0.0 (2025-01-15)

Complete production-ready application with:
- ✅ Interactive GUI
- ✅ Batch processing
- ✅ Quality review dialog
- ✅ Histogram with Gaussian fitting
- ✅ Standalone Windows executable

## Contact & Support

This is free software for academic and research applications. Researchers worldwide are welcome to use it and share ideas.

**For questions, suggestions, or collaboration:**
- 📧 Email: xiaojunyang0805@gmail.com
- 🐛 Issues: [GitHub Issues](https://github.com/xiaojunyang0805/2024_StepAnalyzer/issues)

## Acknowledgments

This software was developed for the analysis of particle-impact electrochemistry experiments as described in the original publication (see Citation above).

---

**Download the latest release to get started!**
