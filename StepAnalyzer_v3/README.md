# StepAnalyzer v3

**Modern software for quantitative analysis of current-blockade particle-impact electrochemistry**

## Overview

StepAnalyzer v3 analyzes electrochemical step signals from particle collisions on ultramicroelectrodes (UMEs). Detects, fits, and quantifies current steps caused by insulating particles (e.g., 1 μm polystyrene beads) impacting disk or ring electrodes.

### Key Features

- **Interactive GUI**: Modern PyQt5 interface with real-time signal visualization
- **Automated Analysis**: Intelligent peak detection and sigmoid curve fitting with quality scoring
- **Quality Review**: Interactive filtering with R², SNR, and confidence sliders
- **Batch Processing**: Process multiple files with combined statistical analysis
- **Histogram Visualization**: Automatic Gaussian fitting and distribution analysis in Excel exports
- **Multi-Setup Support**: Pre-configured for low-noise and high-noise experimental setups
- **Flexible Export**: CSV, Excel, JSON formats with comprehensive metadata
- **Statistical Tools**: Distribution analysis, outlier detection, quality filtering
- **Professional Output**: Publication-ready data with full reproducibility tracking



## Installation

### Requirements

- Python 3.10 or higher
- See `requirements.txt` for package dependencies

### Setup

```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

## Quick Start

### Launching the GUI Application

```bash
# Navigate to the project directory
cd StepAnalyzer_v3

