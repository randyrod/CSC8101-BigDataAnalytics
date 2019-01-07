# Movie Recommendations-BigDataAnalytics
MSc Cloud Computing CSC8101 Big Data Analytics

## Requirements

### Overview
In this coursework, you will use the Spark DataFrames and Machine Learning algorithms provided by Apache Spark to train a movies recommendation model on a subset of the original dataset used in the "2016 Netflix Prize".

### The Data

The data provided is, apart from some minor modifications and the addition of a Neo4j database, the same data as used in the netflix prize. It consists of the following files:

* **netflix_movie_titles.txt**: a text file containing roughly 18 thousand lines, corresponding to the same number of movies. Each line is of the format Id, Year of release, Title. For example:

    ```
    1,2003,Dinosaur Planet
    2,2004,Isle of Man TT 2004 Review
    3,1997,Character
    4,1994,Paula Abdul's Get Up & Dance
    5,2004,The Rise and Fall of ECW
    ```

* **movie_titles_canonical.txt**: a text file containing roughly 13 thousand lines, one per movie, for example:

      ```
      Avatar,2009
      Amélie,2001
      Full Metal Jacket,1987
      E.T.: The Extra-Terrestrial,1982
      Independence Day,1996
      The Matrix,1999
      ```

* **mv_sampled.parquet**: this is a subset of the whole ratings file, containing about 1 million ratings.

* **qualifying_simple.txt**: a text file containing roughly 2.8 million lines, corresponding to the same number of ratings for which we would like you to predict a value. Each line is of the format Movie Id, User Id, Date of rating, obviously the ratings have been omitted. For example:

      ```
      1,1046323,2005-12-19
      1,1080030,2005-12-23
      1,1830096,2005-03-14
      1,368059,2005-05-26
      1,802003,2005-11-07
      1,513509,2005-07-04
      1,1086137,2005-09-21
      ```

### Implementation Requirements

#### Task 1
You must write a simple algorithm to determine where a movie title from the netflix dataset is an alias of a movie title from the canonical dataset. Some examples of aliases would be “The Lion King” => “Lion King”, “Up!” => “Up” and “The matrix” => “The Matrix”.

#### Task 2
* Use spark to load the sampled netflix ratings (in mv_sampled.parquet) into a DataFrame
* Randomly split this DataFrame into two unequal DataFrames (i.e. an 80/20 ratio).
* Use this DataFrame to train an ALS model that can be used to predict user movie ratings (ie which rating a user will give to a movie that they have not already rated).

#### Task 3
For this task you will use the model you generated in Taks 2 to recommend 10 movies to a specific user based on their predicted rating of said movies. The user in question has the id 30878. Once you have used the model to retrieve the 10 recommended movie ids, you should use the alias map created earlier to retrieve their titles and write these recommendations to a file.

#### Task 4
This next task is a quantitative evaluation of the model which you produced in Task 2, rather than just “eyeballing” the output for a single user.

#### Task 5
In this task you will tune your model’s hyperparameters:

* Rank = 10
* Number of Iterations = 5
* Lambda = 0.01

For this, build a ParamGrid in combination with the CrossValidator as seen in class.

#### Task 6
Input File: **qualifying_simple.txt**

Using spark, pull in all the Movie Id, User Id, Date lines from qualifying_simple.txt and produce a DataFrame of (User Id, Movie Id) (you may ignore the dates). Use the model produced in Task 2 to calculate ratings for every element of this DataFrame.

Once you have done this, you should write these ratings to a file.

#### Task 7
The goal of this last task is to establish users similarity based on how they rate the same movies, using the DataFrame that you created in Task 6.

In this exercise, the similarity between users (u1, u2) is defined as the number of movies that both u1 and u2 rate at least 3.

Your task is to find the top 10 most similar users to user 30878.
