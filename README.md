# Credit Risk Intelligence: Analytical Insights and Predictive Solutions

**Project-Based Virtual Internship Program**  
Data Scientist at ID/X Partners x Rakamin Academy

## Executive Summary

This project develops a predictive credit risk model for lending platforms to reduce financial losses from borrower defaults. A LightGBM-based machine learning model achieved a ROC-AUC score of 0.708 and implemented a 5-tier risk segmentation system that reduced portfolio losses by $16 million (31.5% reduction).

**Key Results:**
- Reduced default rate from 28.4% to 19.6% (8.8pp improvement)
- Increased risk-adjusted return by 95 basis points
- Automated approval for 20% of low-risk applications
- Identified 8 critical risk factors driving 50% of total defaults

## Business Problem

Lending platforms face significant credit risk exposure with a baseline default rate of 21.4% across a $6.7B portfolio, resulting in potential losses exceeding $50M annually. Without effective risk assessment mechanisms, the company cannot:
- Differentiate between high-risk and low-risk borrowers systematically
- Optimize pricing strategies based on actual risk profiles
- Automate lending decisions at scale
- Maintain sustainable portfolio health metrics

**Objective:** Build a predictive model achieving 0.70+ AUC-ROC to classify borrowers into actionable risk tiers and enable data-driven lending decisions.

## Dataset Overview

**Source:** Loan application and performance data spanning 2007-2014

**Scale:**
- 466,285 loan records
- 75 features across 6 categories
- 780 MB total size
- Target variable: Binary classification (Good Loan vs Bad Loan)

**Target Distribution:**
- Good Loans (Fully Paid): 78.6%
- Bad Loans (Charged Off, Default, Late): 21.4%

**Feature Categories:**
1. Identification & Administrative (5 features)
2. Loan & Borrower Information (17 features)
3. Credit & Payment History (40 features)
4. Dates & Timeline (5 features)
5. Status & Target (4 features)
6. Joint Application (3 features)

## Methodology

### 1. Data Preparation
- Processed 400K+ records with engineered features
- Applied leakage prevention protocols
- Domain-based imputation for missing values
- Stratified train/validation/test split (60/20/20)
- Business logic-based outlier capping
- Winsorization at 1st and 99th percentiles

### 2. Exploratory Data Analysis
Conducted comprehensive analysis across multiple dimensions:
- Portfolio composition and health metrics (87.7% healthy rate)
- Customer profiling (income, employment, housing status)
- Seasonal default patterns (Chi-square test: p<0.001)
- Risk grade distribution and concentration analysis
- Feature correlation analysis (weak linear relationships observed)

### 3. Model Development
- Benchmarked 16 machine learning algorithms
- Selected LightGBM as champion model (class_weight='balanced')
- Hyperparameter optimization using Optuna (16 trials over 5.2 hours)
- Feature selection: Reduced from 60 to 18 features (70% reduction)
- Maintained 99.83% performance with final ROC-AUC 0.7067

### 4. Model Calibration
- Applied Isotonic Regression with 5-fold cross-validation
- Improved Brier Score and Log Loss metrics
- Validated probability reliability for production deployment

### 5. Risk Segmentation
- Developed 5-tier classification system
- Custom threshold optimization
- Validation: <2% deviation between predicted and actual default rates
- Defined business rules from auto-approve to reject

## Critical Findings

### High-Risk Segments Identified

**1. Income-Based Risk (The Poverty-Grade Paradox)**
- 0-50K income segment: 23.15% default rate (2x higher than 200K+ segment)
- Comprises 43% of portfolio but drives 48% of all defaults
- Single largest risk contributor: 18,617 default cases

**2. Credit Grade Concentration**
- Grades D-G: Only 20% of volume but account for 50% of defaults
- Default rate escalates from 6.6% (Grade A) to 43.9% (Grade G)
- Grade D marks critical inflection point at 28% default rate

**3. Loan Term Risk**
- 60-month loans: 31% default rate vs 16% for 36-month (2x gap)
- Represent 25% of volume but contribute 35% of defaults

**4. Debt-to-Income Impact**
- High DTI borrowers: 26% default rate (83% increase vs Very Low DTI)
- Constitute 25% of portfolio but drive 29% of defaults

**5. Purpose-Specific Risk**
- Small business loans: 30% default rate (highest among all purposes)
- Only 19% of portfolio subset but contribute 28% of defaults

**6. Housing Status**
- Renters: 53% of portfolio and 53% of total defaults
- Homeowners show slightly lower default rate (19.9%)

**7. Seasonal Patterns**
- Q1-Q2: High-risk period (11.67%-12.25% default rates)
- Q4: 20% lower default rates (9.30%-10.19%)
- Statistical significance confirmed (p<0.001)

**8. Verification Paradox**
- Verified loans: 22% default rate vs 15% unverified (counterintuitive)
- Represent 44% of portfolio and contribute 43% of defaults

