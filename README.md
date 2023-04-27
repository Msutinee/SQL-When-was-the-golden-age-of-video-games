## 1. The ten best-selling video games
<p><img src="https://assets.datacamp.com/production/project_1413/img/video_game.jpg" alt="A video game player choosing a game to play on Nintendo Switch." width="400"></p>
<p>Photo by <a href="https://unsplash.com/@retromoon">Dan Schleusser</a> on <a href="https://unsplash.com">Unsplash</a>.</p>
<p>Video games are big business: the global gaming market is projected to be worth more than $300 billion by 2027 according to <a href="https://www.mordorintelligence.com/industry-reports/global-gaming-market">Mordor Intelligence</a>. With so much money at stake, the major game publishers are hugely incentivized to create the next big hit. But are games getting better, or has the golden age of video games already passed?</p>
<p>In this project, we'll explore the top 400 best-selling video games created between 1977 and 2020. We'll compare a dataset on game sales with critic and user reviews to determine whether or not video games have improved as the gaming market has grown.</p>
<p>Our database contains two tables. We've limited each table to 400 rows for this project, but you can find the complete dataset with over 13,000 games on <a href="https://www.kaggle.com/holmjason2/videogamedata">Kaggle</a>. </p>
<h3 id="game_sales"><code>game_sales</code></h3>
<table>
<thead>
<tr>
<th style="text-align:left;">column</th>
<th>type</th>
<th>meaning</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;"><code>game</code></td>
<td>varchar</td>
<td>Name of the video game</td>
</tr>
<tr>
<td style="text-align:left;"><code>platform</code></td>
<td>varchar</td>
<td>Gaming platform</td>
</tr>
<tr>
<td style="text-align:left;"><code>publisher</code></td>
<td>varchar</td>
<td>Game publisher</td>
</tr>
<tr>
<td style="text-align:left;"><code>developer</code></td>
<td>varchar</td>
<td>Game developer</td>
</tr>
<tr>
<td style="text-align:left;"><code>games_sold</code></td>
<td>float</td>
<td>Number of copies sold (millions)</td>
</tr>
<tr>
<td style="text-align:left;"><code>year</code></td>
<td>int</td>
<td>Release year</td>
</tr>
</tbody>
</table>
<h3 id="reviews"><code>reviews</code></h3>
<table>
<thead>
<tr>
<th style="text-align:left;">column</th>
<th>type</th>
<th>meaning</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;"><code>game</code></td>
<td>varchar</td>
<td>Name of the video game</td>
</tr>
<tr>
<td style="text-align:left;"><code>critic_score</code></td>
<td>float</td>
<td>Critic score according to Metacritic</td>
</tr>
<tr>
<td style="text-align:left;"><code>user_score</code></td>
<td>float</td>
<td>User score according to Metacritic</td>
</tr>
</tbody>
</table>
<p>Let's begin by looking at some of the top selling video games of all time!</p>


```sql
%%sql
postgresql:///games

-- Select all information for the top ten best-selling games
-- Order the results from best-selling game down to tenth best-selling

SELECT *
FROM game_sales
WHERE game IS NOT NULL
ORDER BY games_sold DESC

LIMIT 10;
```

    10 rows affected.





