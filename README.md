# neeko_rework
UCSD DSC 80 Project - League of Legends


This is a data science project about League of Legends for the class DSC 80 at UCSD. 

Names: Joyce Hu and Ellie Wang


# Introduction

For our project, we are interested in exploring dataset about the game League of Legends from Oracle's Elixir. As League of Legends continues to constantly update the game, there are changes to all aspects that we want to investigate. 
In this project, we will focus on Neeko, one of the League of Legends champions. Released in 2018, Neeko is a mage champion with chameleon-like abilities. Despite her potential to confuse opponents through shapeshifting, she was not a popular champion--especially in pro play. However, following Patch 13.9, Neeko gained many significant changes to her abilities and power. Thus, we will focus on how those changes may have affected her popularity in League of Legends.


# Data Cleaning and Exploratory Data Analysis

## Data Cleaning

For our project, we worked with smaller dataframes taken from `league`, which is the dataframe that concats together League of Legends datasets from Oracle's Elixir from the years 2021, 2022, 2023, and 2024. To appropriately clean the data, we:

- created `patch_missing`: a new column that holds a binary variable for missing patches 
- imputed missing patches by mapping specific dates to corresponding patch versions
- imputed team statistics; team-level statistics for certain variables (`firstdragon`, `firstherald`, `heralds`, `opp_heralds`) are imputed into missing player-level stats by extracting team summary stats from the dataset and merging them with player-level data based on `gameid` and `teamid`
- created `post_rework`: binary variable for patch rework; checks if patch is greater than or equal to 13.09 
- created `neeko`: binary variable to indicate whether Neeko played n the game 
- created `herald_diff`: represents the difference in number of heralds gained by the team and the opponent team 
- kept the features we need for the rest of the project 


We cleaned the dataset this way to make the data more compatible to  answer our question: is there a higher proportion of games with a Neeko in it after the Patch 13.9 rework? 

| gameid                | teamid                                  |   neeko | position   | datacompleteness   | league   |   patch |   firstdragon |   firstherald |   herald_diff |   goldat15 |   xpat15 |   csat15 |   golddiffat15 |   xpdiffat15 |   csdiffat15 |   killsat15 |   assistsat15 |   deathsat15 |   result |
|:----------------------|:----------------------------------------|--------:|:-----------|:-------------------|:---------|--------:|--------------:|--------------:|--------------:|-----------:|---------:|---------:|---------------:|-------------:|-------------:|------------:|--------------:|-------------:|---------:|
| ESPORTSTMNT03/1632489 | oe:team:2e79800a550f87f2378dbba9368396d |       0 | top        | complete           | KeSPA    |   10.25 |             1 |             1 |             2 |       5407 |     7536 |      114 |            748 |          -56 |           -4 |           2 |             0 |            1 |        1 |
| ESPORTSTMNT03/1632489 | oe:team:2e79800a550f87f2378dbba9368396d |       0 | jng        | complete           | KeSPA    |   10.25 |             1 |             1 |             2 |       6974 |     8232 |      146 |           2120 |         3405 |           62 |           3 |             2 |            0 |        1 |
| ESPORTSTMNT03/1632489 | oe:team:2e79800a550f87f2378dbba9368396d |       0 | mid        | complete           | KeSPA    |   10.25 |             1 |             1 |             2 |       6591 |     7827 |      158 |           1578 |          354 |           15 |           2 |             3 |            0 |        1 |
| ESPORTSTMNT03/1632489 | oe:team:2e79800a550f87f2378dbba9368396d |       0 | bot        | complete           | KeSPA    |   10.25 |             1 |             1 |             2 |       5202 |     5053 |      130 |            124 |          102 |           10 |           0 |             4 |            2 |        1 |
| ESPORTSTMNT03/1632489 | oe:team:2e79800a550f87f2378dbba9368396d |       0 | sup        | complete           | KeSPA    |   10.25 |             1 |             1 |             2 |       3853 |     4681 |       28 |            448 |          450 |            3 |           1 |             4 |            0 |        1 |

## Univariate Data:
<iframe
  src="assets/univariate.html"
  width="800"
  height="500"
  frameborder="0"
></iframe>

Working with only data from games that Neeko played, this plot shows the distribution of positions that Neeko played. From the plot, we can see that `mid` is the most played position by Neeko. 

## Bivariate Data:

<iframe
  src="assets/bivariate.html"
  width="800"
  height="500"
  frameborder="0"
></iframe>

This plot (Neeko only) shows the relationship between the column `goldat15` and `csat15`, which are the amount of gold collected at 15 minutes and the number of minions killed at 15 minutes by Neeko. We can see a positive correlation between the two variables since as the amount of gold collected increases, the number of minions killed increases as well. 

## Interesting Aggregates:
This is a pivot table of the number of games with neeko from patch 12.10 to 14.05, seperated by the position she was played in. It is interesting because we can see the amount of games she was played in increases over time. 

