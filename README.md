# Objective:
A bank in the region wants to build a model to predict credit card defaulters more accurately in order minimize money loss. For this task we have a set of data on default payments and demographic data to help us do our task. They want to answer 2 specific questions:
- Which are the top 5 clients which are least likely to deafult?
- What is the optimum threshhold to maximize profit for the bank?

### The Dataset:
Data is comprised in the following CSV files:
**TRAINING**

**`train_customers.csv`**
 - `ID`: ID of each client
 - `LIMIT_BAL`: Amount of given credit in NT dollars (includes individual and family/supplementary credit
 - `SEX`: Gender (1=male, 2=female)
 - `EDUCATION`: (1=graduate school, 2=university, 3=high school, 4=others, 5=unknown, 6=unknown)
 - `MARRIAGE`: Marital status (1=married, 2=single, 3=others)
 - `AGE`: Age in years
 
**`train_series.csv`**
 - `ID`: ID of each client
 - `MONTH`: The month to wich data is refering
 - `PAY`: Repayment status in the corresponding month (-1=pay duly, 1=payment delay for one month, 2=payment delay for two months, … 8=payment delay for eight months, 9=payment delay for nine months and above)
 - `BILL_AMT`: Amount of bill statement in the corresponding month (NT dollar)
 - `PAY_AMT`: Amount of previous payment in the corresponding month (NT dollar)
 
**`train_target.csv`**
 - `DEFAULT_JULY`: Default payment in July (1=yes, 0=no)
 
 
**TEST**
 - **`test_data.csv`**
 
**SUBMISSION**
 - **`submission_features.csv`**
 
**BACKUP**
 - **`train_data.csv`**

# Process

### A. Data Engineering:
- The demographic, payment and target columns must all be combined in one dataset
- The payment columns also need to be pivoted and used as separate columns eg. month_pay from two separate columns of month and pay.

### B. EDA:
Education Level:
- The highest number of defaulters are customers with a college degree **(over 80% of all defaulters)**. This is interesting. This is because we assume that college graduates have higher incomes and are more likely to pay off their credit card debt. Howeveer this could also arise from the need to pay back college debt.
 - In addition, it is worth noting that the number of delinquents who graduated from high school is low **(less than 20% of all delinquents)**. One possible reason, although small in absolute terms, is that the credit limits given to these customers are very low relative to their income level and therefore the probability of default is very low. It could also be that the bank has fewer credit card holders that have only a high school education

Limit Balance:
- The box of the defaulters is more dense than that of the people that do not default. The outliers for the default category are also less spread out than the non default category. 
- Furthermore the Q1, Q2, Q3 are all higher for non-defaulters than defaulter
- This means that usually the people with lower credit limits tend to default more. 
- However both the categories have many outliers

Marital Status:
- Number of defaulters have a higher proportion of people that are single compared with those that are married or 'other'

Sex:
- There are more female carholders than male. Thus there are more defaulters that are women.

Delayed Repayment:
- It is evident from the above graphs that those with revolving credit consists of the largest number of carholders and maybe that is why also the largest number of defaulters. However it is interesting to see that the second largest category with the most defaulters is 2 which is those that have delayed payment by 2 months. This is significant as the number of non defaulters in this category is almost equal to the defaulters.

## C. Machine Learning