<table>
    <thead>
        <tr>
            <th>game</th>
            <th>platform</th>
            <th>publisher</th>
            <th>developer</th>
            <th>games_sold</th>
            <th>year</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Wii Sports for Wii</td>
            <td>Wii</td>
            <td>Nintendo</td>
            <td>Nintendo EAD</td>
            <td>82.90</td>
            <td>2006</td>
        </tr>
        <tr>
            <td>Super Mario Bros. for NES</td>
            <td>NES</td>
            <td>Nintendo</td>
            <td>Nintendo EAD</td>
            <td>40.24</td>
            <td>1985</td>
        </tr>
        <tr>
            <td>Counter-Strike: Global Offensive for PC</td>
            <td>PC</td>
            <td>Valve</td>
            <td>Valve Corporation</td>
            <td>40.00</td>
            <td>2012</td>
        </tr>
        <tr>
            <td>Mario Kart Wii for Wii</td>
            <td>Wii</td>
            <td>Nintendo</td>
            <td>Nintendo EAD</td>
            <td>37.32</td>
            <td>2008</td>
        </tr>
        <tr>
            <td>PLAYERUNKNOWN&#x27;S BATTLEGROUNDS for PC</td>
            <td>PC</td>
            <td>PUBG Corporation</td>
            <td>PUBG Corporation</td>
            <td>36.60</td>
            <td>2017</td>
        </tr>
        <tr>
            <td>Minecraft for PC</td>
            <td>PC</td>
            <td>Mojang</td>
            <td>Mojang AB</td>
            <td>33.15</td>
            <td>2010</td>
        </tr>
        <tr>
            <td>Wii Sports Resort for Wii</td>
            <td>Wii</td>
            <td>Nintendo</td>
            <td>Nintendo EAD</td>
            <td>33.13</td>
            <td>2009</td>
        </tr>
        <tr>
            <td>Pokemon Red / Green / Blue Version for GB</td>
            <td>GB</td>
            <td>Nintendo</td>
            <td>Game Freak</td>
            <td>31.38</td>
            <td>1998</td>
        </tr>
        <tr>
            <td>New Super Mario Bros. for DS</td>
            <td>DS</td>
            <td>Nintendo</td>
            <td>Nintendo EAD</td>
            <td>30.80</td>
            <td>2006</td>
        </tr>
        <tr>
            <td>New Super Mario Bros. Wii for Wii</td>
            <td>Wii</td>
            <td>Nintendo</td>
            <td>Nintendo EAD</td>
            <td>30.30</td>
            <td>2009</td>
        </tr>
    </tbody>
</table>




```python
%%nose
from decimal import Decimal as D
last_output = _

def test_output_type():
    assert str(type(last_output)) == "<class 'sql.run.ResultSet'>", \
    "Please ensure an SQL ResultSet is the output of the code cell." 

results = last_output.DataFrame()

def test_results():
    assert results.shape == (10, 6), \
    "The results should have six columns and ten rows."
    assert results.columns.tolist() == ["game", "platform", "publisher", "developer", "games_sold", "year"], \
    'The results should have columns named "game", "platform", "publisher", "developer", "games_sold", and "year".'
    assert _.DataFrame().loc[0, 'games_sold'] == D('82.90')
    "The top selling game should be Wii Sports with 82.90 million copies sold."
```






    2/2 tests passed




## 2. Missing review scores
<p>Wow, the best-selling video games were released between 1985 to 2017! That's quite a range; we'll have to use data from the <code>reviews</code> table to gain more insight on the best years for video games. </p>
<p>First, it's important to explore the limitations of our database. One big shortcoming is that there is not any <code>reviews</code> data for some of the games on the <code>game_sales</code> table. </p>


```sql
%%sql 

-- Join games_sales and reviews
-- Select a count of the number of games where both critic_score and user_score are null

SELECT COUNT(*)
FROM game_sales AS g
    LEFT OUTER JOIN reviews AS v
    ON g.game = v.game
WHERE critic_score IS NULL AND
      (user_score IS NULL)
;
```

     * postgresql:///games
    1 rows affected.





<table>
    <thead>
        <tr>
            <th>count</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>31</td>
        </tr>
    </tbody>
</table>




```python
%%nose
last_output = _

def test_output_type():
    assert str(type(last_output)) == "<class 'sql.run.ResultSet'>", \
    "Please ensure an SQL ResultSet is the output of the code cell." 

results = last_output.DataFrame()

def test_results():
    assert results.shape == (1, 1), \
    "The query should return just one value, a count of games where both critic_score and user_score are null."
    assert results.columns.tolist() == ["count"], \
    'The results should have just one column, called "count".'
    assert last_output.DataFrame().loc[0, 'count'] == 31, \
    "There should be 31 games where both critic_score and user_score are null."
```






    2/2 tests passed




## 3. Years that video game critics loved
<p>It looks like a little less than ten percent of the games on the <code>game_sales</code> table don't have any reviews data. That's a small enough percentage that we can continue our exploration, but the missing reviews data is a good thing to keep in mind as we move on to evaluating results from more sophisticated queries. </p>
<p>There are lots of ways to measure the best years for video games! Let's start with what the critics think. </p>


