### [SQLBolt](https://sqlbolt.com/) Learn SQL with simple, interactive exercises.

### SQL Lesson 1: SELECT queries 101 

#### Exercise 1 — Tasks. Find the title of each film
```sql
SELECT title FROM movies;
```

#### Exercise 1 - Tasks. Find the director of each film
```sql
SELECT director FROM movies;
```

#### Exercise 1 - Tasks. Find the title and director of each film
```sql
SELECT title, director FROM movies;
```

#### Exercise 1 - Tasks. Find the title and year of each film
```sql
SELECT title, year FROM movies;
```

#### Exercise 1 - Tasks. Find all the information about each film 
```sql
SELECT * FROM movies;
```

### SQL Lesson 2: Queries with constraints (Pt. 1) 

#### Exercise 2 — Tasks. Find the movie with a row id of 6
```sql
SELECT * FROM movies WHERE id = 6;
```

#### Exercise 2 — Tasks. Find the movies released in the years between 2000 and 2010
```sql
SELECT * FROM movies WHERE year BETWEEN 2000 AND 2010;
```

#### Exercise 2 — Tasks. Find the movies not released in the years between 2000 and 2010
```sql
SELECT * FROM movies WHERE year NOT BETWEEN 2000 AND 2010;
```

#### Exercise 2 — Tasks. Find the first 5 Pixar movies and their release year
```sql
SELECT * FROM movies LIMIT 5;
```

### SQL Lesson 3: Queries with constraints (Pt. 2) 

#### Exercise 3 — Tasks. Find all the Toy Story movies
```sql
SELECT * FROM movies WHERE title LIKE 'Toy Story%';
```

#### Exercise 3 — Tasks. Find all the movies directed by John Lasseter
```sql
SELECT * FROM movies WHERE director = 'John Lasseter';
```

#### Exercise 3 — Tasks. Find all the movies (and director) not directed by John Lasseter
```sql
SELECT * FROM movies WHERE director != 'John Lasseter';
```

#### Exercise 3 — Tasks. Find all the WALL-* movies
```sql
SELECT * FROM movies WHERE title LIKE 'WALL-%';
```

### SQL Lesson 4: Filtering and sorting Query results 

#### Exercise 4 — Tasks. List all directors of Pixar movies (alphabetically), without duplicates
```sql
SELECT DISTINCT director FROM movies GROUP BY director ORDER BY director ASC;
```

#### Exercise 4 — Tasks. List the last four Pixar movies released (ordered from most recent to least)
```sql
SELECT DISTINCT title FROM movies ORDER BY year DESC LIMIT 4;
```

#### Exercise 4 — Tasks. List the first five Pixar movies sorted alphabetically
```sql
SELECT DISTINCT title FROM movies ORDER BY title ASC LIMIT 5;
```

#### Exercise 4 — Tasks. List the next five Pixar movies sorted alphabetically
```sql
SELECT DISTINCT title FROM movies ORDER BY title ASC LIMIT 5 OFFSET 5;
```

### SQL Review: Simple SELECT Queries 

#### Review 1 — Tasks. List all the Canadian cities and their populations
```sql
SELECT * FROM north_american_cities WHERE country = 'Canada';
```

#### Review 1 — Tasks. Order all the cities in the United States by their latitude from north to south
```sql
SELECT * FROM north_american_cities WHERE country = 'United States' ORDER BY latitude DESC;
```

#### Review 1 — Tasks. List all the cities west of Chicago, ordered from west to east
```sql
SELECT * FROM north_american_cities WHERE longitude < (SELECT longitude FROM north_american_cities WHERE city = 'Chicago') ORDER BY longitude;
```

#### Review 1 — Tasks. List the two largest cities in Mexico (by population)
```sql
SELECT city FROM north_american_cities WHERE country = 'Mexico' ORDER BY population DESC LIMIT 2;
```

#### Review 1 — Tasks. List the third and fourth largest cities (by population) in the United States and their population
```sql
SELECT city, population FROM north_american_cities WHERE country = 'United States' ORDER BY population DESC LIMIT 2 OFFSET 2;
```

### SQL Lesson 6: Multi-table queries with JOINs 

#### Exercise 6 — Tasks. Find the domestic and international sales for each movie
```sql
SELECT * FROM movies JOIN boxoffice ON movies.id = boxoffice.movie_id;
```

#### Exercise 6 — Tasks. Show the sales numbers for each movie that did better internationally rather than domestically
```sql
SELECT * FROM movies JOIN boxoffice ON movies.id = boxoffice.movie_id WHERE international_sales > domestic_sales;
```

#### Exercise 6 — Tasks. List all the movies by their ratings in descending order
```sql
SELECT * FROM movies JOIN boxoffice ON movies.id = boxoffice.movie_id ORDER BY rating DESC;
```

### SQL Lesson 7: OUTER JOINs
#### Exercise 7 — Tasks. Find the list of all buildings that have employees
```sql
SELECT DISTINCT building FROM employees;
```

#### Exercise 7 — Tasks. Find the list of all buildings and their capacity
```sql
SELECT * FROM buildings;
```

#### Exercise 7 — Tasks. List all buildings and the distinct employee roles in each building (including empty buildings)
```sql
SELECT DISTINCT building_name, role FROM buildings LEFT JOIN employees ON buildings.building_name = employees.building;
```

### SQL Lesson 8: A short note on NULLs 

#### Exercise 8 — Tasks. Find the name and role of all employees who have not been assigned to a building
```sql
SELECT * FROM employees WHERE building IS NULL;
```

#### Exercise 8 — Tasks. Find the names of the buildings that hold no employees
```sql
SELECT * FROM buildings LEFT JOIN employees ON buildings.building_name = employees.building WHERE employees.role IS NULL;
```

