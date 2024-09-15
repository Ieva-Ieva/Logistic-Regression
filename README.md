# Predictive Modelling of the 10-year Risk of Coronary Heart Disease in Framingham Dataset 

## Introduction  

The analyzed data is based on the cardiovascular study on residents of the town of Framingham, Massachusetts.  

The task is to perform an analysis and fit a logistic regression model for predicting 10-year risk factors of coronary heart disease (CHD) as well as choose the most appropriate classification metric for this problem and calculate the optimal threshold.  

### Source  

The dataset is publicly available on Kaggle: [Cardiovascular Study Dataset](https://www.kaggle.com/datasets/christofel04/cardiovascular-study-dataset-predict-heart-disea).  

## 5. Key Insights and Recommendations

1. **Classification Report With Default Threshold**:
- **Class 0 (Non-CHD)**:
    - **Precision (0.92)**: Of all the cases predicted as Non-CHD, 92% were actually Non-CHD. The high precision indicates that the model is very accurate when it predicts that a patient does not have CHD.
    - **Recall (0.71)**: The model correctly identified 71% of all actual Non-CHD cases, which means that 29% of the Non-CHD cases were misclassified as CHD.
    - **F1-Score (0.80)**: The harmonic mean of precision and recall. A high F1-score indicates a good balance between precision and recall for Non-CHD cases.
- **Class 1 (CHD)**:
    - **Precision (0.28)**: Of all cases predicted as CHD, only 28% were actually CHD, which indicates a high number of false positives (Non-CHD cases predicted as CHD).
    - **Recall (0.65)**: The model correctly identified 65% of all actual CHD cases, missing 35% of CHD cases.
    - **F1-Score (0.40)**: The F1-score here is relatively low, indicating a poor balance between precision and recall for CHD cases.
    - **Overall Accuracy (0.70)**: The model correctly predicted the class in 70% of all cases.
**With Default Threshold**, the model is more conservative, favoring precision over recall, particularly in the Non-CHD class; it is better at ruling out CHD (high precision) but misses more true CHD cases (lower recall).
2. **Classification Report With Optimal Threshold**:
- **Class 0 (Non-CHD)**:
    - **Precision (0.93)**: Slightly increased from 0.92 to 0.93, indicating even fewer false positives for the Non-CHD class.
    - **Recall (0.69)**: Decreased from 0.71 to 0.69, meaning the model missed more Non-CHD cases, increasing the number of false negatives.
    - **F1-Score (0.79)**: Decreased from 0.80 to 0.79, reflecting a slight decline in the overall performance for the Non-CHD class after adjusting the threshold.
- **Class 1 (CHD)**:
    - **Precision (0.29)**: Slightly increased from 0.28 to 0.29.
    - **Recall (0.71)**: Increased from 0.65 to 0.71, meaning that the model correctly identified more CHD cases, reducing the number of false negatives.
    - **F1-Score (0.41)**: Grew from 0.40 to 0.41, showing a slight improvement in the balance between precision and recall for CHD cases.
    - **Overall Accuracy (0.69)**: Decreased from 0.70 to 0.69: while the threshold adjustment improved precision and recall for CHD, it slightly worsened overall accuracy.
**With Optimal Threshold**, the model better detects CHD cases, which might be preferable in areas like health where missing a CHD case has serious consequences, even if it means accepting more false positives.

3. **ROC-AUC** (Receiver Operating Characteristic - Area Under Curve measures the model’s ability to distinguish between positive and negative classes for all possible choices of thresholds). This model has a 72.06% chance of correctly distinguishing between a patient with and without CHD. 
    - **The optimum position for ROC curve** is towards the top left corner where the specificity and sensitivity are at optimum levels.
    - **AUC** quantifies model classification accuracy: the higher the area, the greater the disparity between true and false positives, and the stronger the model in classifying members of the training dataset. An area of 0.5 corresponds to a model that performs no better than random classification and a good classifier stays as far away from that as possible. The closer the AUC to 1 the better.

4. **Confusion Matrix**: **with the default threshold** shows that the model correctly classifies 410 out of 576 negative cases and 66 out of 102 positive cases. However, it misclassifies 166 negative cases as positive and 36 positive cases as negative.
After applying the **optimal threshold**, the model correctly classifies 398 out of 576 negative cases and 72 out of 102 positive cases. However, the number of false positives increased to 178, and false negatives decreased to 30.

5. **Optimal Threshold**: By default, the logistic regression threshold is 0.5, but adjusting it to 0.4833 should improve the balance between precision and recall and maximize the model's performance. In this model, the use of an optimal threshold slightly improved recall and precision. In a healthcare setting, recall might be prioritized over precision to ensure that most CHD cases are identified, even resulting in more false positives. This approach could be particularly important in preventive screenings, where the cost of missing a true positive is higher than the cost of follow-up tests for false positives. 

6. **Feature Importance**
    - **Diabetes**: Having diabetes is the most significant factor, increasing the odds of CHD by 2.11 times. This suggests that diabetes management should be a key focus in preventing CHD.
    - **Prevalent Stroke**: Individuals with a history of stroke are 1.76 times more likely to develop CHD and they need close monitoring for CHD risk factors.
    - **Age**: As age increases, the risk of CHD increases by 1.62 times. This is consistent with the well-known association between aging and cardiovascular diseases.
    - **Sex**: Males have a 1.55 times higher risk of CHD compared to females, which aligns with epidemiological data that males generally have a higher risk of heart disease.
    - **Systolic Blood Pressure**: Higher systolic blood pressure increases CHD risk by 1.40 times, therefore, blood pressure control should be among priorities in healthcare.
    - **Cigarettes Per Day**: Smoking increases the risk of CHD by 1.37 times, highlighting the importance of stopping smoking programs.
    - **Prevalent Hypertension**: Individuals with previous hypertension are 1.25 times more likely to develop CHD and they need close monitoring for CHD risk factors.
    - **Total Cholesterol**: Higher cholesterol levels slightly increase the risk of CHD by 1.14 times, which suggests that lipid-lowering strategies could be beneficial.
    - **Glucose**: Elevated glucose levels have a modest impact on CHD risk (1.05 times increase), suggesting the importance of blood sugar control.
    - **Education**: Potentially higher levels of education are associated with a reduced risk of CHD by 0.91 times, which may reflect the role of education in promoting healthier lifestyles.
    - **Blood Pressure Medications**: The use of blood pressure medications is associated with a reduced risk of CHD by 0.66 times, highlighting the effectiveness of medication in reducing cardiovascular risk.
7. **Recommendations**
- **Focus on High-Risk Groups**: Given that diabetes, stroke history, age, and being male are strong predictors of CHD, targeted interventions should be directed at these high-risk groups. Also, stopping of smoking, blood pressure control, and cholesterol management should be encouraged as these factors significantly impact CHD risk.
- **Increase Education and Awareness**: Increasing public awareness about the importance of education in adopting healthier lifestyles could indirectly reduce CHD risk.
- **Imbalanced Precision Across Classes**: The significant difference in precision between the negative and positive classes (92% vs. 28% at default and 93% vs. 29% at optimal threshold) suggests that the model is better at predicting the absence of CHD than its presence. This imbalance could lead to overconfidence in negative predictions and underdiagnosis in positive cases. To address this, augmenting the dataset with more positive cases (if possible) or employing techniques such as SMOTE (Synthetic Minority Over-sampling Technique) to balance the class distribution could be considered. 
8. **Model Weaknesses**: The recall and F1-score indicate that the model has a notable number of false negatives, which could be problematic in a health setting where missing a positive case is risky. The imbalance between precision and recall, particularly the low precision for the Non-CHD class, suggests that the model is better at identifying CHD than ruling it out in Non-CHD cases.
9. **Next Steps**: Further tuning of the model could be considered, like reviewing feature selection or adjusting the threshold. Additionally, experimenting with other models might improve recall without sacrificing precision.

