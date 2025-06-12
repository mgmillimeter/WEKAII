  
# 📊 Multivariate Analysis of Socioeconomic and Educational Factors Influencing Student Performance in Bangladesh

## Abstract

Student academic performance is shaped by a complex interaction of socioeconomic, educational, and behavioral factors. This study applies a multivariate data mining approach to examine how these variables jointly influence secondary school student performance in Bangladesh. Using the Knowledge Discovery in Databases (KDD) framework, the research involved data selection, preprocessing, transformation through feature engineering and one-hot encoding, followed by model development and evaluation. A publicly available dataset from Kaggle was analyzed using three machine learning classification algorithms: Decision Tree (J48), Random Forest, and Support Vector Machine (SVM). Among the models, Random Forest achieved the highest classification accuracy (77.95%), followed by SVM (77.57%) and Decision Tree (75.78%). Across all models, academic track (Science or Commerce), study time, and attendance consistently emerged as the strongest predictors of academic performance, while variables such as extracurricular activities, parental involvement, and internet access contributed more modestly. Parental education and employment showed limited direct influence in the models. The findings offer both theoretical contributions to educational data mining literature and practical insights for designing targeted interventions that support student learning through academic engagement and behavioral support.

## Keywords

Student Performance, Socioeconomic Factors, Educational Data Mining, Knowledge Discovery in Databases, Bangladesh Education, Machine Learning.

---

## I. INTRODUCTION

Understanding the multifactorial influences on student academic performance is crucial for developing evidence-based educational policies. While innate ability contributes to academic success, socioeconomic and educational factors play substantial roles. This study investigates how parental education, employment, family size, geographic location, study time, attendance, tutoring, extracurricular activities, and internet access influence academic outcomes among secondary school students in Bangladesh. The Knowledge Discovery in Databases (KDD) framework was employed, involving selection, preprocessing, transformation, data mining, and interpretation phases. A structured dataset was extracted from Kaggle, followed by thorough data cleaning, outlier treatment, feature engineering, and multivariate classification using Decision Tree, Random Forest, and Support Vector Machine models. The Decision Tree classifier demonstrated superior performance with 77.7% accuracy, identifying academic group, study time, and attendance as the most significant predictors. The findings contribute to the educational data mining literature and offer practical implications for policymakers and educational institutions in tailoring targeted academic interventions.

## 1.1 Background and Problem Statement

Academic performance is widely regarded as a multidimensional outcome shaped by numerous interacting factors. Beyond cognitive ability, research highlights the role of external determinants such as socioeconomic status (SES), parental education, school environment, and student habits in influencing learning outcomes (Sirin, 2005; OECD, 2019). These factors are particularly significant in developing countries, where educational inequalities often mirror broader socioeconomic disparities. Bangladesh, like many developing nations, faces challenges in ensuring equitable access to quality education. Policymakers and educators require evidence-based insights to better understand how various social, familial, and institutional factors influence student achievement. Despite numerous studies investigating individual influences, limited research explores the combined, multivariate effects of these variables. Therefore, adopting multivariate analytical approaches becomes essential to reveal complex interdependencies often missed by traditional univariate methods.

## 1.2 Existing Literature

Previous studies have consistently found strong links between parental education and student achievement (Coleman et al., 1966; Sirin, 2005). Hanushek and Woessmann (2011) emphasized that family background heavily influences school readiness and learning outcomes. Moreover, Romero and Ventura (2010) highlighted the emerging role of educational data mining as an effective tool to model such complex educational phenomena. Other studies have examined the impact of school-level variables like school type, attendance, and tutoring availability (OECD, 2019). For example, Siemens and Baker (2012) demonstrated how learning analytics can be applied to uncover patterns in student engagement and performance. However, few studies have simultaneously examined the interaction of multiple socioeconomic, demographic, and institutional variables on academic success within the Bangladeshi educational context.

## 1.3 Research Objectives

The primary objectives of this study are:
1. To analyze how socioeconomic and educational factors influence student academic performance.
2. To examine the combined effects of parental education, employment, family size, study habits, school type, attendance, and extracurricular participation.
3. To apply multivariate classification techniques using the KDD process to extract meaningful patterns.

## 1.4 Research Significance

This study provides actionable insights for educators, administrators, and policymakers seeking to improve academic outcomes through data-informed interventions. By adopting a multivariate perspective, the study advances both academic literature and practical applications in educational data mining, contributing to more targeted, evidence-based policy formulation in Bangladesh.

---

## II. Methodology

