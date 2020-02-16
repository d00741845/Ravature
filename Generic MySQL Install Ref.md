# Generic Install & Ref: MySQL & Workbench

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

### Configuring SQL User(s):
```bash
sudo mysql
```
```sql
SELECT User, Host FROM mysql.user;
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'pa$$word';
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'newpa$$word';
GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';
FLUSH PRIVILEGES;

SELECT User, Host FROM mysql.user;
SHOW GRANTS FOR 'newuser'@'localhost';

REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'someuser'@'localhost';

DROP USER 'someuser'@'localhost';
exit;
```

### SQL Root Login 
```bash
mysql -u root -p
```
```sql
show databases;
exit;
```

### SQL User Login & Configure Database: 
```bash
mysql -u newuser -p
```
```sql
show databases;
CREATE DATABASE newDatabase;
DROP DATABASE someDatabase;
USE newDatabase;
exit;
```

## SQL User Login & Configuring Table
```bash
mysql -u someuser -p
```
```sql
DROP DATABASE IF EXISTS newDatabase;
CREATE DATABASE newDatabase;
USE newDatabase;

DROP TABLE IF EXISTS someTable;
CREATE TABLE someTable(
id INT AUTO_INCREMENT,
   firstName VARCHAR(100),
   lastName VARCHAR(100),
   email VARCHAR(150),
   age int,
   isAdmin TINYINT(1),
   registrationDate DATETIME,
   PRIMARY KEY(id)
);
SHOW TABLES;

INSERT INTO someTable (firstName, lastName, email, age, isAdmin, registrationDate) 
values ('Jesse', 'Fore', 'service.awg@gmail.com', '22', 1, now());

INSERT INTO someTable (firstName, lastName, email, age, isAdmin, registrationDate) 
values ('Josh', 'Wadford', 'jw@att.net', '36', 1, now()),
('Donald', 'Trump', 'trump@gmail.com', '55', 0, now()),
('Bill', 'Clinton', 'service@gmail.com', '66', 0, now());

SELECT * FROM someTable;
SELECT firstName, lastName FROM someTable;

SELECT * FROM someTable WHERE firstName='Jesse';
SELECT * FROM someTable WHERE firstName='Jesse' AND age=22;
SELECT * FROM someTable WHERE isAdmin = 1;
SELECT * FROM someTable WHERE isAdmin > 0;

DELETE FROM someTable WHERE id = 6;

UPDATE someTable SET email = 'newmail@gmail.com' WHERE id = 2;

ALTER TABLE someTable ADD childAge VARCHAR(3);

ALTER TABLE someTable MODIFY COLUMN age INT(3);

SELECT * FROM someTable ORDER BY lastName ASC;
SELECT * FROM someTable ORDER BY lastName DESC;

SELECT CONCAT(firstName, ' ', lastName) AS 'Name', age FROM someTable;

SELECT DISTINCT email FROM someTable;

SELECT * FROM someTable WHERE age BETWEEN 20 AND 25;
SELECT * FROM someTable WHERE email LIKE 's%';
SELECT * FROM someTable WHERE email LIKE 'ser%';
SELECT * FROM someTable WHERE email LIKE '%m';
SELECT * FROM someTable WHERE email LIKE '%awg%';
SELECT * FROM someTable WHERE email NOT LIKE 'ser%';
SELECT * FROM someTable WHERE email IN ('s%', '%net');

CREATE INDEX newIndex On someTable(email);
DROP INDEX newIndex ON someTable;
```
---
# Examples:
### Example: Configure Table Data with Foreign key
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

### Example: INNER JOIN
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

### Example: New Table With 2 Foriegn Keys
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

### Example: Add Data to Comments Table
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

### Example: Left Join
```sql
SELECT
comments.body,
tweet.title
FROM comments
LEFT JOIN tweet ON tweet.id = comments.tweet_id
ORDER BY tweet.title;
```

### Example: Join Multiple Tables
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

### Example: Aggregate Functions
```sql
SELECT AVG(age) FROM someTable;
SELECT SUM(age) FROM someTable;
SELECT MAX(age) FROM someTable;
SELECT MIN(age) FROM someTable;
SELECT FIRST(age) FROM someTable;
SELECT LAST(age) FROM someTable;
SELECT COUNT(id) FROM someTable;
SELECT UCASE(first_name), LCASE(last_name) FROM someTable;
```

### Example: Group By
```sql
SELECT age, COUNT(age) FROM someTable GROUP BY age;
SELECT age, COUNT(age) FROM someTable WHERE age > 18 GROUP BY age;
SELECT age, COUNT(age) FROM someTable GROUP BY age HAVING count(age) >=2;
```

---
# Install MySQL Workbench:
```bash
sudo apt-get install mysql-workbench
```


# Reference:
https://stackoverflow.com/questions/52584176/linux-mint-mysql-server-and-mysql-workbench-installation-and-setup-issue
