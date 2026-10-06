<<<<<<< HEAD
# Task 2 – Support Ticket Topic Classification

## Project Overview

This project focuses on classifying support documents into different topic categories using Machine Learning and Natural Language Processing (NLP).

The dataset contains support-related documents and their corresponding topic groups. The objective is to build a classification model that can automatically identify the topic of a given support document.

## Dataset

The dataset contains **47,837 records** and two columns:

- `Document` – Text content of the support request/document
- `Topic_group` – Target category of the document

### Target Classes

The dataset contains the following topic groups:

- Hardware
- HR Support
- Access
- Miscellaneous
- Storage
- Purchase
- Internal Project
- Administrative rights

There are no missing values in the dataset.

## Data Preprocessing

The following preprocessing steps were performed:

1. Loaded the dataset using Pandas.
2. Checked the dataset dimensions and data types.
3. Checked for missing values.
4. Examined the distribution of the target classes.
5. Separated the input feature (`Document`) and target variable (`Topic_group`).
6. Split the dataset into training and testing sets.

## Feature Extraction

Since the input data consists of text, **TF-IDF (Term Frequency-Inverse Document Frequency)** was used to convert text documents into numerical features.

TF-IDF gives higher importance to words that are useful for distinguishing between different documents while reducing the importance of very common words.

The trained TF-IDF vectorizer was saved separately as:

```text
tfidf_vectorizer.joblib
```

## Machine Learning Models

Two classification algorithms were trained and evaluated:

1. **Naive Bayes**
2. **Logistic Regression**

These models were selected because they are commonly used for text classification and work effectively with TF-IDF features.

## Model Evaluation

The models were evaluated using the following metrics:

- Accuracy
- Precision
- Recall
- F1-Score
- Confusion Matrix

Weighted averaging was used for Precision, Recall, and F1-Score because the dataset contains multiple classes with different numbers of samples.

## Model Comparison

The performance of both models was compared using a DataFrame containing Accuracy, Precision, Recall, and F1-Score.

| Model | Accuracy | Precision | Recall | F1-Score |
|---|---:|---:|---:|---:|
| Naive Bayes | Add result | Add result | Add result | Add result |
| Logistic Regression | Add result | Add result | Add result | Add result |

The confusion matrices were also generated to understand the classification performance of each model across the different topic groups.

## Best Model

After comparing the evaluation metrics, the model with the best overall performance was selected as the final model.

The selected model was saved using Joblib:

```text
best_model.joblib
```

The corresponding TF-IDF vectorizer was also saved:

```text
tfidf_vectorizer.joblib
```

These files allow the trained model and text preprocessing pipeline to be reused without retraining the model.

## Project Structure

```text
FUTURE_ML_01/
│
├── data/
│   └── dataset.csv
│
├── models/
│   ├── best_model.joblib
│   └── tfidf_vectorizer.joblib
│
├── notebooks/
│   └── task2.ipynb
│
└── README.md
```
=======
# Sales & Demand Forecasting for Businesses

## Future Interns — ML Task 1

### Project Overview

This project focuses on building a machine learning system for **sales analysis and demand forecasting** using historical business data.

The project uses the **Superstore dataset**, which contains information about orders, products, customers, regions, quantities, discounts, sales, and profits.

The main goal is to understand historical sales patterns, identify important business factors affecting sales, apply machine learning models, evaluate their performance, and present the results in a business-friendly way.

---

## Business Problem

Businesses need accurate sales information to make better decisions about:

- Inventory planning
- Cash flow management
- Staffing
- Product planning
- Regional sales strategies
- Avoiding overstocking
- Identifying high-performing products and regions

This project uses historical sales data to understand these patterns and build machine learning models that can predict sales based on available business information.

---

## Objectives

The main objectives of this project are:

1. Clean and prepare historical sales data.
2. Convert order dates into useful time-based features.
3. Analyze monthly sales trends.
4. Analyze seasonal sales patterns.
5. Identify important business factors related to sales.
6. Prepare features for machine learning.
7. Train a Linear Regression model.
8. Train a Random Forest Regression model.
9. Evaluate the models using MAE, RMSE, and R².
10. Compare model performance.
11. Visualize actual and predicted sales.
12. Generate business-friendly insights from the analysis.

---

## Dataset

The project uses the **Superstore dataset**.

### Dataset Size