| patch   |   bot |   jng |   mid |   sup |   top |   total |
|:--------|------:|------:|------:|------:|------:|--------:|
| 12.1    |     0 |     0 |     0 |     0 |     1 |       1 |
| 12.11   |     0 |     0 |     1 |     0 |     0 |       1 |
| 12.12   |     1 |     0 |     0 |     0 |     0 |       1 |
| 12.13   |     0 |     0 |     1 |     3 |     0 |       4 |
| 12.14   |     0 |     0 |     1 |     0 |     0 |       1 |
| 12.15   |     0 |     0 |     2 |     0 |     0 |       2 |
| 12.16   |     0 |     1 |     0 |     0 |     2 |       3 |
| 12.17   |     0 |     0 |     0 |     0 |     0 |       0 |
| 12.18   |     0 |     0 |     0 |     0 |     0 |       0 |
| 12.19   |     0 |     0 |     1 |     0 |     0 |       1 |
| 12.2    |     0 |     0 |     0 |     0 |     1 |       1 |
| 12.21   |     0 |     0 |     0 |     0 |     0 |       0 |
| 12.23   |     0 |     0 |     0 |     0 |     0 |       0 |
| 13.01   |     0 |     0 |     0 |     0 |     1 |       1 |
| 13.03   |     0 |     0 |     0 |     0 |     0 |       0 |
| 13.04   |     0 |     0 |     2 |     0 |     0 |       2 |
| 13.05   |     0 |     0 |     0 |     0 |     0 |       0 |
| 13.06   |     0 |     0 |     0 |     0 |     0 |       0 |
| 13.07   |     0 |     0 |     0 |     0 |     1 |       1 |
| 13.08   |     0 |     0 |     0 |     0 |     0 |       0 |
| 13.09   |     0 |     0 |     0 |     0 |     0 |       0 |
| 13.1    |     0 |    14 |   103 |     0 |     1 |     118 |
| 13.11   |     0 |    13 |   131 |     3 |     0 |     147 |
| 13.12   |     0 |     3 |   105 |     2 |     0 |     110 |
| 13.13   |     0 |    11 |   117 |     1 |     2 |     131 |
| 13.14   |     0 |     5 |   102 |     1 |     0 |     108 |
| 13.15   |     0 |     0 |    50 |     1 |     1 |      52 |
| 13.16   |     0 |     0 |     4 |     0 |     1 |       5 |
| 13.17   |     0 |     0 |    15 |     0 |     0 |      15 |
| 13.18   |     0 |     0 |    13 |     1 |     0 |      14 |
| 13.19   |     0 |     1 |    50 |     1 |     0 |      52 |
| 13.2    |     0 |     0 |     7 |     0 |     0 |       7 |
| 13.21   |     0 |     0 |    10 |     0 |     0 |      10 |
| 13.22   |     0 |     0 |     1 |     0 |     0 |       1 |
| 13.24   |     0 |     0 |    21 |     1 |     0 |      22 |
| 14.01   |     0 |     0 |   120 |    15 |     0 |     135 |
| 14.02   |     0 |     0 |    95 |    14 |     0 |     109 |
| 14.03   |     0 |     0 |     0 |     0 |     0 |       0 |
| 14.04   |     0 |     0 |    73 |    10 |     0 |      83 |
| 14.05   |     0 |     1 |    36 |     4 |     0 |      41 |
| total   |     1 |    49 |  1061 |    57 |    11 |    1179 |

# Assessment of Missingness

## NMAR Analysis
We do not belive that there is a column in our dataset that is NMAR. While there are a lot of columns with missing data, we believe that most are related to the column `datacompletedness`. 

Additionally, based on our preliminary findings when looking at the "patch" column that has missing data, we believe that the column "league", which is composed of the different leagues played in the game, could explain the missingness since we found that there were only missing patches for two leagues out of the 56.

## Missingness Dependency: `patch`

A column that is important to our hypothesis test is the `patch` column. However, we found that the `patch` column had **382840** missing values. We analyzed its relationship with the `league` and `result` columns to check its missingness dependency. 

### 1. `patch` v. `league`
**Observed Statistic:** 0.8440988106129917

**p-value:** 0.0

**Conclusion:** Since our p-value = 0.0 which is less than our alpha value of 0.5, we conclude that the missingness of `patch` **does** depend on `league`.

<iframe
  src="assets/patch1_2.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>

<iframe
  src="assets/patch1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


### 2. `patch` v. `result`
**Observed Statistic:** 0.00014377205594040543

**p_value:** 1.0

**Conclusion:** Since our p-value = 1.0 which is greater than our alpha level of 0.05, we can conclude that the missingness of `patch` **does not** depend on the `result` column. 

<iframe
  src="assets/fig2_2.html"
  width="800"
  height="450"
  frameborder="0"
></iframe>

<iframe
  src="assets/patch2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


# Hypothesis Testing

**Question:** Is there a higher proportion of games with a Neeko in it after the Patch 13.9 rework?

**Null:** There is no difference in proportion of games with Neeko before and after the Patch 13.9 rework.


