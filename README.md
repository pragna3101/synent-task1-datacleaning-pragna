# Task 1: Titanic Dataset Data Cleaning & Preprocessing

This repository contains my submission for **Task 1** of the Synent Technologies Data Science Internship Program.

## 📌 Problem Statement
Raw, real-world datasets are often messy, incomplete, and inconsistently formatted. In machine learning, a model's predictive power is heavily bounded by the quality of the input data ("garbage in, garbage out"). 

The objective of this project is to take the messy, raw Titanic dataset and perform extensive data cleaning and preprocessing to prepare it for high-accuracy exploratory analysis and predictive machine learning models. 

---

## 📊 Dataset Details
* **Dataset Name**: Titanic - Machine Learning from Disaster
* **Source**: [Kaggle Titanic Competition](https://www.kaggle.com/c/titanic/data)
* **Dataset Shape**: 891 rows, 12 columns
* **Target Variable**: `Survived` (0 = Deceased, 1 = Survived)
* **Key Features**: PassengerId, Pclass, Name, Sex, Age, SibSp, Parch, Ticket, Fare, Cabin, Embarked

---

## 🛠️ Approach
Our data cleaning pipeline consists of the following structured engineering steps:
1. **Initial Inspection**: Profiles the dataset to map types, non-null counts, and statistical descriptions.
2. **Null Value Analysis**: Identifies and quantifies missing data. Highlights missingness in `Age` (19.9%), `Cabin` (77.1%), and `Embarked` (0.2%). Visualized missing distributions via a Seaborn heatmap.
3. **Handling Missing Values**:
   * **Embarked**: Filled the 2 missing records with the mode (`'S'`).
   * **Age**: Imputed missing ages using the median age of the group they belonged to based on Passenger Class (`Pclass`) and `Sex`. This avoids shifting overall demographic structures.
   * **Cabin**: Since over 77% of this feature is null, we dropped the high-noise original column. However, to preserve socio-economic status information, we created a binary flag `has_cabin` (1 if Cabin was present, 0 otherwise).
4. **Data Type Casting**: Cast categorical traits (`survived`, `pclass`, `sex`, `embarked`) to pandas `category` and rounded and cast `age` to `int` for cleaner analytics.
5. **Column Renaming**: Renamed all raw CamelCase columns to standard snake_case conventions.
6. **Outlier Detection & Strategy**: Used the Interquartile Range (IQR) method to find outliers. Boxplots revealed extreme fares. We logically decided to *retain* socioeconomic outliers (high fares paid by 1st class passengers) as they are real historical data highly correlated with survival.
7. **Clean Export**: Saved the clean, modeled dataset to `output/cleaned_titanic.csv`.

---

## 📈 Results
* **Imputed & Complete Schema**: Reduced missing values from 866 to **0**.
* **Cleaned Dataset**: [cleaned_titanic.csv](output/cleaned_titanic.csv) is successfully generated and exported.
* **Saved Visualizations**:
  * Heatmap of missing values: `images/missing_values_heatmap.png`
  * Boxplot outlier study: `images/outliers_boxplot.png`
  * Distribution histogram: `images/distribution_plots.png`
* **Key Finding**: Keeping socioeconomic outliers in `fare` is crucial; first-class passengers who paid premium fares showed dramatically higher survival rates.

---

## 🎥 Video Walkthrough
A complete video demonstration of the project structure, code walk-through, and results in Visual Studio Code is included:
* **Video File**: [task1_walkthrough.mp4](task1_walkthrough.mp4)

---

## 💻 Tech Stack
* **Language**: Python
* **Libraries**: Pandas, NumPy, Matplotlib, Seaborn, Jupyter Notebook
