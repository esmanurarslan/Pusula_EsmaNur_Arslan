# Esma Nur Arslan
# esmanurarslan2016@gmail.com

# Pusula Talent Academy: Data Science Intern Case Study

## 1. Project Overview

This project involves the exploratory data analysis (EDA) and preprocessing of a physical medicine and rehabilitation dataset. The primary goal is to prepare the data for predictive modeling, with the target variable being `TedaviSuresi` (Treatment Duration in Sessions). The process includes data cleaning, in-depth analysis, feature engineering, and encoding to create a model-ready dataset. This project does not involve building a predictive model but focuses entirely on making the data clean, consistent, and analyzable.

---

## 2. Dataset

The dataset consists of 2235 observations and 13 features:

* **HastaNo**: Anonymized patient ID.
* **Yas**: Age.
* **Cinsiyet**: Gender.
* **KanGrubu**: Blood type.
* **Uyruk**: Nationality.
* **KronikHastalik**: Chronic conditions (comma-separated list).
* **Bolum**: Department/Clinic.
* **Alerji**: Allergies (single or comma-separated).
* **Tanilar**: Diagnoses.
* **TedaviAdi**: Treatment name.
* **TedaviSuresi**: Treatment duration in sessions (The Target Variable).
* **UygulamaYerleri**: Application sites.
* **UygulamaSuresi**: Application duration per session in minutes.

---

## 3. Methodology

The project followed a structured pipeline to transform the raw data into a machine-learning-ready format.

1.  **Initial Data Cleaning**:
    * Column names were standardized to a consistent format (e.g., `HastaNo` -> `hasta_no`).
    * Redundant text like "Seans" and "Dakika" was removed from numerical columns, which were then converted to integer types.
    * A total of 928 duplicate rows were identified and removed.
    * All string-based features were converted to lowercase to ensure consistency.

2.  **Exploratory Data Analysis (EDA)**:
    * The distributions of categorical variables like `Cinsiyet`, `KanGrubu`, and `Uyruk` were analyzed and visualized.
    * Numerical features (`Yas`, `TedaviSuresi`, etc.) were examined for their distributions, correlations, and potential outliers using histograms, box plots, and a correlation heatmap.

3.  **Feature Engineering & Advanced Cleaning**:
    * **Complex Text Features**: Columns with comma-separated values (`KronikHastalik`, `Alerji`, `Tanilar`, `UygulamaYerleri`) were systematically cleaned by splitting text, standardizing terminology, and correcting typos.
    * **Diagnosis Grouping**: A key feature, `SGK_Tani_Grubu`, was created. **This was not a random grouping; diagnoses were systematically classified into clinically relevant groups (A, B, C, D) based on the official ICD-10 Physical Therapy and Rehabilitation Diagnosis List (EK-4/D).** This ensures a standardized, domain-specific approach.
    * **Treatment Name Standardization**: The `TedaviAdi` column was heavily processed using regular expressions to standardize names, extract directionality (e.g., right, left, bilateral), and correct abbreviations.

4.  **Handling Missing Values**:
    * Missing values in `Alerji` and `KronikHastalik` were filled with "Yok" (None).
    * Missing `Cinsiyet` and `KanGrubu` were filled with "Bilinmiyor" (Unknown).
    * Missing `UygulamaYerleri` were imputed based on information from the cleaned `TedaviAdi` column.

5.  **Data Preparation for Modeling**:
    * The dataset was split into training (80%) and testing (20%) sets **before** any encoding to prevent data leakage.
    * A variety of encoding techniques were applied:
        * **One-Hot Encoding**: Used for low-cardinality features.
        * **Multi-Label Binarization**: Applied to list-based features like `KronikHastalik`.
        * **One-Hot and Target Encoding**: Used on the `Bolum` feature.
        * **BERT Embeddings & HDBSCAN**: An advanced NLP approach was used for `TedaviAdi` to group semantically similar treatments.

---

 **Dependencies**:
  *Key libraries include: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `transformers`, `hdbscan`.*

