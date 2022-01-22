
# Forcibly Displaced Populations #

---
Every year, millions of people are forced to leave their home due to conflict, violence, persecution, natural hazards and human rights violations. At the end of 2020, 82.4 million people were displaced across the world. 

Many of these populations are forced to flee abroad to a host country or to another region within their home country, to seek refuge and protection. 

The question then becomes, how well does this population socially integrate into the wider society of their new home? This outcome is often determined by the type of accommodation these populations are initially allocated after displacement.  

It has been found that displacement camps tend to have poorer access to basic services, such as sanitation facilities and health services, as well as poor cohesion with host communities, compared to outside of displacement camps.

## Aim ## 

The aim of this project was to use machine learning methods to successfully predict whether a forcibly displaced person would be allocated individual accommodation or a displacement camp based on their demographics.


## Target Audience ##

This project was cultivated with international humanitarian organisations in mind.

## Repository Contents ##

- Data Cleaning
- Exploratory Data Analysis (EDA)
- Model and Evaluation
- Data Visualisation Images

## Objectives ##

1. Predict individual accommodation or not individual accommodation (displacement camp)
2. Identify which demographic factors have the greatest influence on the type of accommodation that will be allocated
3. Create a tool that humanitarian organisations can use to indicate the outcome of a displaced person based on their demographics (classification model).

## Hypothesis ## 

My hypothesis is that the age and gender of an individual have the greatest influence on the type of accommodation that is assigned. Specifically, females aged 0-4 years old will be given priority for individual accommodation allocation.

In addition to verifying this hypothesis, I would like to identify other factors that are likely to influence the type of the accommodation a person will be assigned to, indicating potential successful or unsuccessful social cohesion of a resettled person, within their host community.

## Data Source and Overview ##

The dataset was available from the **United Nations High Commissioner Refugee Agency (UNHCR)**. The UNHCR, also known as the UN Refugee Agency, is a global organisation committed to creating better lives for refugees, forcibly displaced persons communities and stateless populations.


<img align="right" src="https://user-images.githubusercontent.com/96108711/150037417-76715eec-fe2a-489c-a984-8eafa32ce156.png" width="200"/>

- Up-to-date dataset, collected from 2001 to 2021.  
- Available as a CSV file.
- 211 countries of origin and 180 countries of asylum. 		
- 251,626 instances dated back to 2001, with each instance being the demographic information about a particular population that had been displaced each year.
- Features included, the countries of origin and asylum and the country codes, the number of individuals of a particular age and gender, type of population they were classed as and information on the resettlement location.

## Data Cleaning ## 

Cleaning and munging steps taken were as follows:

- Tidied column names, replacing whitespaces with underscores and formatting all letters to lowercase (standard for data analysis)
- Dropped unnecessary columns in relation to my research problem
- Removed foreign characters from countries 
- Population types with few values (VDA and STA), I added to ‘Others of Concern’ population type (feature engineering)
- Removed urban/rural locations coded as unknown or various
- Amended feature dtypes 
- Dropped observations prior to year 2012.
- Binarized the target variable to produce two classes 
    - **I** for individual accommodation and **Q** for displacement camp/other

## Final features ##

Variable                      | Description                                    | Type of Variable
----------------------------- | ---------------------------------------------- | ----------------
Country of Origin             | Orginating country                             | Categorical
Country of Asylum             | Country the person sought asylum in            | Catgeorical
Population Type	              | Type of population the person falls into. REF - Refugee, RET - Returned refugees, ASY - Asylum seekers, VDA - Venezuelans, IDP - Internally displaced persons, RDP - Returned IDPs, STA - Stateless persons, OOC - Others of Concern | Categorical
Urban or Rural Location	      | Indication of whether the location they were allocated was urban or rural. An urban location is classified as a settlement with more than 5,000 inhabitants (defined by UNHCR)| Categorical
Accommodation Type	          | Type of accommodation person was allocated. I - Individual accommodation, S - Self-settled camp, P - Planned/Managed camp, C - Collective centre, R - Reception/Transit camp, U - Undefined  | Categorical
Female aged 0-4 years	      | Integer                                 | Discrete
Female aged 5-11 years	      | Integer                                 | Discrete
Female aged 12-17 years	      | Integer                                 | Discrete
Female aged 18-59 years	      | Integer                                 | Discrete
Female aged over 60 years	  | Integer                                 | Discrete
Male aged 0-4 years	          | Integer                                 | Discrete
Male aged 5-11 years	      | Integer                                 | Discrete
Male aged 12-17 years	      | Integer                                 | Discrete
Male aged 18-59 years	      | Integer                                 | Discrete
Male aged over 60 years       | Integer                                 | Discrete

## Exploratory Data Analysis ##

Before commencing modelling, I explored the data to explore any trends within the data.

**Key trends spotted:**

- Afghanistan top country of origin of forcibly displaced people.
- Turkey was the top country of asylum for forcibly displaced people.
- The majority of forcibly displaced people were:
     - Legally classed as refugees, followed by asylum seekers. Returnees made up the smallest displaced population group. 
     - Males and females between the ages of 18 and 59 years.

