# Coding Explained - Srihari Nagarajan

This document explains steps followed in completing the code.

**Part I:**
 1. Input data used - *patients.csv*
                    - *appointments.csv*
 2. Data was imported from Amber's github and converted into Pandas dataframes.
 3. Data was inner joined using patient_id and id columns using merge command.
 4. id column was dropped since it was a duplicate of patient_id.
 5. Checked resulting table for missing values. None was found.
 6. Day_of_week was a new variable derived using a custom function parse_full_date.
 7. Frequency count of day_of_week column was taken to find out which day has the most number of no-shows (Monday).
 8. Ages were binned into 10 groups and a bar plot was created to plot status by age group.  We found that age group 21-30 had
    the most number of no-shows.
 9. Age group 45-55 had the most representation in the data.
 10. In order to predict whether a person would show up or not, several models were built. But prior to that, data exploration was conducted.
 11. Status variable was the target and it was converted into numeric [1=No-show and 0=show-up]
 12. 30% of the patients did not show up. [There were 2999897 unique patients in the data. 3 patients had more than 1 appointment)
 13. Categorical Variables were converted into dummy variables using pandas get_dummies method.
 14. Target variable was separated from predictor variables.
 15. Correlation was checked between independent variables.  The ones with high correlation were removed.
 16. Correlation matrix was built using seaborn package to ensure that there are no more high correlations.
 17. Age had a fair amount of positive correlation with hypertension.
 18. Variables were scaled using StandardScaler since it is least affected by outliers.
 19. I tried using Age vs Age group as model input and found that there was a slight increase in accuracy on using Age_group.  
 20. Since all categorical variables are converted to dummies, we wouldn't need StandardScaler.
 21. I tried different modeling algorithms from sklearn - logistic regression, polynomial regression with degree 2, Random Forest, MLP Neural
     Networks, Decision Tree, Gaussian Naive Bayes algorithms.  
 22. Decision tree feature importance shows that age_group is the most important variable followed by sms_reminder.
 22. ROC curves were used to evaluate these algorithms and all models have almost the same accuracy.
 23. A better approach would be k-fold cross validation to evaluate the accuracy scores, but since the models are not fitting the data very
     well even on the training data, CV was not performed here.
 24. Since the model doesn't fit the data very well, we would need to identify additional variables that could help increase the accuracy.

**Part II:**

  1. *Locations.csv* file was read from Amber's git and converted to pandas dataframe.
		
  2. Hour of day and date were extracted as separate columns because the API returns weather info at hour level granularity.
		
  3. Latitude and Longitude columns were converted into strings to form the proper API url with parameters.
		
  4. getweather function takes in API weather request url and each row from locations.csv as input and extracts tempF, weatherDesc,          precipMM and cloudcover from the json file returned by the historic weather API.
		
  5. getlocation function takes in API search requeste url and each row from locations.csv as input and extracts areaname, state and          population values from the json file returned by the search API.
		
  6. State column was not asked for but added to understand where each areaname belongs.
		
  7. The extracted columns from the APIs were added to the dataframe and the dataframe was cleaned up to include only the necessary          columns.
		
  8. The dataframe was written to a new CSV file and saved.
