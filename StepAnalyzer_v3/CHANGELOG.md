# StepAnalyzer v3 - Changelog

## [3.0.0] - 2025-01-15

### Added
- **Complete GUI Application**
  - Modern PyQt5 interface with 4-panel visualization layout
  - Real-time signal display and analysis
  - Interactive step navigation with click-to-select
  - Professional matplotlib-based plots

- **Quality Review Dialog**
  - Full signal overview with all detected steps
  - Interactive quality filtering with R², SNR, and Confidence sliders
  - Real-time marker updates (green = passed, red = filtered)
  - Optimized for fine-tuning quality thresholds

- **Batch Processing**
  - Process multiple files simultaneously
  - Progress tracking with cancellation support
  - Automatic parameter optimization per file
  - Combined statistical analysis across all files
  - Professional Excel export with timestamp

- **Histogram Visualization**
  - Automatic histogram generation in batch exports
  - Gaussian distribution fitting
  - Professional bar chart with red fit curve overlay
  - X-axis formatted to 2 decimal places for clarity
  - Gaussian parameters (μ, σ) displayed

- **Export Features**
  - Excel format with multiple sheets (Summary, individual files, Comparison)
  - CSV format for simple text export
  - JSON format for programmatic access
  - Comprehensive metadata and statistics

- **Configuration Management**
  - Pre-configured presets (Low Noise, High Noise)
  - JSON-based configuration storage
  - Automatic validation
  - Parameter optimization suggestions

### Improved
- Automatic unit detection and conversion (nA to A)
- Enhanced error handling and user feedback
- Optimized signal processing algorithms
- Better memory management for large datasets
- Improved fit quality metrics (R², SNR, confidence)

### Technical Details
- Sigmoid fitting with 4 and 5 parameter models
- Savitzky-Golay filtering for noise reduction
- Adaptive threshold detection
- Statistical outlier detection
- Comprehensive quality metrics

### Documentation
- Complete user guide in README.md
- Installation guide (INSTALL.md)
- Development notes (Dev_note.md)
- Configuration guidelines
- Troubleshooting section

### Dependencies
- Python 3.10+
- numpy >= 1.21.0
- scipy >= 1.7.0
- matplotlib >= 3.4.0
- pandas >= 1.3.0
- PyQt5 >= 5.15.0
- openpyxl >= 3.0.0

---

## [3.0.0-alpha] - 2025-01-13

### Added
- Foundation and data layer (Phase 1)
- Core classes: ExperimentData, Step, StepCollection, Config
- Unit tests and validation framework
- Project structure and architecture

---

## [2.0.0] - 2022

### Added
- High-noise setup support
- Enhanced filtering options
- Additional configuration presets

---

## [1.0.0] - 2022

### Added
- Initial PyQt5 GUI version
- Basic step detection and fitting
- CSV export functionality

---

## [0.1.0] - 2022

### Added
- Original research code from publication
- Basic analysis scripts
- Proof-of-concept implementation

---

## References

Based on research published in:

**Moazzenzade, T.; Walstra, T.; Yang, X.; Huskens, J.; Lemay, S. G.**
"Ring Ultramicroelectrodes for Current-Blockade Particle-Impact Electrochemistry"
*Anal. Chem.* **2022**, 94, 10168–10174.
DOI: [10.1021/acs.analchem.2c01503](https://doi.org/10.1021/acs.analchem.2c01503)