## Model Performance

**Classification Metrics:**
- ROC-AUC: 0.708 (Acceptable)
- Brier Score: 0.152 (Excellent calibration)
- Overall Accuracy: 78.98%
- PR-AUC: 0.3977 (reflects class imbalance)

**High-Risk Detection:**
- Precision: 54.6% (Fair)
- Recall: 43.7% (Fair)

**Feature Importance (Top Contributors):**
1. DTI Range (highest risk indicator)
2. Loan Vintage (2012-2014 cohorts)
3. Credit Grade (A-B as protective factors)
4. Interest Rate
5. Sub-grade classification

**Model Interpretability:**
- SHAP analysis implemented for regulatory compliance
- Transparent explanations for credit officers and applicants
- Validation that model learns correct risk patterns

## Risk Tier System

| Tier | Threshold | Volume | Predicted Default | Actual Default | Action |
|------|-----------|--------|-------------------|----------------|--------|
| Very Low | 11% | 10,644 | 7.5% | 7.4% | Auto-approve |
| Low | 23% | 18,514 | 16.3% | 16.3% | Standard Approval |
| Medium | 43% | 14,751 | 30.9% | 30.9% | Manual Review |
| High | 62% | 3,423 | 48.6% | 49.6% | Strict Review |
| Very High | 100% | 2,076 | 69.1% | 66.5% | Reject |

**Calibration Quality:** <2% average deviation between predicted and actual default rates

## Business Impact

**Financial Metrics:**
- **Portfolio Loss Reduction:** $16.0M (31.5% decrease)
- **Default Rate Improvement:** 19.6% (8.8pp reduction from baseline)
- **Risk-Adjusted Return:** 2.22% (+95 basis points)

**Operational Efficiency:**
- 20% of applications can be auto-approved (Very Low risk tier)
- 10% flagged for strict review/rejection (High + Very High tiers)
- 70% require standard or manual review processes

**Portfolio Health:**
- Current healthy portfolio rate: 87.7%
- Minimal default rate: 0.2%
- Strong repayment activity: 40% fully paid

## Strategic Recommendations

### Immediate Actions

**1. Income Segment Restrictions**
- Tighten approval criteria for 0-50K income segment
- Implement enhanced verification for low-income applicants
- Consider higher down payment requirements (15-20%)

**2. Grade-Based Policies**
- Restrict or discontinue lending to Grades F-G
- Implement stricter underwriting for Grade D-E
- Launch targeted campaigns to increase Grade A-B acquisition

**3. Loan Term Management**
- Limit 60-month terms to Grade A-B borrowers only
- Increase pricing for extended terms in medium-risk grades
- Monitor term performance monthly for adjustments

**4. DTI Controls**
- Cap DTI at 35-40% maximum across all grades
- Implement graduated DTI limits by risk grade
- Require additional documentation for high-DTI applicants

**5. Purpose-Specific Rules**
- Require comprehensive cash flow proof for small business loans
- Apply stricter evaluation criteria for business purposes
- Consider declining small business loans in high-risk segments

### Portfolio Optimization

**6. Seasonal Strategy**
- Tighten approval criteria during Q1-Q2 (high-risk periods)
- Launch aggressive acquisition campaigns in Q4
- Adjust pricing dynamically based on seasonal patterns

**7. Housing Status Considerations**
- Require higher down payments for renters (15-20%)
- Prioritize homeowners in marginal approval cases
- Monitor renter portfolio concentration regularly

**8. Verification Enhancement**
- Don't rely on verification status alone as protective factor
- Implement multi-layered verification processes
- Cross-reference verified income with tax documents

## Technologies Used

**Programming & Data Processing:**
- Python 3.8+
- Pandas, NumPy
- Scikit-learn

**Machine Learning:**
- LightGBM (Champion Model)
- XGBoost, CatBoost (Benchmarking)
- Optuna (Hyperparameter Optimization)

**Model Evaluation & Interpretation:**
- SHAP (Model Interpretability)
- Isotonic Regression (Calibration)
- Cross-validation frameworks

**Data Preprocessing:**
- IterativeImputer (MICE algorithm)
- Yeo-Johnson Transformation
- Custom Ordinal Encoding
- L1 Regularization (Feature Selection)

**Statistical Analysis:**
- Chi-Square Tests
- Correlation Analysis
- Distribution Analysis

## Author

**Az-Zukhrufu Fi Silmi Suwondo**

- Email: afsilmis@gmail.com
- LinkedIn: [linkedin.com/in/az-zukhrufu-fi-silmi-suwondo](https://linkedin.com/in/az-zukhrufu-fi-silmi-suwondo/)
- GitHub: [github.com/afsilmis](https://github.com/afsilmis/)
## License

This project is part of an internship program and is intended for educational and portfolio purposes