```sql
%%sql

-- Select release year and average critic score for each year, rounded and aliased
-- Join the game_sales and reviews tables
-- Group by release year
-- Order the data from highest to lowest avg_critic_score and limit to 10 results

SELECT g.year, ROUND(AVG(v.critic_score),2) AS avg_critic_score
FROM game_sales AS g
    LEFT OUTER JOIN reviews AS v
    ON g.game = v.game
GROUP BY year
ORDER BY avg_critic_score DESC
LIMIT 10;
```

     * postgresql:///games
    10 rows affected.





<table>
    <thead>
        <tr>
            <th>year</th>
            <th>avg_critic_score</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1990</td>
            <td>9.80</td>
        </tr>
        <tr>
            <td>1992</td>
            <td>9.67</td>
        </tr>
        <tr>
            <td>1998</td>
            <td>9.32</td>
        </tr>
        <tr>
            <td>2020</td>
            <td>9.20</td>
        </tr>
        <tr>
            <td>1993</td>
            <td>9.10</td>
        </tr>
        <tr>
            <td>1995</td>
            <td>9.07</td>
        </tr>
        <tr>
            <td>2004</td>
            <td>9.03</td>
        </tr>
        <tr>
            <td>1982</td>
            <td>9.00</td>
        </tr>
        <tr>
            <td>2002</td>
            <td>8.99</td>
        </tr>
        <tr>
            <td>1999</td>
            <td>8.93</td>
        </tr>
    </tbody>
</table>




```python
%%nose
from decimal import Decimal as D
last_output = _

def test_output_type():
    assert str(type(last_output)) == "<class 'sql.run.ResultSet'>", \
    "Please ensure an SQL ResultSet is the output of the code cell." 

results = last_output.DataFrame()

def test_results():
    assert results.shape == (10, 2), \
    "Make sure to limit the query to only ten results."
    assert results.columns.tolist() == ["year", "avg_critic_score"], \
    'The results should have two columns, called "year" and "avg_critic_score".'
    assert last_output.DataFrame().loc[0, 'year'] == 1990, \
    "The year with the highest score should be 1990."
    assert last_output.DataFrame().loc[0, 'avg_critic_score'] == D('9.80'), \
    "The highest average critic score should be 9.80."
```






    2/2 tests passed




## 4. Was 1982 really that great?
<p>The range of great years according to critic reviews goes from 1982 until 2020: we are no closer to finding the golden age of video games! </p>
<p>Hang on, though. Some of those <code>avg_critic_score</code> values look like suspiciously round numbers for averages. The value for 1982 looks especially fishy. Maybe there weren't a lot of video games in our dataset that were released in certain years. </p>
<p>Let's update our query and find out whether 1982 really was such a great year for video games.</p>


```sql
%%sql 

-- Paste your query from the previous task; update it to add a count of games released in each year called num_games
-- Update the query so that it only returns years that have more than four reviewed games

SELECT g.year, COUNT(g.game) AS num_games, ROUND(AVG(v.critic_score),2) AS avg_critic_score 
FROM game_sales AS g
    INNER JOIN reviews AS v
    ON g.game = v.game
GROUP BY g.year
HAVING COUNT(g.game) > 4
ORDER BY avg_critic_score DESC
LIMIT 10;

```

     * postgresql:///games
    10 rows affected.





<table>
    <thead>
        <tr>
            <th>year</th>
            <th>num_games</th>
            <th>avg_critic_score</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1998</td>
            <td>10</td>
            <td>9.32</td>
        </tr>
        <tr>
            <td>2004</td>
            <td>11</td>
            <td>9.03</td>
        </tr>
        <tr>
            <td>2002</td>
            <td>9</td>
            <td>8.99</td>
        </tr>
        <tr>
            <td>1999</td>
            <td>11</td>
            <td>8.93</td>
        </tr>
        <tr>
            <td>2001</td>
            <td>13</td>
            <td>8.82</td>
        </tr>
        <tr>
            <td>2011</td>
            <td>26</td>
            <td>8.76</td>
        </tr>
        <tr>
            <td>2016</td>
            <td>13</td>
            <td>8.67</td>
        </tr>
        <tr>
            <td>2013</td>
            <td>18</td>
            <td>8.66</td>
        </tr>
        <tr>
            <td>2008</td>
            <td>20</td>
            <td>8.63</td>
        </tr>
        <tr>
            <td>2012</td>
            <td>12</td>
            <td>8.62</td>
        </tr>
    </tbody>
