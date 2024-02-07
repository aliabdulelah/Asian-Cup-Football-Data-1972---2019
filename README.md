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
<br>
<be>
<be>

### Data Tables
There is 3 tables that will we use to our project analysis :

1. asianfootball.csv. it's content 370 Rows

date - date of the match
  <br>
home_team - the name of the home team
  <br>
away_team -  the name of the away team
  <br>
home_score - full-time home team score including extra time, not including penalty-shootouts
  <br>
away_score - full-time away team score including extra time, not including penalty-shootouts
  <br>
tournament - the name of the tournament
  <br>
city - the name of the city/town/administrative unit where the match was played
  <br>
country - the name of the country where the match was played
  <br>
neutral - TRUE/FALSE column indicating whether the match was played at a neutral venue


2. goalscorers.csv. it's content 43,198 Rows
    
date - date of the match
  <br>
home_team - the name of the home team
  <br>
away_team - the name of the away team
  <br>
team - name of the team scoring the goal
  <br>
scorer - name of the player scoring the goal
  <br>
own_goal - whether the goal was an own-goal
  <br>
penalty - whether the goal was a penalty
  <br>

3. winners.csv. Its content 16 Rows
  

winner_team -: the team win in the final match and gets the cup
  <br>
date of championships: year of the championship which played matches

<br>
<br>

