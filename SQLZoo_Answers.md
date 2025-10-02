
# [SQLZoo](https://sqlzoo.net/wiki/SQL_Tutorial) 
Answers for Tutorial 0-9

## 0 SELECT basics
1. Modify it to show the population of Germany.
```sql
SELECT population 
FROM world
WHERE name LIKE 'Germany'
```
2. Show the name and the population for 'Sweden', 'Norway' and 'Denmark'.
```sql
SELECT name, population
FROM world
WHERE name IN ('Sweden', 'Norway', 'Denmark');
```
3. Which countries are not too small and not too big?
```sql
SELECT name, area 
FROM world
WHERE area BETWEEN 200000 AND 250000
```
## 1 SELECT name
1. Find the country that start with Y.
```sql
SELECT name FROM world
  WHERE name LIKE 'Y%'
```
2. Find the countries that end with y
```sql
SELECT name FROM world
  WHERE name LIKE '%y'
```
3. Find the countries that contain the letter x.
```sql
SELECT name FROM world
  WHERE name LIKE '%x%'
```
4. Find the countries that end with land.
```sql
SELECT name FROM world
  WHERE name LIKE '%land'
```
5. Find the countries that start with C and end with ia.
```sql
SELECT name FROM world
  WHERE name LIKE 'C%ia'
```
6. Find the country that has oo in the name.
```sql
SELECT name FROM world
  WHERE name LIKE '%oo%
```
7. Find the countries that have three or more a in the name.
```sql
SELECT name FROM world
  WHERE name LIKE '%a%a%a%'
```
8. Find the countries that have "t" as the second character.
```sql
SELECT name FROM world
 WHERE name LIKE '_t%'
ORDER BY name
```
9. Find the countries that have two "o" characters separated by two others.
```sql
SELECT name FROM world
 WHERE name LIKE '%o__o%'
```
10. Find the countries that have exactly four characters.
```sql
SELECT name FROM world
 WHERE name LIKE '____'
```
11. Find the country where the name is the capital city.
```sql
SELECT name
  FROM world
 WHERE name = capital
```
12. Find the country where the capital is the country plus "City".
```sql
SELECT name
  FROM world
 WHERE capital = CONCAT(name, ' City')
```
13. Find the capital and the name where the capital includes the name of the country.
```sql 
SELECT capital, name 
FROM world
WHERE capital LIKE CONCAT('%',name,'%')
```
14. Find the capital and the name where the capital is an extension of name of the country.
```sql
SELECT capital, name
FROM world
WHERE capital LIKE CONCAT(name,'_','%')
```
15. Show the name and the extension where the capital is a proper (non-empty) extension of name of the country.
```sql
SELECT name, REPLACE(capital, name, '')
FROM world
WHERE capital LIKE CONCAT (name, '_', '%')
```
## 2 SELECT from World
1. show the name, continent and population of all countries. 
```sql
SELECT name, continent, population FROM world
```
2. Show the name for the countries that have a population of at least 200 million.
```sql
SELECT name FROM world
WHERE population >= 200000000
```
3. Give the name and the per capita GDP for those countries with a population of at least 200 million.
```sql
SELECT name, (gdp/population) AS per_capita_gdp FROM world 
WHERE population >= 200000000
```
4. Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.
```sql
SELECT name , population/1000000 
FROM world 
WHERE continent LIKE 'south america';
```
5. Show the name and population for France, Germany, Italy.
```sql
SELECT name , population 
FROM world 
WHERE name IN ('France','Germany','Italy');
```
6. Show the countries which have a name that includes the word 'United'.
```sql
SELECT name FROM world
WHERE name LIKE 'United%'
```
7. Show the countries that are big by area or big by population. Show name, population and area.
```sql
SELECT name, population ,area 
FROM world 
WHERE area > 3000000 OR population > 250000000
```
8. Exclusive OR (XOR). Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. Show name, population and area.
```sql
SELECT name, population, area 
FROM world
WHERE area > 3000000 XOR population > 250000000;
```
9. Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'.
```sql
SELECT name, ROUND(population/1000000,2) , ROUND(gdp/1000000000,2)
FROM world
WHERE continent = 'South America';
```
10. Show the name and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.
```sql
SELECT name, ROUND(gdp/population,-3)
FROM world 
WHERE gdp >= 1000000000000 ;
```
11. Show the name and capital where the name and the capital have the same number of characters.
```sql
SELECT name, capital
FROM world 
WHERE LENGTH(name) = LENGTH(capital);
```
12. Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.
```sql
SELECT name, capital
FROM world
WHERE LEFT(name,1) = LEFT(capital,1) AND name <> capital;
```
13. Find the country that has all the vowels and no spaces in its name.
```sql
SELECT name
   FROM world
WHERE name LIKE '%a%' AND name LIKE '%e%' AND name LIKE '%i%'AND name LIKE '%o%'AND name LIKE '%u%'
  AND name NOT LIKE '% %'
```
## 3 SELECT from Nobel
1. Change the query shown so that it displays Nobel prizes for 1950.
```sql
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950
```

