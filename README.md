# B2B-Customer-Analytics-And-Survey-Analysis-Project
A comprehensive data science end-to-end project analyzing B2B customer satisfaction, NPS scores, and purchase likelihood through data cleaning, exploratory analysis, and statistical modeling.

## Overview
This project demonstrates a complete data analytics pipeline from raw data to actionable insights:

1) Data Cleaning & Validation: Python-based ETL with intelligent null handling and outlier detection
2) Exploratory Data Analysis: Comprehensive statistical analysis with correlation and groupby studies
3) Statistical Modeling: OLS Regression with heteroscedasticity testing (R² = 0.748)
4) Interactive Excel: VBA-powered search bar automation for operational use
5) Business Intelligence: Power BI dashboard for executive visualization

Dataset: 1,200 B2B survey responses across 9 industries and 7 countries with 14 features

# Data Pipeline & Methodology (Python Workflow)

The data science pipeline implemented in the Jupyter Notebook follows a structured approach:

## 1. Import Dataset/Libraries & Data Cleaning
**Import Dataset & Libraries:**



<img width="1446" height="761" alt="image" src="https://github.com/user-attachments/assets/0654f5de-834b-4dca-b206-80b183253ed3" />




* **Duplicate Management:** Identification and removal of duplicate records to ensure data integrity.


<img width="855" height="187" alt="image" src="https://github.com/user-attachments/assets/c95ca39d-839e-4975-8e58-1944ae6e99d6" />



* **Text Normalization:** Column headers and string data (such as `country`, `industry`, and `free_text_response`) were stripped of leading/trailing whitespaces, and special characters (`-`) in company names were appropriately replaced.

<img width="702" height="197" alt="image" src="https://github.com/user-attachments/assets/c2cb73a8-d3dd-4c8d-95db-db480e1c15f8" />



<img width="610" height="266" alt="image" src="https://github.com/user-attachments/assets/35e28228-22b6-425f-95be-0c0efc1844fc" />



* **Missing Value Imputation:**
  * For the `industry` column, missing fields were tagged as `"Unknown"`.
  * For the `satisfaction_score`, a conditional imputation strategy based on the Net Promoter Score (NPS) was used.
  * For `annual_revenue_usd`, missing financial fields were imputed using the column mean.






<img width="847" height="736" alt="image" src="https://github.com/user-attachments/assets/db6172f1-abc5-4939-8b8b-d88553a9890f" />






* **Data Formatting:** Rounded and converted annual revenue metrics into clean integers for standard formatting.


<img width="621" height="206" alt="image" src="https://github.com/user-attachments/assets/b728cb68-f903-4a11-b835-bbf835b75c91" />




## 2. Exploratory Data Analysis (EDA)
* Extracted descriptive statistics (mean, standard deviation, minimum, maximum values) across a robust sample size of ~1,200 B2B respondents.





<img width="1051" height="747" alt="image" src="https://github.com/user-attachments/assets/eaab2eaf-9005-4568-b757-222e4e09f20b" />





  
### Correlation Matrix


<img width="755" height="691" alt="image" src="https://github.com/user-attachments/assets/27d3424a-ce6b-4d83-bb61-aed0c0709da0" />



There is a strong positive correlation between: 'satisfaction_score' and 'likelihood_to_buy' ~0.82, 'nps_score' and 'satisfaction_score' ~0.68, 'likelihood_to_buy' and 'nps_score' ~0.57 (less strong). Also the correlations ~0 are normal because there is no direct relationship between them.

These results proves to a great extent the validation of the dataset.





### Boxplot + Removing the Outliers

<img width="1027" height="605" alt="image" src="https://github.com/user-attachments/assets/1fefc3a0-862f-4900-8780-a450ead7ad84" />





<img width="600" height="122" alt="image" src="https://github.com/user-attachments/assets/23a38b6c-f078-410e-af73-489e34df7da8" />




A company having annual revenue higher than 1 trillion $ is not possible.





### Barplot (free_text_response)
<img width="942" height="736" alt="image" src="https://github.com/user-attachments/assets/0ef15f27-2e05-4a15-b362-2c3e5f790182" />






The majority of the text responses seems to be the 'Very satisfied with product quality' response (160+ counts). However, the second and third most popular answers indicated that the customers were complaining about the slow response time and that the price could be more flexible




### GROUPING "free_text_response" WITH "satisfaction_score" AND "likelihood_to_buy" COLUMNS



<img width="751" height="676" alt="image" src="https://github.com/user-attachments/assets/03efb683-bbb7-439a-afb5-90ac01c8db30" />