### SQL Lesson 9: Queries with expressions 

#### Exercise 9 — Tasks. List all movies and their combined sales in millions of dollars
```sql
SELECT DISTINCT title, (domestic_sales + international_sales) / 1000000 AS sale FROM movies JOIN boxoffice ON movies.id = boxoffice.movie_id;
```

#### Exercise 9 — Tasks. List all movies and their ratings in percent
```sql
SELECT DISTINCT title, (rating * 10) AS percent_rating FROM movies JOIN boxoffice ON movies.id = boxoffice.movie_id;
```

#### Exercise 9 — Tasks. List all movies that were released on even number years
```sql
SELECT * FROM movies WHERE year % 2 = 0;
```

### SQL Lesson 10: Queries with aggregates (Pt. 1) 

#### Exercise 10 — Tasks. Find the longest time that an employee has been at the studio
```sql
SELECT * FROM employees ORDER BY years_employed DESC LIMIT 1;
```

#### Exercise 10 — Tasks. For each role, find the average number of years employed by employees in that role
```sql
SELECT role, AVG(years_employed) FROM employees GROUP BY role;
```

#### Exercise 10 — Tasks. Find the total number of employee years worked in each building
```sql
SELECT Building, SUM(years_employed) FROM employees GROUP BY Building;
```

### SQL Lesson 11: Queries with aggregates (Pt. 2)

#### Exercise 11 — Tasks. Find the number of Artists in the studio (without a HAVING clause)
```sql
SELECT COUNT(*) FROM employees WHERE role = 'Artist';
```

#### Exercise 11 — Tasks. Find the number of Employees of each role in the studio
```sql
SELECT role, COUNT(*) FROM employees GROUP BY role;
```

#### Exercise 11 — Tasks. Find the total number of years employed by all Engineers
```sql
SELECT SUM(years_employed) FROM employees WHERE role = 'Engineer';
```

### SQL Lesson 12: Order of execution of a Query

#### Exercise 12 — Tasks. Find the number of movies each director has directed
```sql 
SELECT director, count(title) FROM movies GROUP BY director;
```

#### Exercise 12 — Tasks. Find the total domestic and international sales that can be attributed to each director
```sql
SELECT director, SUM(domestic_sales + international_sales) AS total FROM movies JOIN boxoffice ON movies.id = boxoffice.movie_id GROUP BY director;
```

### SQL Lesson 13: Inserting rows

#### Exercise 13 — Tasks. Add the studio's new production, Toy Story 4 to the list of movies (you can use any director)
```sql
INSERT INTO Movies (id, title, director, year, length_minutes)
VALUES (15, 'Toy Story 4', 'Lee Unkrich', 2017, 123);
```

#### Exercise 13 — Tasks. Toy Story 4 has been released to critical acclaim! It had a rating of 8.7, and made 340 million domestically and 270 million internationally. Add the record to the BoxOffice table.
```sql
INSERT INTO Boxoffice (movie_id, rating, domestic_sales, international_sales)
VALUES (15, 8.7, 340000000, 270000000);
```

### SQL Lesson 14: Updating rows 

#### Exercise 14 — Tasks. The director for A Bug's Life is incorrect, it was actually directed by John Lasseter
```sql
UPDATE movies SET director = 'John Lasseter' WHERE title = "A Bug's Life";
```

#### Exercise 14 — Tasks. The year that Toy Story 2 was released is incorrect, it was actually released in 1999
```sql
UPDATE movies SET year = 1999 WHERE title = "Toy Story 2";
```

#### Exercise 14 — Tasks. Both the title and director for Toy Story 8 is incorrect! The title should be "Toy Story 3" and it was directed by Lee Unkrich
```sql
UPDATE movies SET title = 'Toy Story 3', director = 'Lee Unkrich' WHERE title = "Toy Story 8";
```

### SQL Lesson 15: Deleting rows
#### Exercise 15 — Tasks. This database is getting too big, lets remove all movies that were released before 2005.
```sql
DELETE FROM movies WHERE year < 2005;
```

#### Exercise 15 — Tasks. Andrew Stanton has also left the studio, so please remove all movies directed by him.
```sql
DELETE FROM movies WHERE director = 'Andrew Stanton';
```

### SQL Lesson 16: Creating tables

#### Exercise 16 — Tasks. Create a new table named Database with the following columns:
| Column Name    | Data Type | Description                          |
|----------------|-----------|--------------------------------------|
| Name           | TEXT      | A string (text) describing the name of the database. |
| Version        | FLOAT     | A floating-point number representing the latest version of this database. |
| Download_count | INTEGER   | An integer count of the number of times this database was downloaded. |

**Constraints**: This table has no constraints.

```sql
CREATE TABLE IF NOT EXISTS database (
    id INTEGER PRIMARY KEY,
    name TEXT,
    version FLOAT,
    download_count INT
);
```

### SQL Lesson 17: Altering tables

#### Exercise 17 — Tasks. Add a column named Aspect_ratio with a FLOAT data type to store the aspect-ratio each movie was released in.
```sql
ALTER TABLE movies ADD Aspect_ratio FLOAT DEFAULT 3;
```

#### Exercise 17 — Tasks. Add another column named Language with a TEXT data type to store the language that the movie was released in. Ensure that the default for this language is English.
```sql
ALTER TABLE movies ADD Language TEXT DEFAULT English;
```    
    
### SQL Lesson 18: Dropping tables

#### Exercise 18 — Tasks. We've sadly reached the end of our lessons, lets clean up by removing the Movies table
```sql
DROP TABLE IF EXISTS Movies;
```

#### Exercise 18 — Tasks. And drop the BoxOffice table as well
```sql
DROP TABLE IF EXISTS BoxOffice;
```
    



