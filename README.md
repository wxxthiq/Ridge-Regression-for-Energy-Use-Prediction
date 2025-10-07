# 💡 Ridge Regression for Energy Use Prediction

This project was developed as part of the **Foundations of Machine Learning** assignment for the **MSc in Advanced Computer Science program at The University of Manchester**.

This repository contains a Jupyter Notebook that demonstrates the application of Ridge Regression to predict the energy consumption of appliances in a building. The project uses a dataset containing temperature and humidity measurements from various sensors, along with weather data, to build a regularized linear model.

---

## 📖 Dataset

The dataset, `energy_use.csv`, consists of time-series data collected over a period of 4.5 months. It includes 29 features, such as:
- **`Appliances`**: The target variable, representing the total energy consumed by appliances in Wh.
- **`T1`, `RH_1` ... `T9`, `RH_9`**: Temperature and humidity readings from sensors placed in various rooms of the house.
- **`T_out`, `RH_out`**: Temperature and humidity measured outside the building.
- **`Windspeed`, `Visibility`, `Press_mm_hg`**: Weather data from a nearby airport station.

### Data Pre-processing:
- The `date` and `lights` columns were dropped from the feature set.
- The data was split into a training set and a testing set.
- **Feature Scaling**: `StandardScaler` was applied to normalize the features, ensuring that all variables contribute equally to the model's performance.

---

## ⚙️ Analysis and Modeling

The core of this project is the implementation and tuning of a Ridge Regression model.

### 1. Ridge Regression (L2 Regularization)

Ridge Regression is a regularized linear regression model that adds a penalty term (L2 norm) to the loss function. This helps to prevent overfitting by shrinking the model's coefficients towards zero without eliminating them entirely.

* **Objective**: To find a balance between fitting the training data well and keeping the model's coefficients small to improve generalization to unseen data.

### 2. Hyperparameter Tuning with GridSearchCV

To find the optimal regularization strength (`alpha`, also known as lambda), `GridSearchCV` was used with 5-fold cross-validation.

* **Methodology**:
    * A range of `alpha` values (`[0.1, 1, 10, 100, 1000]`) was tested.
    * The model was trained and evaluated for each `alpha` using cross-validation on the training set.
    * The `alpha` that yielded the best average R-squared score was selected as the optimal hyperparameter.
* **Result**: The best `alpha` value was determined to be **100**.

### 3. Model Evaluation

The performance of the Ridge Regression model was evaluated using the R-squared (R²) score, which measures the proportion of the variance in the target variable that is predictable from the features.

* **Key Findings**:
    * As the `alpha` value increased, the R-squared score on the **training set decreased**. This is expected, as stronger regularization reduces the model's ability to fit the training data perfectly.
    * The R-squared score on the **testing set initially increased** with `alpha`, peaking at the optimal value of 100, and then began to decrease. This demonstrates how regularization helps to reduce overfitting and improve the model's performance on unseen data.
    * The final model, with `alpha=100`, achieved an **R-squared score of approximately 0.105** on the testing set.

---

## 💡 Conclusion

This project successfully illustrates the practical application of Ridge Regression for a real-world prediction task. It highlights the importance of hyperparameter tuning through cross-validation to control model complexity and prevent overfitting. The analysis shows that while a simple linear model may have limitations in capturing all the variance in a complex dataset like energy consumption, regularization is a powerful technique for building more robust and generalizable models.

---

## 🛠️ Technologies Used

* **Python**
* **Pandas**: For data loading and manipulation.
* **Scikit-learn**: For implementing Ridge Regression (`Ridge`), hyperparameter tuning (`GridSearchCV`), and data preprocessing (`StandardScaler`, `train_test_split`).
* **Matplotlib**: For plotting the R-squared scores against different alpha values.
* **Jupyter Notebook**: As the environment for conducting the analysis.
