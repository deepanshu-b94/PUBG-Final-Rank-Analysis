# PUBG-Final-Rank-Analysis
## Introduction
From the conception of simple games to arcade gaming and currently, living in the era of virtual gaming world full of characters, the gaming industry has seen a meteoric rise. Game developers are working extensively to bring forward the new ideas, genres and styles. Games have become more complex, supports more players and equipped with richer graphics and mechanics. Player Unknown’s Battlegrounds (PUBG) is a complex and competitive battle game, with global tournaments rewarding cash prizes driving a lot of players to take part. Each match of PUBG pits about 100 players against each other some of which are in squads of two or four while others are alone, and the last person or squad surviving is deemed the winner, rewarded with chicken dinner. Therefore, the chance of winning is slim. As such, the problem many players face is that their chance of winning is very low, especially if they’re a new player. The winning chance increases as one plays the game and becomes more proficient and experienced. Better accuracy, better reaction times and more can contribute to a winning combination for players. There are two simple ways to play the game: kill or stay hidden. There is no particular way in which the game should be played, it all depends on one’s gaming style.

It is interesting to explore player behaviour in PUBG as all players start as equal, with no predefined classes, attributes or weapons. The motivation for the project comes from the idea to explore and identify the key strategies adopted by various players in the game. In this project, we set out to analyse data to predict the rank of a player (solo or in a squad) will end up achieving based on the different gaming predictors offered like kills or damage done, weapons acquired as at the beginning of the game every player is without any weapon. Also, there is certain health-boosting equipment like health kits, energy drink which are acquired by players while scavenging for weapons and these can be used in between the game to increase the player’s health or for recovery and hence, increase one’s lifespan in the game.

## Data Description
The dataset used provides a large number of anonymized PUBG game stats, and each row contains a player’s post-game stats. The data comes from matches of all types: solos, duos, squads, and custom; there is no guarantee of there being 100 players per match, nor at most 4 players per group. Below are the data fields:

DBNOs - Number of enemy players knocked.
Assists - Number of enemy players this player damaged that were killed by teammates.
Boosts - Number of boost items used.
DamageDealt - Total damage dealt. Note: Self-inflicted damage is subtracted.
HeadshotKills - Number of enemy players killed with headshots.
Heals - Number of healing items used.
Id - Player’s Id
KillPlace - Ranking in match of number of enemy players killed.
KillPoints - Kills-based external ranking of player. (Think of this as an Elo ranking where only kills matter.) If there is a value other than -1 in rankPoints, then any 0 in killPoints should be treated as a “None”.
KillStreaks - Max number of enemy players killed in a short amount of time.
Kills - Number of enemy players killed.
LongestKill - Longest distance between player and player killed at time of death. This may be misleading, as downing a player and driving away may lead to a large longestKill stat.
MatchDuration - Duration of match in seconds.
MatchId - ID to identify match. There are no matches that are in both the training and testing set.
MatchType - String identifying the game mode that the data comes from. The standard modes are “solo”, “duo”, “squad”, “solo-fpp”, “duo-fpp”, and “squad-fpp”; other modes are from events or custom matches.
RankPoints - Elo-like ranking of player. This ranking is inconsistent and is being deprecated in the API’s next version, so use with caution. Value of -1 takes place of “None”.
Revives - Number of times this player revived teammates.
RideDistance - Total distance traveled in vehicles measured in meters.
RoadKills - Number of kills while in a vehicle.
SwimDistance - Total distance traveled by swimming measured in meters.
TeamKills - Number of times this player killed a teammate.
VehicleDestroys - Number of vehicles destroyed.
WalkDistance - Total distance traveled on foot measured in meters.
WeaponsAcquired - Number of weapons picked up.
WinPoints - Win-based external ranking of player. (Think of this as an Elo ranking where only winning matters.) If there is a value other than -1 in rankPoints, then any 0 in winPoints should be treated as a “None”.
GroupId - ID to identify a group within a match. If the same group of players plays in different matches, they will have a different groupId each time.
NumGroups - Number of groups we have data for in the match.
MaxPlace - Worst placement we have data for in the match. This may not match with numGroups, as sometimes the data skips over placements.
WinPlacePerc - The target of prediction. This is a percentile winning placement, where 1 corresponds to 1st place, and 0 corresponds to last place in the match.
The data has only one categorical value called the “match type” with standard game modes: solo, duo, squad, solo-fpp, duo-fpp, and squad-fpp

## Data Pre-processing
The dataset is sourced from one of the Kaggle data analysis competition for prediction of PUBG final winning position depending on various factors in the game [2]. Initial exploration of data didn’t highlight any anomalies and didn’t have any missing values. Although the actual data from the competition already was split into training and testing set of 4.45 million records and 1.93 million records respectively. However, due to hardware limitation, the entire analysis was carried out using a scaled-down version of training data with 49144 records. The predictors in the dataset were standardized to have all the values on the same scale for analysis. The margin of error is considered for the analysis is +/- 0.25 units. The size of the testing set (14743 records) was evaluated considering the margin of error. The training data set is worth 30% and the value is used to evaluate the training set size of 34401 records which is worth 70%.

## Methods
The objective variable (winPlacePerc) for the dataset was continuous with 26 predictors. The dataset is unique in a manner that the objective variable is continuous, but it is bounded between 0 and 1. Considering the above factors apart from the fact that the response variable is bounded, we were motivated to implement the following regression methodologies for analyzing the data :

Multiple Linear Regression
Random Forest Regression  

## Results And Discussion
The initial baseline accuracy was established to compare the results from models on testing and training set. For the test set, the baseline accuracy was calculated as the mean of losses between the test response variable and the mean of the test response variable. The mean of test loss evaluated was 0.267 units. For evaluation of model performance on the training set, 5-fold cross-validation was used to calculate the mean squared error. 

Results from the above regression techniques were very close with each other the polynomial model performing the best on the MSE values. Although, the plots of multiple linear regression models highlighted the limitation of linear regression techniques to deal with datasets having response variable within a range. All the 3 multiple regression models predicted values that are less than 0 and more than 1, which are invalid predictions considering the use-case.

In contrast, although the random forest regression technique didn’t perform as well as the polynomial model if compared on MSE values, it had other significant advantages over the multiple linear regression techniques. Random forest model resulted in all valid predictions for the test set within the range 0 and 1 overcoming the limitations of all the 3 multiple linear regression model. Random forest resulted in a much simpler model as compared to the polynomial model with some trade-off on performance. Overall with descent performance and valid predictions, the random forest model was the best model for the analysis done on PUBG dataset.
