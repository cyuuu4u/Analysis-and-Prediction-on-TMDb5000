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
![image](https://github.com/cyuuu4u/readme_add_pic/blob/master/images/Picture1.png)  
  
### 5. Data Analysis
To solve the problem concerning to genre that we address at first, Figure 2. Numbers of Movies of Different Genres shows that drama and comedy are the top 2 types of movies which exist frequently on the screen, while TV movie is the least one. Through normalizing average profit and score of different genres, a scatter plot of profit and score based on genres is generated (figures plotted by plotly in jupyter notebook are interactive, so there is no legend and annotation shown). As we can see from Figure 3. Profit and Score Based on Genres, different types of movies are of great difference at profit, but not much at score. Adventure, fantasy, and animation gain both high profit and high score, while history, war, and music get a good reputation but do not earn money.  
![image](https://github.com/cyuuu4u/readme_add_pic/blob/master/images/Picture2.png)  
![image](https://github.com/cyuuu4u/readme_add_pic/blob/master/images/Picture3.png)  
  
Who is the most profitable director? Who has won the appreciation of most professionals? According to Figure 4. Distribution of Average Score and Profit by Director,  score is almost normal distributed, while profit is clustered at low level. Figure 5. Top 10 Directors with Highest Score and Profit answers our question, Rohit Jugraj gains the highest average score, and James Cameron is the director whose works have the highest profit.  
![image](https://github.com/cyuuu4u/readme_add_pic/blob/master/images/Picture4.png)  
![image](https://github.com/cyuuu4u/readme_add_pic/blob/master/images/Picture5.png)  
  
In terms of actor, the result seems to be similar to director. Figure 6. Distribution of Average Score and Profit by Actor reveals that the average score by actor is a normal distribution, and the average profit is positive skewed. Figure 7. Top 10 Actors with Highest Score and Profit tells that Mel England is the highest scored actor, while movies starring Neel Sethi is the most profitable.  
![image](https://github.com/cyuuu4u/readme_add_pic/blob/master/images/Picture6.png)  
![image](https://github.com/cyuuu4u/readme_add_pic/blob/master/images/Picture7.png)  
  
After a preliminary analysis of our data, we build a random forest classifier with genre, director, and actor as input features to predict whether a movie will be successful or not based on its score. However, these input data are all categorical and cannot be read by our model, so we transform them into binary. To take actor as an example, if the movie contains one specific actor, the corresponding column value will be 1, otherwise 0. Eventually, we get a set of high-dimensional input data, which is ideal for random forest algorithm. As for the corresponding label, we calculate the average score of all the movies in the dataset and consider movies above average as a successful movie and label it as 1, while the opposite is 0. According to Figure 8. Good vs. Bad Movies, there are 2035 movies in our dataset considered to be nice movies. With the data getting prepared, we construct a random forest model using sk-learn package.  
![image](https://github.com/cyuuu4u/readme_add_pic/blob/master/images/Picture8.png)  
  
### 6. Evaluation
We evaluate the model using 10-fold cross validation. The result shows an accuracy of 65%. In addition, according to Figure 9. Confusion Matrix, 369 nice movies and 207 bad movies are predicted correctly. Also, as can be seen in Table 1. Classification Report, the average scores of precision, recall, and F1 are all 0.67, and our model seems to have a better performance on positive samples.  
![image](https://github.com/cyuuu4u/readme_add_pic/blob/master/images/Picture9.png)  
  
### 7. Discussion
The differences in ratings and benefits for different genres are significant, especially in terms of profit, which divides all the genres into two distinct parts. Directors and actors have similar distributions in average score and profit, most of which have a medium average score and lower profit. Although the prediction model has a better performance on positive samples, it can effectively implement the binary classification of good and bad movies with limited input features. The performance of our model still needs to be optimized, and more than 80% is an ideal accuracy rate.  
  
### 8. Conclusion
In this study, we analyze how genre, director, and actor influence the profit and score of a movie. Then, we build a random forest classifier with genre, director, and actor as input features to predict whether a movie will be successful or not based on its score, which may have practical applications in investment advice, box office forecasting, etc. According to the result, we find that adventure, fantasy, and animation are genres that gain both high profit and high score, while history, war, and music get a good reputation but do not earn money. Rohit Jugraj is the director who gains the highest average score, and James Cameron’s works have the highest profit. Mel England is the highest scored actor, while movies starring Neel Sethi is the most profitable.  
  
In the process of data analysis, we also encountered many problems. For one thing, information of director, genre, and actor is stored in json format, and one movie usually has several actors and genres. It is a challenge for us to extract the required information, and to do statistics. For another, since the leading roles and other roles contribute differently to a movie, how do we measure the impact of actors on ratings and profit? In this study, we use the first four actors for analysis and give them different weights, which means the leading role counts the most, while the impact of the other three roles is descending.  
  
A limitation in our study is the low accuracy of prediction, and the model performs significantly better on positive samples. One possible reason is the processing method of input data is not effective enough, so that some features may be lost during the transformation. Another is we use the default parameters in the model, and there might be an increase in accuracy after parameter adjustment.  
  
With regard to future work, it is necessary to improve the performance of the model. In addition to binary classification, a prediction of the exact Imdb score might be more practical and challenging.  
  
### Reference
References
[1] 	T. M. Dataset(TMDb), "TMDB 5000 Movie Dataset," Kaggle, [Online]. Available: https://www.kaggle.com/tmdb/tmdb-movie-metadata.


