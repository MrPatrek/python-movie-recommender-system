# Recommender system in Python

A recommender system for movies written in Python using **pandas** and **NumPy**. *MovieLens* dataset was used for learning the model.

**Jupyter Notebook** was used for writing the code. You can take a look at performed calculations as well as the code itself [**HERE**](https://github.com/MrPatrek/python-movielens-recommender-system/blob/main/python-movielens-rec-sys.ipynb).

## Explanation of the recommender system

### 1. Basic recommendations

#### 1.1 Reading ratings

Load the file as a DataFrame. Convert given dates into datetime format, and then modify local DataFrame in accordance with a range of datetime variables. Count the sum of all ratings for each movie and display only the ones with given allowed minimal number. Display the number of rows for the local DataFrame. Save the previously read DataFrame as a file.

#### 1.2. Reading movies

Load the file as a DataFrame. Return the title of the movie for the given movieID.

#### 1.3. Random predictor

Determine random rating value in a range of given minimum and maximum values for each movie, append it to the results dictionary (where key is movieID and value is random rating) and return this dictionary.

#### 1.4. Recommendation

First, the prediction is made. In case user does not want to see already watched movies, pop the movies from the prediction dictionary that he has already watched. Then, the prediction dictionary is converted into the list of tuples so that we can sort it descending (movies with greater rating first). Return the list of tuples with the number of movies given as an argument to the function.

#### 1.5. Average predictor

Calculate the average rating of all the movies in the dataset. For each movie, we count the number of how many times the rating was given for this particular movie. For each movie, we count the sum of all the ratings this particular movie has. Then calculate the score for each movie with respect to a given formula and the abovementioned numbers. Return the result as a dictionary.

#### 1.6. Recommending the most watched movies

For each movie, calculate the number of its appearances in the dataset (the number of ratings each movie has in the dataset, or simply the number of its appearances in the rating dataset). Return results as a dictionary.

### 2. Collaborative filtering

#### 2.1. Predicting scores with similarity between products

Create a table for storing similarities. First, it will be checked if some value is already stored in the table. If it is stored, then take it, otherwise calculate it and insert into the table. The prediction will only calculate the similarities that it needs, so that when some recommendation is done for the first time, not all the values will be filled in the similarities table (to save execution time). When predicting, we calculate the similarities between all movies that are in our dataset and the ones that this particular user has rated (we suppress the option when two identical movies are compared). For each of the abovementioned similarities we calculate the product of rating and the similarity itself (which is needed for the prediction). Then we sum all products and all similarities and divide first sum with the second one. This is the result for one particular recommendation.

#### 2.2. Most similar movies

First, we calculate all the remaining similarities in our table that are left from Item-Based Predictor. Then, we simply add all similarity table entries to the list of tuples, sort is descending and print the results. The most similar movies will be on the first place.

#### 2.3. Recommendation based on the currently viewed content

We simply look into the table and retrieve a column of the movie similarities that we want to find similar movies for. Then we turn it into the list of tuples, sort it descending and return it.

#### 2.4. Recommendation for yourself

I simply added the movies that I have watched to the database and gave them my rating. Interesting thing is that the prediction has returned me the movies that I did not enter to the table, but which I like and they had high scores, which is fine.

#### 2.5. Prediction with Slope One method

First, calculate all the deviations between the movies that we need to compare for our prediction, and as with Item-Based Predictor, simply store them in the table. When we have deviations needed, we use them to make a prediction for some particular movie. The process is quite similar to the Item-Based Predictor.