# Launch the GUI
python step_analyzer.py
```

The application window will open with four main visualization panels and a control panel on the right.

## User Guide

### Main Interface Overview

The StepAnalyzer GUI consists of:

**Four Visualization Panels:**
1. **Overview Plot** (Top Left): Full signal with detected step markers
2. **Filtered Signal** (Top Right): Processed signal after smoothing and filtering
3. **Step Detail** (Bottom Left): Zoomed view of selected step with fit curve
4. **Histogram** (Bottom Right): Distribution of step heights with statistics

**Control Panel** (Right Side):
- File loading and data display
- Detection and fitting parameters
- Analysis controls
- Export options
- Batch processing

### Single File Analysis Workflow

#### 1. Load Data File

1. Click **"Load File"** button
2. Select your CSV/TXT data file
3. The raw signal will be displayed in the Overview plot
4. File information appears in the control panel

**Supported file formats:**
- CSV files with time and current columns
- Automatic unit detection (converts nA to Amperes if needed)
- Handles various delimiters (comma, tab, space)

#### 2. Configure Analysis Parameters

**Detection Parameters:**
- **Filter Window**: Smoothing window size (31 for low noise, 201 for high noise)
- **Threshold**: Minimum step height to detect (in Amperes)
- **Bounds**: Window size around detected peaks for fitting

**Fitting Parameters:**
- **Model**: 4-parameter or 5-parameter sigmoid
- **Max Iterations**: Maximum fitting iterations
- **Tolerance**: Convergence criterion

**Quality Thresholds:**
- **R² Minimum**: Goodness of fit threshold (0.95 recommended)
- **SNR Minimum**: Signal-to-noise ratio threshold (5.0 recommended)
- **Confidence**: Fit parameter confidence level (0.80 recommended)

**Tip:** Use configuration presets:
- "Low Noise" for clean signals
- "High Noise" for noisy data

#### 3. Detect and Fit Steps

1. Click **"Detect & Fit Steps"** button
2. The analysis will:
   - Apply Savitzky-Golay filter to smooth the signal
   - Detect step peaks using threshold-based detection
   - Fit sigmoid curves to each detected step
   - Calculate quality metrics (R², SNR, confidence)
   - Display results in all four panels

**Overview Plot:** Shows all detected steps as vertical markers
**Filtered Signal:** Shows the smoothed signal used for detection
**Histogram:** Shows distribution of step heights with Gaussian fit

#### 4. Review Individual Steps

1. Click on any step in the overview plot, OR
2. Use **"Previous Step"** / **"Next Step"** buttons to navigate
3. The **Step Detail** panel shows:
   - Raw data points (blue)
   - Fitted sigmoid curve (red)
   - Baseline level (green dashed line)
   - Step parameters and quality metrics

#### 5. Quality Review and Filtering

1. Click **"Quality Review"** button to open the review dialog
2. The Quality Review dialog shows:
   - Full signal overview with all detected steps
   - Green markers: Steps passing quality thresholds
   - Red markers: Steps filtered out by thresholds

3. Adjust quality thresholds using sliders:
   - **R² Threshold**: Drag to change minimum R² value
   - **SNR Threshold**: Drag to change minimum SNR value
   - **Confidence Threshold**: Drag to change minimum confidence

4. Step markers update in real-time as you adjust sliders
5. Use this to optimize quality filtering for your data
6. Click **"Close"** when satisfied with the filtering

#### 6. Export Results

**Single File Export:**
1. Click **"Export Excel"** button
2. Choose save location
3. Excel file contains:
   - **Steps Sheet**: All detected steps with parameters and metrics
   - **Statistics Sheet**: Summary statistics and distributions

**CSV Export:** Available via menu for simple text format

**Excel Export Includes:**
- Step ID, time, baseline current
- Fit parameters (L, k, x0, c, d)
- Quality metrics (R², SNR, confidence, RMSE)
- Step height and relative size
- All values in both SI units and pA for convenience

### Batch Processing Workflow

Process multiple data files at once with combined statistical analysis.

#### 1. Start Batch Processing

1. Click **"Batch Process"** button
2. A file selection dialog opens
3. Select multiple CSV/TXT files (use Ctrl+Click or Shift+Click)
4. Click "Open"

#### 2. Processing Progress

- Progress dialog shows:
  - Current file being processed (X of Y)
  - Filename currently processing
  - "Cancel" button to stop processing

#### 3. Batch Results

After processing completes, a summary dialog shows:
- Total files processed
- Successful files
- Failed files (with error messages if any)
- Total steps detected across all files
- Overall mean and std of step heights
- Total processing time

#### 4. Batch Export

The batch results are automatically exported to Excel with timestamp:
- **Filename format:** `batch_results_YYYYMMDD_HHMMSS.xlsx`

**Summary Sheet includes:**
1. **Overall Statistics Table:**
   - Created timestamp
   - Total files, successful, failed
   - Total steps detected
   - Mean step height (pA)
   - Std step height (pA)
   - Total processing time

2. **Individual File Results Table:**
   - File name
   - Status (Success/Failed)
   - Number of steps detected
   - Mean height (pA)
   - Std height (pA)
   - Mean baseline (pA)
   - Processing time (seconds)

3. **Histogram with Gaussian Fit:**
   - Professional bar chart visualization
   - X-axis: Step height (pA) with 2 decimal places
   - Y-axis: Count
   - Blue bars: Histogram of all step heights
   - Red smooth curve: Gaussian fit overlay
   - Gaussian parameters displayed: μ (mean), σ (std)

4. **Raw Data Table:**
   - Bin centers (pA)
   - Count per bin
   - Gaussian fit values

**Additional Sheets:**
- Individual sheet for each successfully processed file
- **Comparison Sheet**: Side-by-side comparison of all files (if 2+ successful)

### Tips and Best Practices

#### Parameter Optimization

**For Low-Noise Data (< 10 pA RMS noise):**
- Filter window: 31-51
- Threshold: 5-10 pA (5e-12 to 1e-11 A)
- Bounds: [20, 20]
- R² threshold: 0.95 or higher

**For High-Noise Data (> 20 pA RMS noise):**
- Filter window: 101-201 (heavier smoothing)
- Threshold: 20-50 pA (2e-11 to 5e-11 A)
- Bounds: [150, 250]
- R² threshold: 0.90 (more relaxed)

**Auto-Optimization:**
- Batch processing includes automatic parameter optimization
- Each file is analyzed to estimate optimal parameters
- Uses baseline noise and signal characteristics

#### Troubleshooting

**No steps detected:**
- Threshold too high → Decrease threshold value
- Filter window too large → Decrease filter window
- Data unit issue → Check if data needs unit conversion (nA to A)

**Too many false positives:**
- Threshold too low → Increase threshold value
- Increase quality thresholds (R², SNR)
- Use Quality Review dialog to filter interactively

**Poor fit quality:**
- Bounds too small → Increase bounds values
- Wrong model → Try 5-parameter model
- Increase max iterations for complex signals

**Batch processing fails:**
- Check all files have consistent format
- Verify column indices are correct
- Check error messages in results dialog for specific file issues

### Loading Data (Programmatic API)

```python
from src.data import ExperimentData

