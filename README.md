# 📊 Methodology

This project followed a structured approach based on the **Knowledge Discovery in Databases (KDD)** process. The workflow included data selection, cleaning, transformation, modeling, and result interpretation. All data manipulation was performed using **Microsoft Excel** and **WEKA 3.8.6**.

---

## 📁 Data Collection and Selection

The dataset used was `bd_students_per_uncleaned.csv`, containing student information including academic scores, demographics, and family background. Initial exploration was conducted to understand structure and identify irrelevant attributes.

### 🧾 Original Dataset Attributes

| Attribute | Description |
| --------- | ----------- |
| `id` | Unique student identifier (removed) |
| `full_name` | Student's full name (removed) |
| `age` | Age of the student |
| `gender` | Male or Female |
| `location` | Urban, City, or Rural |
| `family_size` | Number of household members |
| `mother_education` / `father_education` | Parental education levels |
| `mother_job` / `father_job` | Parental employment status (Yes/No) |
| `guardian` | Guardian type (Father, Mother, Other) |
| `parental_involvement` | Active academic involvement (Yes/No) |
| `internet_access` | Internet availability (Yes/No) |
| `studytime` | Daily study hours |
| `tutoring` | Private tutoring (Yes/No) |
| `school_type` | Private, Semi-Govt, Govt |
| `attendance` | Attendance percentage |
| `extra_curricular_activities` | Participation in activities (Yes/No) |
| `stu_group` | Academic group (Science, Arts, Commerce) |
| `subject1`–`subject5` | Scores across five subjects |

---

## 🧹 Data Cleaning and Preprocessing

Data cleaning was performed in Microsoft Excel. Key actions included:

| Step | Action | Purpose |
|------|--------|---------|
| Remove Irrelevant Columns | Dropped `id`, `full_name` | Non-predictive |
| Handle Missing Values | Removed 1 row with missing `location` | Prevent bias from imputation |
| Remove Duplicates | Deleted 315 duplicate rows | Avoid skewed results |
| Standardize Categories | Fixed label issues (e.g., "urban" → "Urban") | Ensure consistency |
| Fix Column Names | Corrected encoding (e.g., `Ã¥ge` → `age`) | Prevent confusion |

> ⚠️ Challenge: `location` had inconsistent entries such as "urban", "city", etc. These were manually standardized in Excel.

---

## 🛠️ Feature Engineering

Two new attributes were introduced:

1. **`overall_avg_score`**: Average of subject1–subject5
2. **`performance_category`**: Categorized into:
   - **Low**: Bottom 33.3%
   - **Medium**: Middle 33.3%
   - **High**: Top 33.3%

This enabled a clearer classification of student performance.

---

## 🧪 Dataset Preparation for Modeling

A refined dataset was prepared for use with classification models such as **J48** and **Apriori** in WEKA.

### ✅ Final Dataset Modifications

- **Target Variable**: `performance_category`
- **Removed**: `overall_avg_score` (to avoid data leakage)
- **Binned Attributes**: Converted numeric fields like `studytime` and `attendance` into Low, Medium, High categories

---

## 🤖 Modeling and Evaluation

### 🌳 J48 Decision Tree

- **Tool**: WEKA 3.8.6  
- **Validation**: 10-fold cross-validation  
- **Accuracy**: **96.08%**

**Insights from the model:**
- Science students with >5 hours of study excelled.
- Arts students with ≤3.5 hours tended to perform poorly.
- High attendance boosted performance regardless of study time.

> 📌 Visualization Note: WEKA does not export decision trees as images. The tree text was copied and visualized using [WebGraphviz](https://dreampuf.github.io/GraphvizOnline).

---

### 📐 Apriori Association Rule Mining

The Apriori algorithm identified strong correlations and patterns in the data.

**Example Rules:**
- Low study time + Arts group → Low performance (**99% confidence**)
- High study time + Science group → High performance (**98–99% confidence**)

These rules supported the decision tree findings and provided interpretable insights for educators.

---

## 🧩 Summary of Methodological Choices

| Method | Purpose | Reason for Selection |
|--------|---------|----------------------|
| **J48** | Predict performance | Offers clear, interpretable decision paths |
| **Apriori** | Discover patterns | Reveals frequent attribute combinations |

By combining both models, the analysis provided:
- **Predictive power** (via J48)
- **Actionable patterns** (via Apriori)

These findings are valuable for educators, school leaders, and policy makers aiming to support student success.

---


# 📊 Student Performance Analysis Project

This project analyzes academic performance patterns using **Knowledge Discovery in Databases (KDD)** methodology, implemented with WEKA 3.8.6 and Excel. It includes classification (J48 Decision Tree) and association rule mining (Apriori).

## 📂 Dataset
**Original File**: `bd_students_per_uncleaned.csv`  
**Processed File**: `students_cleaned.csv` ([Download](link_to_processed_data))  

### Key Attributes
| Attribute | Type | Description | Preprocessing |
|-----------|------|-------------|---------------|
| `studytime` | Numeric | Daily study hours | Binned (Low/Med/High) |
| `stu_group` | Nominal | Science/Arts/Commerce | Label standardized |
| `performance_category` | Nominal | Low/Medium/High | Derived from subject averages |

## 🛠️ Methodology
### Data Preprocessing
1. Removed duplicates (315 rows) and irrelevant columns (`id`, `full_name`)
2. Handled missing values (1 row)
3. Created new features:
   - `overall_avg_score` (average of 5 subjects)
   - `performance_category` (target variable)

### Models
| Model | Tool | Purpose | Key Result |
|-------|------|---------|------------|
| J48 Decision Tree | WEKA | Performance prediction | 96.08% accuracy |
| Apriori | WEKA | Pattern mining | Strong rules (e.g., Arts+LowStudy→LowPerformance) |

## 📊 Results
### J48 Decision Tree Insights
- Science students studying >5 hrs/day → High performance (98% accuracy)
- Low attendance (<70%) → 89% chance of Low performance

### Top Association Rules
1. `studytime ≤ 3.5h` + `Arts group` → `Low performance` (99% confidence)
2. `internet_access=Yes` + `tutoring=Yes` → `High performance` (91% confidence)

## 📁 Repository Structure