The study follows the Knowledge Discovery in Databases (KDD) framework, which consists of five systematic steps to extract meaningful knowledge from complex data sources.

## 2.1 Selection (Data Collection)

**Dataset Overview:** The table below details the attributes included in the analysis:

| Attribute Name | Type | Description |
| :----------------------------- | :------- | :---------------------------------------------------------------------- |
| `id` | String | Unique identifier (removed during cleaning) |
| `full_name` | String | Student's full name (removed during cleaning) |
| `age` | Numeric | Age of the student |
| `gender` | Nominal | Gender of the student (Male/Female) |
| `location` | Nominal | Geographic region (Urban, City, Rural) |
| `family_size` | Numeric | Number of family members |
| `mother_education` | Nominal | Mother's highest education level |
| `father_education` | Nominal | Father's highest education level |
| `mother_job` | Nominal | Whether the mother is employed (Yes/No) |
| `father_job` | Nominal | Whether the father is employed (Yes/No) |
| `guardian` | Nominal | Primary guardian (Father, Mother, Other) |
| `parental_involvement` | Nominal | Parental involvement in studies (Yes/No) |
| `internet_access` | Nominal | Access to internet at home (Yes/No) |
| `studytime` | Numeric | Hours spent studying per day |
| `tutoring` | Nominal | Whether the student has private tutoring (Yes/No) |
| `school_type` | Nominal | Type of school (Government, Semi-Govt, Private) |
| `attendance` | Numeric | Attendance percentage |
| `extra_curricular_activities` | Nominal | Participation in extracurricular activities (Yes/No) |
| `english` | Numeric | Score in English subject |
| `math` | Numeric | Score in Mathematics |
| `science` | Numeric | Score in Science subject |
| `social_science` | Numeric | Score in Social Science subject |
| `art_culture` | Numeric | Score in Arts & Culture subject |
| `stu_group` | Nominal | Academic group (Science, Arts, Commerce) |

1. Data Source
- While the dataset offers valuable insight into student performance patterns in Bangladesh, it was obtained from a publicly available Kaggle repository. The exact sampling frame, geographic coverage, and institutional types represented in the dataset are not fully specified. As a result, the sample may not perfectly reflect the full diversity of Bangladesh’s national secondary education system, including regional variations (urban vs rural), types of institutions (public, private, madrasah), or socioeconomic strata.

Furthermore, since some variables may rely on student or parental self-reports (e.g. parental education, employment, internet access), minor reporting inaccuracies or recall bias may exist.

2. Variables of Interest
- Dependent Variables: Academic subject scores (English, Math, Science, Social Science, Art & Culture), Total Score, and derived Performance Category (Low, Average, High).
- Independent Variables: Socioeconomic and educational factors, including parental education, parental job, family size, location, study time, attendance, tutoring, extracurricular activities, internet access, guardian type, and student group.

3. Data Extraction
- File type: CSV (Comma-Separated Values); Extraction method: Direct download; Sample size: 8,608 student records (after cleaning).

## 2.2 Preprocessing (Data Cleaning)

1. Missing Values
- Only one missing value was identified (in location).
  
Action Taken:
- filled missing location with "Urban" (the most common value in dataset).

2. Duplicate and Inconsistent Records
- No duplicate rows detected.

Action Taken:
- Inconsistencies in categorical values (e.g., Hons vs. Honors, urban vs. Urban) were standardized.

3. Outliers
- Outlier detection applied using the Interquartile Range (IQR method, 1.5 × IQR rule). The Interquartile Range (IQR) method detects outliers by measuring data spread. Calculate the IQR (Q3 - Q1) and set lower/upper bounds at **Q1 - 1.5×IQR** and **Q3 + 1.5×IQR**. Data points outside these bounds are flagged as outliers. A simple, robust rule for identifying extreme values in skewed or non-normal distributions.

_Table 1: Quantified summary of outliers detected using the IQR (Interquartile Range) method_

| Variable         | Normal | Outlier |
| ---------------- | ------ | ------- |
| `english`        | 8610   | 1       |
| `math`           | 8609   | 2       |
| `science`        | 8611   | 0       |
| `social_science` | 8611   | 0       |
| `art_culture`    | 8610   | 1       |
| `attendance`     | 8611   | 0       |
| `age`            | 8482   | 129     |

Interpretation: Most variables have very few outliers, except for age, which has 129 outliers. Ages like 10 and 24 are quite unusual for secondary students.
Majority of "outliers" are simply 19 years old, which seems acceptable.

