## Solution de Atelier 2
# Création des tables Departments et Employees:
# table Departement:
```sql
CREATE TABLE Departments (
  Code INTEGER PRIMARY KEY,
  Name varchar(255) NOT NULL ,
  Budget decimal NOT NULL 
);
```
# table Employees:
```sql
CREATE TABLE Employees (
  SSN INTEGER PRIMARY KEY,
  Name varchar(255) NOT NULL ,
  LastName varchar(255) NOT NULL ,
  Department INTEGER NOT NULL , 
  foreign key (department) references Departments(Code) 
);
```
```sql
INSERT INTO Departments(Code,Name,Budget) VALUES(14,'IT',65000);
INSERT INTO Departments(Code,Name,Budget) VALUES(37,'Accounting',15000);
INSERT INTO Departments(Code,Name,Budget) VALUES(59,'Human Resources',240000);
INSERT INTO Departments(Code,Name,Budget) VALUES(77,'Research',55000);

INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('123234877','Michael','Rogers',14);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('152934485','Anand','Manikutty',14);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('222364883','Carol','Smith',37);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('326587417','Joe','Stevens',37);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('332154719','Mary-Anne','Foster',14);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('332569843','George','ODonnell',77);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('546523478','John','Doe',59);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('631231482','David','Smith',77);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('654873219','Zacary','Efron',59);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('745685214','Eric','Goldsmith',59);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('845657245','Elizabeth','Doe',14);
INSERT INTO Employees(SSN,Name,LastName,Department) VALUES('845657246','Kumar','Swamy',14);
```


# 2.1 Sélectionnez le nom de famille de tous les employés
```sql
SELECT LastName FROM employees; 
 
 ```

# 2.2 Sélectionnez le nom de famille de tous les employés, sans doublons.
```sql
SELECT DISTINCT LastName FROM employees;
```
#   2.3 Sélectionnez toutes les données des employés dont le nom de famille est "Smith".
```sql
SELECT * FROM employees WHERE LastName='smith';
```
# 2.4 Sélectionnez toutes les données des employés dont le nom de famille est "Smith" ou "Doe".
```sql
SELECT * FROM employees WHERE LastName IN ('Smith','Doe');
```
# 2.5 Sélectionnez toutes les données des employés qui travaillent dans le département 14.
```sql
SELECT * FROM employees WHERE Department=14;
```
# 2.6 Sélectionner toutes les données des employés qui travaillent dans le département 37 ou le département 77.
```sql
SELECT * FROM employees WHERE Department IN (37 , 77);
```
# 2.7 Sélectionner toutes les données des employés dont le nom de famille commence par un "S".
```sql
SELECT * FROM employees WHERE LastName LIKE ('s%')
```
# 2.8 Sélectionner la somme des budgets de tous les départements.
```sql
SELECT SUM(Budget) FROM departments;
```
#  2.9 Sélectionnez le nombre d'employés dans chaque département (vous devez seulement indiquer le code du département et le nombre d'employés).
```sql
SELECT COUNT(*) AS conteur,Department AS code FROM employees GROUP BY Department;
```
# 2.10 Sélectionnez toutes les données des employés, y compris les données du département de chaque employé.
```sql
SELECT p.Name AS employee,d.Name AS departement FROM employees p INNER JOIN departments d ON p.Department=d.Code;
```
#  2.11 Sélectionnez le nom et le prénom de chaque employé, ainsi que le nom et le budget du département de l'employé.
```sql
SELECT e.Name, e.LastName, d.Name, d.budget from employees e INNER join departments d ON e.Department = d.code;
```
#  2.12 Sélectionnez le nom et le nom de famille des employés travaillant pour des ministères dont le budget est supérieur à 60 000 $.
```sql
SELECT e.Name, e.LastName, d.budget
FROM employees e INNER JOIN departments d ON e.department = d.Code
WHERE d.budget > 60000
```
# 2.13 Sélectionnez les départements dont le budget est supérieur au budget moyen de l'ensemble des départements.
```sql
SELECT *
FROM departments
WHERE budget>(SELECT AVG(budget) FROM departments)
```
#  2.14 Sélectionnez les noms des départements ayant plus de deux employés.
```sql
SELECT d.Name 
FROM departments d INNER JOIN employees e ON e.Department=d.code
GROUP BY d.Name HAVING COUNT(*) >2
```
# 2.15 Très important - Sélectionnez le nom et le nom de famille des employés travaillant pour les ministères dont le budget est le deuxième plus bas.
```sql
SELECT * FROM Departments d ORDER BY d.budget DESC LIMIT 2;
SELECT e.Name, e.LastName, d.Budget FROM Employees e INNER JOIN departments d ON e.Department = d.code WHERE e.Department = (SELECT sub.Code FROM (SELECT * FROM Departments d ORDER BY d.budget desc LIMIT 2) sub ORDER BY budget DESC LIMIT 1);
```
# 2.16 Ajoutez un nouveau service appelé "Quality assurance", avec un budget de 40 000 $ et le code de service 11. Et ajoutez un employé appelé "Mary Moore" dans ce département, avec le code SSN 847-21-9811.
```sql
insert into departments values(11, 'Quality Assurance', 40000);
insert into employees values(847219811, 'Mary', 'Moore', 11);
```
# 2.17 Réduire le budget de tous les départements de 10 %.
```sql
update departments set budget = 0.9 * budget;
```
#  2.18 Réaffecter tous les employés du département de la recherche (code 77) au département informatique (code 14).
```sql
update employees set department = 14 where department = 77;
```
#  2.19 Supprimer du tableau tous les employés du département informatique (code 14).
```sql
delete from employees where department = 14;
```
# 2.20 Supprimer du tableau tous les employés qui travaillent dans des départements dont le budget est supérieur ou égal à 60 000 $.
```sql
DELETE FROM employees WHERE departement IN (SELECT Code FROM departments WHERE Budget >= 60000 )

```
# 2.21 Supprimer du tableau tous les employés.
```sql
delete from employees;

```




