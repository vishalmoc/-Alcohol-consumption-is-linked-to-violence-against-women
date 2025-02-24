# -Alcohol-consumption-is-linked-to-violence-against-women

Data from the National Family Health Survey (NFHS) suggests a correlation between men's alcohol consumption and increased violence against women. Analysis Report on the Impact of Men's Alcohol Consumption on Women's Violence

Objective: 
The goal of this analysis is to investigate the relationship between men’s alcohol consumption and its impact on women’s safety—particularly in terms of spousal violence, physical violence during pregnancy, and sexual violence at a young age.

Dependent Variable (Target):
Men_Alcohol_Consumption (%): Proportion of men (age 15+) consuming alcohol.

Independent Variables (Predictors):
Spousal_Violence (%): Ever-married women (18-49) who experienced spousal violence.
Physical_Violence_Pregnancy (%): Women (18-49) who faced physical violence during pregnancy.
Sexual_Violence_Young (%): Young women (18-29) who experienced sexual violence by age 18.
Women_Bank_Account (%): Women (15-49) having and using a bank/savings account.
Female_Education (%): Female population (6+ years) who ever attended school.

Preliminary Data Cleaning and Transformation
✅ Handling Missing Values
Non-numeric values were converted to NA, and missing values were removed.
✅ Correlation Check
A correlation matrix was generated to check for highly correlated variables, as strong correlations may cause multicollinearity in regression models.
✅ Multicollinearity Check (VIF Analysis) VIF (Variance Inflation Factor) was computed to identify independent variables with high collinearity (>5). "Female_Education" was removed due to its high correlation with other predictors, reducing redundancy.

Modeling Approaches and Findings
1. Linear Regression Model
The first model was a multiple linear regression, where all independent variables were used to predict men’s alcohol consumption.
The model summary output helped check which predictors were statistically significant (p < 0.05).
Insignificant variables were dropped, and a refined model was created.
Final Linear Regression Model:
Significant predictors: Spousal Violence, Physical Violence during Pregnancy
Removed variables: Sexual Violence (p > 0.05), Women Bank Account (p > 0.05)
R² value indicates how much variation in alcohol consumption is explained by predictors.
RMSE (Root Mean Squared Error) was used to measure model error.
2. Decision Tree Model
A Decision Tree (CART) model was built to account for non-linearity in relationships.
The tree graphically identifies the most important factors affecting alcohol consumption.
RMSE for Decision Tree was higher than Linear Regression, indicating possible overfitting.
3. Random Forest Model
A Random Forest model (500 trees) was built to reduce overfitting and improve prediction accuracy.
Feature importance was plotted, showing Spousal Violence and Physical Violence during Pregnancy as the most influential factors.
Random Forest outperformed Decision Tree in RMSE, making it the best predictive model.
Key Findings and Interpretations
1. Alcohol Consumption Strongly Correlates with Domestic Violence
Spousal Violence (%) and Physical Violence during Pregnancy (%) were significant predictors in Linear Regression, confirming a strong statistical association.
Higher alcohol consumption in men is linked to a higher risk of domestic violence.
2. Weak or Insignificant Predictors Were Removed
Sexual Violence (%) and Women Bank Account (%) were statistically insignificant (p > 0.05), meaning they do not significantly impact alcohol consumption in this dataset.
Female Education (%) was dropped due to multicollinearity with other variables.
3. Model Performance
Model	RMSE	R² (if available)
Linear Regression	Moderate	Good interpretability
Decision Tree	High	Overfitting risk
Random Forest	Lowest RMSE	Best overall model
Final Recommendations
1. Best Model Selection
If the goal is Interpretability: Linear Regression is preferred (as it shows statistical significance of each variable).
If the goal is High Prediction Accuracy: Random Forest is better (lower RMSE).
2. Policy Implications
Since alcohol consumption is strongly linked to domestic violence, policy interventions like awareness campaigns, alcohol regulation, and domestic violence prevention programs should be prioritized.
Financial empowerment of women (like access to bank accounts) did not show a direct impact on alcohol consumption, but it may still play a role in long-term gender equality initiatives.
Conclusion
Men’s alcohol consumption significantly increases the risk of domestic violence.
Spousal Violence (%) and Physical Violence during Pregnancy (%) were the most important predictors.
Random Forest provided the most accurate predictions, but Linear Regression provided the clearest statistical insights.
Policy changes should focus on reducing alcohol consumption and protecting women from violence.
