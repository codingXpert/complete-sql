## Working with Default and Check 
```bash

CREATE SCHEMA College;
CREATE TABLE students
(
	id INT NOT NULL PRIMARY KEY,
    Name VARCHAR(20) NOT NULL,
    age INT NOT NULL CHECK(age >= 18),
    gender VARCHAR(10) NOT NULL ,
    phone VARCHAR(10) NOT NULL UNIQUE,
    city VARCHAR(20) NOT NULL DEFAULT 'AGRA'
);

INSERT INTO students VALUES
(
	(1 , 'Pratap' , 20 , 'male' , '123456789' , 'hazaribagh'),
    (2 , 'Ranjeet' , 24 , 'male' , '9876543210' , 'agra'),
    (3 , 'Abhishek' , 23 , 'male' , '9087654321', 'ranchi' ),
    (4 , 'Deepak' , 24 , 'male' , '897654321' , 'patna'),
    (5 , 'Rahul' , 26 , 'male' , '8689754321' , 'hazaribagh')
);

# checking for default values
INSERT INTO students(id , name , age , gender , phone)   #here we don't add city , however the default value of city can be shown in city
VALUES(6 , 'Vivek' , 24 , 'male', '8976543213');


SELECT * FROM students;

 ```


 ## AND , OR , NOT Clause

```sql
SELECT * FROM students 
WHERE age >= 18 AND age <= 23;
SELECT * FROM students;

SELECT * FROM students 
WHERE age >= 18 AND city = 'hazaribagh';
SELECT * FROM students;

SELECT * FROM students 
WHERE age >= 18 OR age <= 23;
SELECT * FROM students;

SELECT * FROM students 
WHERE NOT city = 'hazaribagh';
SELECT * FROM students;

SELECT * FROM students 
WHERE NOT city = 'hazaribagh' AND age <= 23;
SELECT * FROM students;

```

## IN operator

```sql
SELECT * FROM students 
WHERE age IN (20 , 23);  --All students whose age is 20 and 23
```

```sql
SELECT * FROM students 
WHERE age NOT IN (20 , 23);  --All students whose age is not 20 and 23
```

```sql
SELECT * FROM students 
WHERE city IN ('hazaribagh' , 'xyz');   -- All students who are from city hazaribagh and xyz
```

```sql
SELECT * FROM students 
WHERE city NOT IN ('hazaribagh' , 'xyz');  --All students who are not from hazaribagh and xyz
```


## Between ans Not Between

```sql
SELECT * FROM students
WHERE age BETWEEN 23 AND 25;
```

```sql
SELECT * FROM students
WHERE age NOT BETWEEN 23 AND 25;
```

```sql
SELECT * FROM students
WHERE name  BETWEEN 'a' AND 'r';   -- shows the the record only whose name's first character starts with a and r(including a and excluding r)
```

```sql
SELECT * FROM students
WHERE name NOT BETWEEN 'a' AND 'r';   -- shows the the record only whose name's first character does not start with a and r(excluding a and including r) 
```   

## LIKE OPERATOR

```sql
![Screenshot (354)](https://user-images.githubusercontent.com/101451924/204613649-e828109c-aafd-4eb4-bd65-e0a73ab4bcd5.png)

```


```sql
SELECT * FROM students
WHERE name  LIKE "v%";
```


```sql
SELECT * FROM students
WHERE name  LIKE "rm%";  -- No name starts with rm
```


```sql
SELECT * FROM students
WHERE name  LIKE "%t"; 
```


```sql
SELECT * FROM students
WHERE name  LIKE "r%" OR name LIKE "a%";  -- name starts with r OR a
```


```sql
SELECT * FROM students
WHERE name NOT LIKE "r%" ;   -- all students whose name does not starts with r
```


```sql
SELECT * FROM students
WHERE BINARY name LIKE "r%" ;   -- all students whose name starts with small r(BEcause of BINARY).
```


```sql
SELECT * FROM students
WHERE BINARY name LIKE "R%"; -- all students whose name starts with capital R
```


```sql
SELECT * FROM students
WHERE phone LIKE "89%"; 
```