# Load from CSV file
data = ExperimentData.load_from_file(
    'your_data.csv',
    time_col=0,
    current_col=1,
    skip_rows=1,
    unit_conversion=1e-9  # If data is in nA
)

# Get data summary
print(data.get_summary())
```

### Using Configuration Presets

```python
from src.data import Config

# Load preset for low-noise setup
config = Config.load_preset('low_noise')

# Or for high-noise setup
config = Config.load_preset('high_noise')

# View configuration
print(config.get_summary())

# Validate configuration
is_valid, errors = config.validate()
if not is_valid:
    print("Errors:", errors)
```

### Working with Steps

```python
from src.data import Step, StepCollection
import numpy as np

# Create a step (normally done by detector)
step = Step(
    step_id=1,
    peak_index=500,
    time_center=5.0,
    time_window=np.linspace(4.9, 5.1, 100),
    current_window=np.random.randn(100) * 1e-12,
    baseline_current=850e-12
)

# Calculate quality metrics
step.calculate_all_metrics(noise_level=1e-13)

# Create collection
collection = StepCollection()
collection.add_step(step)

# Get statistics
stats = collection.get_statistics()
print(f"Mean step height: {stats['step_height']['mean']:.3e} A")

# Export results
collection.export_csv('results.csv')
collection.export_excel('results.xlsx')
```

## Configuration Presets

### Low Noise Setup
Optimized for clean signals with low baseline noise (original paper setup).
- Filter window: 31
- Threshold: 7e-15 A
- Bounds: [20, 20]
- Stricter quality criteria

### High Noise Setup
Optimized for noisy signals (second experimental setup).
- Filter window: 201 (heavy smoothing)
- Threshold: 4e-14 A
- Bounds: [250, 250]
- More relaxed quality criteria
- Includes nA to A conversion

See `config/README.md` for detailed parameter guidelines.

## Current Status

**Version:** 3.0.0
**Status:** Complete - Production Ready

**Completed Features:**
- ✅ Phase 1: Foundation and Data Layer
- ✅ Phase 2: Signal Processing Engine
- ✅ Phase 3: Interactive PyQt5 GUI
- ✅ Phase 4: Enhanced Features (Quality Review Dialog, Batch Processing with Histogram)

See `Dev_note.md` for detailed development timeline and technical notes.

## API Documentation

### Main Classes

**`ExperimentData`** - Raw data container
- Load from CSV/TXT files with flexible column mapping
- Automatic noise and drift estimation
- Unit conversion support (e.g., nA → A)

**`Step`** - Individual step event
- Stores fit parameters and quality metrics
- Supports 4 & 5 parameter sigmoid models
- Classification: single, double, multi-particle

**`StepCollection`** - Collection with analysis
- Statistical summaries and distributions
- Quality filtering and outlier detection
- Export to multiple formats

**`Config`** - Parameter management
- Load/save presets (JSON)
- Hierarchical configuration structure
- Automatic validation

See docstrings in source code for detailed API reference.

## Testing

```bash
# Run all tests
pytest tests/ -v

# With coverage report
pytest tests/ --cov=src --cov-report=html
```

## Development

See `Dev_note.md` for:
- Development timeline and milestones
- Technical decisions and rationale
- Architecture details
- Performance metrics
- Future enhancement plans

## References

**Original Paper:**
Moazzenzade, T.; Walstra, T.; Yang, X.; Huskens, J.; Lemay, S. G.
"Ring Ultramicroelectrodes for Current-Blockade Particle-Impact Electrochemistry"
*Anal. Chem.* **2022**, 94, 10168–10174.
DOI: [10.1021/acs.analchem.2c01503](https://doi.org/10.1021/acs.analchem.2c01503)

## License

[To be determined]

## Version History

- **v3.0.0** (2025-01-15): Production release
  - Complete GUI application with 4-panel visualization
  - Interactive Quality Review dialog with real-time filtering
  - Batch processing with histogram and Gaussian fitting
  - Auto-optimization for detection parameters
  - Professional Excel exports with statistical analysis
- **v3.0.0-alpha** (2025-01-13): Phase 1 complete - Foundation and data layer
- **v2.0** (2022): High-noise setup support
- **v1.0** (2022): PyQt5 GUI version
- **v0.1** (2022): Original research code from paper