- Records: **9,994**
- Columns: **21**

### Original Columns

```text
Row ID
Order ID
Order Date
Ship Date
Ship Mode
Customer ID
Customer Name
Segment
Country
City
State
Postal Code
Region
Product ID
Category
Sub-Category
Product Name
Sales
Quantity
Discount
Profit
```

---
>>>>>>> 53e918ff62bd37ced76792e5ea7bc8e0f00c3bd7

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
<<<<<<< HEAD
- Joblib
- Jupyter Notebook

## Conclusion

This project demonstrates an NLP-based multi-class classification system for automatically categorizing support documents.

TF-IDF was used for text feature extraction, followed by Naive Bayes and Logistic Regression classification models. The models were evaluated using multiple performance metrics and confusion matrices. The better-performing model was selected and saved as a Joblib file for future use.
=======
- Jupyter Notebook
- GitHub

---

## Project Workflow

```text
Superstore Dataset
        ↓
Data Cleaning
        ↓
Date Conversion
        ↓
Time-Based Feature Creation
        ↓
Monthly Business Aggregation
        ↓
Feature Selection
        ↓
Categorical Encoding
        ↓
Time-Based Train/Test Split
        ↓
Linear Regression
        ↓
Random Forest Regression
        ↓
Model Evaluation
        ↓
Model Comparison
        ↓
Sales Trend Analysis
        ↓
Seasonality Analysis
        ↓
Business Insights
```

---

## 1. Data Loading and Cleaning

The dataset was loaded using Pandas.

Because the original CSV file contained a non-UTF-8 character, `latin1` encoding was used while loading the dataset.

```python
data = pd.read_csv("superstore.csv", encoding="latin1")
```

The `Order Date` column was converted into a datetime format:

```python
data["Order Date"] = pd.to_datetime(data["Order Date"])
```

Time-based features were then created:

```text
Year
Month
Month_Name
```

The dataset was also checked for missing values and basic statistical information.

---

## 2. Monthly Sales Analysis

The historical transaction data was aggregated by:

```text
Year
Month
Category
Region
```

The following business metrics were calculated:

- Quantity → total quantity sold
- Discount → average discount
- Profit → total profit
- Sales → total sales

A previous-month sales feature was also created for each Category and Region combination.

```text
Previous_Month_Sales
```

This allowed the model to use historical sales information as an input.

---

## 3. Machine Learning Features

The following features were selected as model inputs:

```text
Quantity
Discount
Profit
Category
Region
Month
Previous_Month_Sales
```

### Target Variable

```text
Sales
```

Therefore:

```text
X = Business and time-based features
y = Sales
```

---

## 4. Categorical Encoding

`Category` and `Region` contain categorical values.

Machine learning models require numerical input, so these columns were converted using **One-Hot Encoding**.

```python
OneHotEncoder(handle_unknown="ignore")
```

A Scikit-learn `ColumnTransformer` and `Pipeline` were used so that preprocessing and model training could be handled together.

---

## 5. Train/Test Split

Since this project deals with time-based sales data, the dataset was **not randomly shuffled**.

The earlier observations were used for training, while the later observations were used for testing.

```text
Earlier Data → Training
Later Data   → Testing
```

This approach better represents a real forecasting scenario because the model should learn from historical information and be evaluated on later information.

---

# 6. Machine Learning Models

Two regression models were implemented.

## Linear Regression

Linear Regression was used as the first baseline machine learning model.

```python
LinearRegression()
```

The model learns the relationship between the selected business features and sales.

---

## Random Forest Regression

A Random Forest Regressor was also implemented.

```python
RandomForestRegressor(
    n_estimators=200,
    random_state=42
)
```

Random Forest can capture more complex relationships between business features and sales than a simple linear model.

---

# 7. Model Evaluation

The models were evaluated using three metrics.

### Mean Absolute Error (MAE)

MAE measures the average absolute difference between actual and predicted sales.

Lower MAE indicates better performance.

### Root Mean Squared Error (RMSE)

RMSE gives more importance to larger prediction errors.

Lower RMSE indicates better performance.

### R² Score

R² measures how well the model explains the variation in sales.

A value closer to 1 generally indicates better performance.

---

## 8. Model Comparison

The performance of Linear Regression and Random Forest Regression was compared using:

```text
MAE
RMSE
R²
```

