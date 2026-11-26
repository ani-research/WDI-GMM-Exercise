# Ecotrix: Government Education Expenditure and Secondary School Enrolment

## Overview

**Ecotrix** is an empirical econometrics project investigating the relationship between government expenditure on education and secondary school enrolment across low- and middle-income countries.

The study examines whether greater public investment in education translates into improved access to secondary education, accounting for the persistence of enrolment outcomes, country-specific heterogeneity, and potential endogeneity.

The empirical analysis uses a balanced panel of **43 countries over 2011–2020**, constructed using data from the World Bank's World Development Indicators (WDI).

The project combines exploratory data analysis, descriptive statistics, correlation analysis, dynamic panel estimation using Generalised Method of Moments (GMM), and robustness checks.

## Research Question

**Does higher government expenditure on education lead to greater secondary school enrolment across low- and middle-income countries?**

The analysis focuses on four variables:

| Variable | Description | WDI Indicator |
|---|---|---|
| Secondary School Enrolment | Gross secondary enrolment ratio (%) | `SE.SEC.ENRR` |
| Government Education Expenditure | Government expenditure on education (% of GDP) | `SE.XPD.TOTL.GD.ZS` |
| GDP per Capita | GDP per capita, PPP (constant international dollars) | `NY.GDP.PCAP.PP.KD` |
| Urban Population | Urban population (% of total population) | `SP.URB.TOTL.IN.ZS` |

## Dataset and Sample

- **Source:** World Bank – World Development Indicators (WDI).
- **Initial coverage:** 131 low- and middle-income countries.
- **Final sample:** 43 countries.
- **Time period:** 2011–2020.
- **Panel structure:** Balanced panel.
- **Total observations:** 430 country-year observations.

The dataset was cleaned and transformed to address missing observations and ensure comparability across countries.

Linear mean interpolation was used exclusively to fill isolated one-year gaps where observations were available in the preceding and subsequent years. Countries were subsequently selected based on the availability of complete observations across all four variables.

## Methodology

The empirical strategy proceeds in several stages.

### 1. Data Cleaning and Preparation
- Extraction of relevant WDI indicators.
- Transformation of GDP per capita using natural logarithms.
- Identification and treatment of missing observations.
- Construction of a balanced country-year panel.

### 2. Exploratory Data Analysis
- Country-wise trends in education expenditure, enrolment, GDP per capita and urbanisation.
- Aggregate and country-level descriptive statistics.
- Mean, standard deviation and interquartile range analysis.
- Visual examination of potential outliers.

### 3. Correlation Analysis
Three approaches are employed:
- Cross-country Pearson correlation using country-level averages.
- Pooled Pearson correlation matrix.
- Country-wise correlations to investigate heterogeneity in the relationship between education expenditure and enrolment.

### 4. Dynamic Panel GMM Estimation

The primary empirical approach uses dynamic panel Generalised Method of Moments estimators.

The baseline specification is:

\[
\begin{aligned}
Enrolment_{it} ={}& \alpha Enrolment_{i,t-1}\\
&+\beta Expenditure_{it}\\
&+\gamma_1 LogGDP_{it}\\
&+\gamma_2 Urban_{it}\\
&+\mu_i+\lambda_t+\varepsilon_{it}
\end{aligned}
\]

Where:

- \(Enrolment_{it}\): Gross secondary school enrolment.
- \(Enrolment_{i,t-1}\): Lagged enrolment.
- \(Expenditure_{it}\): Government education expenditure as a percentage of GDP.
- \(LogGDP_{it}\): Logarithm of GDP per capita (PPP).
- \(Urban_{it}\): Urban population as a percentage of total population.
- \(\mu_i\): Country-specific effects.
- \(\lambda_t\): Time-specific effects.
- \(\varepsilon_{it}\): Error term.

The following estimators and specifications are examined:

- Two-Step System GMM.
- Two-Step Difference GMM.
- One-Step System GMM.
- System GMM with predetermined education expenditure.

Diagnostic tests include:
- Arellano-Bond AR(1) and AR(2) tests.
- Hansen J test.
- Sargan test.
- Difference-in-Hansen test.
- Instrument count assessment.

### 5. Robustness and Additional Diagnostics

The results are further examined using:

- Pooled Ordinary Least Squares (OLS).
- Fixed Effects (FE).
- Comparison of lagged dependent variable coefficients across estimators.
- Variance Inflation Factor (VIF) analysis to assess multicollinearity.

