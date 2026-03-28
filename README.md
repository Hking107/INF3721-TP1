# World Bank Income Classification - Data Science Project

## Academic Context
This project was carried out as part of the course:

**INF372 – Supervised and Unsupervised Learning**  
Department of Computer Science  
University of Yaoundé I

The objective is to automatically build a dataset from World Bank economic indicators and prepare it for machine learning models.

---

##  Project Objectives

- Scrape economic indicators for all countries
- Build a structured dataset
- Handle missing values
- Encode target variable
- Prepare data for Machine Learning
- Classify countries based on **Income_Group**

---

## Data Source

World Bank Open Data:

https://donnees.banquemondiale.org/pays

For each country:
- 1516 economic indicators
- Year used: **2023**
- Target class: **Income_Group**

---

##  Dataset Description

| Feature | Description |
|---------|-------------|
| Observations | 216 Countries |
| Indicators | 1516 |
| Identifier | Country Code |
| Target | Income_Group |
| Total Columns | ≈ 1518 |

---

##  Data Science Pipeline

### 1. Data Scraping
- Automatic download via World Bank API
- ZIP extraction
- Organization per country

### 2. Dataset Construction
- Selection of 2023 indicators
- Pivot transformation
- Merge all countries
- Add `Income_Group`

### 3. Data Preprocessing
- Keep missing values
- Median imputation by income group
- Global median imputation
- Encode target variable

### 4. Dataset Ready for ML
- Numeric features
- No critical missing values
- Encoded target

---

##  Project Structure
