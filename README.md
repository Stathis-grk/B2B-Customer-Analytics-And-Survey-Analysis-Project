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

#### These results proves to a great extent the validation of the dataset.





### Boxplot + Removing the Outliers

<img width="1027" height="605" alt="image" src="https://github.com/user-attachments/assets/1fefc3a0-862f-4900-8780-a450ead7ad84" />





A company having annual revenue higher than 1 trillion $ is not possible.



<img width="600" height="122" alt="image" src="https://github.com/user-attachments/assets/23a38b6c-f078-410e-af73-489e34df7da8" />


### Barplot (free_text_response)
<img width="942" height="736" alt="image" src="https://github.com/user-attachments/assets/0ef15f27-2e05-4a15-b362-2c3e5f790182" />






The majority of the text responses seems to be the 'Very satisfied with product quality' response (160+ counts). However, the second and third most popular answers indicated that the customers were complaining about the slow response time and that the price could be more flexible




### GROUPING "free_text_response" WITH "satisfaction_score" AND "likelihood_to_buy" COLUMNS



<img width="751" height="676" alt="image" src="https://github.com/user-attachments/assets/03efb683-bbb7-439a-afb5-90ac01c8db30" />




Both satisfaction_score and likelihood_to_buy columns have similar rankings based on the free_text_response column. The paradox is that the text 'Great platform and responsive support' has lower satisfaction_score and likelihood_to_buy means. To conclude positive texts are not always compatible with high satisfaction scores



### GROUPING "industry" WITH "annual_revenue_usd" AND "satisfaction_score" COLUMNS
<img width="703" height="711" alt="image" src="https://github.com/user-attachments/assets/8c7db1c7-4820-43ea-8df7-eaa28d7fd61e" />





The top 3 industries with the highest satisfactions score are: Manufacturing(6.7), Finance(6.5), Retail(6.5). Also the means of the satisfaction score are between 6-7 and generally above 6. However the industries with higher revenue are tend to have lower satisfaction score. We assume that the greater the revenue in an industry, the greater the industry's demands.
