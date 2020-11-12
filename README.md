# Telco Churn


Business Case
-------------

In today’s telecommunications landscape, competition in the mobile space is high with switching providers becoming more easy and numerous Mobile Virtual Network Operators (MVNOs) offering cheap deals. Since the 2008 recession, telco operators have faced declining revenue and margins, more so that the overall market ([McKinsey, 2019](https://www.mckinsey.com/~/media/McKinsey/Industries/Technology%20Media%20and%20Telecommunications/Telecommunications/Our%20Insights/Telecom%20operators%20Surviving%20and%20thriving%20through%20the%20next%20downturn/Telecom-operators-Surviving-and-thriving-through-the-next-downturn.pdf?shouldIndex=false)).

To retain customers whilst face with shrinking OpEx, telco operators need to have well thought out and implemented retention campaigns. A vital part in launching such a campaign would be to identify customers at risk of churning in an accurate and automated manner.

This aim of this project was to retain customers by pre-emptively contacting customers and offering them a discount to their service if they re-contract. 



The Data Science Process
-------------

The data used within this project was sourced from Kaggle [here](https://www.kaggle.com/blastchar/telco-customer-churn).

Each row in the data relates to a customer with a label of 'Churn' being 'Yes' or 'No' to indicate if they have churned or not.
The features in the data include:
- demographics (e.g. gender, having dependents or partners, seniority) 
- account and service details (e.g tenure, products taken, contract type, payment methods, monthly and total charges).

**Exploratory Data Analysis (EDA)** explored and identified the features most likely to be important to predicting churn e.g.:
- being on a monthly contract increases churn risk
- whereas being a senior citizen decreases churn risk

During **Feature Selection** and **Feature Engineering**, uninformative features were dropped e.g. gender, certain services, and the remaining features were transformed:
- filling in nulls with the median and performing standardization (where numeric) 
- one hot encoded (where categoric) 

By using **Pipeline** from the sckit-learn library, I was able to transform the test data to the same scales as the train data.

During **Model Selection**, I used cross validation to short list 3 promising algorithms to further tune. I assessed the model's performance on highest recall whilst maintaining decent precision; 
> it is more important to identify the most potential churners in order to maximise revenue retention than to minimise misclassing non-churners as churners (this will have some revenue erosion but not as significant as losing a customer).

Moving on to **Model Training**, I utilised randomised search to provide a good starting point to define the hyperparameter space for grid search. Using the results of the grid search, I identified the best model with it's hyperparameters.

The final model identifies customers who are likely to churn, outputting a 1 (Churn) or 0 (No Churn) and will be joined back to the customerID, the data will be used to pull customers into a retention campaign.

Conclusion
-------------

Through implementing this model, an operator can expect to retain potential churner revenue and ensure they are less likely to churn in the future. 

Although there will could be some erosion in revenue of non-churners, on balance, the potential revenue benefits of retaining potential churners far exceeds erosion risk- with **61% net revenue retention** through implementation of the model.