</table>




```python
%%nose
from decimal import Decimal as D
last_output = _

def test_output_type():
    assert str(type(last_output)) == "<class 'sql.run.ResultSet'>", \
    "Please ensure an SQL ResultSet is the output of the code cell." 

results = last_output.DataFrame()

def test_results():
    assert results.shape == (10, 3), \
    "Make sure to limit the query to only ten results."
    assert set(last_output.DataFrame().columns) == set(["year", "num_games", "avg_critic_score"]), \
    'The results should have three columns: "year", "num_games", and "avg_critic_score".'
    assert last_output.DataFrame().loc[0, 'year'] == 1998, \
    "The year with the highest score should be 1998."
    assert last_output.DataFrame().loc[0, 'num_games'] == 10, \
    "In the year with the highest critic score, there were 10 games released."
    assert last_output.DataFrame().loc[0, 'avg_critic_score'] == D('9.32'), \
    "The highest average critic score should be 9.32."
```






    2/2 tests passed




## 5. Years that dropped off the critics' favorites list
<p>That looks better! The <code>num_games</code> column convinces us that our new list of the critics' top games reflects years that had quite a few well-reviewed games rather than just one or two hits. But which years dropped off the list due to having four or fewer reviewed games? Let's identify them so that someday we can track down more game reviews for those years and determine whether they might rightfully be considered as excellent years for video game releases!</p>
<p>It's time to brush off your set theory skills. To get started, we've created tables with the results of our previous two queries:</p>
<h3 id="top_critic_years"><code>top_critic_years</code></h3>
<table>
<thead>
<tr>
<th style="text-align:left;">column</th>
<th>type</th>
<th>meaning</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;"><code>year</code></td>
<td>int</td>
<td>Year of video game release</td>
</tr>
<tr>
<td style="text-align:left;"><code>avg_critic_score</code></td>
<td>float</td>
<td>Average of all critic scores for games released in that year</td>
</tr>
</tbody>
</table>
<h3 id="top_critic_years_more_than_four_games"><code>top_critic_years_more_than_four_games</code></h3>
<table>
<thead>
<tr>
<th style="text-align:left;">column</th>
<th>type</th>
<th>meaning</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;"><code>year</code></td>
<td>int</td>
<td>Year of video game release</td>
</tr>
<tr>
<td style="text-align:left;"><code>num_games</code></td>
<td>int</td>
<td>Count of the number of video games released in that year</td>
</tr>
<tr>
<td style="text-align:left;"><code>avg_critic_score</code></td>
<td>float</td>
<td>Average of all critic scores for games released in that year</td>
</tr>
</tbody>
</table>


```sql
%%sql 

-- Select the year and avg_critic_score for those years that dropped off the list of critic favorites 
-- Order the results from highest to lowest avg_critic_score

SELECT * 
FROM top_critic_years
WHERE year NOT IN
(SELECT year
FROM top_critic_years_more_than_four_games)
--ORDER BY t.avg_critic_score DESC;
```

     * postgresql:///games
    6 rows affected.





<table>
    <thead>
        <tr>
            <th>year</th>
            <th>avg_critic_score</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1990</td>
            <td>9.80</td>
        </tr>
        <tr>
            <td>1992</td>
            <td>9.67</td>
        </tr>
        <tr>
            <td>2020</td>
            <td>9.20</td>
        </tr>
        <tr>
            <td>1993</td>
            <td>9.10</td>
        </tr>
        <tr>
            <td>1995</td>
            <td>9.07</td>
        </tr>
        <tr>
            <td>1982</td>
            <td>9.00</td>
        </tr>
    </tbody>
</table>




```python
%%nose
last_output = _

def test_output_type():
    assert str(type(last_output)) == "<class 'sql.run.ResultSet'>", \
    "Please ensure an SQL ResultSet is the output of the code cell." 

results = last_output.DataFrame()

def test_results():
    assert results.shape == (6, 2), \
    "There should be six years that dropped off the critics' favorite list after implementing the criteria that the year had to have at least five games released to be considered."
    assert results.columns.tolist() == ["year", "avg_critic_score"], \
    'The results should have two columns: "year" and "avg_critic_score".'
    assert last_output.DataFrame().loc[5, 'year'] == 1982, \
    "The last year returned by the query should be 1982."
    assert last_output.DataFrame().loc[5, 'avg_critic_score'] == 9.00, \
    "1982's average critic score should be 9.00."
```






    2/2 tests passed




