\# ✈️ Flight Fare Prediction



\## 📌 Project Overview



Flight ticket prices can vary significantly depending on factors such as airline, journey date, duration, number of stops, route, departure time, and destination.



The objective of this project is to develop a \*\*Machine Learning regression model\*\* that can predict flight ticket prices based on these travel-related features.



Multiple regression algorithms were trained and evaluated, followed by lightweight hyperparameter tuning of the best-performing model.



\---



\## 🎯 Problem Statement



To build a machine learning model that predicts the price of a flight ticket using information such as:



\* Airline

\* Source

\* Destination

\* Route

\* Total Stops

\* Journey Date

\* Departure Time

\* Arrival Time

\* Duration



The model can help understand the factors influencing flight fares and provide reasonably accurate price predictions.



\---



\## 📂 Dataset



The dataset contains flight booking information and the target variable \*\*Price\*\*.



\### Dataset Summary



\* Original records: \*\*10,683\*\*

\* Duplicate records removed: \*\*220\*\*

\* Final records: \*\*10,462\*\*

\* Original features: \*\*11\*\*

\* Target variable: \*\*Price\*\*



The target variable represents the flight ticket price.



\---



\## 🔧 Data Preprocessing



The following preprocessing steps were performed:



1\. Loaded the dataset from an Excel file.

2\. Checked the dataset structure and data types.

3\. Removed duplicate records.

4\. Checked for missing values.

5\. Filled missing values in `Route` and `Total\_Stops`.

6\. Converted `Total\_Stops` into numerical values.

7\. Extracted useful information from journey and time-related columns.

8\. Created `Duration\_Minutes`.

9\. Created `Route\_Count`.

10\. Applied One-Hot Encoding to categorical variables.

11\. Applied feature scaling where required for KNN.

12\. Split the data into training and testing datasets.



\### Train-Test Split



\* Training data: \*\*8,369 records\*\*

\* Testing data: \*\*2,093 records\*\*



\---



\## 📊 Exploratory Data Analysis



Exploratory Data Analysis was performed to understand the distribution and relationships within the dataset.



Some key observations:



\* Most flight prices are concentrated approximately between \*\*₹3,000 and ₹15,000\*\*.

\* The `Price` variable is right-skewed.

\* Flight duration has a positive relationship with flight price.

\* Duration showed a correlation of approximately \*\*0.50\*\* with Price.

\* Departure and arrival hours showed relatively weak correlation with Price.

\* Outliers were identified in both Price and Duration.



The identified outliers were analyzed and retained where appropriate because they may represent genuine high-priced flights or long-duration journeys.



\---



\## 🤖 Machine Learning Models



The following regression models were trained and evaluated:



1\. Linear Regression

2\. Decision Tree Regressor

3\. Random Forest Regressor

4\. Gradient Boosting Regressor

5\. KNN Regression



The models were evaluated using:



\* Mean Absolute Error (MAE)

\* Mean Squared Error (MSE)

\* Root Mean Squared Error (RMSE)

\* R² Score



\---



\## 📈 Model Performance



| Model             |       MAE |      RMSE |     R² |

| ----------------- | --------: | --------: | -----: |

| Linear Regression | ₹1,999.99 | ₹2,945.72 | 0.5838 |

| Decision Tree     | ₹1,448.46 | ₹2,493.32 | 0.7018 |

| Random Forest     | ₹1,213.79 | ₹1,989.51 | 0.8102 |

| Gradient Boosting | ₹1,546.57 | ₹2,278.11 | 0.7511 |

| KNN Regression    | ₹1,412.20 | ₹2,193.91 | 0.7692 |



\### 🏆 Best Original Model



The \*\*Random Forest Regressor\*\* performed best among the original models, achieving:



\* \*\*MAE:\*\* ₹1,213.79

\* \*\*RMSE:\*\* ₹1,989.51

\* \*\*R²:\*\* 0.8102



\---



\## ⚙️ Hyperparameter Tuning