## REGULAR EXPRRESSION
![Screenshot (355)](https://user-images.githubusercontent.com/101451924/204861753-1b142bf5-f6c9-4db8-a229-9ac19d0275cc.png)

```sql
SELECT * FROM students
WHERE name REGEXP 'ra' ; -- all students contaning 'ra'  any where in name
```

```sql
SELECT * FROM students
WHERE name REGEXP '^ra' ;  --name starting with 'ra'
```

```sql
SELECT * FROM students
WHERE name REGEXP '[ra]' ;  -- All students whose name contains either 'r' or 'a'
```

## ORDER BY and DISTINCT CLAUSE

```sql
SELECT * FROM students
ORDER BY name DESC;     --ASC by-default
```


```sql
SELECT * FROM students
WHERE city = 'agra'
ORDER BY name DESC;
```


```sql
SELECT DISTINCT city FROM students;   -- list of all cities
```


```sql
SELECT DISTINCT city AS Distinct_City FROM students;
```

## IS NULL and NOT NULL CLAUSE

```sql
SELECT * FROM students
WHERE age IS NULL;       -- all students whose age is null
```


```sql
SELECT * FROM students
WHERE age IS NOT NULL;     --all students is not null
```

## LIMIT and OFFSET CLAUSE

```sql
SELECT * FROM students
LIMIT 2;               -- list first 2 records only
```


```sql
SELECT * FROM students
WHERE City = "hazaribagh"
ORDER BY age DESC
LIMIT 2;
```


```sql
SELECT * FROM students
LIMIT  3 , 2;            -- starts after 3(offset) records and list 2(limit) records
```

## AGGREGATE FUNCTIONS(COUNT , MAX , MIN , SUM , AVG)

```sql
SELECT COUNT(name) FROM students;  --count total no. of name
```

```sql
SELECT COUNT(DISTINCT city) FROM students;   -- count total no. of distinct city
```


```sql
SELECT MAX(age) AS MAX_AGE FROM students;   -- finds max age
```


```sql
SELECT MIN(age) AS MIN_AGE FROM students;
```


```sql
SELECT SUM(age) AS TOTAL_SUM FROM students;    -- total sum of age
```


```sql
SELECT AVG(age) AS AVG_AGE FROM students;
```

## Updating Tabel's Record
```sql
UPDATE  students 
SET city = "ranchi" 
WHERE id =3 ;
```


```sql
UPDATE  students 
SET city = "ranchi" , age = 20    --Updating the two record of two IDs
WHERE id IN (1,2) ;
```

## COMMIT and ROLLBACK
```sql
COMMIT ;      --commiting or saving all the changes(after commiting rollback is not possiable) 
ROLLBACK ; -- Undo all the changes 
```

## DELETING a record or DELETING a row
```sql
DELETE FROM students   -- if we don't add a where clause with delete then all the records or rows will be deleted.
WHERE id =2;
```

## PRIMARY KEY 
```sql
### A primary key always has unique data
### A primary key can not have null value
### A table can contain only one primary key
```


```sql
### Setting primary key while creating  table
CREATE TABLE table_name(
    id INT NOT NULL AUTO_INCREMENT 
    PRIMARY KEY(id);
);

### Setting primary key after table is created.

ALTER TABLE table_name
ADD PRIMARY KEY(id);
```

## FOREIGN KEY
```sql
### A FOREIGN KEY is key used to link two tables together.
### A FOREIGN key in one table used to point PRIMARY key in another table.
 
```


```sql
### Setting FOREIGN key while creating table

CREATE TABLE students(
    id INT NOT NULL AUTO_INCREMENT,
    PRIMARY KEY (id),
    FOREIGN KEY(city) REFERENCES City(cid);
);


### Setting FOREIGN KEY after creation of table

ALTER TABLE table_name
ADD FPREIGN KEY(city) REFERENCES City(cid);
```


```sql
### Eg.

CREATE TABLE personal(
id INT NOT NULL , 
name VARCHAR(50) NOT NULL,
precentage INT NOT NULL,
age INT NOT NULL ,
gender VARCHAR(1) NOT NULL,
city INT NOT NULL,
PRIMARY KEY(id),
FOREIGN KEY(city) REFERENCES City(cid)
);

INSERT INTO personal (id , name , precentage , age , gender , city)
VALUES(1 , "Ram Kumar" , 45 , 19 , "M" , 1),
(2 , "Sarita Kumari" , 55 , 22 , "F" , 2),
(3 , "Salman Khan" , 62 , 20 , "M" , 1),
(4 , "Juhi Chawala" , 47 , 18 , "F" , 3),
(5 , "Anil Kapoor" , 74 , 22 , "M" , 1),
(6 , "Jhon Abraham" , 64 , 21 , "M" , 2),
(7 , "Shahid kapoor" , 52 , 20, "M" , 1);
```

## INNER JOIN Clause

![Screenshot (357)](https://user-images.githubusercontent.com/101451924/205965984-9d267f0e-b399-4c4f-a9f7-905fd4c48bc7.png)

![Screenshot (358)](https://user-images.githubusercontent.com/101451924/205966452-6bc79007-fa15-40bc-9dfe-246ae42f98e5.png)

![Screenshot (359)](https://user-images.githubusercontent.com/101451924/205966584-01674838-2260-4439-a4c3-75efcdf8b72a.png)


```sql
SELECT * FROM personal INNER JOIN city
ON personal.city = city.cid;       -- ON means on which column we want to apply inner join

### Use aliases to see the records  

SELECT * FROM personall p INNER JOIN city c  -- p and c(alias name) are made short of prersonal and city
ON p.city = c.cid;  

###  Displaying only selected records from table

SELECT p.id,p.name,p.precentage,p.age,p.gender,c.cityname 
FROM personal p INNER JOIN city c
ON p.city = c.cid;


SELECT p.id,p.name,p.precentage,p.age,p.gender,c.cityname 
FROM personal p INNER JOIN city c
ON p.city = c.cid
WHERE c.cityname = 'agra';


SELECT p.id,p.name,p.precentage,p.age,p.gender,c.cityname 
FROM personal p INNER JOIN city c
ON p.city = c.cid
WHERE c.cityname = 'agra'
ORDER BY name;
```

## LEFT JOIN Clause 

![Screenshot (360)](https://user-images.githubusercontent.com/101451924/205976175-4359dc03-e5fc-4f28-a1c6-f90c0b781a97.png)

![Screenshot (361)](https://user-images.githubusercontent.com/101451924/205976857-70ff8485-c78c-424d-af86-803584d8ec3b.png)

![Screenshot (364)](https://user-images.githubusercontent.com/101451924/205976887-692b429b-925f-4950-8eba-f1222039894c.png)



```sql
SELECT * FROM personal LEFT JOIN city 
ON personal.city = city.cid;
```


# RIGHT JOIN Clause

![Screenshot (365)](https://user-images.githubusercontent.com/101451924/205979797-9d9d2abe-f7e6-44c6-9564-4a26d520e462.png)

![Screenshot (366)](https://user-images.githubusercontent.com/101451924/205979817-5aa2922d-1600-4415-9c2a-c3b582004f38.png)

![Screenshot (367)](https://user-images.githubusercontent.com/101451924/205979822-101c1fd6-5720-4e14-af76-15af86825087.png)


```sql
SELECT * FROM personal RIGHT JOIN city 
ON personal.city = city.cid;
```

## CROSS JOIN Clause

### Unlike all the previous three joins cross join does not use the concept of Primary and Foreign Key . CROSS JOINs are used to combine each row of one table with each row of another table, and return the Cartesian product of the # sets of rows from the tables that are joined.

![Screenshot (368)](https://user-images.githubusercontent.com/101451924/205982714-3edcc9d2-4264-4d9c-9b2e-48e8586505e3.png)

![Screenshot (369)](https://user-images.githubusercontent.com/101451924/205982757-30ba1596-33a5-4cf6-b419-dd64d21af708.png)

![Screenshot (370)](https://user-images.githubusercontent.com/101451924/205982768-ec7916bd-0fc7-4ffd-9689-411db6c033e2.png)


```sql
SELECT * FROM personal CROSS JOIN city;


SELECT * FROM presonal , city;   -- Prints the same result
```

## MULTIPLE JOINS
![Screenshot (373)](https://user-images.githubusercontent.com/101451924/206842922-9dd296b5-9fe4-481f-8ed2-d9a6d003f0ea.png)

![Screenshot (374)](https://user-images.githubusercontent.com/101451924/206842924-3142cad5-5cd9-428a-9c00-1423bc8d50bc.png)

![Screenshot (376)](https://user-images.githubusercontent.com/101451924/206842930-98c3e04a-f368-40ef-9955-97fff84b7cb8.png)

```sql
CREATE TABLE courses(
    course_id INT NOT NULL AUTO INCREMENT
    course_name VARCHAR(20)
);

INSERT INTO `college`.`courses` (`course_id`, `course_name`) VALUES ('1', 'B.tech');
INSERT INTO `college`.`courses` (`course_id`, `course_name`) VALUES ('2', 'BCA');
INSERT INTO `college`.`courses` (`course_id`, `course_name`) VALUES ('3', 'MCA');

### NOTE:- ADD a new column in the personal table
ALTER TABLE `college`.`personal` 
ADD COLUMN `courses` VARCHAR(45) NOT NULL AFTER `city`;

### And Insert values in this column
UPDATE `college`.`personal` SET `courses` = '1' WHERE (`id` = '1');
UPDATE `college`.`personal` SET `courses` = '2' WHERE (`id` = '2');
UPDATE `college`.`personal` SET `courses` = '1' WHERE (`id` = '3');
UPDATE `college`.`personal` SET `courses` = '1' WHERE (`id` = '4');
UPDATE `college`.`personal` SET `courses` = '3' WHERE (`id` = '5');
UPDATE `college`.`personal` SET `courses` = '2' WHERE (`id` = '6');
UPDATE `college`.`personal` SET `courses` = '3' WHERE (`id` = '7');

### Now apply multiple join

SELECT * FROM personal p
INNER JOIN city c 
ON p.city = c.cid
INNER JOIN courses cr
ON p.courses = cr.course_id;
```
## GROUP BY & HAVING Clause
------------------------------------
### GROUP BY

![Screenshot (377)](https://user-images.githubusercontent.com/101451924/206849389-406609fe-d6b0-4f77-ad30-a264c7f95cbc.png)

![Screenshot (378)](https://user-images.githubusercontent.com/101451924/206849402-b2c7a3d6-fd3b-4a1d-b36d-5171c40173e9.png)

![Screenshot (379)](https://user-images.githubusercontent.com/101451924/206849406-751b06d6-565d-40da-80a8-150c794a825a.png)

```sql
SELECT city , COUNT(city)
FROM personal 
GROUP BY city

-----------------------------------------
SELECT c.cityname , COUNT(p.city)
FROM personal p INNER JOIN city c
ON p.city = c.cid
GROUP BY city;

-----------------------------------------
SELECT c.cityname , COUNT(p.city)
FROM personal p INNER JOIN city c
ON p.city = c.cid
WHERE p.age >= 20      --total student whose age is grater equals to 20
GROUP BY city;

------------------------------------------
SELECT c.cityname , COUNT(p.city)
FROM personal p INNER JOIN city c
ON p.city = c.cid
GROUP BY city
ORDER BY COUNT(p.city) DESC;

-------------------------------------------
### HAVING Clause

![Screenshot (381)](https://user-images.githubusercontent.com/101451924/206850567-6ee785a1-7bbc-4f30-ad33-d307d3beced9.png)

![Screenshot (382)](https://user-images.githubusercontent.com/101451924/206850571-bf482043-0268-4be5-9201-b3ce7a1cab8c.png)

SELECT c.cityname , COUNT(p.city)
FROM personal p INNER JOIN city c
ON p.city = c.cid
GROUP BY city                 -- we apply condition on that result which we obtained from GROUP BY
HAVING COUNT(p.city) > 3 ;    -- Name of city where no. of students grater than 3.

```

## SubQuery Or Nested Query (Query inside a query)

![Screenshot (383)](https://user-images.githubusercontent.com/101451924/206851702-b599645f-a544-41e0-a25e-6e4b8e1a529d.png)

![Screenshot (384)](https://user-images.githubusercontent.com/101451924/206851707-8832bba9-dc7d-43bf-8309-560d584c5a7d.png)

```sql
SELECT name FROM Personal
WHERE courses = (SELECT  course_id FROM courses WHERE course_name="B");
```

## EXISTS And NOT EXISTS

![Screenshot (385)](https://user-images.githubusercontent.com/101451924/206853038-1fb783c0-3567-40c5-9763-8fa3a6d97a3a.png)

![Screenshot (386)](https://user-images.githubusercontent.com/101451924/206853062-4fa8da72-0391-470a-8ff1-98abbb990222.png)
 

```sql
SELECT name FROM Personal
WHERE EXISTS (SELECT  course_id FROM courses WHERE course_name="BCA");

-----------------------------------------
SELECT name FROM Personal
WHERE NOT EXISTS (SELECT  course_id FROM courses WHERE course_name="B.Com");

```

## UNION & UNION ALL

![Screenshot (388)](https://user-images.githubusercontent.com/101451924/206853886-e387404c-3fc1-4d67-93bd-f115e0263d2b.png)

![Screenshot (390)](https://user-images.githubusercontent.com/101451924/206853889-50ad57c0-7ea5-435b-b875-e1a49fc03370.png)

## IF & CASE Statment

### IF Statment
```bash
![Screenshot (394)](https://user-images.githubusercontent.com/101451924/206868997-1cba05dd-a092-496a-8b5a-d3bfd8a5a2b6.png)

![Screenshot (395)](https://user-images.githubusercontent.com/101451924/206869004-c5666aaa-022f-4677-baec-ef7686ea7fb5.png)

```
### Add a column of percentage in students table
```sql
ALTER TABLE `college`.`students` 
ADD COLUMN `percentage` VARCHAR(45) NOT NULL AFTER `gender`;

### Now add value in that column

UPDATE `college`.`students` SET `percentage` = '45' WHERE (`id` = '1');
UPDATE `college`.`students` SET `percentage` = '85' WHERE (`id` = '2');
UPDATE `college`.`students` SET `percentage` = '29' WHERE (`id` = '3');
UPDATE `college`.`students` SET `percentage` = '47' WHERE (`id` = '4');
UPDATE `college`.`students` SET `percentage` = '23' WHERE (`id` = '5');
UPDATE `college`.`students` SET `percentage` = '45' WHERE (`id` = '6');


### The Query Time!!

SELECT Id , name , percentage ,
IF(percentage >= 33 ,"pass" , "fail") AS Result
FROM students;

### CASE Statment
-----------------
![Screenshot (396)](https://user-images.githubusercontent.com/101451924/206887539-af596aeb-aee4-47c0-9c41-132d46a54ed9.png)
![Screenshot (397)](https://user-images.githubusercontent.com/101451924/206887544-ce375c36-510b-442b-ad05-6101967e13e9.png)

SELECT Id , name , percentage ,
CASE 
   WHEN percentage >= 80 AND percentage <= 100 THEN "Merit"
   WHEN percentage >= 60 AND percentage < 80 THEN "Ist Division"
   WHEN percentage >= 45 AND percentage < 60 THEN "IInd Division"
   WHEN percentage >= 33 AND percentage < 45 THEN "IIIrd Division"
   WHEN percentage < 33 THEN "Fail"
   ELSE "Invalid %"
END AS Grade
FROM students;


### Updating multiple records at the same time

UPDATE students SET 
percentage = (
CASE id 
		WHEN 3 THEN 64     -- when id = 3 set % = 64 
        WHEN 6 THEN 120    -- when id = 7 set % = 120
END
)
WHERE id IN (3 , 6);    

```


## MySQL Arithmetic Functions


![Screenshot (398)](https://user-images.githubusercontent.com/101451924/206889261-92bfed5c-a30a-4330-a97a-ecee585169fb.png)

![Screenshot (399)](https://user-images.githubusercontent.com/101451924/206889264-d6b97613-a0bb-467c-a35b-377fc9177e48.png)

![Screenshot (400)](https://user-images.githubusercontent.com/101451924/206889265-2bc368ec-580e-4957-b1eb-801bd0095627.png)

![Screenshot (401)](https://user-images.githubusercontent.com/101451924/206889266-a4bc09cf-cea0-4086-ab11-b06e5ab2a5b2.png)

![Screenshot (403)](https://user-images.githubusercontent.com/101451924/206889270-ce1edee8-d447-466b-988f-c608a45080f5.png)

```sql

SELECT id , name , (percentage+5)  AS 'NEW %'
FROM students;


### Some examples 

SELECT PI() ;           -- 3.141593

SELECT ROUND(4.51) ;    -- 5
SELECT ROUND(4.49) ;    -- 4
SELECT ROUND(-4.49) ;   --  -4
SELECT ROUND(-4.51) ;   --  -5
SELECT ROUND(1234.987); -- 1235
SELECT ROUND(1234.987,2); -- 1234.99

SELECT CEIL(1.36);   --  2
SELECT CEIL(1,56);   --  2

SELECT FLOOR(4.40)   --  4
SELECT FLOOR(4.90)   --  4

SELECT POW(2,2)   --  4
SELECT POW(2,3)   --  8

SELECT SQRT(16)   --  4
SELECT SQRT(5)    --  2.23606797749979
SELECT ROUND(SQRT(5))  --2

SELECT RAND()        -- Produces a random no. B/W 0-1 each time we execute the function (with decimal value)
SELECT RAND() *100  -- Produces a random no. B/W 1-100 each time we execute(with Decimal Value) 
SELECT ROUND(RAND()*100)    -- Produces a random no. B/W 1-100 each time we execute(without Decimal Value) 
SELECT FLOOR(1+ (RAND()*5))    -- Produces a random no. B/W 1-5 each time we execute(without Decimal Value) 

SELECT id , name , percentage     -- each time we execute the code it the result in different order
FROM students ORDER BY RAND();
```

# String Functions
```sql
![Screenshot (404)](https://user-images.githubusercontent.com/101451924/207106831-c9204e3a-d0c1-47b2-932b-94053a12a870.png)

![Screenshot (405)](https://user-images.githubusercontent.com/101451924/207106852-9f3c646b-16d4-4361-af9d-84fc74e38d3c.png)

![Screenshot (406)](https://user-images.githubusercontent.com/101451924/207106887-a41e9680-adb0-4117-bf8b-80d768baf14f.png)

![Screenshot (407)](https://user-images.githubusercontent.com/101451924/207106903-1ef44546-891c-4317-99fb-f476bddfb004.png)

![Screenshot (408)](https://user-images.githubusercontent.com/101451924/207106918-4de40c1a-dd09-4561-b856-44de5a48a37d.png)

![Screenshot (409)](https://user-images.githubusercontent.com/101451924/207106938-e94cf168-17b0-4fca-a470-d8146f55c698.png)

![Screenshot (410)](https://user-images.githubusercontent.com/101451924/207106954-5617e3f2-aebd-4d34-8af3-5ae7a1908e3a.png)

![Screenshot (411)](https://user-images.githubusercontent.com/101451924/207106973-861927ab-610a-4732-824f-622fd203459b.png)

![Screenshot (412)](https://user-images.githubusercontent.com/101451924/207107242-18866f72-171a-4c26-9576-ce0ecd4e2cd1.png)

![Screenshot (413)](https://user-images.githubusercontent.com/101451924/207107258-5bdc2746-bcb2-41ed-a8a0-40e861458a52.png)

![Screenshot (414)](https://user-images.githubusercontent.com/101451924/207107276-bf82d636-ad82-43ea-b439-a6a18dde9695.png)

![Screenshot (415)](https://user-images.githubusercontent.com/101451924/207107284-82f3a6d6-1963-40c6-a0c1-bb80c61a3899.png)

![Screenshot (418)](https://user-images.githubusercontent.com/101451924/207107321-a4a85492-7498-4f72-a0fc-947be8fcb698.png)

![Screenshot (419)](https://user-images.githubusercontent.com/101451924/207107549-6b1bf3ca-3a7a-4699-8c93-520b31a1f264.png)

![Screenshot (420)](https://user-images.githubusercontent.com/101451924/207107559-b628c39b-adeb-4ee4-8445-439a084b4471.png)

![Screenshot (421)](https://user-images.githubusercontent.com/101451924/207107567-829f964e-2b8d-4aba-bd1f-243263f6e728.png)

![Screenshot (422)](https://user-images.githubusercontent.com/101451924/207107575-6ec9f1db-e822-4cbe-bfec-74d781f731dc.png)

![Screenshot (423)](https://user-images.githubusercontent.com/101451924/207107591-36bde67f-47a7-4bd3-9df7-c474b3f41495.png)

![Screenshot (424)](https://user-images.githubusercontent.com/101451924/207107601-1cc3eb3f-ecac-4079-81be-3edaaa2ecc72.png)

![Screenshot (425)](https://user-images.githubusercontent.com/101451924/207107620-08710b51-534f-459c-8a7d-8509d8c0128e.png)

![Screenshot (426)](https://user-images.githubusercontent.com/101451924/207107646-7aba010d-7bc7-4155-b390-ba01c468c855.png)

![Screenshot (427)](https://user-images.githubusercontent.com/101451924/207107669-776224fd-f6c1-4b60-a886-d0557d338625.png)

![Screenshot (428)](https://user-images.githubusercontent.com/101451924/207107689-0ddb442e-129e-4833-9270-f2ba43291adc.png)

![Screenshot (429)](https://user-images.githubusercontent.com/101451924/207107953-b5c96710-7a84-4c36-ad81-6a48ba382bd1.png)

![Screenshot (430)](https://user-images.githubusercontent.com/101451924/207107741-d3c87e7e-04a5-4917-ac3a-cff5fc9ec0de.png)

![Screenshot (431)](https://user-images.githubusercontent.com/101451924/207107758-bca06398-2495-442d-9093-e34d9b792309.png)

```

```sql

```

```sql

```

```sql

```

```sql

```

```sql

```

```sql

```

```sql

```

```sql

```

```sql

```

```sql

```


```sql

```


```sql

```

```sql

```


```sql

```


```sql

```


```sql

```