## 6. Years video game players loved
<p>Based on our work in the task above, it looks like the early 1990s might merit consideration as the golden age of video games based on <code>critic_score</code> alone, but we'd need to gather more games and reviews data to do further analysis. </p>
<p>Let's move on to looking at the opinions of another important group of people: players! To begin, let's create a query very similar to the one we used in Task Four, except this one will look at <code>user_score</code> averages by year rather than <code>critic_score</code> averages.</p>


```sql
%%sql 

-- Select year, an average of user_score, and a count of games released in a given year, aliased and rounded
-- Include only years with more than four reviewed games; group data by year
-- Order data by avg_user_score, and limit to ten results

SELECT  g.year, 
        ROUND(AVG(r.user_score), 2) AS avg_user_score, 
        COUNT(g.game) AS num_games
FROM game_sales AS g
    INNER JOIN reviews AS r
    ON g.game = r.game
GROUP BY g.year
HAVING COUNT(g.game) > 4
ORDER BY avg_user_score DESC
LIMIT 10;
```

     * postgresql:///games
    10 rows affected.





<table>
    <thead>
        <tr>
            <th>year</th>
            <th>avg_user_score</th>
            <th>num_games</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1997</td>
            <td>9.50</td>
            <td>8</td>
        </tr>
        <tr>
            <td>1998</td>
            <td>9.40</td>
            <td>10</td>
        </tr>
        <tr>
            <td>2010</td>
            <td>9.24</td>
            <td>23</td>
        </tr>
        <tr>
            <td>2009</td>
            <td>9.18</td>
            <td>20</td>
        </tr>
        <tr>
            <td>2008</td>
            <td>9.03</td>
            <td>20</td>
        </tr>
        <tr>
            <td>1996</td>
            <td>9.00</td>
            <td>5</td>
        </tr>
        <tr>
            <td>2005</td>
            <td>8.95</td>
            <td>13</td>
        </tr>
        <tr>
            <td>2006</td>
            <td>8.95</td>
            <td>16</td>
        </tr>
        <tr>
            <td>2000</td>
            <td>8.80</td>
            <td>8</td>
        </tr>
        <tr>
            <td>1999</td>
            <td>8.80</td>
            <td>11</td>
        </tr>
    </tbody>
</table>




```python
%%nose
last_output = _

def test_output_type():
    assert str(type(last_output)) == "<class 'sql.run.ResultSet'>", \
    "Please ensure an SQL ResultSet is the output of the code cell." 

results = last_output.DataFrame()

def test_results():
    assert results.shape == (10, 3), \
    "Don't forget to limit the query results to ten."
    assert set(results.columns.tolist()) == set(["year", "num_games", "avg_user_score"]), \
    'The results should have three columns: "year", "num_games", and "avg_user_score".'
    assert last_output.DataFrame().loc[0, 'year'] == 1997, \
    "The year with the highest user score should be 1997."
    assert last_output.DataFrame().loc[0, 'num_games'] == 8, \
    "In the year with the highest user score, there were eight games released."
    assert last_output.DataFrame().loc[0, 'avg_user_score'] == 9.50, \
    "The highest average user score should be 9.50."
```






    2/2 tests passed




