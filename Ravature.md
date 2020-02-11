# Ravature

## Instructions: One-To-Many Relationships
> Creat two tables supporting a one-to-many relationship.
>
> Create tables to represent a link between Students and their Pets. We can set that up with two tables as such
>
>Students Table

## One-To-Many Relationships

```sql
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
	classId	INT,
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

INSERT INTO classes (classId, className, shortName) 
values (101, 'Chemistry 101', 'CHEM101'),
(102, 'Calculus 101', 'MATH101'),
(103, 'Biology 101', 'BIO101'),
(104, 'English 102', 'ENG102');

```
## Instructions: DDL - Data Definition Language
> Create, alter and drop a table in a database.
>
> Practice using DDL commands to manage data structures within our database..

## DDL - Data Definition Language

```sql
DROP DATABASE IF EXISTS `Revature_DB`;
CREATE DATABASE `Revature_DB`;
USE `Revature_DB`;

DROP TABLE IF EXISTS Students;
CREATE TABLE Students(
  firstname varchar(30),
  lastname varchar(30),
  age integer
);

alter table Students add column middlename varchar(30);

drop table Students;

```

