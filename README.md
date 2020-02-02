# Analysis-and-Prediction-on-Tmdb5000
### 1. Introduction  
A commercial success movie not only entertains the audience, but also enables film companies to gain tremendous profit. A lot of factors such as good directors, experienced actors are considerable for creating good movies. However, famous directors and actors can always bring an expected box-office income but cannot guarantee a highly rated Imdb score. The problem is what kind of movie will be more successful than others? Can we predict whether a movie will succeed before it is released? In this project, we analyze different factors related to profit and Imdb score, and apply random forest classifier to operate a binary classification aiming at distinguishing nice from bad movies.  
  
### 2. Probelm Description  
We try to figure out the following problems through our analysis:  
  
a.	What kind of genres earns the highest average Imdb score/profit?  
In order to find out factors leading to a successful movie, we first take genres into consideration. In our dataset, all the movies are categorized into twenty genres. Is it possible that some specific genre would always attract the audience and then invite income and reputation? We do statistics to see the total amount of each genre in our dataset. Also, we scale score and profit based on genres into 0 to 1 to analyze the relationship among genre, profit, and score.  
  
b.	Top 10 directors with the highest Imdb score/profit?  
In the film market, some directors who are good at using cutting-edge technology, such as animation effects, may be more likely to achieve commercial success. However, literary film directors who win by connotation and plot may be more favored by ratings. Do directors have an influence on the movie’s income and ratings? We want to see the distribution of profit and score by director in general, and then calculate the average score and profit based on each director.  
  
c.	Do actors have an effect on Imdb score/profit?  
The same as directors, actors are also very likely to affect the success of a movie. popular movie stars might bring high revenue, while top performing actors may bring reputation. We perform a similar analysis of the actor’s influence as the director. However, what is the difference is a movie usually has several actors. How can we decide how much an actor contributes to a movie? In order to handle this problem, we use the first four actors for analysis and give them different weights, which means the leading role counts the most, while the impact of the other three roles is descending.  
  
d.	Can we predict a movie is good or bad before it is released?  
In the last part of our study, we build a random forest model, through which we try to predict a successful movie before it is released. Through the analysis of the above problems, we can find some influencing factors on profit and scoring. Using these factors that can be known before the movie is released, such as director, actor, genre, as features, and then inputting them into random forest classifiers to achieve simple binary classification. The result can show whether a movie is good or bad.
  
### 3. Methodology
We use plotly for Python as our main visualization tool. Plotly provides a complete scientific graphing library that enables users to plot various kinds of graphs. The visualization is elegant, fancy, and also interactive. However, its documentation is incomplete and the community is inactive as well, so users can hardly get support when it comes to some problems.  
As for the prediction model, we use random forest to help us figuring out which movie will succeed. Random forest is a classifier containing multiple decision trees, and its output category is determined by the mode of the categories output by the individual trees. It can deal with high dimensional data, which matches our data characteristics very well. However, one of its problems is it tends to overfit on some classification or regression problems with high noise in the data.  
In order to evaluate both the model and predicting result efficiently, we use 10-fold cross validation and generate confusion matrix, score of precision, recall, and F1.
  
### 4. Data Description
The source of data is TMDb 5000 Movie Dataset on Kaggle [1]. The Movie Database (TMDb) is a movie and television database created by the community. The platform is a movie information query website established in 2008. This dataset contains 24 variables for 4803 movies, spanning across 100 years in 66 countries. There are 2399 unique director names, and thousands of actors/actresses.   
Most columns in the dataset are completed, except the homepage and tagline, which have 1712 and 3959 pieces of data respectively, compared to 4803 rows in total. We then drop these two columns with too much missing value and drop other columns that are unrelated to our study. Also, as can be seen in Figure 1. Movies Released Per Year, most movies in this dataset are released after 2000, so we extract the data after 2000 for analysis.  
![image](https://github.com/cyuuu4u/readme_add_pic/tree/master/images/Picture1.png)
