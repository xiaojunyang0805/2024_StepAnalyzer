# Configuration Presets

This directory contains preset configurations for StepAnalyzer v3.

## Available Presets

### default.json
General-purpose configuration suitable for most experiments. Uses moderate parameters that work well across different signal qualities.

**Key Parameters:**
- Filter window: 31
- Threshold: 7e-15 A
- Bounds: [20, 20]
- Quality: R² ≥ 0.90, SNR ≥ 3.0

### low_noise.json
Optimized for the original low-noise experimental setup from the 2022 paper.

**Key Parameters:**
- Filter window: 31 (smaller window preserves detail)
- Threshold: 7e-15 A
- Bounds: [20, 20]
- Quality: R² ≥ 0.92, SNR ≥ 4.0 (stricter criteria)

**Use when:**
- Data has low baseline noise
- Steps are sharp and well-defined
- High temporal resolution is needed

### high_noise.json
Optimized for the second experimental setup with higher noise levels.

**Key Parameters:**
- Filter window: 201 (larger window for heavy smoothing)
- Threshold: 4e-14 A (higher to avoid false positives)
- Bounds: [250, 250] (wider window for fitting)
- Quality: R² ≥ 0.85, SNR ≥ 2.5 (more relaxed)
- Unit conversion: 1e-9 (nA to A)

**Use when:**
- Data has significant noise
- Steps are broader and less sharp
- Raw data is in nanoamperes

## Creating Custom Presets

To create a custom preset:

1. Copy an existing preset file
2. Modify the parameters as needed
3. Save with a descriptive name (e.g., `my_setup.json`)
4. Update the `setup_name` and `description` fields

## Parameter Guidelines

### Filter Parameters

**window_size**: Number of points for Savitzky-Golay filter
- Smaller (11-51): Preserves detail, less smoothing
- Medium (51-101): Balanced
- Larger (101-301): Heavy smoothing for noisy data
- Must be odd number

**polynomial_order**: Typically 3-5
- Lower: More smoothing
- Higher: Preserves features better

### Detection Parameters

**threshold**: Minimum derivative magnitude to detect a step
- Estimate from noise level: ~3-5× noise STD
- Too low: False positives
- Too high: Missed steps

**prominence**: Minimum peak prominence
- Related to expected step size
- Typically 0.1-0.5× typical step height

### Fitting Parameters

**model**:
- `sigmoid_4param`: For stable baselines (L, k, x0, c)
- `sigmoid_5param`: For drifting baselines (L, k, x0, c, d)

**bounds_left/right**: Points to include in fit window
- Should cover entire step transition
- Typical: 2-3× step duration
- Larger for noisy data

### Quality Parameters

**min_r_squared**: Goodness of fit (0-1)
- 0.95+: Excellent fit
- 0.90-0.95: Good fit
- 0.85-0.90: Acceptable for noisy data
- <0.85: Poor fit

**min_snr**: Signal-to-noise ratio
- 5+: Excellent
- 3-5: Good
- 2-3: Acceptable for noisy data
- <2: Poor

## Loading Presets in Code

```python
from src.data import Config

# Load named preset
config = Config.load_preset('low_noise')

# Load custom preset from specific directory
config = Config.load_preset('my_setup', config_dir='path/to/configs')

# Load from specific file
config = Config.load_from_file('path/to/config.json')
```

## Preset Validation

All presets are validated when loaded. Common validation errors:

- Window size must be odd and ≥3
- Polynomial order must be less than window size
- Threshold and prominence must be positive
- R² must be between 0 and 1
- Bounds must be ≥1

Use `config.validate()` to check for errors:

```python
is_valid, errors = config.validate()
if not is_valid:
    print("Configuration errors:", errors)
```
