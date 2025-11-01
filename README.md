# Fraud Policy Analysis 
# - Vendor Data Integration for Fraud Detection

## 📋 Overview

This project evaluates the effectiveness of integrating new vendor phone number ownership and risk factor data to enhance fraud detection capabilities for merchant onboarding. The analysis compares rule-based detection methods with machine learning models, demonstrating improved fraud detection performance and significant ROI improvements.

## 🎯 Problem Statement

**Case Part 1:** Should we engage with a new vendor providing phone number ownership and risk factor information to improve our fraud detection capabilities?

**Case Part 2:** How to manage fraud risk at new seller onboarding while balancing growth?

## 📊 Dataset

The dataset includes:
- **Internal Scores**: IdentityScore, EAScore, UWScore
- **Vendor Phone Data**: Phone verification components, linkage indicators, service status, carrier information, VoIP indicators, and more
- **Target Variable**: Fraud label (0 = legitimate, 1 = fraudulent)

## 🔍 Methodology

### Step 1: Rule-Based Detection Strategy

**Objective**: Design a decision strategy using existing internal scores.

**Approach**:
- Analyzed data distribution by fraud label
- Implemented SMOTE (Synthetic Minority Oversampling Technique) to handle class imbalance
- Created Decision Tree visualization for rule-based detection
- Evaluated detection results including False Positives (FP)

### Step 2: Vendor Data Analysis

**Qualitative Analysis**: Identified key vendor data factors correlated with fraudulent behavior:
- Identity completeness
- Service Discontinued Indicator
- Voice over IP (VoIP) indicators
- Business Phone Indicator

**Quantitative Analysis**: Four parallel methods to evaluate vendor data effectiveness:

1. **Multivariate Analysis**: Examined distribution differences of fraud labels across vendor feature values
2. **Correlation Analysis**: 
   - Analyzed relationships between fraud and new variables
   - Examined relationships between old and new variables
   - Identified new features with low correlation to internal scores (carrying unique information)
3. **Chi-Square Test**: Statistical significance testing on numerical vendor data features
4. **Model Comparison**: Built models on two datasets:
   - Dataset 1: Only internal scores
   - Dataset 2: Internal scores + vendor features

**Preprocessing**:
- One-Hot Encoding for `Owner_MVNO_Indicator_category`
- Target Encoding for other categorical features
- SMOTE for class balancing

**Model Training**:
- XGBoost Classifier
- Grid Search for hyperparameter optimization
- Model evaluation using:
  - Confusion Matrix
  - Classification Report
  - ROC-AUC Score

### Step 3: Hybrid Detection Methods

A three-step approach combining rule-based and ML methods:

1. **Rule-Based Filter**: Approve/reject based on clear conditions from domain expertise
2. **ML Model Detection**: Review all approved cases from Step 1 using the ML model
3. **Manual Review**: Review cases flagged as fraud by the ML model in Step 2

**Rationale**:
- Rule-based methods efficiently handle simple, well-defined fraud patterns
- ML models detect complex patterns difficult to define through rules
- Manual review ensures high-precision final decisions

### Step 4: ROI Analysis

**Key Assumptions**:
- Revenue per approved merchant: $40/month
- Loss per fraudulent merchant: $500
- Cost per manual review: $50
- Cost per vendor call: $0.50
- Manual review approval rate: 30%

**ROI Without Vendor Data**: 25x
- Revenue: $16,950 × 40 × (1+...+12) = $4,068,000
- Cost: 326 × 500 × 12 = $1,956,000

**ROI With Vendor Data**: 64x
- Revenue: $18,970 × 40 × (1+...+12) = $4,552,800
- Cost: (1,314 × 50 × 12) + (19,890 × 0.5 × 12) = $788,400 + $119,340 = $907,740

**Conclusion**: Integration of vendor data increases ROI from 25x to 64x, demonstrating significant value.

## 📈 Results

### Model Performance

| Metric | Internal Scores Only | Internal + Vendor Data |
|--------|---------------------|------------------------|
| ROC-AUC | 0.95 | 0.97 |
| 95% CI | [0.9380, 0.9620] | [0.9670, 0.9730] |

**Key Finding**: The model with vendor data shows a 2% improvement in ROC-AUC, with all performance metrics superior to the rule-based method.

### Detection Strategy Comparison

The ML model with all data sources outperforms the rule-based method across all performance metrics.

### Feature Importance

Analysis reveals that vendor-provided features contribute unique information beyond internal scores, enhancing fraud detection capabilities.

## 🚀 Next Steps

1. **Model Improvement**: 
   - Explore more advanced models
   - Experiment with different decision thresholds
   - Fine-tune feature engineering

2. **Deployment**:
   - Deploy on cloud infrastructure
   - Test online performance with real-time data
   - Monitor model performance in production

3. **Continuous Monitoring**:
   - Track long-term performance metrics
   - Iterate and improve detection algorithms
   - Update models based on new fraud patterns

## 💡 Additional Analysis Opportunities

### Account Level Risk Data
- Historical transaction patterns (frequency, amounts, geolocation)
- Merchant demographics (industry, location, business size, registration date)
- Account creation date vs. first fraudulent activity
- Temporal patterns (time of day, day of week)
- Location distance metrics (billing address, IP, phone number)
- High-risk region identification

### External Data Sources
- Historical blacklists (email, phone, IP address associations)
- Additional third-party data providers

### Advanced Techniques
- NLP analysis on textual data
- More sophisticated AI/ML models (deep learning, ensemble methods)

## 🏢 Managing Fraud Risk While Balancing Growth

### Strategy Components

1. **Strengthen Identity Verification** (Engineering/Product)
2. **Fraud Detection Models and Algorithms** (Risk)
3. **Proactive Fraud Education** (Operations)
4. **Monitor Early Transactions** (Operations/Risk)

### Key Metrics System

**🌟 North Star Metrics**:
- Fraud Loss Amount per week
- New sellers per week

**🧱 Guardrail Metrics**:
- Onboarding Time increase
- Latency time due to complex onboarding

**⚡️ Driver Metrics**:
- Onboarding dropout rate
- Revenue created by new merchants

### Balancing Growth and Fraud Prevention

1. Minimize false positive rate
2. Simplify onboarding process for low-risk sellers
3. Improve UI/UX to decrease onboarding dropout
4. Monitor dropout rates and establish feedback systems

### Cross-Functional Communication

**Product Team**: Focus on seamless fraud tool integration without disrupting user experience

**Engineering Team**: Ensure technical feasibility and system performance scalability

**Marketing Team**: Highlight fraud management's role in protecting platform reputation and enabling targeted campaigns

**Operations Team**: Demonstrate how fraud detection reduces manual checks and improves operational efficiency

**Finance Team**: Show how proactive fraud prevention reduces chargebacks, fines, and financial losses while maintaining growth

## 📁 Project Structure

```
.
├── Craft Demo- Fraud Policy DataSet.csv          # Main dataset
├── Fraud Policy Analysis.pdf                     # Analysis documentation
├── CS - Craft Demo- Fraud Policy EP .pdf         # Problem statement
└── README.md                                     # This file
```

## 🔬 Technical Details

- **Algorithm**: XGBoost Classifier
- **Preprocessing**: SMOTE, One-Hot Encoding, Target Encoding
- **Evaluation**: Confusion Matrix, Classification Report, ROC-AUC
- **Statistical Tests**: Chi-square test, Correlation analysis, Multivariate analysis
