## Question 1
```sql
SELECT Title  FROM Movies; 
 ```

## question 2
```sql
SELECT DISTINCT Rating  FROM Movies; 
 ``` 

## question 3
```sql
 SELECT *  FROM Movies  WHERE Rating IS NULL; 
 ```

## question 4
```sql
 SELECT *  FROM MovieTheaters  WHERE Movie IS NULL; 
``` 

## question 5
```sql
 SELECT * FROM MovieTheaters LEFT JOIN Movies ON MovieTheaters.Movie = Movies.Code; 
 ```

## question 6
```sql 
SELECT * FROM MovieTheaters RIGHT JOIN Movies ON MovieTheaters.Movie = Movies.Code; 
 ```

## question 7 
```sql 
SELECT Title FROM Movies 
 WHERE Code NOT IN 
   ( 
     SELECT Movie FROM MovieTheaters 
     WHERE Movie IS NOT NULL 
   ); 
 ```
 


## question 8
```sql
 INSERT INTO Movies(Title,Rating) VALUES('One, Two, Three',NULL);
```

## question 9
```sql
 UPDATE Movies SET Rating='G' WHERE Rating IS NULL
 ``` 
## quetion 10
```sql
DELETE FROM MovieTheaters WHERE Movie IN 
   (SELECT Code FROM Movies WHERE Rating = 'NC-17');
   ```