# Asian-Cup-Football-Data-1972---2019

![Asian Cup Football Anlaysis 1972 - 2019](https://github.com/aliabdulelah/Asian-Cup-Football-Data-1972---2019/assets/129835709/b2422dc8-2676-40f3-be41-8dd154e16917)


## Table of contents 
- [Project Overview](#Project-Overview)
- [Data Source](#Data-Source)
- [Data Tables](#Data-Tables)
- [Tools](#Tools)
- [ Data Cleaning / Preparation](#Data-Cleaning-Preparation)
- [Exploratory Data Analysis](#Exploratory-Data-Analysis)
- [Results/Findings](#Data-Analysis-Results-Findings)

  <br>
  <br>

## Project Overview

Our project aims to conduct a comprehensive analysis of the Asian Cup Football Data spanning from 1972 to 2019. The dataset encompasses a rich repository of international football matches, including FIFA World Cup fixtures and regular friendly matches, exclusively focusing on men's full internationals. Leveraging SQL data analysis techniques, we delve into various facets of the tournament's history to extract valuable insights and trends.



### Data Source
In this project, you are going to analyze analysis this big  [dataset](https://www.kaggle.com/datasets/martj42/international-football-results-from-1872-to-2017). The dataset contains information about 45,315 results of international football matches starting from the very first official match to in 1872 up to 2023. We are going to find the answers to questions like:

1.  top 10 for teams scores
2.  The most 10 teams wins
3.  champions list history 


### Data Tables
There is 3 tables that will we use to our project analysis :

1. asianfootball.csv. it's content 370 Rows

date - date of the match
home_team - the name of the home team
away_team -  the name of the away team
home_score - full-time home team score including extra time, not including penalty-shootouts
away_score - full-time away team score including extra time, not including penalty-shootouts
tournament - the name of the tournament
city - the name of the city/town/administrative unit where the match was played
country - the name of the country where the match was played
neutral - TRUE/FALSE column indicating whether the match was played at a neutral venue

2. goalscorers.csv. it's content 43,198 Rows
   
date - date of the match
home_team - the name of the home team
away_team - the name of the away team
team - name of the team scoring the goal
scorer - name of the player scoring the goal
own_goal - whether the goal was an own-goal
penalty - whether the goal was a penalty

3. winners.csv. Its content 16 Rows

winner_team -: the team win in the final match and gets the cup
date of championships: year of the championship which played matches

<br>
<br>

### Tools 
- Excel - Data Cleaning
- PostgreSQL - Data Analysis
- Tableau - Data Visualization

<br>
<be>

### Data Cleaning Preparation 

 In the initial data preparation phase, we performed the following tasks:

- Data loading and inspection.
- Handling missing values.
- Data cleaning and formatting.

<br>
<br>
<be>

### Exploratory Data Analysis
EDA involves exploring delve into various facets of the tournament's history to extract valuable insights and trends, such as:

1.  top 10 for teams scores
2.  The most 10 teams wins
3.  champions list history 
4.  loctaions for countries host 
5.  Top 10 scorers 
6.  Top 5 countries host for matches
7.  Avg scores for each champion overtime


1.  top 10 for teams scores
   

   
