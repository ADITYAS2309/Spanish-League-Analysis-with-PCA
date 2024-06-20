# **Analysis of LaLiga 2023/24 Using Unsupervised Learning**

## **Overview**

In the modern era of sports analytics, understanding player performance and characteristics through data is crucial for gaining competitive advantages. This project applies Principal Component Analysis (PCA) to La Liga players from the 2023/2024 season. PCA is a statistical technique used to reduce the dimensionality of large datasets while preserving as much variance as possible. By doing so, it simplifies the complexity of player data, making it easier to identify patterns and insights.

The primary objectives of this project are:

1. Utilize PCA to reduce the multidimensional player performance dataset into a concise set of principal components, simplifying analysis and interpretation.
2. Compare individual players or groups of players based on their principal components to uncover similarities and differences in playing styles, strengths, and weaknesses.
3. Identify distinct player types based on performance metrics, facilitating a deeper understanding of player roles and contributions within teams.
4. Generate actionable insights into the key factors influencing player performance, which can inform strategic decisions related to player development, recruitment/transfers, and tactical planning.

## **Data**

The data was taken from kaggle. 
Link to the dataset: https://www.kaggle.com/datasets/sdelquin/laliga-data3

## **Python Libraries Used**

* Pandas
* Numpy
* Matplotlib
* Seaborn
* Sklearn

## **Data Cleaning & Pre-processing**

* The dataset consisted of 681 players measured along over 150 characteristics. The data had players teams that were not part of Laliga 2023/24. These were players who played in Laliga for a short time before being transferred to other teams. These players were removed.

* Columns like gender, nickname, player.url and other unnessary columns were dropped.

* DOB was replace by Age. The Age was calculated with reference to the starting data of the season.

* Duplicated players were removed.

* Null values for height and weigth were imputed with there respective means.

* For all other columns which measured different characterirics, a null value meant a measurement of 0. For example, the null under goals_scored column meant the respective player scored 0 goals for the season. Such nulls were replaced with value of 0 over all other columns.

* Selection of players for Analysis: There were players with a small game time. These would be outliers and were removed.Laliga and sport leagues generally have a criteria to filter players for conducting analysis, and using that criteria, we will consider players who have played 900 minutes (equivalent to 10 full matches).
  
* We split the datasets based on the positions of the players. Since players play at different positions, it will be meaningfull to categorize them as per position and then conduct the analysis. This is because each position have distinct roles and skill sets and combining these diverse metrics in a single PCA might obscure patterns specific to each position.
  
* All the columns were standardize to have a mean of 0 and standard deviation of 1

## **Results**

### PCA on Defenders

PCA was carried on the datasets with columns relevant to the defenders. 4 principle components were selected from scree plot which explain 63% of the total variance.

**1st Principle Component: Consistent vs Irregular Starters/Gametime**

The 1st principle component accounts for 32% of the total variance. Majority of the signifcant loadings are positive. The first component represents their involvement in the game . Defenders with positive PC1 score are stable, highly involved in the game, pivotal in maintaining and rgaining possession, and are regular starters because of their reliability. These include defenders like S. Ramos, J. Kounde, S. Cardona, M. Marmal etc. While defenders with negative PC1 score are those who do not get much game time, infrequently make the starting 11, because of their unreliable nature or being injury-prone. They aren't much involved in the game and hence don't get consistent game time. These include players like  A. Sedlar, D. Alaba, A. Centelles, J. Gimenez, etc. Refer the plot to know more about differnt players.
 
**2nd Principle Component: Aerial Dominant vs Ground Dominant**

The 2nd principle component explains 16% of the total variance. The significant loadings are evently distributed across the 2 signs. The 2nd principle component is along the dominant nature of defenders. The positive loadings describe strong dominance on ground while the negative loadings describe the towering nature of defenders, who have strong aerial dominance. Defenders with high positive PC2 score excel in abilities on ground. These include Y. Couto, J. Cancelo, M. Gutierrez etc. While defenders with large negative PC2 score are dominant in air. These include R. Le Normand, S. Ramos, F. Lejeune etc.

**3rd Principle Component: Ball Playing Defenders vs Defensive Liable Defenders**

This component explains around 9% of the total variance. It is along the direction of ball playing nature vs defensively liable defenders. Players with high PC3 score are ball playing defenders, who love distributing the ball from back to building attacks. The excel in their passing abilites. These include M. Gutierrez, D. Carvajal, D. Blind, etc. Players with large negative PC3 score struggle in maintaining defensive stability, vulnerabilites in backline, undisciplined, defense liability, and not good at keeping cleansheets. These include R. Marin, A. Abqar, A. Gorosabel etc.

**4th Principle Component: Goal Scoring vs Traditional Defenders**

4th component explains 6% of the toal variance. It represents thier attacking vs traditional nature of defenders. Majority of significant loadings are positive. Defenders with high PC4 score are goal scoring defenders, who show their attacking nature and score goals. These include D. Carvajal, E. Garcia, A. Raillo etc. While defenders with large negative PC4 are traditional defenders, who are more defendsively focus, and prefer to sit back and defend. These include D. Blind, M. Marmol, C. Neva, etc.


Similar analysis can be performed on forwards, midfielders, and goalkeepers. Analysis on forwards in done in the jupyter notebooks.


## Other Analysis

**Team Analysis**

The principle component scores of players can be aggregated to get team principle scores, which can be used for analysis. This is done in jupyter notebook for comparing the defensive attributes across teams. Analysis for it can be done in same way as above. 

Aggregated team scores can be computed in various ways which include sum of individual PC scores, average, weighted average, and so on. Weighted average is used in the notebook with minutes played by each player as weight.


**Player Comparision**

The principle scores for individual players can we used to compare players across different attributes, to find players with similar/different nature. This can be done by clustering the combined PC scores to group players who show similar playng patterns/styles. Another method is using principle compomemt score vector norm for each player and computing the euclidean distance between 2 players. Players with small distance would show similar patterns and those with large distances would be different from each other.
