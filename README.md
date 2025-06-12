
# 📊 Multivariate Analysis of Socioeconomic and Educational Factors Influencing Student Performance in Bangladesh

## Abstract

Understanding the multifactorial influences on student academic performance is crucial for developing evidence-based educational policies. While innate ability contributes to academic success, socioeconomic and educational factors play substantial roles. This study investigates how parental education, employment, family size, geographic location, study time, attendance, tutoring, extracurricular activities, and internet access influence academic outcomes among secondary school students in Bangladesh. The Knowledge Discovery in Databases (KDD) framework was employed, involving selection, preprocessing, transformation, data mining, and interpretation phases. A structured dataset was extracted from Kaggle, followed by thorough data cleaning, outlier treatment, feature engineering, and multivariate classification using Decision Tree, Random Forest, and Support Vector Machine models. The Decision Tree classifier demonstrated superior performance with 77.7% accuracy, identifying academic group, study time, and attendance as the most significant predictors. The findings contribute to the educational data mining literature and offer practical implications for policymakers and educational institutions in tailoring targeted academic interventions.

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
- The dataset was obtained from Kaggle’s Bangladesh Student Performance EDA repository. The data integrates school records and student survey responses.

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

Interpretaion: Most variables have very few outliers, except for age, which has 129 outliers. Ages like 10 and 24 are quite unusual for secondary students.
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
Two derived variables were generated to facilitate classification tasks:
- The Total Score was computed as the sum of five subject scores, represented mathematically as:
  
![image](https://github.com/user-attachments/assets/34d4f799-d723-405c-9ceb-ebb8bf22b2b3)

where _Si_ represents the score for each (English, Mathematics, Science, Social Science, and Art & Culture).
- The Performance Category was created using the 20th and 80th percentiles to ensure balanced class sizes

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

| Variable         | Mean  | Std. Dev | Min  | Max  |
|-------------------|-------|----------|------|------|
| English Score     | 58.0  | 19.0     | 0    | 100  |
| Math Score        | 55.0  | 21.0     | 0    | 100  |
| Science Score     | 53.0  | 20.0     | 0    | 100  |
| Social Science    | 60.0  | 16.0     | 0    | 100  |
| Art & Culture     | 65.0  | 17.0     | 0    | 100  |
| Total Score       | 291.0 | 65.0     | 54   | 500  |
| Study Time (hrs)  | 4.2   | 1.8      | 0    | 10   |
| Attendance (%)    | 80.0  | 15.0     | 0    | 100  |
| Age (years)       | 16.5  | 1.7      | 13   | 20   |
| Family Size       | 5.0   | 1.5      | 1    | 10   |

*Note: N = 8,608 student records.*

_Table 1: Descriptive Statistics of Student Performance Variables_

Table 1 summarizes the key continuous variables. Subject scores showed moderate variation, with averages ranging from 53 to 65 out of 100. Total Score averaged 291, reflecting the combined subject scores. Study Time varied widely, with some students reporting no study time, while others studied up to 10 hours daily. Attendance also ranged from full absence to perfect attendance. Age and family size showed typical distributions for secondary school students.













