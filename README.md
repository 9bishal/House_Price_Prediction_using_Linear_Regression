# House_Price_Prediction_using_Linear_Regression
A Machine Learning project that predicts house prices using Linear Regression. This model analyzes real estate data to estimate home values based on various factors. Built with Python, Pandas, Scikit-Learn, and Matplotlib.


Sure Bishal! Here's a clean and professional version of your `README.md` without excessive hashtags. It’s formatted in a way that looks great on GitHub:

---

**Bangalore House Price Prediction**

This project aims to predict the **price of residential properties** in Bangalore based on user inputs such as location, square footage, number of bathrooms, and number of bedrooms (BHK). It uses a machine learning model trained on real housing data.

---

**Dataset Overview**

The original dataset included the following columns:
- `location`
- `total_sqft`
- `bath`
- `bhk`
- `price`

---

**Data Cleaning and Preprocessing**

To ensure the model's accuracy, the dataset was cleaned through the following steps:

- **Missing Values**: Removed rows with missing values in key columns such as location, sqft, bath, or price.
- **Non-Numeric Square Foot Values**: Handled values like "2100 - 2850" by averaging and removed non-convertible strings like "34.46Sq. Meter".
- **Outlier Removal**: 
  - Removed data where `price per sqft` was abnormally high/low.
  - Removed entries where BHK was too high for the given area.
  - Removed properties where `bath` count was more than `BHK + 2`.
- **Location Simplification**: Combined rare locations (with less than 10 data points) into a single `'other'` category.
- **One-Hot Encoding**: Applied dummy variables for location to convert categorical data into numerical format and dropped the `'other'` column to avoid multicollinearity.

---

**Feature Engineering**

The final features used in the model were:
- `total_sqft`
- `bath`
- `bhk`
- Dummy variables for location (excluding 'other')

---

**Model Building and Selection**

Three regression models were tested using cross-validation:
- Linear Regression
- Lasso Regression
- Decision Tree Regressor

Using `GridSearchCV`, the best performing model was selected based on accuracy.

**Selected Model**: Linear Regression  
**Model Accuracy**: Approximately 84% (based on testing)

---

**Prediction Function**

A custom prediction function was created to estimate house prices:

```python
def predict_price(location, sqft, bath, bhk):
    loc_index = np.where(x.columns == location)[0]
    x_input = np.zeros(len(x.columns))
    x_input[0] = sqft
    x_input[1] = bath
    x_input[2] = bhk
    if len(loc_index) > 0:
        x_input[loc_index[0]] = 1
    return lr_clf.predict([x_input])[0]
```

**Example Usage:**

```python
predict_price('BTM Layout', 1200, 2, 2)
# Output: Approximate price in lakhs
```

---

**Handling Unknown Locations**

If the input location is not present in the training data, the prediction is made using other available features (sqft, bath, BHK). The location won’t contribute in such a case, but the model still gives a reasonable estimate.

---

**Summary**

- Cleaned and prepared real-world housing data
- Removed outliers and invalid entries
- Applied feature engineering and encoding
- Used GridSearchCV to choose the best model
- Created a working price prediction function

---

Let me know if you'd like me to include any charts, graphs, or a deployment guide as well!
