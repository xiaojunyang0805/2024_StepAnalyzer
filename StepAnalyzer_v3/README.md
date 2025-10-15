# StepAnalyzer v3.0.0

**Standalone Windows Application for Current-Blockade Particle-Impact Electrochemistry Analysis**

---

## Welcome!

Thank you for downloading StepAnalyzer! This is a **ready-to-use application** that requires **no Python installation** or additional software. Simply run `StepAnalyzer.exe` to start analyzing your electrochemical data.

## Quick Start

1. **Launch the Application**
   - Double-click `StepAnalyzer.exe`
   - The main window will open with four visualization panels

2. **Load Your Data**
   - Click **"Load File"** button
   - Select your CSV or TXT data file
   - The signal will be displayed automatically

3. **Analyze**
   - Click **"Detect & Fit Steps"** to run automated analysis
   - Review detected steps in the interactive plots
   - Use **"Quality Review"** to filter results

4. **Export Results**
   - Click **"Export Excel"** for comprehensive Excel reports
   - Batch process multiple files with **"Batch Process"**

See `Quick_Start.txt` for detailed step-by-step instructions with screenshots.

---

## What's Included

- **StepAnalyzer.exe** - Main application (no installation needed)
- **_internal/** - Application dependencies (do not modify)
- **config/** - Pre-configured settings for different experimental setups
- **LICENSE** - MIT License for free academic use
- **CHANGELOG.md** - Version history and updates
- **Quick_Start.txt** - Detailed user guide with examples
- **README.md** - This file

---

## System Requirements

- **Operating System**: Windows 10 or higher (64-bit)
- **RAM**: 4 GB minimum (8 GB recommended)
- **Disk Space**: 500 MB free space
- **Display**: 1920×1080 or higher recommended for best visualization

---

## Key Features

### Interactive Analysis
- **4-Panel Visualization**: Overview, filtered signal, step detail, and histogram
- **Real-Time Detection**: Immediate feedback as you adjust parameters
- **Quality Review Dialog**: Interactive filtering with R², SNR, and confidence sliders
- **Step Navigation**: Click-to-select or browse through detected steps

### Batch Processing
- Process multiple data files simultaneously
- Automatic parameter optimization per file
- Combined statistical analysis across all files
- Professional Excel reports with:
  - Individual file statistics
  - Overall summary with histogram
  - Gaussian fitting of step height distribution
  - Side-by-side file comparison

### Export Options
- **Excel**: Multi-sheet reports with statistics and visualizations
- **CSV**: Simple text format for further analysis
- **JSON**: Structured data for programmatic access

### Pre-Configured Setups
- **Low Noise**: Optimized for clean signals (< 10 pA RMS noise)
- **High Noise**: Optimized for noisy data (> 20 pA RMS noise)

---

## Data File Format

StepAnalyzer accepts CSV or TXT files with time and current data:

```
Time (s), Current (A)
0.0, 8.5e-10
0.001, 8.48e-10
0.002, 8.52e-10
...
```

**Supported formats:**
- Comma, tab, or space-separated values
- Automatic unit detection (converts nA to Amperes if needed)
- Custom column selection in settings

---

## Getting Help

### Documentation
- **Quick_Start.txt** - Detailed usage instructions
- **CHANGELOG.md** - Version history and known issues

### Troubleshooting

**Problem: Application won't start**
- Ensure you're running Windows 10 or higher (64-bit)
- Check Windows Defender/antivirus hasn't blocked the executable
- Try running as administrator

**Problem: No steps detected**
- Threshold may be too high → Use lower threshold value
- Try loading a configuration preset (Low Noise or High Noise)
- Check data file format matches expected columns

**Problem: Too many false detections**
- Threshold may be too low → Use higher threshold value
- Increase quality thresholds using Quality Review dialog
- Adjust R² and SNR thresholds

**Problem: Export fails**
- Ensure you have write permissions to the target folder
- Close any existing Excel files with the same name
- Check available disk space

### Contact & Support

For questions, bug reports, or suggestions:
- **Email**: xiaojunyang0805@gmail.com
- **GitHub Issues**: https://github.com/xiaojunyang0805/2024_StepAnalyzer/issues

---

## Citation

If you use this software in your research, please cite:

**Moazzenzade, T.; Walstra, T.; Yang, X.; Huskens, J.; Lemay, S. G.**
"Ring Ultramicroelectrodes for Current-Blockade Particle-Impact Electrochemistry"
*Anal. Chem.* **2022**, 94, 10168–10174.
DOI: [10.1021/acs.analchem.2c01503](https://doi.org/10.1021/acs.analchem.2c01503)

---

## License

This software is licensed under the MIT License and is **free for academic and research use**.

Researchers worldwide are welcome to use this software for their scientific work. We encourage users to:
- Cite the original publication when using this software in research
- Share ideas and suggestions for improvement
- Contribute to the development of this tool

See `LICENSE` file for full license text.

---

## Version Information

**Version**: 3.0.0
**Release Date**: 2025-01-15
**Status**: Production Ready

**What's New in v3.0.0:**
- ✅ Standalone Windows executable (no Python required)
- ✅ Interactive GUI with 4-panel visualization
- ✅ Batch processing with histogram and Gaussian fitting
- ✅ Quality review dialog with real-time filtering
- ✅ Professional Excel exports with statistical analysis
- ✅ Pre-configured setups for different noise levels

---

## About This Software

StepAnalyzer was developed for the quantitative analysis of current-blockade signals from particle-impact electrochemistry experiments. It automates the detection, fitting, and statistical analysis of step-shaped current transients caused by insulating particles (e.g., polystyrene beads) impacting ultramicroelectrodes.

This free software is provided to the research community to facilitate reproducible electrochemical analysis.

**Developed by**: Xiaojun Yang
**Affiliated Publication**: Moazzenzade et al., Anal. Chem. 2022

---

**Download the latest version**: https://github.com/xiaojunyang0805/2024_StepAnalyzer/releases

**Thank you for using StepAnalyzer!**
