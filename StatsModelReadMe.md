# CRJA Statistical Analysis Toolkit

**Statistical analysis toolkit for California Racial Justice Act (CRJA) litigation**

Developed as part of UC Davis MSBA Practicum with [Redo.io](https://redo.io)

---

## 🎯 What This Does

This toolkit provides **multiple linear regression analysis** to detect racial disparities in California criminal sentencing. The analysis tests whether Black and Hispanic defendants receive longer sentences than White defendants after controlling for legally relevant factors like offense severity, criminal history, and suitability scores.

All analyses are designed to meet CRJA evidentiary standards and produce defensible results for legal filings.

---

## 📊 Example Results

```
Multiple Linear Regression Results:
Black defendants receive +12.4 months longer sentences (p<0.001) 
compared to similarly situated White defendants, controlling for 
suitability score, offense severity, and county.

R² = 0.42
N = 12,345 defendants
95% CI: [8.9, 15.9]
```

---

## 🚀 Quick Start

```bash
# 1. Clone repository
git clone https://github.com/YOUR_ORG/crja-statistical-analysis.git
cd crja-statistical-analysis

# 2. Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Clone Redo.io population_metrics tool
cd external_repos
git clone https://github.com/redoio/population_metrics.git
cd ..

# 5. Configure and run analysis
cd scripts
python 01_configure_population_metrics.py --source github --auto

cd ../external_repos/population_metrics
python run.py --out ../../outputs/population_metrics.csv

cd ../../notebooks
jupyter notebook
# Open: 03_prepare_regression_data.ipynb → Run all cells
# Open: 04_multiple_linear_regression.ipynb → Run all cells
```

---

## 📁 Project Structure

```
crja-statistical-analysis/
│
├── notebooks/
│   ├── 03_prepare_regression_data.ipynb       # Data merging & cleaning
│   └── 04_multiple_linear_regression.ipynb    # Main analysis
│
├── scripts/
│   ├── 01_configure_population_metrics.py     # Configure suitability scoring
│   └── update_penal_codes.py                  # Clean offense codes
│
├── data/                                       # Raw CDCR data files
│
├── outputs/                                    # Analysis results
│   ├── regression_analysis_data.csv
│   ├── population_metrics.csv
│   └── figures/
│
├── external_repos/
│   └── population_metrics/                    # Redo.io's suitability scoring tool
│
└── requirements.txt
```

---

## 📖 Analysis Workflow

### Step 1: Prepare Data
**Notebook:** `03_prepare_regression_data.ipynb`
- Merges demographics, current/prior commitments, and suitability scores
- Cleans missing values and outliers
- Creates derived variables (race indicators, offense categories)
- **Output:** `outputs/regression_analysis_data.csv`

### Step 2: Multiple Linear Regression
**Notebook:** `04_multiple_linear_regression.ipynb`
- Tests racial disparities in sentence length
- Controls for legally relevant factors
- Generates court-ready interpretations
- **Output:** Regression tables, diagnostic plots, plain-English findings

---

## 🔬 Statistical Method

### Multiple Linear Regression

**Research Question:**  
*Do Black defendants receive longer sentences than White defendants with similar offense profiles and suitability scores?*

**Model:**
```
Sentence = β₀ + β₁(Black) + β₂(Hispanic) + β₃(Suitability) + β₄(Offense_Severity) + β₅(County) + ε
```

**Interpretation:**
- **β₁ coefficient** = Additional months for Black defendants vs White defendants
- **p-value** = Statistical significance (p < 0.05 = significant)
- **R²** = Proportion of variance explained by model

**Example Finding:**
```
Black defendants receive +12.4 months longer sentences (SE=1.8, p<0.001)
after controlling for suitability score, offense severity, and county.
This constitutes evidence of racial disparity under the CRJA.
```

---

## 💾 Data Sources

### Option 1: GitHub Data (Recommended)
Scripts and notebooks are configured to use Redo.io's public datasets:
```python
demographics_url = "https://raw.githubusercontent.com/redoio/resentencing_data_initiative/main/data/demographics.csv"
df = pd.read_csv(demographics_url)
```

### Option 2: Local CDCR Data
Place your California Department of Corrections data files in `data/` directory:
- `demographics.csv` - Ethnicity, sentence length, county
- `current_commitments.csv` - Current offenses
- `prior_commitments.csv` - Criminal history
- `selection_criteria.xlsx` - Offense severity classifications (Tables A-F)

---

## 🛠️ Key Technologies

- **pandas** - Data manipulation and analysis
- **statsmodels** - Multiple linear regression (OLS)
- **matplotlib/seaborn** - Visualization
- **Jupyter** - Interactive analysis notebooks

---

## 📊 Expected Runtime

| Task | Duration |
|------|----------|
| Data preparation (Step 1) | 5-10 minutes |
| Multiple linear regression (Step 2) | 2-5 minutes |
| **Total** | **7-15 minutes** |

---

## 🤝 Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Submit a pull request with clear description of changes

---

## 📜 License

This project is licensed under the MIT License.

---

## 🙏 Acknowledgments

- **[Redo.io](https://redo.io)** - Population metrics tool and partnership
- **UC Davis MSBA Program** - Project support and guidance
- **CDCR** - Data access via California Public Records Act

---

## 📧 Questions?

Open an issue on GitHub for technical questions or bug reports.

---

**Version:** 1.0.0  
**Last Updated:** November 2024