## Key Findings

The principal findings of the empirical exercise are:

1. **No statistically significant expenditure effect:** Government education expenditure does not exhibit a statistically significant relationship with secondary school enrolment in the baseline Two-Step System GMM specification.

2. **Strong persistence in enrolment:** The lagged enrolment coefficient is 0.9845 and statistically significant at the 1% level, indicating substantial persistence in educational participation.

3. **Robustness across specifications:** The expenditure coefficient remains statistically insignificant across System GMM, Difference GMM, Pooled OLS and Fixed Effects estimations.

4. **Cross-country heterogeneity:** Although the pooled correlation between government education expenditure and enrolment is positive, country-wise correlations reveal considerable variation in both magnitude and direction.

5. **Economic development matters:** Secondary school enrolment exhibits a strong positive pooled correlation with log GDP per capita (0.81).

6. **Instrument diagnostics:** The baseline System GMM specification produces a Hansen J-test p-value of 0.535 and an AR(2) p-value of 0.232, providing some support for the specification, although the diagnostics do not conclusively establish instrument validity.

The findings suggest that public education expenditure alone may not adequately explain differences in secondary school enrolment. Institutional capacity, resource allocation efficiency and broader socioeconomic conditions may also influence educational outcomes.

## Technology Stack

The project uses Python for data processing, statistical analysis, visualisation and econometric estimation.

| Library / Tool | Application |
|---|---|
| Python 3.14 | Primary programming language |
| NumPy | Numerical computation |
| Pandas | Data manipulation and panel construction |
| SciPy | Statistical calculations |
| Matplotlib | Data visualisation |
| Seaborn | Statistical visualisation |
| Plotly | Interactive visualisations |
| PyDynPD | Dynamic panel GMM estimation |
| PanelBox | System and Difference GMM estimation |
| Linearmodels | Pooled OLS and Fixed Effects |
| Statsmodels | Statistical diagnostics and VIF |

## Repository Structure

```text
Ecotrix/
│
├── Ecotrix.ipynb       # Complete empirical analysis
├── Report.pdf          # Econometrics assignment and findings
├── WDI_DATA.xlsx       # Input World Bank dataset
└── README.md           # Project documentation
```

## Getting Started

### 1. Clone the Repository

```bash
git clone <repository-url>
cd Ecotrix
```

### 2. Create a Virtual Environment

```bash
python -m venv .venv
```

Activate it:

**Windows (PowerShell):**

```powershell
.\.venv\Scripts\Activate.ps1
```

### 3. Install Dependencies

```bash
pip install numpy pandas scipy matplotlib seaborn plotly jupyter statsmodels linearmodels pydynpd panelbox openpyxl
```

### 4. Run the Notebook

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open `Ecotrix.ipynb` and execute the cells sequentially.

**Note:** The notebook expects the input dataset `WDI_DATA.xlsx` to be available in the working directory. The dataset should be obtained from the World Bank WDI database and structured to match the notebook's data-processing steps.

## Limitations

The empirical exercise has several limitations:

- The relatively short time dimension (10 years) limits the ability to capture long-term effects of education expenditure.
- High persistence in secondary enrolment creates additional econometric challenges.
- GMM estimates can be sensitive to instrument selection and specification.
- Education expenditure as a percentage of GDP does not directly capture per-student spending or the efficiency of public resource utilisation.
- Potential omitted variables, including institutional quality and household characteristics, may influence the estimated relationship.
- The final country sample is determined by data availability, which may introduce sample selection concerns.

Consequently, the absence of a statistically significant expenditure coefficient should not be interpreted as evidence that public education spending is ineffective.

## Conclusion

This project explores the relationship between public education financing and secondary school enrolment through a cross-country dynamic panel framework.

The empirical results highlight the persistence of educational participation and the absence of a statistically significant independent expenditure effect across the estimated specifications. They also underline the importance of accounting for country-level heterogeneity, socioeconomic conditions and institutional factors when examining the effectiveness of public expenditure.

The project demonstrates the application of Python-based data analysis and dynamic panel econometric techniques to an empirical question in development economics.

---

**Research Area:** Development Economics | Public Economics | Applied Econometrics | Dynamic Panel Data

**Data Source:** [World Bank – World Development Indicators](https://databank.worldbank.org/source/world-development-indicators)

**Language:** Python