The model with lower prediction errors and better overall performance was selected as the better-performing model for the tested dataset.

---

## 9. Actual vs Predicted Sales

The project visualizes actual sales against predicted sales for the testing period.

This visualization helps understand how closely the machine learning model follows the real sales values.

```text
Actual Sales
      vs
Predicted Sales
```

If the two lines are close to each other, the model is making relatively accurate predictions.

---

# 10. Sales Trend Analysis

Monthly sales were analyzed across the complete historical period.

This helps identify:

- Overall sales growth or decline
- High-sales periods
- Low-sales periods
- Changes in sales over time

A monthly sales trend graph was created using Matplotlib.

---

# 11. Seasonality Analysis

Average sales were calculated for each month of the year.

This helps identify recurring seasonal patterns in the business.

For example:

```text
January → Average Sales
February → Average Sales
March → Average Sales
...
December → Average Sales
```

The highest and lowest average-sales months were also identified.

This information can help businesses prepare inventory and resources for high-demand and low-demand periods.

---

# 12. Business Analysis

Additional analysis was performed to identify:

### Category Performance

Total sales were calculated for each product category.

This helps identify which categories contribute most to overall sales.

### Regional Performance

Total sales were calculated for each region.

This helps identify high-performing and low-performing geographical markets.

### Business Metrics

The project also calculates:

- Total Sales
- Average Monthly Sales
- Highest Sales
- Lowest Sales

These metrics provide a simple overview of the business performance.

---

# Important Forecasting Consideration

The machine learning model uses:

```text
Quantity
Discount
Profit
Category
Region
Month
Previous_Month_Sales
```

to predict:

```text
Sales
```

The historical evaluation demonstrates how these business factors can be used to predict sales for later observations in the available dataset.

However, for a genuine future forecast, future values of variables such as `Quantity`, `Discount`, and `Profit` may not be known beforehand.

Therefore, these variables should not be artificially generated just to produce future predictions.

A production forecasting system could instead:

- Forecast sales using historical sales and time-based features.
- Forecast future business variables separately.
- Use planned future values for variables such as discounts.
- Build separate forecasting models for relevant business segments.

This distinction keeps the forecasting system realistic and avoids using information that would not actually be available at prediction time.

---

# Key Business Benefits

This project demonstrates how machine learning can support business decision-making by helping organizations:

- Understand sales trends
- Identify seasonal patterns
- Compare product categories
- Compare regional performance
- Estimate sales based on business factors
- Evaluate prediction accuracy
- Support inventory planning
- Improve resource planning
- Reduce potential overstocking

---

# Project Structure

```text
FUTURE_ML_01/
│
├── data/
│   └── superstore.csv
│
├── notebooks/
│   └── sales_forecasting.ipynb
│
├── README.md
│
└── requirements.txt
```

---

# Requirements

Install the required Python libraries using:

```bash
pip install pandas numpy matplotlib scikit-learn jupyter
```

Or install them from `requirements.txt`:

```bash
pip install -r requirements.txt
```

---

# How to Run

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
```

### 2. Open the project

```bash
cd FUTURE_ML_01
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Open Jupyter Notebook

```bash
jupyter notebook
```

### 5. Open the forecasting notebook

Run the notebook cells in order to reproduce the analysis, model training, evaluation, visualizations, and business insights.

---

# Conclusion

This project demonstrates an end-to-end machine learning workflow for sales analysis and forecasting.

Historical Superstore data was cleaned and transformed into meaningful time-based and business-level information. Linear Regression and Random Forest Regression were trained and evaluated using chronological train/test data.

The project also analyzes sales trends, seasonality, category performance, and regional performance to make the results understandable from a business perspective.

The combination of **machine learning, time-based analysis, and business insights** provides a practical foundation for developing more advanced sales forecasting systems.

---

## Future Improvements

The project can be further improved by:

- Implementing dedicated time-series forecasting models such as ARIMA or SARIMA.
- Using advanced forecasting models.
- Adding automated future-month forecasting.
- Creating interactive dashboards using Power BI or Tableau.
- Performing hyperparameter tuning.
- Adding more detailed category-level forecasting.
- Adding regional demand forecasting.
- Deploying the model as a web application or API.
- Monitoring model performance over time.
>>>>>>> 53e918ff62bd37ced76792e5ea7bc8e0f00c3bd7