**Alternative:** There is a higher proportion of games with Neeko after the Patch 13.9 rework. 


**Test Statistic:** Difference in Proportion, more specifically the proportion of games with Neeko after minus before the patch 13.9
- We chose difference in proportion because our data is categorical and directional.
- Our observed statistic: 0.1404526229251691

**Significance Level:** 0.05
- We used a significance level of 5% to increase accuracy of our randomized test result. 


**Result p-value:** 0
- We ran 10,000 repetitions. 

**Conclusion:** As the p-value is 0, we reject the null hypothesis in favor of the alternative hypothesis, which is that there is a higher proportion of games with Neeko after the Patch 13.9 rework. 

# Prediction
#### Can we predict whether Neeko's team wins the game based on her stats at 15 minutes?
Our prediction problem focuses on trying to predict whether Neeko's team can win the game at 15 minutes because that is when the team can choose to forfeit the game if they think they will lose. 

For our prediction problem, we are performing binary classification. Our response variable is the `result` column, where the values represent whether Neeko's team won the game or not. We chose this variable because it is a interpretable measure of success (win or loss) and aligns well with our objective of prediciting the game outcomes. 

The metric we chose for evaluating the model's performance is recall because it is more harmful to the team to forfeit when they could have won. False positives are less harmful because even if they lose later on, forfeiting is a guaranteed loss. However, we will also consider the F1-score just to make sure there is balance between the recall and precision of our model. 

We will include 2021 data in our training model to include more data into the model. It is not a concern because Neeko doesn't change much between seasons. 

### Baseline Model

**Here is a list with explanations of the columns we will be looking at for our baseline model:**

`goldat15`: Total amount of gold accumulated by Neeko at 15 minutes.

`xpat15`: Total amount of experience points earned by Neeko at 15 minutes. 

`csat15`: Total number of minion kills by Neeko's **team** at 15 minutes. 

`killsat15`: Total number of enemy champions killed by Neeko at 15 minutes. 

`assistsat15`:	Total number of assists obtained by Neeko at 15 minutes. 

`deathsat15`: Total number of deaths of Neeko at 15 minutes.

`position`: Neeko's position in the game (`bot`, `top`, `mid`, `sup`, and `jng`) 


Our baseline model is a binary classifier using a `LogisticRegression` model that predicts whether Neeko's team wins the game or not given features recorded at 15 minutes of the game. 

For the baseline, we included nominal features, which are the one-hot encoded columns of Neeko's position, and the quantitative columns of Neeko's gold, experience points, number of minions, deaths, kills, and assists at 15 minutes. 

We performed the one hot endcoding using the `OneHotEncoder()` method from scikit-learn.

#### Baseline Model Analysis

The Baseline Model achieved a test set recall of 0.79 and a F1 score of 0.72, so its overall performance is pretty good but can still be improved. The recall and F1 scores are also similar to its training scores so it is unlikely that it is overfitting. 

### Improving on Baseline

To improve on the model, we added a new variable, `herald_diff`, which indicates how many more rift heralds the opposing team has. We will also added binary variables for whether Neeko or her opponent was performing better at 15 minutes. Lastly, we standardized some of the numeric columns so we could know how much better in general her stats are at 15 minutes that in other games. 

Furthermore, we utilized different techniques to find the best model overall. First we searched for the best threshold to use in the `LogisticRegression` model. Next, we tried a `RandomForestClassifier` and hypertuned its parameters using `GridSearchCV` to find the best `min_samples_split`, `max_depth`, and `criterion`. 

## Final Model

In the end, we decided to choose the `RandomForestClassifier` model with tuned hyperparameters (`criterion` = 'entropy', `max_depth` = 22, and `min_samples_split` = 40) as the final model.  
Although our base model actually had a higher recall score (testing set = 0.79), this final model has a higher F1 score (0.74) and a much better accuracy (0.72). Since we still do care about False Positives too, we decided to go with the model with the higher F1 score overall. 

Our final model probably performed better than the Baseline model because we added more features and preprocessing steps. Also, a `RandomForestClassifier` fits many trees to find the best prediction. 

# Fairness Analysis

#### Does our model perform better for Tier 1 leagues than non-Tier 1 leagues?

**Null Hypothesis**: Our model is fair. Its F1 score for Tier 1 leagues and non-Tier 1 leagues are roughly the same, and any differences are due to random chance.  
Alternative Hypothesis: Our model is unfair. Its F1 score for non-Tier 1 leagues are lower than its F1 score for Tier 1 leagues.  

**Evaluation Metric**: Our evaluation metric is the F1 score because we want to balance between not having too many false positives or negatives. 

**Test Statistic**: Difference in F1 Scores

**Significance Level**: 0.01

From our p-value of 0.508, we fail to reject our null hypothesis. There does not seem to be any significant differences in our model's F1 prediction scores for Tier 1 and non-Tier 1 leagues. Thus, it appears that our model achieves parity for these two groups.

<iframe
  src="assets/f1_hyptest.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>