- The age range with the smallest number of people to be displaced was older adults over 60 years old.

<img src="https://user-images.githubusercontent.com/96108711/150025489-aba43c28-6672-495c-9d9d-f204f034fd03.png" width="425" height="400" /> <img src="https://user-images.githubusercontent.com/96108711/150025528-ee3c5cde-815e-4b18-ba2f-64ace569dc23.png" width="525" height="400" /> 

- Majority of males and females aged 18-59 years orginate from: Democratic Republic of Congo, Afghanistan, Syria, Somalia and Yemen.
<img src="https://user-images.githubusercontent.com/96108711/150039041-4f1e54f4-521a-4c1f-a019-d96a3322bdb3.png" width="1000" height="400" />

- Many, almost all of the people being displaced are being displaced as a group, presumably families, with many having infants under 4 years old. 

- Generally, a weighty majority are allocated an urban location to resettle in and individual accommodation over a displacement camp, with there being a strong correlation between urban location settlement and individual accommodation. 

<img src="https://user-images.githubusercontent.com/96108711/150026982-e39e9921-17e2-45be-b5b6-c31efe97809e.png" width="425" height="400" /> <img src="https://user-images.githubusercontent.com/96108711/150026998-9605f7eb-8c47-41fb-b7a7-900e1a4b6559.png" width="425" height="400" /> 

- Network analysis was carried out to visualise the movement of populations from the countries, specifically investigating countries that had the greatest incoming and outcoming traffic to and from **other countries**. Visuals show the connections the countries Canada and Syrian Arab Republic have with other countries.
    - Canada had the greatest incoming traffic, followed by Germany and Brazil.
    - Syrian Arab Republic had the greatest outcoming traffic, followed by Somalia and Nigeria.

<img src="https://user-images.githubusercontent.com/96108711/150030102-31d2ced7-64f5-4bed-b1db-e5f2844a57a2.png" width="400" height="400"/> <img src="https://user-images.githubusercontent.com/96108711/150030184-825ad524-b8a5-4824-a070-70e0b900584f.png" width="400" height="400" /> 

## Preliminary Chi-square Test ##

A preliminary Chi-square test was carried out on the features, to give an indication of which features were likely to have the greatest effect on the target variable. 

Though this was carried out, it was not used to select features prior to modelling. Instead, all of the features were used in the modelling stages and then the top features highlighted from the top-performing model were then compared to the features highlighted from the Chi-square test. 

## Modelling ##

The initial approach to modelling was to use all the available cleaned data in eight different classification models, to determine the final best model for predicting accommodation allocation.

Each model was evaluated and compared to one another using standard classification model metrics: 
- Accuracy score - both the training and test sets
- Mean cross-validation scores
- Visualising the receiver-operating curve (ROC curve)
- Area under the curve (AUC)

To aid evaluation of the best performing model, my **baseline accuracy score was 0.85**. 

As an evaluation metric, the greater the amount above the baseline accuracy score the model accuracy score was, the better the model performed. The score indicates the model’s ability to correctly predict the classes of the target variable (score of 1 being perfect prediction and 0 being extremely poor prediction).

Classification models used were:

1. Logistic Regression - Ridge
2. Logistic Regression - Lasso
3. KNN
4. SVM (Linear SVC)
5. Random Forest Classifier
6. Decision Tree Classifier 
7. Naive Bayes Multinomial
8. Neural Networks 

The steps were as follows:

1. Firstly, I used the labelbinarizer from the sklearn preprocessing package, to map my two classes (target variable) numerically, as this impacts how the data is treated by the model and confusion matrix at a later stage.
2. This produced an array which I then flatted using a NumPy function.
3. Categorical features were then converted into dummy variables using Pandas get_dummies function. 
4. Data was standardised using StandardScaler (though this was not applied when using Random Forest and Decision Tree Classifiers). 
5. Lastly, the data was split into train and test samples. 
6. A Grid Search was performed on each model, to find the best hyperparameters to produce the best prediction for the dataset. 

## Results ##

Model                       | Accuracy score (unseen data)   | Mean CV Score | AUC  
--------------------------- | ------------------------------ | ------------- | -----
Decision Tree Classifier    | 0.941                          | 0.94          | 0.93
Random Forest Classifier    | 0.96                           | 0.96          | 0.99
KNN                         | 0.95                           | 0.94          | 0.99 
Naive Bayes Multinomial     | 0.86                           | 0.86          | 0.81
Neural Networks             | 0.95                           | 0.95          | 0.98
Logistic Regression - Ridge | 0.94                           | 0.94          | 0.98
Logistic Regression - Lasso | 0.94                           | 0.94          | 0.98
Linear SVM                  | 0.92                           | 0.92          | 0.85

The Random Forest Classifier performed the best on unseen data, with an accuracy score of 0.96, as well as the best AUC score of 0.99.

It was imperative that I was able to extract the feature importances, i.e. the feature that had the greatest effect on the prediction, based on the particular model. This ruled out my KNN model as it was not possible to extract the feature importances due to how the model works.

## Evaluation ##

**Confusion matrix: Random Forest Classifier (top performing model)** 

