# Ravature

## Instructions: One-To-Many Relationships
> Creat two tables supporting a one-to-many relationship.
>
> Create tables to represent a link between Students and their Pets. We can set that up with two tables as such
>
>Students Table

## One-To-Many Relationships

```sql
SELECT User, Host FROM mysql.user;

DROP DATABASE IF EXISTS `Revature_DB`;
CREATE DATABASE `Revature_DB`;
USE `Revature_DB`;

DROP TABLE IF EXISTS students;
CREATE TABLE students(
	studentId INT AUTO_INCREMENT,
	studentFirstName VARCHAR(50),
	studentLastName VARCHAR(50),
	PRIMARY KEY(studentId)
); 

DROP TABLE IF EXISTS pets;
CREATE TABLE pets(
	petId INT NOT NULL,
	petName VARCHAR(50),
	petType VARCHAR(50),
	studentId INT,
	PRIMARY KEY(petId)
); 

INSERT INTO students (studentFirstName, studentLastName) 
values ('jack', 'stone'),
('brittany', 'jones'),
('Talia', 'morrison'),
('STEVEN', 'smith'),
('kourtney', 'klein');

INSERT INTO pets (petId, petName, petType, studentId) 
values (101, 'fluffy', 'hamster',1),
(102, 'fido', 'dog',2),
(103, 'spot', 'dog',2),
(104, 'princess', 'cat',3),
(105, 'goldie', 'dog',2),
(106, 'roy', 'fish',4),
(107, 'susie', 'cat',3);
```

## Instructions: Many-To-Many Relationships
> Creating two tables that will support a many-to-many relationship.
>
> Create tables to represent a link between Students and their Classes.

## Many-To-Many Relationships

```sql
SELECT User, Host FROM mysql.user;

DROP DATABASE IF EXISTS `Revature_DB`;
CREATE DATABASE `Revature_DB`;
USE `Revature_DB`;

DROP TABLE IF EXISTS students;
CREATE TABLE students(
	studentId INT AUTO_INCREMENT,
	studentFirstName VARCHAR(50),
	studentLastName VARCHAR(50),
	PRIMARY KEY(studentId)
); 

DROP TABLE IF EXISTS classes;
CREATE TABLE classes(
	classId	INT AUTO_INCREMENT,
	className VARCHAR(50),
	shortName VARCHAR(50),
	PRIMARY KEY(classId)
); 

INSERT INTO students (studentFirstName, studentLastName) 
values ('jack', 'stone'),
('brittany', 'jones'),
('Talia', 'morrison'),
('STEVEN', 'smith'),
('kourtney', 'klein');

INSERT INTO classes (className, shortName) 
values ('Chemistry 101', 'CHEM101'),
('Calculus 101', 'MATH101'),
('Biology 101', 'BIO101'),
('English 102', 'ENG102');

```