2. Show who won the 1962 prize for literature.
```sql
SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'literature';
```

3. Show the year and subject that won 'Albert Einstein' his prize.
```sql
SELECT yr, subject 
FROM nobel
WHERE winner LIKE 'ALBERT EINSTEIN';
```

4. Give the name of the 'peace' winners since the year 2000, including 2000.
```sql
SELECT winner
FROM  nobel 
WHERE yr >= 2000 AND subject LIKE 'peace';
```

5. Show all details (yr, subject, winner) of the literature prize winners for 1980 to 1989 inclusive.
```sql
SELECT * 
FROM nobel
WHERE subject LIKE 'literature' AND yr BETWEEN 1980 AND 1989 ;
```

6. Show all details of the presidential winners:

    Theodore Roosevelt
    Thomas Woodrow Wilson
    Jimmy Carter
    Barack Obama
```sql

SELECT * FROM nobel
 WHERE winner IN (    'Theodore Roosevelt',
    'Thomas Woodrow Wilson',
    'Jimmy Carter',
    'Barack Obama')
```

7. Show the winners with first name John
```sql
SELECT winner 
FROM nobel
WHERE winner LIKE 'john%';
```

8. Show the year, subject, and name of physics winners for 1980 together with the chemistry winners for 1984.
```sql
SELECT yr, subject, winner 
FROM nobel
WHERE yr = 1980 AND subject = 'physics' OR 
yr = 1984 AND subject = 'chemistry';
```

9. Show the year, subject, and name of winners for 1980 excluding chemistry and medicine.
```sql
SELECT yr, subject, winner 
FROM nobel 
WHERE yr = 1980 AND subject NOT IN ('chemistry','medicine');
```

10. Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004) 
```sql
SELECT yr, subject, winner 
FROM nobel
WHERE yr < 1910 AND subject = 'medicine' OR
 yr >= 2004 AND subject = 'literature';
```

11. Find all details of the prize won by PETER GRÜNBERG.
```sql
SELECT * 
FROM nobel
WHERE winner = 'Peter GrÜnberg';
```

12. Find all details of the prize won by EUGENE O'NEILL.
```sql
SELECT * 
FROM nobel 
WHERE winner = 'EUGENE O''NEILL'
```

13. List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order.
```sql
SELECT winner, yr, subject 
FROM nobel 
WHERE winner LIKE 'Sir %' ORDER BY yr DESC ,winner;
```

