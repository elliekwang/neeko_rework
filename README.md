# neeko_rework
UCSD DSC 80 Project - League of Legends


This is a data science project about League of Legends for the class DSC 80 at UCSD. 

Names: Joyce Hu and Ellie Wang


# Introduction

For our project, we are interested in exploring dataset about the game League of Legends from Oracle's Elixir. As League of Legends continues to constantly update the game, there are changes to all aspects that we want to investigate. More specifically, we aim to answer qusetions about the champion Neeko.


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

## Bivariate Data:
<iframe
  src="assets/file-name.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

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
  src="assets/patch1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


### 2. `patch` v. `result`
**Observed Statistic:** 0.00014377205594040543

**p_value:**: 1.0

**Conclusion:** Since our p-value = 1.0 which is greater than our alpha level of 0.05, we can conclude that the missingness of `patch` **does not** depend on the `result` column. 

<iframe
  src="assets/patch2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>