Both satisfaction_score and likelihood_to_buy columns have similar rankings based on the free_text_response column. The paradox is that the text 'Great platform and responsive support' has lower satisfaction_score and likelihood_to_buy means. To conclude positive texts are not always compatible with high satisfaction scores



### GROUPING "industry" WITH "annual_revenue_usd" AND "satisfaction_score" COLUMNS
<img width="703" height="711" alt="image" src="https://github.com/user-attachments/assets/8c7db1c7-4820-43ea-8df7-eaa28d7fd61e" />





The top 3 industries with the highest satisfactions score are: Manufacturing(6.7), Finance(6.5), Retail(6.5). Also the means of the satisfaction score are between 6-7 and generally above 6. However the industries with higher revenue are tend to have lower satisfaction score. We assume that the greater the revenue in an industry, the greater the industry's demands.




## 3. Data Quality Assessment
### Suspicious Responce Detection





<img width="657" height="356" alt="image" src="https://github.com/user-attachments/assets/b9180762-29b9-4c24-866e-87e2bd519ac7" />





5% (60) of the responses are unusually quick. This may indicate to unreliable answers


### Same Answers in Multiple Different Columns





<img width="807" height="292" alt="image" src="https://github.com/user-attachments/assets/8a2cb0ea-ea2c-4c89-856e-3fddbc9bc164" />





5.3% (64) of the companies have given the same answers to multiple columns. This may be due to an automation tool.



### Detection Of Incosistent Responses



<img width="525" height="201" alt="image" src="https://github.com/user-attachments/assets/345caaf1-d371-408f-b05c-eadb26a3bf62" />





* 2 rows are having a marginal incosistent responses between satisfaction score and likelihood to buy
* 0 rows are having a marginal incosistent responses between satisfaction score and nps_score
* 48 rows are having a marginal incosistent responses between satisfaction score and likelihood to buy

Those results are reasonable because satisfaction_score and likelihood_to_buy are less strongly correlative.




### Completion Rate Insight




<img width="468" height="113" alt="image" src="https://github.com/user-attachments/assets/92de0745-378d-4dfb-b3f9-0f2ce6bdf832" />




## 4. Statistical Modeling
### Regression Model Specification:





<img width="642" height="487" alt="image" src="https://github.com/user-attachments/assets/d0b31c40-3059-48cb-a69b-204902a979f8" />







<img width="652" height="553" alt="image" src="https://github.com/user-attachments/assets/52246f35-09e7-495b-ad93-5adc438fcd9f" />


### Heteroskedasity Test 


<img width="423" height="383" alt="image" src="https://github.com/user-attachments/assets/7ff31afe-de59-4219-a027-202c7bd4bb4c" />




### Model Results 
The OLS regression model demonstrates strong performance with an R-squared of 0.748, with likelihood to buy (β = 1.24, p < 0.001) and NPS score (β = 0.61, p < 0.001) as the primary predictors of satisfaction. The Breusch-Pagan test (p = 0.927) confirms the absence of heteroscedasticity, and diagnostic tests reveal no autocorrelation or multicollinearity issues. While the Jarque-Bera test flags non-normality in residuals, this is expected with large sample sizes (N = 1,199), where minor deviations become statistically detectable without affecting model reliability. Also the assumption that the industries with higher revenue are tend to have lower satisfaction score is not proven by our model BUT manufacturing industry showed a modest but significant positive effect (the customers in this field shows 0.078 bigger satisfaction).



# Excel Features & Analysis
## The Final Cleaned Dataset





<img width="971" height="430" alt="image" src="https://github.com/user-attachments/assets/5b9b9fb6-752f-4dee-b262-cd4dc3df27ca" />







## Dynamic Search Bar & Data Querying 





<img width="673" height="428" alt="image" src="https://github.com/user-attachments/assets/26de3682-b92c-4a62-b570-7ff9c062fc02" />






The Excel file includes a custom-built search bar with:

1) ActiveX Controls for user interface
2) Dynamic filtering without external tools
3) Real-time results based on user input
4) ID column search support





## Aggregated Pivot Tables





<img width="832" height="272" alt="image" src="https://github.com/user-attachments/assets/090c5441-46fe-492e-91db-9a617bf316d5" />





Designed a master **Pivot Table** to instantly summarize, cross-examine, and slice categorical metrics (such as industries and company sizes) against numeric performance KPIs like Net Promoter Score (NPS) and Average Satisfaction.
Serves as the operational intermediary link, validating data summaries before final publication to the BI environment.
