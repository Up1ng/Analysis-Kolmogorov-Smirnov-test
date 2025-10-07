# Distribution Analysis using Kolmogorov-Smirnov Test

A Python tool for statistical comparison of data distributions using the two-sample Kolmogorov-Smirnov test.

## Project Description

This tool enables you to:
- Load data from CSV files
- Perform statistical analysis of distributions
- Visualize comparison results
- Automatically determine whether samples come from the same distribution

## Quick Start

### Installation Requirements

```bash
pip install numpy pandas scipy matplotlib
```

### Basic Usage

1. **Run the script directly:**
```bash
python kolmogorov_smirnov_analysis.py
```

2. **The program will:**
   - Look for `sample_data.csv` in the current directory
   - If not found, automatically create a demo dataset
   - Perform statistical analysis
   - Generate visualizations
   - Display interpretation of results

## Data Format

### Supported CSV Structure
Your CSV file should contain at least 2 columns with numerical data:

```csv
sample1,sample2,sample3
1.23,4.56,7.89
2.34,5.67,8.90
3.45,6.78,9.01
...
```

### Creating Test Data
You can use the following code to generate test data:

```python
import numpy as np
import pandas as pd

np.random.seed(42)
data = {
    'normal_distribution': np.random.normal(0, 1, 1000),
    'uniform_distribution': np.random.uniform(-3, 3, 1000),
    'exponential_distribution': np.random.exponential(1, 1000)
}
df = pd.DataFrame(data)
df.to_csv('my_data.csv', index=False)
```

## Statistical Methodology

### Kolmogorov-Smirnov Test
- **Null Hypothesis (H0)**: Both samples come from the same distribution
- **Alternative Hypothesis (H1)**: Samples come from different distributions
- **Significance Level**: α = 0.05

### Interpretation
- **p-value < 0.05**: Reject H0 - distributions are significantly different
- **p-value ≥ 0.05**: Fail to reject H0 - no significant difference detected

## Functions Overview

### `load_data_from_csv(filename)`
Loads numerical data from CSV file for analysis.

### `create_demo_csv()`
Generates synthetic demo data with normal and uniform distributions.

### `perform_ks_test(data1, data2, name1, name2)`
Performs the two-sample Kolmogorov-Smirnov test and returns statistics.

### `visualize_distributions(df, columns)`
Creates comprehensive visualizations:
- Distribution histograms
- Box plot comparisons
- Empirical cumulative distribution functions (ECDF)

### `main()`
Orchestrates the complete analysis workflow.

## Output Features

### Statistical Results
- K-S test statistic and p-value
- Sample sizes after cleaning
- Descriptive statistics (mean, std, min, max, quartiles)

### Visualizations
- **Histograms**: Compare distribution shapes
- **Box Plots**: Show quartiles and outliers
- **ECDF Plots**: Display cumulative probabilities

### Automated Analysis
- Automatic column selection
- Multiple comparison handling
- Missing value treatment
- Sample size validation

## Use Cases

### A/B Testing
Compare performance metrics between two groups

### Quality Control
Check if production batches come from the same process

### Scientific Research
Validate similarity of experimental and control groups

### Data Validation
Ensure data consistency across different sources

## Example Output

```
=== KOLMOGOROV-SMIRNOV TEST WITH CSV IMPORT ===

File 'sample_data.csv' successfully loaded
Columns in file: ['normal_sample', 'uniform_sample', 'normal_sample2']
Data size: (1000, 3)

--- Comparison: 'normal_sample' vs 'uniform_sample' ---
Sample size normal_sample: 1000
Sample size uniform_sample: 1000
K-S statistic: 0.1120
P-value: 0.000000

CONCLUSION: Samples come from DIFFERENT distributions
   (p-value < 0.05 - reject null hypothesis)
```

## Important Notes

- Minimum recommended sample size: 10 observations per group
- Missing values are automatically handled
- Results are reproducible with fixed random seed
- Visualizations help interpret statistical findings

## Advanced Usage

### Custom Data Analysis
```python
from your_script import perform_ks_test, visualize_distributions
import pandas as pd

# Load your custom data
df = pd.read_csv('your_data.csv')
stat, pval = perform_ks_test(df['group_A'], df['group_B'], 'Group A', 'Group B')
```

### Multiple Comparisons
The script automatically performs pairwise comparisons when multiple columns are present in the CSV file.

## References

- Kolmogorov-Smirnov test documentation: `scipy.stats.ks_2samp`
- Statistical significance: α = 0.05 standard threshold
- Sample size considerations for statistical power

## Contributing

Feel free to extend functionality:
- Additional statistical tests
- More visualization options
- Data preprocessing features
- Export capabilities

---
