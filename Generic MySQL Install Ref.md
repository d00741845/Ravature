# Generic Install Ref: MySQL & MySQL Workbench

## Verify Current Version:
```bash
mysql -V
```

## Install MySQL:
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install mysql-server
sudo service mysql status
```

## Configureing Users:
```bash
sudo mysql
```
```sql
SELECT User, Host FROM mysql.user;
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'pa$$word';
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'newpassword';
GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';
FLUSH PRIVILEGES;

SELECT User, Host FROM mysql.user;

SHOW GRANTS FOR 'someuser'@'localhost';

REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'someuser'@'localhost';

DROP USER 'someuser'@'localhost';
exit;
```

## Login
```bash
mysql -u root -p
```
```sql
show databases;
exit;
```

## Configureing Database
```bash
mysql -u newuser -p
```
```sql
show databases;
CREATE DATABASE new_db;
DROP DATABASE someDataBase;
USE new_db;
exit;
```

## Configureing Table
```bash
mysql -u someuser -p
```
```sql
CREATE TABLE new_table(
id INT AUTO_INCREMENT,
   first_name VARCHAR(100),
   last_name VARCHAR(100),
   age int;
   is_admin TINYINT(1),
   registration_date DATETIME,
   PRIMARY KEY(id)
);
DROP TABLE some_table_name;
SHOW TABLES;
exit;
```


## Table Data
```sql
INSERT INTO some_table_name (first_name, last_name, age, is_admin, registration_date) 
values ('Jesse', 'Fore', 'service.awg@gmail.com', '22', 1, now());

INSERT INTO some_table_name (first_name, last_name, age, is_admin, registration_date) 
values ('Josh', 'Wadford', 'jw@att.net', '36', 1, now()),
('Donald', 'Trump', 'trump@gmail.com', '55', 0, now()),
('Bill', 'Clinton', 'service@gmail.com', '66', 0, now());
);

SELECT * FROM some_table;
SELECT first_name, last_name FROM some_table;

SELECT * FROM some_table WHERE first_name='Jesse';
SELECT * FROM some_table WHERE first_name='Jesse' AND age=22;
SELECT * FROM some_table WHERE is_admin = 1;
SELECT * FROM some_table WHERE is_admin > 0;

DELETE FROM some_table WHERE id = 6;

UPDATE some_table SET email = 'newmail@gmail.com' WHERE id = 2;

ALTER TABLE some_table ADD childAge VARCHAR(3);

ALTER TABLE some_table MODIFY COLUMN age INT(3);

SELECT * FROM some_table ORDER BY last_name ASC;
SELECT * FROM some_table ORDER BY last_name DESC;

SELECT CONCAT(first_name, ' ', last_name) AS 'Name', age FROM some_table;

SELECT DISTINCT email FROM some_table;

SELECT * FROM some_table WHERE age BETWEEN 20 AND 25;

SELECT * FROM some_table WHERE email LIKE 's%';
SELECT * FROM some_table WHERE email LIKE 'ser%';
SELECT * FROM some_table WHERE email LIKE '%m';
SELECT * FROM some_table WHERE email LIKE '%awg%';

SELECT * FROM some_table WHERE email NOT LIKE 'ser%';

SELECT * FROM some_table WHERE email IN ('s%', '%net');

CREATE INDEX newIndex On some_table(location);
DROP INDEX newIndex ON some_table;

```

## Table Data Forign key
```sql
CREATE TABLE tweet(
id INT AUTO_INCREMENT,
   userId INT,
   title VARCHAR(100),
   body TEXT,
   publish_date DATETIME DEFAULT CURRENT_TIMESTAMP,
   PRIMARY KEY(id),
   FOREIGN KEY (user_id) REFERENCES some_table(id)
);

INSERT INTO tweet(user_id, title, body) 
VALUES (1, 'Tweet One', 'This is tweet 1'),
(3, 'Tweet Two', 'This is tweet 2'),
(1, 'Tweet Three', 'This is tweet 3'),
(2, 'Tweet Four', 'This is tweet 4'),
(5, 'Tweet Five', 'This is tweet 5'),
(4, 'Tweet Six', 'This is tweet 6'),
(2, 'Tweet Seven', 'This is tweet 7'),
(1, 'Tweet Eight', 'This is tweet 8'),
(3, 'Tweet Nine', 'This is tweet 9'),
(4, 'Tweet Ten', 'This is tweet 10');

```

## INNER JOIN

```sql
SELECT
  some_table.first_name,
  some_table.last_name,
  tweet.title,
  tweet.publish_date
FROM some_table
INNER JOIN tweet
ON some_table.id = tweet.user_id
ORDER BY tweet.title;
```

## New Table With 2 Foriegn Keys

```sql
CREATE TABLE comments(
	id INT AUTO_INCREMENT,
    tweet INT,
    some_table_id INT,
    body TEXT,
    publish_date DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY(id),
    FOREIGN KEY(some_table_id) references some_table(id),
    FOREIGN KEY(tweet_id) references tweet(id)
);
```

## Add Data to Comments Table

```sql
INSERT INTO comments(tweet_id, some_table_id, body) 
VALUES (1, 3, 'This is comment one'),
(2, 1, 'This is comment two'),
(5, 3, 'This is comment three'),
(2, 4, 'This is comment four'),
(1, 2, 'This is comment five'),
(3, 1, 'This is comment six'),
(3, 2, 'This is comment six'),
(5, 4, 'This is comment seven'),
(2, 3, 'This is comment seven');
```

## Left Join

```sql
SELECT
comments.body,
tweet.title
FROM comments
LEFT JOIN tweet ON tweet.id = comments.tweet_id
ORDER BY tweet.title;

```

## Join Multiple Tables

```sql
SELECT
comments.body,
tweey.title,
some_table.first_name,
some_table.last_name
FROM comments
INNER JOIN tweet on posts.id = comments.tweet_id
INNER JOIN users on some_table.id = comments.some_table_id
ORDER BY tweey.title;

```

## Aggregate Functions

```sql
SELECT COUNT(id) FROM someTable;
SELECT MAX(age) FROM someTable;
SELECT MIN(age) FROM someTable;
SELECT SUM(age) FROM someTable;
SELECT UCASE(first_name), LCASE(last_name) FROM someTable;

```

## Group By

```sql
SELECT age, COUNT(age) FROM someTable GROUP BY age;
SELECT age, COUNT(age) FROM someTable WHERE age > 18 GROUP BY age;
SELECT age, COUNT(age) FROM someTable GROUP BY age HAVING count(age) >=2;

```


## Install MySQL Wrokbench:
```bash
sudo apt-get install mysql-workbench
```


## Referece:
https://stackoverflow.com/questions/52584176/linux-mint-mysql-server-and-mysql-workbench-installation-and-setup-issue

