# IMDB Movie Rating Prediction

## Introduction
We will be using IMDB 5000 Movie Dataset to build models that predict the IMDB score based on a bunch of features associated with a movie. IMDB score is an important measure of how good a movie is and is maintained by IMDb (Internet Movie Database) owned by Amazon. As of March 2022, the database has records of over 600,000 movies and over 6.5 million TV episodes.
## Dataset
Tthe datset has the following attributes:-

1. Color :- Movie is black or coloured
2. Director_name:- Name of the movie director
3. num_critic_for_reviews :- No of critics for the movie
4. duration:- movie duration in minutes
5. director_facebook_likes:-Number of likes for the Director on his Facebook Page
6. actor_3_facebook_likes:- No of likes for the actor 3 on his/her facebook Page
7. actor2_name:- name of the actor 2
8. actor_1_facebook_likes:- No of likes for the actor 1 on his/her facebook Page
9. gross:- Gross earnings of the movie in Dollars
10. genres:- Film categorization like ‘Animation’, ‘Comedy’, ‘Romance’, ‘Horror’, ‘Sci-Fi’, ‘Action’, ‘Family’
11. actor_1_name:- Name of the actor 1
12. movie_title:-Title of the movie
13. num_voted_users:-No of people who voted for the movie
14. cast_total_facebook_likes:- Total facebook like for the movie
15. actor_3_name:- Name of the actor 3
16. facenumber_in_poster:- No of actors who featured in the movie poster
17. plot_keywords:-Keywords describing the movie plots
18. movie_imdb_link:-Link of the movie link
19. num_user_for_reviews:- Number of users who gave a review
20. language:- Language of the movie
21. country:- Country where movie is produced
22. content_rating:- Content rating of the movie
23. budget:- Budget of the movie in Dollars
24. title_year:- The year in which the movie is released
25. actor_2_facebook_likes:- facebook likes for the actor 2
26. imdb_score:- IMDB score of the movie
27. aspect_ratio :- Aspect ratio the movie was made in
28. movie_facebook_likes:- Total no of facebook likes for the movie

The dataset has 5043 records for these 28 attributes.
## EDA and Data Preprocessing
The work concerning EDA and data preprocessing is available in the [IMDB_mrp_EDA_and_Visualizations](https://github.com/NBK-code/IMDB_Movie_Rating_Prediction/blob/main/IMDB_mrp_EDA_and_Visualizations.ipynb) notebook.

Steps invoved in getting the data ready for model training and selection are:

1. Initial data exploration
2. Getting rid of unnecessary features
3. Dealing with missing values (either by deletion or filling in)
4. One-hot encoding categorical values
5. Train-test split
6. scaling and normalization of quantitative features
7. Removing highly correlated features

Special attention was paid to the following issues:

1. **Dummy variable trap**: remove one column of one-hot encoded categorical variable to avoid correlation between features.
2. **Multicollinearity**: find the correlation matrix of quantitative variables and remove any correlated feature that has a correlation coefficient of >0.7 with any other feature.
3. **Data leakage**: First perform the train-test split and then impute the missing values (in train, val and test set) based only on the train data.
4. **Feature normalization**: Decision tree based algorithms are scale invariant. But neural networks perform better with normaly distributed features. Most of our quantitative variables turned out to have a highly skewed distributions. Sklearn PowerTransformer was used to normalize the features.

## Model Selection
The work concerning model selection is available in the [IMDB_mrp_Model_Selection.ipynb](https://github.com/NBK-code/IMDB_Movie_Rating_Prediction/blob/main/IMDB_mrp_Model_Selection.ipynb) notebook.

The following models were trained on the data:

1. Decision Tree Regressor
2. Random Forest Regressor
3. XGBoost Regressor
4. Neural Network

To control the problem of overfitting in the first three models, an optimal value for the hyperparameter max_depth (maximum depth of trees) was found using a simple for loop based search. For the neural network model, we just choose the model that provides the least validation error. The performance of the models on the test data are as follows:

| Model | Mean Absolute Error | Accuracy |
| --- | --- | --- |
| Decision Tree Regressor | 1.006 | 87.29% |
| Random Forest Regressor | 1.005 | 89.33% |
| XGBoost Regressor | 1.003 | 89.68% |
| Neural Network | 1.059 | 80.23% |

We see that the XGBoost regressor works better than other models, although the random forest regressor is a close second. 

## Conclusion
