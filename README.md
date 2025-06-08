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

### In simple terms: J48 tells us how to predict student performance, like a step-by-step decision flow, while Apriori shows us strong patterns that often happen together, like “students who study less and are in the Arts group usually perform poorly.”

So, while J48 answers “How can we classify students?”, Apriori answers “What common traits do low or high performers share?”

Together, they give a fuller picture:

J48 = prediction and structure

Apriori = patterns and insights

This supports your objective to understand what affects student performance and how different traits are connected.



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





------------------------------------------------------------------

# Decision Tree Explanation

---

## 🎯 Objective Recap:

> To understand **what factors influence student performance** in secondary education in Bangladesh — especially **socioeconomic**, **educational**, and **personal factors** — so that **interventions** and **policies** can be better designed.

---

## 🌳 Decision Tree: Layman's Explanation (Top-Level Rules)

Your decision tree works like a **smart guide** that classifies students as **High**, **Medium**, or **Low** performers by asking **a series of questions** about their background and behavior.

Here’s how it works, step by step:

---

### 🔹 1. **What academic group is the student in?**

* If the student is in the **Arts** group →
  🎯 They are most likely to be **Low performers**.

> This tells us: Students in the Arts track may need **more academic support or engagement strategies**, possibly due to fewer academic resources or lower perceived difficulty levels.

---

### 🔹 2. **If they’re in the Science or Commerce group**, we ask:

> **How much time do they spend studying?**

* If they study **more than 5 hours a day** →
  🎯 They are likely to be **High performers**.

> So, **study time** is a very strong predictor of success — more time spent learning clearly correlates with better results.

---

### 🔹 3. **If they study 5 hours or less**, we ask:

> **How often do they attend school?**

* If their **attendance is high (above 91%)** →
  🎯 They still have a good chance of being **High performers**.

* If their **attendance is low (91% or less)** →
  We look deeper...

---

### 🔹 4. Next, we ask:

> **Does the student come from a very small family?**

* If **yes (family size = 0)** →
  🎯 They are more likely to be **Low performers** (likely due to lack of support system).

* If **not**, we ask about the **type of school**.

---

### 🔹 5. **School Type Matters:**

* Students from **Private schools** →
  🎯 More likely to be **High performers**

* Students from **Government schools** →
  Performance depends on **father’s education**:

  * If father finished **SSC (10th grade)** → 🎯 Likely **High performer**
  * If father finished **HSC (12th grade)** → 🎯 Likely **Medium performer**

> This shows that **family background**, especially **parental education**, still plays a role — particularly in government schools.

---

## 💡 What This All Means in Simple Terms:

* Students in **Arts** need **more academic support**
* **Study time** is the strongest single factor for performance
* **Attendance** also strongly affects performance, even when study time is low
* **Family support and parental education** still matter — especially for students in public schools

---

## 📝 Recommendation for Stakeholders (Based on Tree):

* **Encourage more daily study time** — it’s the most reliable predictor of success.
* **Track attendance** as an early warning signal.
* **Support students in the Arts group** with tutoring, engagement, or academic resources.
* In **Government schools**, increase parental engagement and mentorship — especially where parental education is low.

---


