# A Predictive Modeling Approach to Understand and Address H1N1 Vaccine Hesitancy

![flu-vaccine](https://github.com/user-attachments/assets/1bdabd80-16b2-4ede-8356-e53b06896391)

Source:https://www.flickr.com/photos/ftmeade/15242740638/


## Business Understanding

### Business Overview

Vaccination is one of the most effective tools in public health to combat the spread of infectious diseases. In addition to protecting individuals, vaccines contribute to herd immunity, reducing transmission within communities. While modern attention has focused on the COVID-19 pandemic, this project revisits the public health response to a prior global outbreak: the 2009 H1N1 (swine flu) pandemic.

The H1N1 virus emerged in early 2009 and led to an estimated 151,000 to 575,000 deaths worldwide during its first year. A vaccine was introduced in October 2009, and to assess public response, the U.S. launched the National 2009 H1N1 Flu Survey. This telephone survey gathered data on whether individuals received the H1N1  vaccines, alongside questions about their personal, economic, and demographic backgrounds, opinions on vaccine safety and effectiveness, and behaviors related to disease prevention. Despite the availability of the vaccine, not everyone chose to get vaccinated.



### The Business Problem

Public health organizations face the challenge of increasing vaccine uptake during pandemics. To design more targeted and effective vaccination campaigns, they need to identify which individuals are likely — or unlikely — to receive the H1N1 vaccine.

This project aims to analyze survey data collected during the 2009 H1N1 pandemic to uncover patterns in vaccination behavior. By building a predictive model, we seek to identify key factors influencing vaccine acceptance. These insights can support public health agencies in developing data-driven strategies to better understand and address vaccine hesitancy in future campaigns.


### Stakeholders

The outcomes of this project are valuable to several key stakeholders:

* Public Health Agencies (CDC, WHO, local departments):
Use predictions and feature insights to tailor outreach and vaccine education campaigns.

* Healthcare Providers:
Identify at-risk populations for vaccine refusal and intervene through personalized guidance and education.

* Policy Makers:
Allocate resources more effectively by targeting communities or demographics less likely to get vaccinated.

* Non-Profit Organizations and NGOs:
Support data-driven public awareness campaigns and deliver educational programs where needed most.

* Data Scientists and Researchers:
Gain insights into behavioral modeling and apply findings to health-related prediction tasks.

## Data Understanding

### Data Source:

This project uses data from the National 2009 H1N1 Flu Survey (NHFS), conducted in the United States following the emergence of the H1N1 (swine flu) pandemic. The survey was designed to assess vaccine uptake and gather individual-level data on demographics, opinions, and behaviors related to flu prevention and vaccination. It is a relevant and high-quality source for modeling public health behavior during a real-world pandemic scenario.

The dataset is divided into three files:

* **training_set_features.csv** – Includes responses from 26,707 individuals with 36 features related to demographic, behavioral, and opinion-based attributes.

* **training_set_labels.csv** – Contains binary indicators of whether the respondent received the H1N1 vaccine and the seasonal flu vaccine.

* **test_set_features.csv** – Contains data for 26,708 individuals with the same features as the training set; target labels are not provided.

The dataset includes:

* **Demographic features** (e.g., age group, sex, race, income, education):
Important for identifying population-level trends in vaccine uptake.

* **Behavioral features** (e.g., face mask use, hand washing, social behavior):
Reflect how seriously individuals took preventive measures, which may correlate with vaccination behavior.

* **Opinion features** (e.g., trust in vaccine effectiveness, perceived risk of illness):
Crucial for understanding personal beliefs and vaccine hesitancy.

These features are highly relevant for predicting H1N1 vaccine behavior, as they reflect key factors studied in public health research: health beliefs, socio-demographics, and behavioral intentions.

## Exploratory Data Analysis

### A) Target Variable Distribution

<img width="589" height="453" alt="image" src="https://github.com/user-attachments/assets/45fe346b-b2ed-4630-8935-029fd2984897" />


The bar chart above visualizes the distribution of the target variable:

* Label 0 → Individuals who did not receive the H1N1 vaccine

* Label 1 → Individuals who did receive the vaccine

As evident from the plot, a large majority of 17,000 respondents were not vaccinated, while only around 4,000 were.

This highlights a significant class imbalance in the dataset. Such an imbalance can bias machine learning models toward predicting the majority class (label 0) more often, reducing the model’s effectiveness in correctly identifying minority class cases (label 1).

To address this, techniques like class weighting is necessary.

### B) Distribution of Numerical Features

<img width="1784" height="3265" alt="image" src="https://github.com/user-attachments/assets/7ea0bca8-c0cb-47ac-98b3-e77562d5c7f2" />


The figure above visualizes the distribution of all numerical features in the dataset.

Binary Features:
Many features — including behavioral_avoidance, behavioral_face_mask, doctor_recc_h1n1, chronic_med_condition, and health_worker — are binary (values of 0 or 1). These features are heavily skewed toward 0, indicating that most respondents:

did not engage in certain preventive behaviors, or

did not belong to specific groups (e.g., not healthcare workers or not chronically ill).

Opinion-Based Features:
Variables such as opinion_h1n1_vacc_effective, opinion_h1n1_risk, and opinion_seas_sick_from_vacc are ordinal, typically ranging from 1 to 5. These features exhibit multimodal distributions, reflecting varying public beliefs on vaccine safety, effectiveness, and illness risk.

Household Variables:
Features like household_adults and household_children show right-skewed distributions, with most households having fewer members. Large households are relatively rare in the dataset.

Skewness and Modeling Impact:
The strong skewness in binary and ordinal variables indicates potential class imbalance. This can influence model training and should be considered during preprocessing and model selection (e.g. using class weights)

### C) Relationship between Categorical Features and Target

<img width="579" height="517" alt="image" src="https://github.com/user-attachments/assets/983e7673-0269-4750-98e4-b9de1883d08f" />


The chart above highlights differences in H1N1 vaccination rates across age groups:

The 55–64 age group recorded the highest vaccination rate, with approximately 24–25% of individuals receiving the vaccine.

This was closely followed by the 65+ age group at around 22–23%.

In comparison, younger groups — 18–34, 35–44, and 45–54 — showed lower and relatively uniform vaccination rates, all clustered around 19–20%.

These trends suggest that older adults were more likely to get vaccinated, possibly due to greater perceived vulnerability to illness or more frequent interaction with healthcare services.

## Modelling 

I Used the following models :

**1.** **Logistic Regression**  -  I have selected Logistic regression as the baseline model due to it's interpretability and simplicity. It provides a good starting point to understand how well the preprocessed data can predict H1N1 vaccination uptake. 

**2.**  **Logistic Regression(Balanced)** - By applying the class_weight='balanced' method which helps to address class imbalance by penalizing mistakes on the minority class more heavily, which often leads to better recall on people who received vaccine.

**3.** **Random Forest Classifier** - Helps improve prediction performance with imbalanced classes (more people did not get vaccinated than those who did).

### Top 10 Feature Importance Analysis

<img width="984" height="584" alt="image" src="https://github.com/user-attachments/assets/517ea9cb-9005-4d1e-9430-b1e9665a6acb" />


* The most influential factors driving H1N1 vaccination includes Doctor's recommendation, Perceived personal risk and Belief in vaccine effectiveness -These highlight the importance of trust in medical advice and confidence in the vaccine.

* Fear of side effects and larger household size are linked to lower vaccination rates, suggesting potential areas of hesitancy.

## Evaluation

These model's performance was evaluated using the following classification metrics ROC-AUC score , F1 score, Accuracy, Precision, Confusion Matrix and Recall.

### Classification Report Summary 

**1.** **Logistic Regression (Balanced)** - This model achieved the best recall of 72%, effectively identifying most individuals who received the H1N1 vaccine. While it had lower precision, resulting in more false positives, this trade-off is acceptable when the goal is to avoid missing actual vaccinated cases. It also delivered a higher F1-score, indicating a strong balance between precision and recall. Additionally, the model attained a better ROC AUC, demonstrating a more reliable ability to distinguish between vaccinated and non-vaccinated individuals across all classification thresholds.

**2.** **Random Forest Classifier** - It achieved higher overall accuracy, largely by correctly classifying the majority class (those not vaccinated). However, it suffers from lower recall for class 1, meaning it fails to identify many vaccinated individuals. On the positive side, it has higher precision, indicating that when it predicts someone is vaccinated, it’s usually correct. Despite this, the model shows a lower F1-score and slightly lower ROC AUC, reflecting a less balanced performance and weaker ability to distinguish between the two classes compared to the logistic regression model.

| Model                          | Accuracy | Precision | Recall | F1 Score | ROC AUC |
| ------------------------------ | -------- | --------- | ------ | -------- | ------- |
| Logistic Regression (Balanced) | 0.78     | 0.54      | 0.72   | 0.62     | 0.83    |
| Random Forest                  | 0.83     | 0.71      | 0.37   | 0.49     | 0.82    |



### ROC Curve Comparison 

<img width="784" height="584" alt="image" src="https://github.com/user-attachments/assets/11d1df66-86e5-4603-872f-91bd0dd42abe" />


### Model Evaluation Summary 

After evaluating individual metrics, Logistic Regression (Balanced) demonstrates stronger recall and F1 performance, making it suitable for minimizing false negatives. This advantage is further supported by the ROC Curve analysis, where it achieves a slightly higher AUC (0.83 vs. 0.82) compared to Random Forest. Though both models perform well, Logistic Regression maintains a better balance between identifying vaccinated individuals and overall classification reliability.

## Conclusion 

* **Balanced Logistic Regression** is the more effective model for identifying vaccinated individuals, achieving a strong recall of 72%. This makes it especially suitable for public health applications, where understanding and promoting vaccine uptake is crucial. Despite slightly lower accuracy, its balanced performance across recall, precision, and ROC AUC makes it a reliable and interpretable choice for behavior modeling.

* **Random Forest** delivers higher overall accuracy and precision but falls short in recalling vaccinated individuals (37%). While it offers useful insights through feature importance, its lower sensitivity limits its practical value for outreach or intervention strategies.

**Final takeaway:** When the primary objective is to identify vaccinated individuals and inform public health decisions, **Balanced Logistic Regression** is the preferred model.

## Recommendations

1. **Adopt Balanced Logistic Regression as the primary model**:
   - Offers stronger recall, F1 score, and AUC—essential for accurately identifying vaccinated individuals.
   - Effectively manages class imbalance while remaining transparent and interpretable.
   - Best aligned with public health objectives focused on maximizing outreach and driving vaccine adoption.
   

2. **Use Random Forest as a complementary model**:
   - Valuable for uncovering complex feature interactions.
   - Useful in exploratory analysis and model validation stages.

**In Summary** Logistic Regression should drive decision-making, while Random Forest supports deeper insights.
