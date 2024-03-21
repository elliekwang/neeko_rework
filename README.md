# neeko_rework
UCSD DSC 80 Project - League of Legends

<iframe
  src="assets/file-name.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


This is a data science project about League of Legends for the class DSC 80 at UCSD. 

Names: Joyce Hu and Ellie Wang


# Introduction

For our project, we are interested in exploring dataset about the game League of Legends from Oracle's Elixir. As League of Legends continues to constantly update the game, there are changes to all aspects that we want to investigate. More specifically, we aim to answer qusetions about the champion Neeko.


# Data Cleaning and Exploratory Data Analysis

For our project, we worked with smaller dataframes taken from `league`, which is the dataframe that concats together League of Legends datasets from Oracle's Elixir from the years 2021, 2022, 2023, and 2024. To appropriately clean the data, we:

- created `patch_missing`: a new column that holds a binary variable for missing patches 
- imputed missing patches by mapping specific dates to corresponding patch versions
- imputed team statistics; team-level statistics for certain variables (`firstdragon`, `firstherald`, `heralds`, `opp_heralds`) are imputed into missing player-level stats by extracting team summary stats from the dataset and merging them with player-level data based on `gameid` and `teamid`
- created `post_rework`: binary variable for patch rework; checks if patch is greater than or equal to 13.09 
- created `neeko`: binary variable to indicate whether Neeko played n the game 
- created `herald_diff`: represents the difference in number of heralds gained by the team and the opponent team 
- kept the features we need for the rest of the project 


We cleaned the dataset this way to make the data more compatible to  answer our question: is there a higher proportion of games with a Neeko in it after the Patch 13.9 rework? 