### Tools 
- Excel - Data Cleaning
- PostgreSQL - Data Analysis
- Tableau - [Data Visualization]([https://www.kaggle.com/datasets/martj42/international-football-results-from-1872-to-2017](https://tabsoft.co/3ummkfy))

<br>
<be>

### Data Cleaning Preparation 

 In the initial data preparation phase, we performed the following tasks:

- Data loading and inspection.
- Handling missing values.
- Data cleaning and formatting.

<br>
<br>
<br>

### Exploratory Data Analysis
EDA involves exploring delve into various facets of the tournament's history to extract valuable insights and trends, such as:

1.  top 10 for teams scores
2.  The most 10 teams wins
3.  champions list history 
4.  loctaions for countries host 
5.  Top 10 scorers 
6.  Top 5 countries host for matches
7.  Avg scores for each championships overtime

<br>

1.  top 10 for teams scores
   <br>
   
![top 10 for teams scores](https://github.com/aliabdulelah/Asian-Cup-Football-Data-1972---2019/assets/129835709/9f8569a1-e78b-4912-874c-71ac43ce1c1b)

   ```sql
--Total Teamm scores
--We used CTE to find total scores for each home_team
WITH home AS (SELECT home_team,
SUM(home_score) AS total_home_score
FROM 'asianfootball.csv'
			  WHERE date > '1968-12-31T00:00:00.000'
GROUP BY home_team
ORDER BY total_home_score DESC)
,
--We used CTE to find total scores for each away_team
away AS (SELECT away_team,
SUM(away_score) AS total_away_score
FROM 'asianfootball.csv'
		 WHERE date > '1968-12-31T00:00:00.000'
GROUP BY away_team
ORDER BY total_away_score DESC)
--we used FULL JOIN for match and combine CTE ( home and away)
SELECT home.home_team As team , (home.total_home_score + away.total_away_score) AS Total_Scores
FROM home
FULL JOIN away 
ON home.home_team = away.away_team
ORDER BY total_scores DESC
LIMIT 10;
```

2.  The most 10 teams wins
<br>

![The most 10 teams wins](https://github.com/aliabdulelah/Asian-Cup-Football-Data-1972---2019/assets/129835709/f4b4300b-453f-4644-8ac0-e79b86de87d3)

 ```sql
  --- we used CTE to Sum home_team wins 
WITH Teams_win_home AS (SELECT home_team ,
	  SUM(Case When Home_score > Away_score THEN 1
	 Else 0 End ) AS results_home
	 
	 FROM 'asianfootball.csv'
						WHERE date > '1968-12-31T00:00:00.000'
GROUP BY home_team
ORDER BY results_home DESC)
,
-- we used CTE to Sum away_team wins 
Teams_win_Away AS (SELECT Away_team ,
	  SUM(Case When Home_score < Away_score THEN 1
	 Else 0 End ) AS results_away
				   
FROM 'asianfootball.csv'
				   WHERE date > '1968-12-31T00:00:00.000'
GROUP BY Away_team
ORDER BY results_away DESC)
	 

-- we used INNER JOIN to combine CTE(Teams_win_home , Teams_win_)
SELECT h.home_team AS Team_name, (h.results_home + a.results_away) AS No_Win_of_Teams
FROM teams_win_home AS h
INNER JOIN teams_win_away AS a
ON h.home_team = a.away_team
WHERE No_Win_of_Teams <> 0
ORDER BY No_Win_of_Teams DESC
LIMIT 10; 
   
```

3. champions list history

![champions list history](https://github.com/aliabdulelah/Asian-Cup-Football-Data-1972---2019/assets/129835709/80fe7b88-be82-4766-83d6-f1ca52feb274)


 ```sql
SELECT *
FROM 'winners.csv'
WHERE date_of_championship > 1968;
```

4.  loctaions for countries host

![loctaions for countries host](https://github.com/aliabdulelah/Asian-Cup-Football-Data-1972---2019/assets/129835709/99b6ccab-19fd-4460-97c3-0a77977a7758)


5.  Top 10 scorers 

![Top 10 scorers ](https://github.com/aliabdulelah/Asian-Cup-Football-Data-1972---2019/assets/129835709/02045ae8-cda3-41d4-8923-a2417c9cbd55)

 ```sql
--we used Left join to match with Asian games and group by team and scorers
SELECT g.team , 
g.Scorer,
Count(g.*) AS Scores
FROM 'asianfootball.csv' AS r
LEFT JOIN 'goalscorers.csv' AS g
ON r.date = g.date And r.home_team = g.home_team And r.away_team = g.away_team
WHERE g.team IS NOT NULL AND r.date > '1968-12-31T00:00:00.000'
GROUP BY g.team , g.scorer
ORDER BY Scores DESC , scorer ASC
LIMIT 10;
```

6.  Top 5 countries host for matches

![Top 5 countries host for matches](https://github.com/aliabdulelah/Asian-Cup-Football-Data-1972---2019/assets/129835709/66ea233f-d6a2-43a6-8d6e-3446700d1dff)

 ```sql
--we used count with group to find top 5 countries host matches
SELECT country ,
COUNT(*) AS no_matches_host
FROM 'asianfootball.csv'
WHERE date > '1968-12-31T00:00:00.000'
GROUP BY country
ORDER BY no_matches_host DESC
LIMIT 5;
```
7.  Avg scores for each championships overtime
   ![Avg scores for each championships overtime](https://github.com/aliabdulelah/Asian-Cup-Football-Data-1972---2019/assets/129835709/1fc2b5b7-c337-4f17-8fe3-320a99303b81)


 ```sql
--we used matches and sum of home_team and away away_team then we use average funciton to get avg_score and we found in 2007 there 4 countries hosted this champion so we used UNION all to process this issue 
SELECT country,
EXTRACT(year FROM date) AS year ,
ROUND(Avg(home_score + away_score),1) AS Avg_Score_Cup
FROM 'asianfootball.csv'
WHERE date > '1968-12-31T00:00:00.000' AND year <> 2007
GROUP BY country ,year
UNION ALL
SELECT
  'Vietnam,Malaysia,Thailand ,Indonesia' AS country,
  EXTRACT(year FROM date) AS year,
  ROUND(AVG(home_score + away_score), 1) AS Avg_Score_Cup
FROM 'asianfootball.csv'
WHERE EXTRACT(year FROM date) = 2007
GROUP BY year
ORDER BY year ASC;
```


### Data-Analysis-Results-Findings

 In our analysis, we uncovered findings within the Asian Cup Football Data from 1972 to 2019.

1. Notably, Iran emerged as the team with the highest number of wins, boasting 37 wins, alongside the highest goals of 120 goals. 

2. Japan secured the title of the most champions 4 cups.

3. the UAE stands out as the nation that hosted the most matches. 

4. Ali Daei of the Iran national team holds the distinction of being the top scorer across all championships.
   
5. the year 1980 witnessed the highest average goals per match. reaching an impressive 3.2 goals. 

These insights underscore the diverse dynamics and historical achievements within the Asian Cup tournament.
