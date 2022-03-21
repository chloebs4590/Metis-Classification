### Predicting Level 2, 3 and 4 Injuries during NYPD Force Incidents

### Abstract

The goal of this project was to use a classification model to a) predict whether a non-NYPD subject will suffer a level 2, 3 or 4 injury during a force incident and b) identify factors that are most useful in making these predictions. By leveraging feature engineering, oversampling methods and hyperparameter tuning, I built a model that identified the type of force used by an NYPD member of service (e.g., impact weapon) and the basis for the encounter (e.g., vehicle traffic law infraction) as the features with the strongest impact on the probability a non-NYPD subject will suffer a level 2, 3 or 4 injury. In the future, if granted access to more detailed data from the NYPD (such as that referenced in the department's annual <a href=\"https://www1.nyc.gov/assets/nypd/downloads/pdf/use-of-force/use-of-force-2020-issued-2021-12.pdf\">Use of Force Report</a>, I would like to improve upon the model by adding more/replacing existing features with those that have greater predictive power of whether a non-NYPD subject suffers a level 2, 3 or 4 injury.

### Design

I designed this project with the New York City Police Department as my hypothetical client. In this scenario, they are interested in improving their relationship with the communities they serve. One way in which they seek to do this is by reducing the rate of level 2, 3 and 4 injuries (i.e., serious-level injuries) among non-NYPD subjects involved in force incidents.

My hypothesis was the following: by being able to predict whether a non-NYPD subject involved in a force incident will suffer a level 2, 3 or 4 injury based on various aspects of a force incident and those involved - such as the type of force used by 1+ members of service and the type of force used (if any) by non-NYPD subjects - the NYPD will be able to identify which aspects contribute most to the likelihood of these injuries occuring and can make changes to its training and use of force policy based on them to reduce the rate of non-NYPD subjects suffering from injuries of these levels.

### Data

I compiled the data using three separate datasets publicly available from New York City's Open Data website:
- <a href=\"https://data.cityofnewyork.us/Public-Safety/NYPD-Use-of-Force-Incidents/f4tj-796d\">NYPD Use of Force Incidents</a>
- <a href=\"https://data.cityofnewyork.us/Public-Safety/NYPD-Use-of-Force-Subjects/dufe-vxb7\">NYPD Use of Force: Subjects</a>
- <a href=\"https://data.cityofnewyork.us/Public-Safety/NYPD-Use-of-Force-Members-of-Service/v5jd-6wqn\">NYPD Use of Force: Members of Service</a>

All of the force incidents occurred between January 2020 - December 2021.

The final dataset contained 13,230 rows (each row represented a single non-NYPD subject involved in a force incident). The only null values were in the age column for non-NYPD subjects, so I replaced them with the median age. Before converting the categorical features to binary dummy variables, there were 11 features (9 categorical, 4 continous) plus the target variable. Afterwards, there were 52 features.

### Algorithm

***Feature Engineering***

- Engineering new features based on existing ones (e.g., # of non-NYPD subjects per incident, # of NYPD members of service per incident, whether the subject's race different differed from the NYPD member(s) of service involved in the incident, the season in which the incident occurred)
- Converting categorical features to binary dummy variables
- Re-scaling continuous features to be on the same scale

***Models***

I used logistic regression for this project because model interpretability - not just predictability - was important for my business problem. I iterated on the base model multiple times, ultimately creating 6 models in total. In the base model, I included all of the features and no oversampling, despite my data being extremely imbalanced (approximately 2% in the positive class and 98% in the negative). Next, I experimented with different oversampling ratios before selecting one and oversampling my the training data to use in subsequent iterations. In the third - sixth models, I tuned the penalty and class weights hyperpameters to improve the model's performance.

***Model Evaluation and Selection***

For my business problem, a false negative (i.e., predicting a subject won’t suffer a level 2, 3 or 4 injury during a force incident when they actually will) is worse than a false positive (i.e., predicting a subject will suffer a level 2, 3 or 4 injury when they won’t). Therefore, I evaluated each iteration of the logistic regression model based on its recall and F2 scores.

**Recall score of holdout dataset: 0.576**
**F2 score of holdout dataset: 0.157**

### Tools

- Numpy, Pandas, Seaborn and Matplotlib for data cleaning and EDA
- Imblearn for resampling unbalanced classes
- Scikit-learn for modeling
- Tableau, Seaborn and Matplotlib for data visualizations
- SQL for data storage
    
# Communication
My complete code and presentation slides are available in this project's repo.
    