14. Show the 1984 winners and subject ordered by subject and winner name; but list chemistry and physics last.
```sql
SELECT winner, subject
FROM nobel
WHERE yr=1984
ORDER BY subject IN ('physics','chemistry'),subject,winner
```
## 4 SELECT within SELECT
1. List each country name where the population is larger than that of 'Russia'. 
```sql

SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')
```
2. Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.
```sql
SELECT name
FROM world
WHERE (gdp/population) > (SELECT gdp/population
FROM world
WHERE name = 'United Kingdom')
AND continent = 'europe'
```
3. List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.
```sql
SELECT name, continent 
FROM world
WHERE continent IN (SELECT continent FROM world
WHERE name IN ('Argentina','Australia')) ORDER BY name;
```
4. Which country has a population that is more than United Kingdom but less than Germany? Show the name and the population.
```sql
SELECT name, population 
FROM world 
WHERE population > (SELECT population FROM world WHERE name = 'United Kingdom') AND 
population < (SELECT population FROM world WHERE name = 'Germany');
```
5. Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.
```sql
SELECT name, CONCAT(ROUND(population/(SELECT population FROM world WHERE name = 'Germany') * 100, 0), '%') as percentage
FROM world
WHERE continent = 'europe'
```
6. Which countries have a GDP greater than every country in Europe? [Give the name only.] (Some countries may have NULL gdp values).
```sql
SELECT name 
FROM world
WHERE gdp > ALL(
SELECT gdp 
FROM world
WHERE gdp>0 AND continent = 'Europe'
)
```
7. Find the largest country (by area) in each continent, show the continent, the name and the area: 
```sql
SELECT continent, name, area FROM world x
  WHERE area >= ALL
    (SELECT area FROM world y
        WHERE y.continent=x.continent
          AND population>0)
```
8. List each continent and the name of the country that comes first alphabetically.
```sql
SELECT continent , name
FROM world x
WHERE name <= ALL (
SELECT name FROM world y
WHERE y.continent = x.continent 
)
```
9. Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population.
```sql
SELECT name, continent, population
FROM world x
WHERE 25000000 >= ALL(SELECT population FROM world y
WHERE x.continent = y.continent)
```
10. Some countries have populations more than three times that of all of their neighbours (in the same continent). Give the countries and continents.
```sql
SELECT name, continent
FROM world x
WHERE population >= ALL(SELECT 3*population FROM 
world y WHERE name <> x.name AND x.continent = y.continent )
```