Actions Taken:
- Keep 19-year-old records — likely valid senior secondary students.
- Remove extreme age outliers: Remove rows where age < 13 or age > 20 — beyond the typical secondary education range.
- For other variables (english, math, art_culture): The number of outliers is negligible (1–2 records).

_Table 2: Detecting Outlier Summary_

| Description                         | Count |
| ----------------------------------- | ----- |
| Original Rows                       | 8611  |
| Rows Removed (Extreme Age Outliers) | 3     |
| Final Rows After Cleaning           | 8608  |

- Only 3 records had extreme ages (below 13 or above 20) and were removed.
- All other outliers in subject scores were retained since they were minimal and likely reflect genuine performance.

4. Normalization
- Normalization was not applied because the selected models (such as Decision Trees and Random Forests) are not sensitive to the scale or range of the input values. These algorithms make decisions based on data splits rather than mathematical distances, allowing them to handle variables with different units or magnitudes without requiring normalization.
  
## 2.3 Transformation (Feature Engineering)
1. Derived Variables
To enhance the dataset for predictive modeling, two key derived variables were created:

Total Score (total_score):
This variable represents the student’s overall academic performance, calculated by summing the scores across five subjects:
  
![image](https://github.com/user-attachments/assets/34d4f799-d723-405c-9ceb-ebb8bf22b2b3)

where _Si_ corresponds to the score in one of the individual subjects.
- Performance Category (performance_category):
  
To convert the continuous total scores into discrete classes suitable for classification tasks, the 20th and 80th percentiles of the total score distribution were used as cut-off points:

- Low Performance: total score ≤ 20th percentile

- Average Performance: total score > 20th percentile and < 80th percentile

- High Performance: total score ≥ 80th percentile

This method helps ensure that each category contains a sufficient and relatively balanced number of cases. Using percentiles also accounts for the data's actual distribution, rather than applying arbitrary fixed thresholds, which improves both the interpretability and performance of classification models.

2. Encoding
- Categorical variables, such as parental education, guardian type, and school group, were converted into numerical format using One-Hot Encoding to allow machine learning algorithms to process them effectively. This technique creates separate binary columns for each category, preserving all available information without introducing artificial ranking. Since the number of features remained reasonable after encoding, dimensionality reduction was not necessary, allowing the models to consider all relevant factors during analysis.

3. Dimensionality Reduction
- Dimensionality reduction techniques were not applied since the total number of features remained relatively small and manageable. Retaining all available variables allowed the models to consider as much information as possible without risking overfitting or excessive computational complexity.

## 2.4 Data Mining (Pattern Extraction)
1. Models Applied:
- Three classification algorithms were implemented to predict student performance: Decision Tree, Random Forest, and Support Vector Machine (SVM). These models were selected to provide a balance between interpretability (Decision Tree), robustness (Random Forest), and non-linear classification capabilities (SVM).

2. Evaluation:
- An 80/20 stratified train-test split was applied to maintain class proportions across both training and testing sets. Model performance was evaluated using accuracy and F1-score to capture both overall correctness and performance across all classes. Feature importance was extracted from tree-based models to identify key predictors contributing to student performance outcomes.

## 2.5 Interpretation & Evaluation
- The Decision Tree model identified Academic Group, Study Time, and Attendance as the most influential predictors of student performance. Model performance was validated through comparison across multiple classifiers, demonstrating consistent results. Visualizations, including decision trees and feature importance plots, were generated to enhance interpretability and support the understanding of key patterns within the data.

---

## 3. Results and Discussion
3.1 Results Presentation

3.1.1 Descriptive Statistics

_Table 1: Descriptive Statistics of Student Performance Variables_

| Variable         | Mean   | Std. Dev | Min | Max |
| ---------------- | ------ | -------- | --- | --- |
| English Score    | 73.61  | 15.35    | 18  | 100 |
| Math Score       | 72.94  | 15.82    | 33  | 100 |
| Science Score    | 73.52  | 15.12    | 33  | 100 |
| Social Science   | 74.47  | 14.95    | 36  | 100 |
| Art & Culture    | 76.24  | 13.62    | 36  | 100 |
| Total Score      | 370.78 | 67.73    | 220 | 489 |
| Study Time (hrs) | 4.75   | 2.19     | 1   | 16  |
| Attendance (%)   | 74.03  | 13.29    | 30  | 100 |
| Age              | 16.62  | 0.96     | 15  | 19  |
| Family Size      | 4.50   | 1.66     | 0   | 11  |


*Note: N = 8,608 student records.*

The dataset reflects generally strong academic performance, with average subject scores clustered in the mid-70s. Total scores ranged widely, indicating variability in overall academic achievement. Study time averaged nearly 5 hours per day, while attendance rates averaged 74%, suggesting room for improvement in classroom participation. The student population primarily consisted of individuals aged 15 to 19, with typical family sizes of 4 to 5 members.

3.1.2 Correlation Analysis

The correlation analysis showed that study time had a strong positive relationship with total score (r = 0.84), indicating that increased study hours are closely linked to better academic performance. Attendance also demonstrated a moderate positive correlation with total score (r = 0.49), suggesting that regular class participation contributes meaningfully to student achievement.

![correlation_heatmap](https://github.com/user-attachments/assets/d91d9766-21da-4ba1-9b15-10fc335780d0)

_Figure 1: Correlation Analysis_

3.1.3 Model Performance

_Table 2: Classification Model Performance Summary_

| Model               | Accuracy |
| -----------------   | ------   |
| J48 Decision Tree   | 75.78    |
| Random Forest       | 77.95    |
| SVM                 | 77.57    |

All three models performed well, with Random Forest achieving the highest accuracy (77.95%), followed by SVM (77.57%) and J48 (75.78%). Random Forest’s ensemble approach captured complex patterns more effectively, while SVM handled non-linear relationships. Despite slightly lower accuracy, J48 offers interpretable rules useful for practical decision-making.

_Table 3: Random Forest Classification Performance (Per Class)_

| Class             | Precision  | Recall     | F1-Score   |
| ----------------- | ---------- | ---------- | ---------- |
| High              | 0.6670     | 0.8359     | 0.7419     |
| Average           | 0.8914     | 0.7190     | 0.7960     |
| Low               | 0.6829     | 0.9029     | 0.7776     |
| **Macro Average** | **0.7471** | **0.8193** | **0.7718** |

The Random Forest model performed well, especially in identifying low-performing students with 90% recall, which is useful for early interventions. It was most accurate for average performers (89% precision), but slightly overestimated some high performers (67% precision). With a macro F1-score of 77%, the model strikes a good balance between catching at-risk students and correctly classifying stronger ones.

3.1.4 Feature Importance

_Table 4: Top Predictive Features_

| Rank | Attribute                         | InfoGain | Importance (%) |
| ---- | --------------------------------- | -------- | -------------- |
| 1    | `studytime`                       | 0.610647 | **35.55%**     |
| 2    | `stu_group_Science`               | 0.460502 | **26.82%**     |
| 3    | `stu_group_Commerce`              | 0.330212 | **19.23%**     |
| 4    | `attendance`                      | 0.225069 | **13.11%**     |
| 5    | `location_city`                   | 0.017566 | 1.02%          |
| 6    | `mother_education_Hons`           | 0.009069 | 0.53%          |
| 7    | `school_type_Semi_Govt`           | 0.009032 | 0.53%          |
| 8    | `age`                             | 0.008335 | 0.49%          |
| 9    | `location_urban2`                 | 0.007677 | 0.45%          |
| 10   | `school_type_Private`             | 0.006769 | 0.39%          |

The most influential predictors of student performance are studytime, stu_group, and attendance, indicating that academic habits and chosen academic track strongly affect outcomes. Socio-demographic variables contribute only marginally to performance prediction.

3.1.5 Statistical Validation of Key Features

_Table 5: Chi-Square Ranking & Test (Categorical vs Class)_

| Feature    | Chi² Statistic | p-value |
| ---------- | -------------- | ------- |
| stu\_group | 8120.55        | 0.000   |

_Table 6: ANOVA (Numerical vs Class)_

| Feature    | F-Statistic | p-value |
| ---------- | ----------- | ------- |
| studytime  | 4533.19     | 0.000   |
| attendance | 830.89      | 0.000   |

To strengthen the validity of the identified key predictors, statistical tests were conducted. A Chi-square test confirmed a strong association between academic track (stu_group) and performance category (χ² = 8120.55, p < 0.001). ANOVA further demonstrated that both study time (F = 4533.19, p < 0.001) and attendance (F = 830.89, p < 0.001) have significant effects on academic performance. These statistical results provide additional confirmation that study habits, academic track selection, and class attendance are highly influential in determining student achievement, consistent with the machine learning model outputs.

3.2 Discussion Based on the KDD Process

Step 1: Selection (Data Collection)
- An important limitation of the present study is the potential sample bias due to the unknown representativeness of the Kaggle dataset. While the internal data quality was carefully addressed through cleaning and preprocessing, external generalizability requires caution. Future studies could benefit from nationally representative, government-sourced educational data to validate these findings across broader student populations.

Step 2: Preprocessing (Data Cleaning)
- Data cleaning addressed missing values, inconsistencies, and outliers to ensure reliability. Mode imputation was used for categorical missing values, while unrealistic age values were filtered out. Categorical variables were converted into numerical format through one-hot encoding to prepare the data for machine learning algorithms.

Step 3: Transformation (Feature Engineering)
- A new target variable, performance category, was created to group students based on academic performance levels, facilitating multi-class classification. After encoding, the number of features remained manageable, and no dimensionality reduction was necessary.

Step 4: Data Mining (Key Findings from Analysis)
- Three classification algorithms were applied: Decision Tree (J48), Random Forest, and Support Vector Machine (SVM). Among them, Random Forest achieved the highest accuracy (77.95%), followed closely by SVM (77.57%) and J48 (75.78%). Feature importance analysis using Information Gain identified studytime, academic group, and attendance as the most influential predictors of student performance. In contrast, many socioeconomic factors such as parental education, job status, and family size contributed minimally to prediction accuracy.

Step 5: Interpretation & Evaluation

- The findings highlight that students’ study habits, choice of academic track, and consistent attendance play a more significant role in academic success than most background characteristics. Educational interventions focusing on improving study discipline, academic guidance, and attendance monitoring may yield meaningful improvements in student outcomes. However, limitations include the restricted scope of available features, the absence of psychological or motivational factors, and potential sample bias. Future research may benefit from more comprehensive datasets and the integration of additional variables to capture a fuller picture of academic performance drivers.

- It is important to note that the identified relationships reflect predictive associations rather than definitive causal effects. For example, high-performing students may naturally study more or attend classes more consistently, introducing possible reverse causality. While the models effectively highlight which variables are most strongly linked to academic outcomes, they cannot confirm that modifying these factors alone will improve performance. Longitudinal or experimental research designs may better establish causal relationships.

- Regarding socioeconomic status (SES), parental education, employment, and family background showed limited predictive power in this study. One possible reason is that the dataset may have contained limited SES variability, as most students belonged to broadly similar socioeconomic backgrounds without extreme income disparities. Additionally, educational behaviors such as study time and attendance may have had a more immediate and direct impact on academic outcomes compared to background SES characteristics. Indirect effects of SES may exist but were not strongly detected within this sample.
  
## 4. Conclusion

- This study examined the combined influence of socioeconomic and educational factors on the academic performance of secondary school students in Bangladesh using the Knowledge Discovery in Databases (KDD) framework. By applying three machine learning classification models—Decision Tree, Random Forest, and Support Vector Machine—key predictors of student performance were identified. Among these, study time, academic track (Commerce or Science), and attendance emerged as the most influential factors across models, while extracurricular participation, parental involvement, and guardianship showed smaller but positive effects. Parental education, occupation, and other demographic variables demonstrated limited direct predictive power. These findings provide actionable insights for educators and policymakers seeking to design targeted interventions. The multivariate, data-driven approach applied here contributes to the growing field of educational data mining, highlighting the potential of predictive modeling to inform student-centered educational policies.

## 5. Recommendations

For Educational Institutions and Policymakers

- Interventions should prioritize students in Commerce tracks who exhibit lower study time and poor attendance. Programs that strengthen study habits and time management may help improve academic outcomes. Attendance monitoring systems should be reinforced to promote consistent school participation. Schools may also consider expanding extracurricular activities to increase student engagement, while actively involving parents in supporting their children's academic progress.

For Future Research

- Future research should aim to work with larger and more representative datasets that better capture students across different regions, school types, and socioeconomic backgrounds in Bangladesh. This would help improve the generalizability of the findings and ensure that conclusions apply to a wider population. Incorporating additional variables such as psychological factors (e.g., motivation, stress, learning habits, and emotional well-being) may provide deeper insights into non-academic influences on student performance that were not captured in this study.

Moreover, applying more advanced data analysis techniques — such as deep learning models, ensemble approaches, or hybrid methods — could potentially improve the accuracy and depth of predictions. Longitudinal studies, which follow students over time, may also reveal how academic performance evolves and how early interventions affect long-term outcomes. Finally, cross-country or regional comparisons could help determine whether the observed patterns are specific to Bangladesh or reflect broader global trends in education.