## 7. Years that both players and critics loved
<p>Alright, we've got a list of the top ten years according to both critic reviews and user reviews. Are there any years that showed up on both tables? If so, those years would certainly be excellent ones!</p>
<p>Recall that we have access to the <code>top_critic_years_more_than_four_games</code> table, which stores the results of our top critic years query from Task 4:</p>
<h3 id="top_critic_years_more_than_four_games"><code>top_critic_years_more_than_four_games</code></h3>
<table>
<thead>
<tr>
<th style="text-align:left;">column</th>
<th>type</th>
<th>meaning</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;"><code>year</code></td>
<td>int</td>
<td>Year of video game release</td>
</tr>
<tr>
<td style="text-align:left;"><code>num_games</code></td>
<td>int</td>
<td>Count of the number of video games released in that year</td>
</tr>
<tr>
<td style="text-align:left;"><code>avg_critic_score</code></td>
<td>float</td>
<td>Average of all critic scores for games released in that year</td>
</tr>
</tbody>
</table>
<p>We've also saved the results of our top user years query from the previous task into a table:</p>
<h3 id="top_user_years_more_than_four_games"><code>top_user_years_more_than_four_games</code></h3>
<table>
<thead>
<tr>
<th style="text-align:left;">column</th>
<th>type</th>
<th>meaning</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;"><code>year</code></td>
<td>int</td>
<td>Year of video game release</td>
</tr>
<tr>
<td style="text-align:left;"><code>num_games</code></td>
<td>int</td>
<td>Count of the number of video games released in that year</td>
</tr>
<tr>
<td style="text-align:left;"><code>avg_user_score</code></td>
<td>float</td>
<td>Average of all user scores for games released in that year</td>
</tr>
</tbody>
</table>


```sql
%%sql 

-- Select the year results that appear on both tables

SELECT tc.year
FROM top_critic_years_more_than_four_games AS tc
     INNER JOIN
     top_user_years_more_than_four_games AS tu
     ON tc.year = tu.year;
```

     * postgresql:///games
    3 rows affected.





<table>
    <thead>
        <tr>
            <th>year</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1998</td>
        </tr>
        <tr>
            <td>2002</td>
        </tr>
        <tr>
            <td>2008</td>
        </tr>
    </tbody>
</table>




```python
%%nose
last_output = _

def test_output_type():
    assert str(type(last_output)) == "<class 'sql.run.ResultSet'>", \
    "Please ensure an SQL ResultSet is the output of the code cell." 

results = last_output.DataFrame()

def test_results():
    assert results.shape == (3, 1), \
    "There should be three years present in both tables."
    assert results.columns.tolist() == ["year"], \
    'The results should just have one column: "year".'
    assert last_output.DataFrame().loc[0, 'year'] == 1998, \
    "The first year returned by the query should be 1998."
```






    2/2 tests passed




## 8. Sales in the best video game years
<p>Looks like we've got three years that both users and critics agreed were in the top ten! There are many other ways of measuring what the best years for video games are, but let's stick with these years for now. We know that critics and players liked these years, but what about video game makers? Were sales good? Let's find out.</p>
<p>This time, we haven't saved the results from the previous task in a table for you. Instead, we'll use the query from the previous task as a subquery in this one! This is a great skill to have, as we don't always have write permissions on the database we are querying.</p>


```sql
%%sql 

-- Select year and sum of games_sold, aliased as total_games_sold; order results by total_games_sold descending
-- Filter game_sales based on whether each year is in the list returned in the previous task
SELECT  year, 
        SUM(games_sold) AS total_games_sold
FROM game_sales
WHERE year IN
    (SELECT tc.year
     FROM top_critic_years_more_than_four_games AS tc
     INNER JOIN
     top_user_years_more_than_four_games AS tu
     ON tc.year = tu.year)
GROUP BY year
ORDER BY total_games_sold DESC;
```

     * postgresql:///games
    3 rows affected.





<table>
    <thead>
        <tr>
            <th>year</th>
            <th>total_games_sold</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>2008</td>
            <td>175.07</td>
        </tr>
        <tr>
            <td>1998</td>
            <td>101.52</td>
        </tr>
        <tr>
            <td>2002</td>
            <td>58.67</td>
        </tr>
    </tbody>
</table>




```python
%%nose
from decimal import Decimal as D
last_output = _


def test_output_type():
    assert str(type(last_output)) == "<class 'sql.run.ResultSet'>", \
    "Please ensure an SQL ResultSet is the output of the code cell." 

results = last_output.DataFrame()

def test_results():
    assert results.shape == (3, 2), \
    "There should be games sales data for three years: the same three years from the previous query."
    assert results.columns.tolist() == ["year", "total_games_sold"], \
    'The results should have two columns: "year" and "total_games_sold".'
    assert last_output.DataFrame().loc[0, 'year'] == 2008, \
    "Just like in the last query, the first year returned should be 2008."
    assert last_output.DataFrame().loc[0, 'total_games_sold'] == D('175.07'), \
    "In 2008, the total_games_sold value should be 175.07."
```






    2/2 tests passed




