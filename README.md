# Criminal Commitments Statistical Analysis

Statistical analysis of criminal commitments data, examining patterns in offenses, sentencing, time served, enhancements, and recidivism.

## Project Overview

This project contains two analyses:

### 1. Prior Commitments Analysis
Analysis of historical criminal commitments including:
- Descriptive Statistics
- Categorical Analysis (offense types, relationships)
- Time-Based Analysis (time served calculations)
- Statistical Tests (Chi-square, t-tests, correlation, Kruskal-Wallis)
- Recidivism Analysis

### 2. Current Commitments Analysis
Analysis of current criminal commitments including:
- Descriptive Statistics
- Categorical Analysis
- Time-Based Analysis
- **Enhancement Analysis** (sentence enhancements)
- Statistical Tests (Chi-square, t-tests, correlation, Kruskal-Wallis)
- Current Commitment Patterns

## Project Structure

```
prior_commitments_analysis/
├── README.md                 # This file
├── requirements.txt          # Python dependencies
├── .gitignore               # Git ignore rules
├── data/
│   ├── prior_commitments.csv     # Prior commitments dataset
│   └── currentcommits.xlsx       # Current commitments dataset (add manually - >30MB)
└── notebooks/
    ├── prior_commitments_analysis.ipynb    # Prior commitments analysis
    └── current_commitments_analysis.ipynb  # Current commitments analysis
```

## Setup Instructions

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd prior_commitments_analysis
```

### 2. Create Virtual Environment (Recommended)

```bash
# Create virtual environment
python -m venv venv

# Activate it
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Add Your Data

- `prior_commitments.csv` is included in the repo
- **Add `currentcommits.xlsx` manually** to the `data/` folder (file too large for GitHub)

### 5. Run the Notebooks

```bash
# Start Jupyter
jupyter notebook

# Navigate to notebooks/ folder and open desired notebook
```

## Data Overview

**Dataset**: `prior_commitments.csv`  
**Records**: 191,436  
**Unique Individuals**: 43,498  

### Data Dictionary

| Column | Description | Example |
|--------|-------------|---------|
| `cdcno` | Anonymized unique identifier for individuals | `2cf2a233c4` |
| `sentencing county` | County where sentencing occurred (59 unique) | `Los Angeles`, `San Diego` |
| `case number` | Court case number | `KA048775` |
| `sentence from abstract of judgement` | Sentence length from court documents | `1 Years 4 Months` |
| `offense` | Offense code (Penal Code/Health & Safety Code) | `HS11350(a)`, `PC459 2nd` |
| `offense description` | Human-readable offense description | `Possess Controlled Substance` |
| `offense category` | Category of offense (5 categories) | See below |
| `in prison` | Current prison status (mostly empty) | `In-Prison` or blank |
| `offense begin date` | Start date of offense | `2000-06-06` |
| `offense end date` | End date of offense | `2000-06-06` |
| `offense time with enhancement` | Time including enhancements | `1 Year 4 Months` |
| `relationship` | Sentence relationship to other sentences | See below |
| `release date` | Release date from custody | `2001-03-08` |

### Offense Categories

| Category | Count | Percentage |
|----------|-------|------------|
| Crimes Against Persons | 61,722 | 32.2% |
| Property Crimes | 55,792 | 29.1% |
| Other Crimes | 28,525 | 14.9% |
| Drug Crimes | 23,314 | 12.2% |
| Case Enhancement | 22,083 | 11.5% |

### Relationship Types

| Type | Description | Count |
|------|-------------|-------|
| Concurrent | Served at the same time as another sentence | 76,178 |
| Initial | First/primary sentence | 63,839 |
| Consecutive | Served after another sentence | 41,418 |
| Stayed | Sentence suspended | 10,000 |

### Top Sentencing Counties

1. Los Angeles (55,548)
2. Riverside (15,824)
3. San Diego (15,536)
4. San Bernardino (13,673)
5. Orange (10,631)

## Dependencies

- Python 3.8+
- pandas
- numpy
- matplotlib
- seaborn
- scipy

See `requirements.txt` for version details.

## Statistical Methods

| Test | Purpose | Variables |
|------|---------|-----------|
| Chi-square | Test categorical associations | Offense Category vs Relationship |
| Independent t-test | Compare means between two groups | Days Served: Drug vs Property Crimes |
| Spearman Correlation | Non-parametric correlation | Prior Commitments vs Days Served |
| Kruskal-Wallis | Compare distributions across groups | Days Served across all Offense Categories |

## Authors

- [Your Name]

## License

[Add your license here]