After comparing the models, hyperparameter tuning was performed on the Random Forest model using `RandomizedSearchCV`.



A lightweight tuning approach was used to reduce computational requirements.



\### Best Parameters



```text

n\_estimators = 100

max\_depth = 15

min\_samples\_split = 5

min\_samples\_leaf = 1

max\_features = sqrt

```



\### Tuned Random Forest Performance



\* \*\*MAE:\*\* ₹1,304.36

\* \*\*MSE:\*\* 3,942,047.66

\* \*\*RMSE:\*\* ₹1,985.46

\* \*\*R²:\*\* 0.8109



The tuning resulted in a small improvement in R², RMSE, and MSE, while MAE increased slightly.



Based on the overall R², RMSE, and MSE, the \*\*Tuned Random Forest\*\* was selected as the final model.



\---



\## 🔍 Feature Importance



Feature importance analysis was performed using the final tuned Random Forest model.



The most important features were:



1\. \*\*Duration\_Minutes\*\*

2\. \*\*Total\_Stops\*\*

3\. \*\*Journey\_Day\*\*

4\. \*\*Route\_Count\*\*

5\. \*\*Jet Airways\*\*

6\. \*\*Jet Airways Business\*\*

7\. \*\*Journey\_Month\*\*

8\. \*\*Arrival\_Hour\*\*

9\. \*\*IndiGo\*\*

10\. \*\*Dep\_Hour\*\*



The results indicate that journey characteristics, number of stops, route information, airline, and travel timing play important roles in predicting flight fares.



Feature importance represents the model's predictive contribution and does not necessarily imply a direct causal relationship.



\---



\## 📉 Error Analysis



The final Tuned Random Forest model achieved:



| Metric |        Value |

| ------ | -----------: |

| MAE    |    ₹1,304.36 |

| MSE    | 3,942,047.66 |

| RMSE   |    ₹1,985.46 |

| R²     |       0.8109 |



\### Interpretation



\* \*\*MAE of ₹1,304.36:\*\* On average, the predicted fare differs from the actual fare by approximately ₹1,304.

\* \*\*RMSE of ₹1,985.46:\*\* Larger prediction errors have a greater influence on this metric.

\* \*\*R² of 0.8109:\*\* The model explains approximately \*\*81.09% of the variation in flight fares\*\*.



\---



\## 💾 Saved Model Files



The final trained model and preprocessing object were saved using `joblib`.



\### Model



```text

flight\_fare\_tuned\_random\_forest.pkl

```



\### Preprocessor



```text

flight\_fare\_preprocessor.pkl

```



The preprocessor is saved separately because new input data must undergo the same preprocessing steps before being passed to the trained model.



\---



\## 📁 Project Structure



```text

Flight-Fare-Prediction/

│

├── Flight\_Fare\_Prediction.ipynb

├── Flight\_Fare.xlsx

├── PRCP-1025-FlightPricePrediction.docx

├── flight\_fare\_tuned\_random\_forest.pkl

└── flight\_fare\_preprocessor.pkl

```



\---



\## 🛠️ Technologies Used



\* Python

\* Pandas

\* NumPy

\* Matplotlib

\* Scikit-learn

\* Joblib

\* Jupyter Notebook



\---



\## 🏁 Final Conclusion



The Flight Fare Prediction project successfully developed a machine learning model to predict flight ticket prices using journey, airline, timing, route, and stop-related features.



After evaluating multiple regression algorithms and performing hyperparameter tuning, the \*\*Tuned Random Forest Regressor\*\* was selected as the final model. It achieved an \*\*R² score of 0.8109\*\* and an \*\*RMSE of ₹1,985.46\*\*.



Feature importance analysis showed that \*\*Duration\_Minutes, Total\_Stops, Journey\_Day, Route\_Count, airline, and timing-related features\*\* were among the most influential variables.



Overall, the results demonstrate that the Tuned Random Forest model can effectively capture complex relationships between flight characteristics and ticket prices and can provide reasonably accurate flight fare predictions.