## 5 SUM and COUNT
1. Show the total population of the world. 
```sql
SELECT SUM(population)
FROM world
```
2. List all the continents - just once each. 
```sql
SELECT DISTINCT continent
FROM world
```
3. Give the total GDP of Africa 
```sql
SELECT SUM(gdp)
FROM world
WHERE continent = 'Africa'
```
4. How many countries have an area of at least 1000000.
```sql
SELECT COUNT(name)
FROM world 
WHERE area >= 1000000
```
5. What is the total population of ('Estonia', 'Latvia', 'Lithuania') 
```sql
SELECT SUM(population)
FROM world
WHERE name in ('Estonia', 'Latvia', 'Lithuania')
```
6. For each continent show the continent and number of countries. 
```sql
SELECT continent , COUNT(name)
FROM world
GROUP BY continent
```
7. For each continent show the continent and number of countries with populations of at least 10 million. 
```sql
SELECT continent , COUNT(name)
FROM world
WHERE population >= 10000000
GROUP BY continent
```
8. List the continents that have a total population of at least 100 million. 
```sql
SELECT continent
FROM world 
GROUP BY continent
HAVING SUM(population) >= 100000000
```
## 6 JOIN
1. Modify it to show the matchid and player name for all goals scored by Germany. To identify German players, check for: teamid = 'GER'.
```sql
SELECT matchid, player
FROM goal
WHERE teamid = 'GER'
```
2. Show id, stadium, team1, team2 for just game 1012
```sql
SELECT id,stadium,team1,team2
  FROM game
WHERE id = (SELECT matchid
FROM goal
WHERE player LIKE '%Bender')
```
3. Modify it to show the player, teamid, stadium and mdate for every German goal.
```sql
SELECT player, teamid, stadium, mdate
  FROM game JOIN goal ON (id=matchid)
  WHERE teamid = 'GER'
```
4. Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'
```sql
SELECT team1, team2, player
FROM game
JOIN goal
ON matchid = id
WHERE player LIKE 'Mario%'
```
5. Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10.
```sql
SELECT player, teamid, coach, gtime
  FROM goal 
  JOIN eteam ON teamid = id
 WHERE gtime<=10
```
6. List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.
```sql
SELECT mdate, teamname
FROM game
JOIN eteam ON team1 = eteam.id
WHERE coach = 'Fernando Santos'
```
7. List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'
```sql
SELECT player
FROM game
JOIN goal
ON matchid = id
WHERE stadium = 'National Stadium, Warsaw'
```
8. Instead show the name of all players who scored a goal against Germany.
```sql
SELECT DISTINCT player
  FROM game JOIN goal ON matchid = id 
    WHERE (team1='GER' OR team2='GER') AND teamid <> 'GER'
```
9. Show teamname and the total number of goals scored.
```sql
SELECT teamname, COUNT(*)
  FROM eteam JOIN goal ON id=teamid
  GROUP BY teamname
 ORDER BY teamname
```
10. Show the stadium and the number of goals scored in each stadium. 
```sql
SELECT stadium, COUNT(*)
FROM game
JOIN goal
ON matchid = id
GROUP BY stadium
```
11. For every match involving 'POL', show the matchid, date and the number of goals scored.
```sql
SELECT matchid,mdate, COUNT(*)
  FROM game JOIN goal ON matchid = id 
 WHERE (team1 = 'POL' OR team2 = 'POL')
GROUP BY matchid, mdate
```
12. For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'.
```sql
SELECT matchid, mdate, COUNT(*)
FROM game
JOIN goal
ON matchid = id
WHERE (team1 = 'GER' OR team2 = 'GER') AND teamid = 'GER'
GROUP BY matchid, mdate
```
13. List every match with the goals scored by each team as shown.
```sql
SELECT mdate,
  team1,
  SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) score1,
  team2,
  SUM(CASE WHEN teamid=team2 THEN 1 ELSE 0 END) score2

  FROM goal RIGHT JOIN game ON matchid = id

  GROUP BY mdate, matchid, team1, team2
```
## 7 More JOIN operations
1. List the films where the yr is 1962 and the budget is over 2000000 [Show id, title].
```sql
SELECT id, title
 FROM movie
 WHERE yr=1962 AND budget > 2000000
```
2. Give year of 'Citizen Kane'. 
```sql
SELECT yr
FROM movie
WHERE title = 'Citizen Kane'
```
3. List all of the Star Trek movies, include the id, title and yr (all of these movies start with the words Star Trek in the title). Order results by year.
```sql
SELECT id, title, yr
FROM movie
WHERE title LIKE 'Star Trek%'
ORDER BY yr
```
4. What id number does the actor 'Glenn Close' have?
```sql
SELECT id
FROM actor
WHERE name = 'Glenn Close'
```
5. What is the id of the 1942 film 'Casablanca'
```sql
SELECT id
FROM movie
WHERE title = 'Casablanca' and yr= 1942
```
6. Obtain the cast list for 1942's 'Casablanca'.
```sql
SELECT name
FROM movie
JOIN casting ON movie.id = movieid
JOIN actor ON actor.id = actorid
WHERE title = 'Casablanca' AND yr = 1942
```
7. Obtain the cast list for the film 'Alien' 
```sql
SELECT name
FROM movie
JOIN casting ON movie.id = movieid
JOIN actor ON actor.id = actorid
WHERE title = 'Alien'
```
8. List the films in which 'Harrison Ford' has appeared
```sql
SELECT title 
FROM movie 
JOIN casting ON movie.id = movieid
JOIN actor ON actor.id = actorid
WHERE actor.name = 'Harrison Ford'
```
9. List the films where 'Harrison Ford' has appeared - but not in the starring role. [Note: the ord field of casting gives the position of the actor. If ord=1 then this actor is in the starring role]
```sql
SELECT title 
FROM movie 
JOIN casting ON movie.id = movieid
JOIN actor ON actor.id = actorid
WHERE actor.name = 'Harrison Ford'
AND ord > 1
```
10. List the films together with the leading star for all 1962 films.
```sql
SELECT title, name
FROM movie 
JOIN casting ON movie.id = movieid
JOIN actor ON actor.id = actorid
WHERE yr = 1962 AND ord = 1
```
11. Which were the busiest years for 'Rock Hudson', show the year and the number of movies he made each year for any year in which he made more than 2 movies.
```sql
SELECT yr, COUNT(title)
FROM movie
JOIN casting ON movie.id = movieid
JOIN actor ON actor.id = actorid
WHERE name = 'Rock Hudson'
GROUP BY yr
HAVING COUNT(title) > 2
```
12. List the film title and the leading actor for all of the films 'Julie Andrews' played in. 
```sql
SELECT movie.title, actor.name
FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON actor.id = casting.actorid
WHERE casting.movieid IN (SELECT casting.movieid FROM casting JOIN actor ON actor.id = actorid WHERE actor.name = 'Julie Andrews') AND casting.ord = 1
```
13. Obtain a list, in alphabetical order, of actors who've had at least 15 starring roles. 
```sql
SELECT name
FROM movie
JOIN casting ON movie.id = movieid
JOIN actor ON actor.id = actorid
WHERE ord = 1
GROUP BY name
HAVING COUNT(ord) >= 15
```
14.  List the films released in the year 1978 ordered by the number of actors in the cast, then by title. 
```sql
SELECT title, COUNT(actorid) FROM movie
JOIN casting ON movie.id = movieid
JOIN actor ON actor.id = actorid
WHERE yr = 1978
GROUP BY title
ORDER BY COUNT(actorid) DESC, title
```
15. List all the people who have worked with 'Art Garfunkel'.
```sql

SELECT DISTINCT name 
FROM casting 
JOIN actor ON actor.id = actorid
WHERE movieid IN
  (SELECT movieid
  FROM casting
  JOIN actor ON actor.id = actorid
  WHERE name = 'Art Garfunkel') AND name <> 'Art Garfunkel'
```
## 8 Using NULL
1. List the teachers who have NULL for their department. 
```sql
SELECT name
FROM teacher
WHERE dept IS NULL
```
2. Note the INNER JOIN misses the teachers with no department and the departments with no teacher. 
```sql
SELECT teacher.name, dept.name
 FROM teacher INNER JOIN dept
           ON (teacher.dept=dept.id)
```
3. Use a different JOIN so that all teachers are listed. 
```sql
SELECT teacher.name, dept.name
FROM teacher LEFT JOIN dept
ON teacher.dept = dept.id
```
4. Use a different JOIN so that all departments are listed. 
```sql
SELECT teacher.name , dept.name 
FROM teacher RIGHT JOIN dept 
ON teacher.dept = dept.id
```
5. Show teacher name and mobile number or '07986 444 2266'.
```sql
SELECT name, COALESCE(mobile, '07986 444 2266') AS mobile
FROM teacher
```
6. Use the COALESCE function and a LEFT JOIN to print the teacher name and department name. Use the string 'None' where there is no department. 
```sql
SELECT teacher.name , COALESCE(dept.name , 'None') AS dept
FROM teacher LEFT JOIN dept 
ON dept.id = teacher.dept
```
7. Use COUNT to show the number of teachers and the number of mobile phones. 
```sql
SELECT COUNT(*), COUNT(mobile) 
FROM teacher
```
8. Use COUNT and GROUP BY dept.name to show each department and the number of staff. Use a RIGHT JOIN to ensure that the Engineering department is listed. 
```sql
SELECT dept.name, COUNT(teacher.id)
FROM teacher
RIGHT JOIN dept ON dept.id = teacher.dept
GROUP BY dept.name
```
9. Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2 and 'Art' otherwise. 
```sql
SELECT teacher.name, 
CASE WHEN dept = 1 OR dept = 2
THEN 'Sci'
WHEN dept IS NULL
THEN 'Art'
END
FROM teacher
```
10. Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2, show 'Art' if the teacher's dept is 3 and 'None' otherwise. 
```sql
SELECT teacher.name , 
CASE WHEN dept = 1 OR dept = 2
THEN 'Sci'
WHEN dept = 3
THEN 'Art'
WHEN dept IS NULL
THEN 'None'
END 
FROM teacher
```
## 8+ Numeric Examples
1. Show the the percentage who STRONGLY AGREE.
```sql
SELECT AVG(A_STRONGLY_AGREE)
  FROM nss
 WHERE question='Q01'
   AND institution='Edinburgh Napier University'
   AND subject='(8) Computer Science'
```
2. Show the institution and subject where the score is at least 100 for question 15. 
```sql
SELECT institution, subject
  FROM nss
 WHERE question='Q15'
   AND score >= 100 
```
3. Show the institution and score where the score for '(8) Computer Science' is less than 50 for question 'Q15' 
```sql
SELECT institution,score
  FROM nss
 WHERE question='Q15'
   AND score < 50
   AND subject='(8) Computer Science'
```
4. Show the subject and total number of students who responded to question 22 for each of the subjects '(8) Computer Science' and '(H) Creative Arts and Design'. 
```sql
SELECT subject, SUM(response)
  FROM nss
 WHERE question='Q22'
   AND (subject='(8) Computer Science' OR subject='(H) Creative Arts And Design')
GROUP BY subject
```
5. Show the subject and total number of students who A_STRONGLY_AGREE to question 22 for each of the subjects '(8) Computer Science' and '(H) Creative Arts and Design'. 
```sql
SELECT subject, SUM(A_STRONGLY_AGREE*response/100) AS num
  FROM nss
 WHERE question='Q22'
   AND (subject='(8) Computer Science' OR subject='(H) Creative Arts And Design')
GROUP BY subject
```
6. Show the percentage of students who A_STRONGLY_AGREE to question 22 for the subject '(8) Computer Science' show the same figure for the subject '(H) Creative Arts and Design'. 
```sql
SELECT subject, ROUND(SUM(A_STRONGLY_AGREE*response)/SUM(response),0)
  FROM nss
 WHERE question='Q22'
   AND (subject='(8) Computer Science' OR subject='(H) Creative Arts And Design')
GROUP BY subject
```
7. Show the average scores for question 'Q22' for each institution that include 'Manchester' in the name. 
```sql
SELECT institution, ROUND(SUM(score*response)/SUM(response),0) AS score
  FROM nss
 WHERE question='Q22'
   AND (institution LIKE '%Manchester%')
GROUP BY institution
```
8. Show the institution, the total sample size and the number of computing students for institutions in Manchester for 'Q01'. 
```sql
SELECT institution, SUM(sample), 
     SUM(CASE WHEN subject='(8) Computer Science' THEN sample END) AS comp
  FROM nss
 WHERE question='Q01'
   AND institution LIKE '%Manchester%'
GROUP BY institution
```
## 9- Window function
1.  Show the lastName, party and votes for the constituency 'S14000024' in 2017. 
```sql
SELECT lastName, party, votes
  FROM ge
 WHERE constituency = 'S14000024' AND yr = 2017
ORDER BY votes DESC
```
2. Show the party and RANK for constituency S14000024 in 2017. List the output by party.
```sql
SELECT party, votes,
       RANK() OVER (ORDER BY votes DESC) as posn
  FROM ge
 WHERE constituency = 'S14000024' AND yr = 2017
ORDER BY party
```
3. Use PARTITION to show the ranking of each party in S14000021 in each year. Include yr, party, votes and ranking (the party with the most votes is 1).
```sql
SELECT yr,party, votes,
      RANK() OVER (PARTITION BY yr ORDER BY votes DESC) as posn
  FROM ge
 WHERE constituency = 'S14000021'
ORDER BY party,yr
```
4. Use PARTITION BY constituency to show the ranking of each party in Edinburgh in 2017. Order your results so the winners are shown first, then ordered by constituency.
```sql
SELECT constituency,party, votes,
  RANK() OVER(PARTITION BY constituency ORDER BY votes DESC) AS posn
  FROM ge
 WHERE constituency BETWEEN 'S14000021' AND 'S14000026'
   AND yr  = 2017
ORDER BY posn,constituency
```
5. Show the parties that won for each Edinburgh constituency in 2017.
```sql
SELECT constituency, party
FROM ge AS ge1 
WHERE ge1.constituency BETWEEN 'S14000021' AND 'S14000026' 
AND ge1.yr = '2017'
AND votes >= ALL (
SELECT votes FROM ge AS ge2
 WHERE ge1.constituency = ge2.constituency 
 AND ge1.yr = ge2.yr
)
ORDER BY constituency, votes DESC
```
6. Show how many seats for each party in Scotland in 2017.
```sql
SELECT party, COUNT(1)
FROM ge AS ge1 
WHERE ge1.constituency LIKE 'S%'
AND ge1.yr = '2017'
AND votes >= ALL (
SELECT votes FROM ge AS ge2
 WHERE ge1.constituency = ge2.constituency 
 AND ge1.yr = ge2.yr
)
GROUP BY party
```
## 9+ Covid 19
1. Modify the query to show data from Spain
```sql
SELECT name, DAY(whn),confirmed, deaths, recovered
FROM covid
WHERE name = 'Spain'
AND MONTH(whn) = 3 AND YEAR(whn) = 2020
ORDER BY whn
```
2. Modify the query to show confirmed for the day before.
```sql
SELECT name, DAY(whn), confirmed,
                    LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn)
FROM covid
WHERE name = 'Italy'
AND MONTH(whn) = 3 AND YEAR(whn) = 2020
ORDER BY whn
```
3. Show the number of new cases for each day, for Italy, for March.
```sql
SELECT name, DAY(whn),
                  confirmed - LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn) AS new
 FROM covid
WHERE name = 'Italy'
AND MONTH(whn) = 3 AND YEAR(whn) = 2020
ORDER BY whn
```
4. Show the number of new cases in Italy for each week in 2020 - show Monday only.
```sql
SELECT name, DATE_FORMAT(whn,'%Y-%m-%d'),
                  confirmed - LAG(confirmed,1 )OVER (PARTITION BY name ORDER BY whn) as weekly_new
FROM covid
WHERE name = 'Italy'
AND WEEKDAY(whn) = 0 AND YEAR(whn) = 2020
ORDER BY whn
```
5. You can JOIN a table using DATE arithmetic. This will give different results if data is missing.
Show the number of new cases in Italy for each week - show Monday only.
```sql
SELECT tw.name, DATE_FORMAT(tw.whn,'%Y-%m-%d'), 
 tw.confirmed - lw.confirmed
 FROM covid tw LEFT JOIN covid lw ON 
  DATE_ADD(lw.whn, INTERVAL 1 WEEK) = tw.whn
   AND tw.name=lw.name
WHERE tw.name = 'Italy' AND WEEKDAY(tw.whn) = 0
ORDER BY tw.whn
```
6. Add a column to show the ranking for the number of deaths due to COVID.
```sql
SELECT 
   name,
   confirmed,
   RANK() OVER (ORDER BY confirmed DESC) rc,
   deaths,
   RANK() OVER (ORDER BY deaths DESC) death_rank
  FROM covid
WHERE whn = '2020-04-20'
ORDER BY confirmed DESC
```
7. Show the infection rate ranking for each country. Only include countries with a population of at least 10 million.
```sql
SELECT 
   world.name,
   ROUND(100000*confirmed/population,2),
   RANK() OVER(ORDER BY 100000*confirmed/population) AS rank
  FROM covid JOIN world ON covid.name=world.name
WHERE whn = '2020-04-20' AND population > 10000000
ORDER BY population DESC
```
8. For each country that has had at least 20000 new cases in a single day, show name of country, the date of the peak number of new cases and the peak value.
```sql
SELECT covid_new_cases.name , date , peak_cases
FROM
(
SELECT 
    name, 
    DATE_FORMAT(whn,'%Y-%m-%d') AS date,
    (confirmed - LAG(confirmed , 1 ) OVER(PARTITION BY name ORDER BY whn)) AS new_cases
    FROM covid
) AS covid_new_cases
INNER JOIN
(
SELECT name,
       MAX(new_cases) AS peak_cases
       FROM (SELECT name,
                    DATE_FORMAT(whn,'%Y-%m-%d') AS date,
                    confirmed - LAG(confirmed , 1 ) 
                    OVER(PARTITION BY name ORDER BY whn) AS new_cases
            FROM covid) AS covid_new_cases
                        GROUP BY name
            HAVING MAX(new_cases) >= 20000
) AS covid_peak_cases

ON 
covid_new_cases.new_cases = covid_peak_cases.peak_cases 
AND 
covid_new_cases.name = covid_peak_cases.name
```
## 9 Self JOIN
1. How many stops are in the database. 
```sql
SELECT COUNT(*)
FROM stops
```
2. Find the id value for the stop 'Craiglockhart' 
```sql
SELECT id 
FROM stops
WHERE name = 'Craiglockhart'
```
3. Give the id and the name for the stops on the '4' 'LRT' service. 
```sql
SELECT id, name
FROM stops
JOIN route 
ON stops.id = route.stop
WHERE num = '4' AND company = 'LRT'
```
4. The query shown gives the number of routes that visit either London Road (149) or Craiglockhart (53). Run the query and notice the two services that link these stops have a count of 2. Add a HAVING clause to restrict the output to these two routes. 
```sql
SELECT company, num, COUNT(*)
FROM route WHERE stop=149 OR stop=53
GROUP BY company, num
HAVING COUNT(*) = 2
```
5. Execute the self join shown and observe that b.stop gives all the places you can get to from Craiglockhart, without changing routes. Change the query so that it shows the services from Craiglockhart to London Road. 
```sql
SELECT a.company, a.num, a.stop, b.stop
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
WHERE a.stop=53 AND b.stop = 149
```
6. The query shown is similar to the previous one, however by joining two copies of the stops table we can refer to stops by name rather than by number. Change the query so that the services between 'Craiglockhart' and 'London Road' are shown. If you are tired of these places try 'Fairmilehead' against 'Tollcross' 
```sql
SELECT a.company, a.num, stopa.name, stopb.name
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' AND stopb.name = 'London Road'
```
7. Give a list of all the services which connect stops 115 and 137 ('Haymarket' and 'Leith') 
```sql
SELECT DISTINCT a.company, a.num
FROM route AS a
JOIN route AS b
ON a.company = b.company AND a.num = b.num
WHERE a.stop = 115 AND b.stop = 137
```
8. Give a list of the services which connect the stops 'Craiglockhart' and 'Tollcross' 
```sql
SELECT a.company, a.num
FROM route AS a
JOIN route AS b
ON a.num = b.num AND a.company = b.company
JOIN stops AS a_stop
ON a.stop = a_stop.id
JOIN stops AS b_stop
ON b.stop = b_stop.id
WHERE a_stop.name = 'Craiglockhart' AND b_stop.name = 'Tollcross'
```
9. Give a distinct list of the stops which may be reached from 'Craiglockhart' by taking one bus, including 'Craiglockhart' itself, offered by the LRT company. Include the company and bus no. of the relevant services. 
```sql
SELECT b_stop.name, a.company, a.num
FROM route AS a
JOIN route AS b
ON a.num = b.num AND a.company = b.company
JOIN stops AS a_stop
ON a.stop = a_stop.id
JOIN stops AS b_stop
ON b.stop = b_stop.id
WHERE a_stop.name = 'Craiglockhart' AND a.company = 'LRT'
```
10. Find the routes involving two buses that can go from Craiglockhart to Lochend.
Show the bus no. and company for the first bus, the name of the stop for the transfer,
and the bus no. and company for the second bus.
```sql
SELECT a.num, a.company, stops_b.name, d.num, d.company

FROM route AS a
JOIN route AS b
  ON b.num = a.num AND b.company = a.company
JOIN route AS c
  ON c.stop = b.stop
JOIN route AS d
  ON d.num = c.num AND d.company = c.company

JOIN stops AS stops_a
  ON stops_a.id = a.stop
JOIN stops AS stops_b
  ON stops_b.id = b.stop
JOIN stops AS stops_d
  ON stops_d.id = d.stop

WHERE stops_a.name = 'Craiglockhart' 
AND stops_d.name = 'Lochend'

ORDER BY a.num, stops_b.name, d.num
```
