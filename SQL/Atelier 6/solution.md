## Question 1
```sql
SELECT s.Name, p.Name as Name_Project, p.Hours FROM scientists s INNER JOIN assignedto a ON s.SSN=a.Scientist INNER JOIN projects p ON a.Project = p.Code ORDER BY p.Name, s.Name;
```
## Question 2
```sql
SELECT name FROM projects WHERE CODE not IN (SELECT project FROM assignedto)
```