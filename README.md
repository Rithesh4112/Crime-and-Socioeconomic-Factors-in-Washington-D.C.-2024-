### Crime and Socioeconomic Factors in Washington, D.C. (2024)
This project explores the relationship between crime incidents and socioeconomic factors in Washington, D.C. during 2024. By integrating open crime data with neighborhood-level economic indicators, we aim to uncover spatial and temporal patterns in criminal activity and assess the feasibility of predictive modeling for both violent and non-violent crimes.

### Objectives
Understand the structure of crime in D.C.
Perform exploratory data analysis and visualization to identify trends across time, geography, and crime categories.

Integrate economic context
Enrich crime data with socioeconomic features (e.g., income, education, poverty rate) at the ANC or Ward level to provide explanatory insights.

Build predictive models

Binary classification: Violent vs. non-violent crimes

Multi-class classification: Predict specific non-violent crime types (e.g., burglary, theft)

Evaluate models including Random Forest, XGBoost, and Neural Networks using techniques such as class weighting and SMOTE for imbalanced data

### Data Sources
Crime_Incidents_in_2024.csv: Official crime records for Washington, D.C., including offense type, location, method, and time.

Socioeconomic and Housing Data: Public datasets by Ward/ANC covering demographics, income, education, housing, and employment.

### Methodology
Data Preparation
Standardized and cleaned crime and economic datasets

Handled missing or inconsistent geographic join fields using string similarity and contextual imputation (e.g., neighborhood, coordinates)

### Exploratory Analysis
Temporal trends: Monthly and hourly distributions

Geographic trends: Mapping crimes by Ward/ANC

Crime type distribution: Violent vs. non-violent patterns

Socioeconomic Correlation
Merged housing and economic indicators by Ward

Identified key relationships:

Higher rental rates → more crime

Lower homeownership → more crime

Greater residential mobility → more property crime

Overcrowding → more violent crime

Detached housing → less crime

Predictive Modeling
### Classifiers Used:
Logistic Regression
Random Forest
XGBoost
Feedforward Neural Network (FNN)

### Imbalance Handling Techniques:
Baseline (no adjustment)

SMOTE (Synthetic Minority Oversampling)
Class Weights (cost-sensitive learning)

### Performance Highlights:
Baseline models (no imbalance handling) achieved high overall accuracy (~88%) but failed to detect violent crimes, with near-zero recall.

SMOTE improved recall but led to lower precision due to oversampling, causing more false positives.

Class weights proved most effective for handling imbalance:

XGBoost with class weights achieved the best F1 Score (0.29), offering the most balanced trade-off between precision and recall.

Random Forest with class weights was also strong, with high recall (49%) and decent precision.

Logistic Regression, while simpler, matched SMOTE in recall but underperformed in overall expressiveness.



Baseline models failed to detect violent crimes effectively

Class weighting outperformed SMOTE, especially with XGBoost

XGBoost with class weights yielded the best balance of recall and precision

### Tools & Libraries
Python (pandas, seaborn, matplotlib, scikit-learn, XGBoost, imbalanced-learn)

Jupyter Notebooks

Folium/Plotly for interactive maps

### Future Work
Expand analysis to additional cities for geographic generalization

Incorporate fairness-aware modeling and causal inference techniques

Use alternative metrics (e.g., balanced accuracy, ROC AUC) for better evaluation

Assess real-world implications (e.g., false positives in predictive policing)

### Key Takeaways
Stable housing and homeownership correlate with lower crime rates

Violent crimes are relatively rare but concentrated in specific wards

Class weighting and tree-based models are effective for imbalanced classification

Responsible modeling must consider fairness, bias, and broader social impacts