<img src="https://user-images.githubusercontent.com/96108711/150639812-6ba26ead-3d7b-436c-86d3-90cb1255829d.png" width="400" height="400" />

**Feature Importances: Random Forest Classifier**

<img src="https://user-images.githubusercontent.com/96108711/150640257-3e171474-3e73-4e54-b42f-3c5a5196ff61.png" width="400" height="700"/><img src="https://user-images.githubusercontent.com/96108711/150640287-d80ea37a-83fd-446f-8e54-542bad3b79e3.png" width="400" height="700"/>


## Conclusions ##

The top feature importances that have the greatest influence on a person being allocated individual accommodation and not a displacement camp were as follows (highlighted by the Random Forest Classifier model): 

- Resettling in an urban location 
- Having a legal status of refugee
- Seeking asylum in one of the following countries;
    - Bulgaria, Hungary, Indonesia, Croatia and Turkey
- Adults aged 18-59 years old (males predominantly), followed by females aged 5-11 years old and males aged 12-17 years old.

Essentially, this means that an individual possessing the above features will have the greatest chance of being allocated individual accommodation and not a displacement camp.

Subsequently this suggests that an individual holding all or most of these named features, will have increased chances of social integration with their host community. This will not only benefit both the resettled person and host community, by preventing marginalisation and enabling resettled individuals to develop their full potential within their new community, and for peaceful co-existence.

Surprisingly to me, country of origin does not appear to be a major determining factor of whether a person will be allocated individual accommodation or a displacement camp. Additionally, infants aged 0-4 years old did not take priority over the other age groups (except over 60s), which **disproves** my hypothesis.

## Limitations and Challenges ##

Some of the limitations and challenges I faced over the 4-week duration of this capstone project: 
- Difficult to determine outliers
    - Due to the sensitive nature of this topic, it is difficult to highlight which figures may be outliers. Determining a value as an outlier must       be down to context, for example if the number of seniors over 60 was high from one country in one particular year, this figure cannot simply         be removed from the dataset. Further investigations into world events need to be done before determining which values are outliers. 
- Class imbalance 
    - This would have affected the performance of my classification models, favouring the higher class. As expected this was initially indicated by       the relatively high baseline prediction (0.85), with my top performing classification model producing an accuracy score of 0.96 on unseen           data.
- Poor computational power 
    - This affected the speed of my grid searches and application of the SMOTE (Synthetic Minority Over-sampling Technique) algorithm, which I had        intended to use to even out my imbalanced classes. This took up a significant amount of memory on my computer, therefore I could not use the        SMOTE algorithm. 
- Possible data collection bias
    - There was a specific population type dedicated to Venezuelans displaced abroad (VDA). This is in relation to the 5 million Venezuelans               displaced abroad to date, and has been coined as the largest displacement crisis in the world by the UNHCR. However it still highlights the         focus on particular countries. 


## Future Work ##

There are several avenues I would like to explore further with regards to this dataset: 

1. Keeping the ‘Year’ Column from the original dataset, to conduct a Time Series Analysis (ARIMA specifically) on the dataset. I would then do the following:
   - Identify trends in the movement of people over the years.
   - Forecasting - predict future displacements of populations and where they are likely to resettle, based on the existing data.

2. Handling the class imbalance with another technique besides the tried SMOTE algorithm
   - For example undersampling the majority class, or applying a boosting algorithm to my final chosen classification model.

3. Supplementing the dataset with other accessible datasets, for example:
   - GDP information on each country of asylum.
   - Data about political violence events or natural hazards in each country of origin.

4. Creative compelling visuals 
   - As all of the data variables were categorical, I found it difficult to create compelling visuals to help tell a story about the data when            presenting. I would like to delve further into visualisations for categorical variable types.

5. Using the features highlighted from the Chi-square test to select features before modelling, then performing modelling stages on fewer features.
   - This would have improved the efficiency of the predictive models and reduced dimensionality, to reduce the chances of overfitting the models.

## Key Learnings ##

It was great to combine many of the skills that I acquired over the duration of the General Assembly bootcamp, as well as getting hands-on experience of classic machine learning algorithms in this end-to-end independent data science project. The experience shaped my understanding of the different data science processes. I have three key learning points: 

- **Data analysis will never feel complete**. There are often countless insights that can be extracted from a dataset. Similarly, there are endless ways    with which data manipulation can be carried out and for that reason, there are numerous conclusions that can be drawn from a dataset. It is         important to know when to move on from an analysis step.

- **EDA is there for a reason!** Admittedly, I overlooked the purpose of EDA to begin with. I learnt that valuable insights are often discovered during   the EDA process. Moreover, what is uncovered can often determine how you will manipulate your data in future steps (or conversely, going back to      cleanse your data in a more refined way).

- **Machine Learning algorithms are very sensitive to any tweaks in the data cleansing process.** This highlighted the importance of justifying the       steps carried out in the cleansing stages. This is particularly important when it comes to analysing real-world data, where the outcomes of your      model affect business decisions.

---

Libraries and softwares used: 

- NumPy
- Pandas
- SciKit-Learn
- SciPy
- Seaborn
- Matplotlib
- Tableau
- NetworkX
