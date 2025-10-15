# StepAnalyzer v3.0.0 - Quick Start Guide

## Table of Contents
1. [Installation](#installation)
2. [Getting Started](#getting-started)
3. [Basic Workflow](#basic-workflow)
4. [Interface Overview](#interface-overview)
5. [Step-by-Step Usage](#step-by-step-usage)
6. [Quality Review](#quality-review)
7. [Batch Processing](#batch-processing)
8. [Export Options](#export-options)
9. [Configuration Presets](#configuration-presets)
10. [Troubleshooting](#troubleshooting)

---

## Installation

### System Requirements
- **Operating System**: Windows 10 or higher (64-bit)
- **RAM**: 4 GB minimum (8 GB recommended)
- **Disk Space**: 500 MB free space
- **Display**: 1920×1080 or higher recommended

### Installation Steps
1. **Extract the Application**
   - Unzip the downloaded file to your preferred location
   - Keep ALL files together in the same folder

2. **Important**: Do NOT move `StepAnalyzer.exe` away from the `_internal` folder!

3. **First Launch**
   - Double-click `StepAnalyzer.exe`
   - Windows may show a security warning for unsigned applications
   - Click "More info" then "Run anyway" if prompted

**No Python installation needed!** This is a standalone application.

---

## Getting Started

### Data File Format

StepAnalyzer accepts CSV or TXT files with time and current data:

```
Time (s), Current (A)
0.0, 8.5e-10
0.001, 8.48e-10
0.002, 8.52e-10
...
```

**Supported formats:**
- Comma-separated (`.csv`)
- Tab-separated (`.txt`)
- Space-separated
- Automatic unit detection (converts nA to Amperes if needed)

---

## Basic Workflow

```
Load File → Detect Steps → Review Quality → Export Results
```

1. **Load** your experimental data file
2. **Detect & Fit** steps automatically
3. **Review** detected steps and filter by quality
4. **Export** results to Excel, CSV, or JSON

---

## Interface Overview

The main window has **4 visualization panels**:

```
┌─────────────────────────────┬─────────────────────────────┐
│  1. Overview Signal         │  2. Filtered Signal         │
│  (Raw data + detected steps)│  (Derivative + peak markers)│
├─────────────────────────────┼─────────────────────────────┤
│  3. Step Detail             │  4. Histogram               │
│  (Selected step + fit curve)│  (Step height distribution) │
└─────────────────────────────┴─────────────────────────────┘
```

### Panel Descriptions

1. **Overview Signal (Top-Left)**
   - Shows the entire raw current signal
   - Green vertical lines mark detected step locations
   - Shaded regions show the fitting window for each step

2. **Filtered Signal (Top-Right)**
   - Shows the derivative (filtered signal) used for detection
   - Red dots mark detected peaks
   - Updates when quality filters are applied

3. **Step Detail (Bottom-Left)**
   - Displays the selected step in detail
   - Blue line: experimental data
   - Red dashed line: fitted sigmoid curve
   - Shows fit quality metrics (R², SNR, Confidence)

4. **Histogram (Bottom-Right)**
   - Shows distribution of all detected step heights
   - Red curve: Gaussian fit
   - Displays mean (μ) and standard deviation (σ)

---

## Step-by-Step Usage

### 1. Load Your Data File

**Method 1: Using the Button**
- Click **"Load File"** button in the toolbar
- Navigate to your data file
- Select a `.csv` or `.txt` file
- Click "Open"

**Method 2: Using the Menu**
- Go to `File → Open`
- Select your data file

**What happens:**
- The raw signal appears in the Overview panel
- File information is displayed in the status bar

---

### 2. Detect & Fit Steps

**Click "Detect & Fit Steps" button**

**What happens:**
1. The software applies Savitzky-Golay filtering
2. Detects peaks in the derivative signal
3. Fits a sigmoid curve to each detected step
4. Calculates quality metrics for each fit
5. All four panels update with results

**Results displayed:**
- Overview: Green markers show detected steps
- Filtered: Red dots show detected peaks
- Histogram: Distribution of step heights
- Status bar: Total number of steps detected

**Tip**: Click on any step in the Overview panel to view its detailed fit in the Step Detail panel.

---

### 3. Navigate Through Steps

**Method 1: Click to Select**
- Click on any green vertical line in the Overview panel
- The Step Detail panel updates to show that step

**Method 2: Use Navigation Buttons**
- Click **"Previous Step" (◄)** or **"Next Step" (►)** buttons
- Browse through all detected steps sequentially

**Step Detail Information:**
- **R²**: Goodness of fit (higher is better, 0-1)
- **SNR**: Signal-to-noise ratio (higher is better)
- **Confidence**: Overall confidence score (0-1)
- **Step Height**: Magnitude of the current change

---

## Quality Review

The Quality Review dialog allows you to filter steps based on quality metrics.

### Opening Quality Review

**Click "Quality Review" button**

**The dialog shows:**
- Full signal overview with all detected steps
- Three sliders for quality thresholds:
  - **R² (Min)**: Minimum R-squared value
  - **SNR (Min)**: Minimum signal-to-noise ratio
  - **Confidence (Min)**: Minimum confidence score
- Real-time marker color updates:
  - **Green**: Step passes all thresholds
  - **Red**: Step fails at least one threshold

---

### Using Quality Filters

**Step-by-step:**

1. **Open Quality Review**
   - Click "Quality Review" button

2. **Adjust Thresholds**
   - Move the **R² slider** (range: 0.00 - 1.00)
     - Recommended: 0.85 - 0.95 for good fits
   - Move the **SNR slider** (range: 0.0 - 20.0)
     - Recommended: 3.0 - 5.0 for clean signals
   - Move the **Confidence slider** (range: 0.00 - 1.00)
     - Recommended: 0.60 - 0.90

3. **Observe Real-Time Updates**
   - Watch markers change color as you adjust sliders
   - Green markers = steps that pass your criteria
   - Red markers = steps that are filtered out

4. **Review Statistics**
   - Top of dialog shows: "X of Y steps pass quality criteria"

5. **Apply Filters**
   - Click **"Apply & Close"** to accept the filtered results
   - OR click **"Cancel"** to discard changes

**What happens after "Apply & Close":**
- All four main window panels update
- Only filtered steps are shown
- Histogram updates with filtered data
- Threshold values are saved for next time

**Tip**: The software remembers your threshold values. When you reopen Quality Review, it shows your last-used settings.

---

### Quality Metrics Explained

**R² (R-Squared)**
- Measures how well the sigmoid curve fits the data
- Range: 0 to 1
- **0.90+**: Excellent fit
- **0.80-0.90**: Good fit
- **< 0.80**: Poor fit (consider filtering)

**SNR (Signal-to-Noise Ratio)**
- Measures step clarity relative to noise
- Higher values = cleaner, more distinct steps
- **> 5.0**: Very clear step
- **3.0-5.0**: Good step
- **< 3.0**: Noisy or unclear (may be artifact)

**Confidence**
- Combined metric considering multiple quality factors
- Range: 0 to 1
- **> 0.80**: High confidence
- **0.60-0.80**: Moderate confidence
- **< 0.60**: Low confidence (likely false detection)

---

## Batch Processing

Process multiple data files simultaneously with automatic parameter optimization.

### Starting Batch Processing

1. **Click "Batch Process" button**

2. **Select Files**
   - Multi-select your data files (Ctrl+Click or Shift+Click)
   - Click "Open"

3. **Choose Export Location**
   - Select a folder for the combined results
   - Enter a base filename (e.g., "experiment_2025")

4. **Monitor Progress**
   - Progress bar shows overall completion
   - Current file being processed is displayed
   - Click "Cancel" to abort if needed

---

### Batch Processing Outputs

**Excel File** (recommended for most users)
- **Summary Sheet**: Combined statistics across all files
  - Total steps detected per file
  - Mean step height per file
  - Standard deviation per file
  - Gaussian fit parameters (μ, σ) for combined data
  - **Histogram visualization** with Gaussian fit curve

- **Individual File Sheets**: Detailed results for each file
  - Step number
  - Step height
  - R², SNR, Confidence values
  - Fit parameters

- **Comparison Sheet**: Side-by-side file comparison
  - Easy to compare experimental conditions
  - Statistical summary for each file

**Histogram Visualization**
- Professional bar chart showing step height distribution
- Red curve: Gaussian fit overlay
- X-axis: Step height (formatted to 2 decimal places)
- Y-axis: Frequency (count)
- Gaussian parameters (μ, σ) displayed on chart

---

### When to Use Batch Processing

**Use batch processing when:**
- You have multiple experimental replicates
- You want to compare different conditions
- You need combined statistical analysis
- You want automatic histogram generation with Gaussian fitting

**Tips:**
- Ensure all files use the same experimental setup
- Use consistent file naming for easy identification
- Check individual file results before combining

---

## Export Options

### Single File Export

After analyzing a file, you can export in three formats:

**1. Excel Export** (Recommended)
- Click **"Export Excel"** button
- Contains:
  - File metadata (name, date, parameters)
  - Summary statistics
  - Detailed step list with all metrics
  - Configuration parameters used

**2. CSV Export**
- Click **"Export CSV"** button
- Simple text format
- Columns: Step Number, Step Height, R², SNR, Confidence, etc.
- Easy to import into other software

**3. JSON Export**
- Click **"Export JSON"** button
- Structured data format
- Complete analysis results
- Ideal for programmatic access or custom scripts

---

### What's Included in Exports

**Metadata:**
- File name and path
- Analysis date and time
- StepAnalyzer version
- Configuration parameters used

**Step Data:**
- Step number
- Step height (Amperes)
- Peak index (location in data)
- Fit quality metrics (R², SNR, RMSE, Confidence)
- Sigmoid fit parameters (amplitude, midpoint, slope, etc.)

**Summary Statistics:**
- Total steps detected
- Mean step height
- Standard deviation
- Median, min, max values
- Coefficient of variation (CV%)

---

## Configuration Presets

StepAnalyzer includes pre-configured settings for different experimental conditions.

### Available Presets

**1. Default**
- General-purpose settings
- Moderate noise tolerance
- Good starting point for most experiments

**2. Low Noise**
- Optimized for clean signals (< 10 pA RMS noise)
- More sensitive detection
- Stricter quality criteria
- **Use when**: Your signal is very clean with minimal baseline fluctuation

**3. High Noise**
- Optimized for noisy data (> 20 pA RMS noise)
- Less sensitive to avoid false detections
- Relaxed quality criteria
- **Use when**: Your signal has significant baseline noise or drift

---

### Loading a Preset

**Method 1: Using the Menu**
1. Go to `Settings → Load Configuration`
2. Navigate to the `config` folder
3. Select a preset file (e.g., `low_noise.json`)
4. Click "Open"

**Method 2: Using Configuration Dialog**
1. Go to `Settings → Configure Parameters`
2. Click "Load Preset"
3. Select preset name from dropdown
4. Click "Apply"

**What happens:**
- All detection, filtering, and quality parameters update
- The new parameters take effect for the next "Detect & Fit Steps" operation
- You can re-analyze the current file with new parameters

---

### Custom Configuration

**Advanced users can customize parameters:**

1. **Go to `Settings → Configure Parameters`**

2. **Adjust Parameter Groups:**

   **Filter Settings:**
   - Window Size: Savitzky-Golay filter window (must be odd)
   - Polynomial Order: Smoothing polynomial degree
   - Derivative Order: Order of derivative for peak detection

   **Detection Settings:**
   - Threshold: Minimum peak height in derivative
   - Prominence: Minimum peak prominence
   - Min Peak Distance: Minimum samples between peaks

   **Fitting Settings:**
   - Model: 4-parameter or 5-parameter sigmoid
   - Bounds Left/Right: Window size around peak for fitting
   - Max Iterations: Maximum fitting iterations

   **Quality Settings:**
   - Min R²: Minimum R-squared threshold
   - Min SNR: Minimum signal-to-noise ratio
   - Max RMSE Ratio: Maximum root-mean-square error ratio
   - Min Confidence: Minimum overall confidence

3. **Save Custom Configuration**
   - Click "Save Configuration"
   - Enter a name for your custom preset
   - File is saved in `config` folder

---

## Troubleshooting

### Application Won't Start

**Problem**: Double-clicking `StepAnalyzer.exe` does nothing

**Solutions:**
- Ensure you're running Windows 10 or higher (64-bit)
- Check Windows Defender hasn't blocked the executable
  - Go to Windows Security → Virus & threat protection → Protection history
  - If blocked, click "Allow on device"
- Try running as administrator:
  - Right-click `StepAnalyzer.exe` → Run as administrator
- Check system requirements (4 GB RAM minimum)

---

### No Steps Detected

**Problem**: "Detect & Fit Steps" finds 0 steps

**Possible causes and solutions:**

1. **Threshold too high**
   - Load "Low Noise" preset for more sensitive detection
   - OR manually decrease threshold in `Settings → Configure Parameters`

2. **Wrong data format**
   - Check file has two columns: Time, Current
   - Verify units (software expects Amperes)
   - Check for header row (should be plain text, not special characters)

3. **No actual steps in data**
   - Visually inspect the Overview panel
   - Verify experimental data quality

---

### Too Many False Detections

**Problem**: Many detected steps are noise artifacts

**Solutions:**

1. **Use Quality Review to filter**
   - Click "Quality Review"
   - Increase R² threshold (try 0.90 or higher)
   - Increase Confidence threshold (try 0.70 or higher)
   - Click "Apply & Close"

2. **Increase detection threshold**
   - Load "High Noise" preset
   - OR manually increase threshold in `Settings → Configure Parameters`

3. **Adjust minimum peak distance**
   - Go to `Settings → Configure Parameters`
   - Increase "Min Peak Distance" to avoid detecting closely-spaced noise

---

### Poor Fit Quality

**Problem**: Sigmoid curves don't match step shapes well

**Solutions:**

1. **Adjust fitting window**
   - Go to `Settings → Configure Parameters`
   - Increase "Bounds Left" and "Bounds Right" for wider fitting window
   - OR decrease for narrower window if steps are very sharp

2. **Try different sigmoid model**
   - 4-parameter model: Simpler, faster
   - 5-parameter model: More flexible, better for asymmetric steps

3. **Check data quality**
   - Verify sufficient data points around each step
   - Check for baseline drift or noise

---

### Export Fails

**Problem**: Cannot save Excel/CSV/JSON file

**Solutions:**

1. **Check file permissions**
   - Ensure you have write permissions to target folder
   - Try saving to a different location (e.g., Desktop)

2. **Close existing files**
   - Close any Excel files with the same name
   - File may be locked by another program

3. **Check disk space**
   - Verify sufficient free disk space
   - Large batch exports may require significant space

---

### Application Crashes or Freezes

**Problem**: Software becomes unresponsive

**Solutions:**

1. **For large files (> 1 million points)**
   - Processing may take time - wait patiently
   - Consider downsampling data before import

2. **Memory issues**
   - Close other applications to free RAM
   - Restart StepAnalyzer
   - Process files individually instead of batch

3. **Report the issue**
   - Note what you were doing when crash occurred
   - Email: xiaojunyang0805@gmail.com
   - GitHub Issues: https://github.com/xiaojunyang0805/2024_StepAnalyzer/issues

---

## Tips & Best Practices

### For Best Results

1. **Start with presets**
   - Use "Low Noise" or "High Noise" as starting point
   - Fine-tune parameters only if needed

2. **Always use Quality Review**
   - Even with good detection, filtering improves accuracy
   - Recommended thresholds: R² > 0.85, Confidence > 0.60

3. **Visually inspect steps**
   - Click through steps to verify fit quality
   - Check for systematic issues (baseline drift, saturation)

4. **Use batch processing for experiments**
   - Combine replicates for statistical analysis
   - Automatic histogram with Gaussian fitting

5. **Save configurations**
   - Once you find good parameters for your setup, save as custom preset
   - Reuse for consistent analysis

---

## Getting Help

### Documentation
- **README.md** (in root folder): Overview and features
- **CHANGELOG.md** (in root folder): Version history
- **LICENSE** (in root folder): MIT License information

### Support
- **Email**: xiaojunyang0805@gmail.com
- **GitHub Issues**: https://github.com/xiaojunyang0805/2024_StepAnalyzer/issues

### Citation

If you use this software in your research, please cite:

**Moazzenzade, T.; Walstra, T.; Yang, X.; Huskens, J.; Lemay, S. G.**
"Ring Ultramicroelectrodes for Current-Blockade Particle-Impact Electrochemistry"
*Anal. Chem.* **2022**, 94, 10168–10174.
DOI: [10.1021/acs.analchem.2c01503](https://doi.org/10.1021/acs.analchem.2c01503)

---

**Thank you for using StepAnalyzer v3.0.0!**

*Developed by Xiaojun Yang*
*Free for academic and research use under MIT License*
