# Maritime Ship Detention Forecasting

This project focuses on the development of machine learning models for the prediction of ship detentions.

In this work, vessel data from the year **2023** were used. An extensive review of the relevant literature was conducted in order to identify the most appropriate features to retain, as well as the algorithms that perform effectively on datasets characterized by severe class imbalance.

The repository includes the notebook **EDA_ships.ipynb**, which presents the full process of data cleaning, preprocessing, and detailed exploratory data analysis of the original dataset **paper_2023.xlsx**. Executing this notebook produces the final dataset **final_cleaned_dataset.csv**, which is then used by the predictive models developed in **models.ipynb**. Since the grid search procedure performed in *models.ipynb* is computationally expensive and time-consuming, the optimized models have been saved in **grid_search_final_results.joblib** to allow experimentation and evaluation of the final results without repeating the full optimization process.

The models tested include multiple combinations of under-sampling, over-sampling, and ensemble sampling techniques, alongside experiments with deep learning approaches. After extensive experimentation and parameter tuning — particularly for the neural network — the best-performing model was obtained using **Random Undersampling** combined with **Logistic Regression**, achieving:

- **Class 0 (Not Detained / Healthy):** Precision: 99.7% | Recall: 89.0%  
- **Class 1 (Detained / High-Risk):** Precision: 25.8% | Recall: 93.0%

## Threshold Optimization & Risk Justification

To align the model with critical operational priorities — specifically maximizing the detection of high-risk vessels — decision threshold optimization was applied to the selected Logistic Regression model. A custom probability threshold of **0.4568** was strategically selected. This adjustment intentionally sacrifices part of Precision in order to achieve a high Recall (93%) for the minority class.

Although this trade-off increases the False Positive rate — meaning some compliant vessels may undergo unnecessary inspections or operational delays — the model remains operationally reliable. From a risk management perspective, this is a necessary and acceptable compromise. The delay caused by inspecting a healthy vessel is significantly less severe than the potential consequences of a False Negative, which could involve loss of human life and irreversible environmental damage caused by allowing a substandard vessel to operate.
