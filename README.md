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

## Feedforward Neural Network (FNN) Results & Interpretation

### Interpretation of Class Weighting Results

The class-weighted version of the FNN successfully detected violent crimes, achieving 424 correct predictions. This marks a clear improvement over the unweighted baseline, indicating that class weighting increases the model’s sensitivity to the minority (violent) class.

However, this came with a trade-off. The model misclassified 2006 property crimes as violent, significantly increasing false positives and reducing overall accuracy to 60%. Despite that, recall for violent crimes improved to 0.65, which is a substantial gain if identifying violent crimes is the top priority.

Precision for the violent class was low at 0.17, meaning most violent predictions were incorrect. In contrast, the property class maintained a high precision of 0.93, but its recall dropped to 0.59. Overall, class weighting made the model more aggressive in detecting violence but less precise.

Whether this is a better model depends on the application. If missing a violent crime is more harmful than triggering false alarms, this model is preferable. However, if false positives must be minimized and precision is crucial, the baseline performs better.

---

## SMOTE vs Class Weighting (FNN)

Both SMOTE and class weighting produced nearly identical results across metrics. Accuracy remained at 60%, and ROC AUC was approximately 0.675 for both.

SMOTE slightly improved recall for violent crimes, increasing it from 0.65 to 0.66. It also raised the number of true positives from 424 to 430. However, it also increased false positives, with 2030 property crimes misclassified as violent, compared to 2006 in the class-weighted model.

Precision for the violent class remained low at 0.17 in both models. This shows that while both methods improve recall, they still struggle with precision. The SMOTE model was marginally more aggressive in flagging violent crimes, resulting in more false alarms.

Overall, SMOTE and class weighting achieved almost equivalent performance. SMOTE offered a very small increase in recall but at the cost of slightly more false positives. This suggests SMOTE did not meaningfully outperform class weighting, though it may still be viable with further tuning, such as threshold adjustment or hybrid techniques.

The SMOTE model stopped training early at epoch 6, likely due to the balanced nature of the oversampled data, allowing quick optimization but also early convergence.

---

## Combined Model Evaluation Summary (Classical and Neural)

Logistic Regression in its baseline form failed to detect any violent crimes. When combined with SMOTE or class weighting, it achieved around 60% recall for violent crimes but suffered from very low precision (17%) and moderate accuracy (\~61%).

Random Forest performed slightly better. With class weighting, it achieved 49% recall and 20% precision for violent crimes, showing moderate improvement. SMOTE brought the recall up to 27%, but again with low precision.

XGBoost with class weighting achieved the best balance among classical models, reaching 60% recall and 19% precision for violent crimes, with an overall accuracy of 65%. It outperformed its own baseline and SMOTE variants.

PyTorch FNN with either class weighting or SMOTE outperformed classical models in terms of violent crime recall, reaching 65% and 66% respectively. However, both models had equally low precision (17%) and high false positive rates, which lowered overall confidence in violent predictions.

---

### Key Takeaways

* PyTorch FNN models with class weighting or SMOTE achieved the best recall for violent crimes but generated a high number of false positives due to low precision.
* XGBoost with class weights was the most balanced among classical models, offering good recall with slightly better precision.
* SMOTE consistently improved recall across all models, but often reduced precision, making it a trade-off strategy.
* Baseline models failed to detect violent crimes altogether, making them unsuitable in contexts where identifying violent incidents is critical.


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

