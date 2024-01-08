Assignment: Understanding Primary Keys and Foreign Keys in an Election Database
Overview:
In this assignment, you will be working with a database related to an election. You'll apply your knowledge of primary keys and foreign keys by creating tables, manipulating data, and establishing relationships between them.

Tasks:
# 1. CREATE TABLE with PRIMARY KEY:

Create a table named Candidates with the following columns:
candidate_id (INTEGER) as the primary key
name (TEXT)
party_affiliation (TEXT)
position (TEXT)
# 2. DROP PRIMARY KEY:

Remove the primary key constraint from the Candidates table (if it exists).
# 3. ADD PRIMARY KEY:

Add a primary key constraint to the Candidates table on the candidate_id column.
# 4. COMPOSITE PRIMARY KEY:

Create a table named Votes with the following columns:
voter_id (INTEGER)
candidate_id (INTEGER)
Make a composite primary key using both voter_id and candidate_id.
# 5. FOREIGN KEY:

Alter the Votes table to add a foreign key constraint to reference the Candidates table's candidate_id column.
# 6. CREATE TABLE with FOREIGN KEY:

Create a table named Voters with the following columns:
voter_id (INTEGER) as the primary key
name (TEXT)
age (INTEGER)
voted_for (INTEGER) as a foreign key referencing candidate_id in the Candidates table.
# 7. DROP FOREIGN KEY:

Remove the foreign key constraint from the Voters table (if it exists).
# 8. ADD FOREIGN KEY:

Add a foreign key constraint to the Voters table referencing the candidate_id column in the Candidates table.
# Data Manipulation:
## Populate the Candidates table with at least 5 records of hypothetical candidates and their respective party affiliations and positions.
## Insert data into the Voters table with at least 10 records containing names, ages, and candidates they voted for.
## Manipulate the data to perform queries like finding candidates' details, voters who voted for a specific candidate, etc.





mysql> CREATE DATABASE pf_exercise3;
Query OK, 1 row affected (0,02 sec)

mysql> USE pf_exercise3;
Database changed
mysql> CREATE TABLE Candidates (candidate_id INT PRIMARY KEY, name VARCHAR(100), party_affiliation VARCHAR(100), position VARCHAR(100));
Query OK, 0 rows affected (0,03 sec)

mysql> ALTER TABLE Candidates DROP PRIMARY KEY;
Query OK, 0 rows affected (0,04 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> ALTER TABLE Candidates ADD PRIMARY KEY (candidate_id);
Query OK, 0 rows affected (0,03 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> CREATE TABLE Votes (voter_id INT, candidate_id INT);
Query OK, 0 rows affected (0,02 sec)

mysql> ALTER TABLE Votes ADD PRIMARY KEY (voter_id, candidate_id);
Query OK, 0 rows affected (0,03 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> ALTER TABLE Votes ADD CONSTRAINT fk_candidate_id FOREIGN KEY (candidate_id) REFERENCES Candidates(candidate_id);
Query OK, 0 rows affected (0,04 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> CREATE TABLE Voters (voter_id INT PRIMARY KEY, name VARCHAR(100), age INT, voted_for INT, FOREIGN KEY (voted_for) REFERENCES Candidates (candidate_id));
Query OK, 0 rows affected (0,03 sec)

mysql> SHOW CREATE TABLE Voters;
+--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Table  | Create Table                                                                                                                                                                                                                                                                                                                                                                     |
+--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Voters | CREATE TABLE `Voters` (
  `voter_id` int NOT NULL,
  `name` varchar(100) DEFAULT NULL,
  `age` int DEFAULT NULL,
  `voted_for` int DEFAULT NULL,
  PRIMARY KEY (`voter_id`),
  KEY `voted_for` (`voted_for`),
  CONSTRAINT `Voters_ibfk_1` FOREIGN KEY (`voted_for`) REFERENCES `Candidates` (`candidate_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci |
+--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0,00 sec)

mysql> ALTER TABLE Voters DROP FOREIGN KEY Voters_ibfk_1;
Query OK, 0 rows affected (0,02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> ALTER TABLE Voters ADD CONSTRAINT fk_voted_for FOREIGN KEY (voted_for) REFERENCES Candidates(candidate_id);
Query OK, 0 rows affected (0,04 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> INSERT INTO Candidates (candidate_id, name, party_affiliation, position)
    -> VALUES
    -> (1, 'John Doe', 'Independent', 'Mayor'),
    -> (2, 'Jane Smith', 'Green Party', 'Councilor'),
    -> (3, 'Alice Johnson', 'Democratic Party', 'Senator'),
    -> (4, 'Robert Williams', 'Republican Party', 'Governor'),
    -> (5, 'Emily Brown', 'Libertarian Party', 'Congressperson');
Query OK, 5 rows affected (0,00 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> INSERT INTO Voters (voter_id, name, age, voted_for)
    -> VALUES
    -> (1, 'Michael Adams', 28, 2),
    -> (2, 'Sarah Clark', 35, 4),
    -> (3, 'David Lee', 42, 3),
    -> (4, 'Emma Garcia', 31, 1),
    -> (5, 'Olivia Rodriguez', 26, 2),
    -> (6, 'William Martinez', 39, 5),
    -> (7, 'Sophia Hernandez', 45, 3),
    -> (8, 'Daniel Nguyen', 29, 4),
    -> (9, 'Ava Kim', 33, 1),
    -> (10, 'James Jackson', 37, 5);
Query OK, 10 rows affected (0,01 sec)
Records: 10  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM Candidates;
+--------------+-----------------+-------------------+----------------+
| candidate_id | name            | party_affiliation | position       |
+--------------+-----------------+-------------------+----------------+
|            1 | John Doe        | Independent       | Mayor          |
|            2 | Jane Smith      | Green Party       | Councilor      |
|            3 | Alice Johnson   | Democratic Party  | Senator        |
|            4 | Robert Williams | Republican Party  | Governor       |
|            5 | Emily Brown     | Libertarian Party | Congressperson |
+--------------+-----------------+-------------------+----------------+
5 rows in set (0,00 sec)

mysql> SELECT * FROM Voters;
+----------+------------------+------+-----------+
| voter_id | name             | age  | voted_for |
+----------+------------------+------+-----------+
|        1 | Michael Adams    |   28 |         2 |
|        2 | Sarah Clark      |   35 |         4 |
|        3 | David Lee        |   42 |         3 |
|        4 | Emma Garcia      |   31 |         1 |
|        5 | Olivia Rodriguez |   26 |         2 |
|        6 | William Martinez |   39 |         5 |
|        7 | Sophia Hernandez |   45 |         3 |
|        8 | Daniel Nguyen    |   29 |         4 |
|        9 | Ava Kim          |   33 |         1 |
|       10 | James Jackson    |   37 |         5 |
+----------+------------------+------+-----------+
10 rows in set (0,00 sec)

mysql> SELECT * FROM Voters WHERE voted_for = 3;
+----------+------------------+------+-----------+
| voter_id | name             | age  | voted_for |
+----------+------------------+------+-----------+
|        3 | David Lee        |   42 |         3 |
|        7 | Sophia Hernandez |   45 |         3 |
+----------+------------------+------+-----------+
2 rows in set (0,00 sec)

mysql> SELECT * FROM Voters LEFT JOIN Candidates ON Voters.voter_id = Candidates.candidate_id;
+----------+------------------+------+-----------+--------------+-----------------+-------------------+----------------+
| voter_id | name             | age  | voted_for | candidate_id | name            | party_affiliation | position       |
+----------+------------------+------+-----------+--------------+-----------------+-------------------+----------------+
|        1 | Michael Adams    |   28 |         2 |            1 | John Doe        | Independent       | Mayor          |
|        2 | Sarah Clark      |   35 |         4 |            2 | Jane Smith      | Green Party       | Councilor      |
|        3 | David Lee        |   42 |         3 |            3 | Alice Johnson   | Democratic Party  | Senator        |
|        4 | Emma Garcia      |   31 |         1 |            4 | Robert Williams | Republican Party  | Governor       |
|        5 | Olivia Rodriguez |   26 |         2 |            5 | Emily Brown     | Libertarian Party | Congressperson |
|        6 | William Martinez |   39 |         5 |         NULL | NULL            | NULL              | NULL           |
|        7 | Sophia Hernandez |   45 |         3 |         NULL | NULL            | NULL              | NULL           |
|        8 | Daniel Nguyen    |   29 |         4 |         NULL | NULL            | NULL              | NULL           |
|        9 | Ava Kim          |   33 |         1 |         NULL | NULL            | NULL              | NULL           |
|       10 | James Jackson    |   37 |         5 |         NULL | NULL            | NULL              | NULL           |
+----------+------------------+------+-----------+--------------+-----------------+-------------------+----------------+
10 rows in set (0,00 sec)

mysql> SELECT * FROM Voters RIGHT JOIN Candidates ON Voters.voter_id = Candidates.candidate_id;
+----------+------------------+------+-----------+--------------+-----------------+-------------------+----------------+
| voter_id | name             | age  | voted_for | candidate_id | name            | party_affiliation | position       |
+----------+------------------+------+-----------+--------------+-----------------+-------------------+----------------+
|        1 | Michael Adams    |   28 |         2 |            1 | John Doe        | Independent       | Mayor          |
|        2 | Sarah Clark      |   35 |         4 |            2 | Jane Smith      | Green Party       | Councilor      |
|        3 | David Lee        |   42 |         3 |            3 | Alice Johnson   | Democratic Party  | Senator        |
|        4 | Emma Garcia      |   31 |         1 |            4 | Robert Williams | Republican Party  | Governor       |
|        5 | Olivia Rodriguez |   26 |         2 |            5 | Emily Brown     | Libertarian Party | Congressperson |
+----------+------------------+------+-----------+--------------+-----------------+-------------------+----------------+
5 rows in set (0,00 sec)

mysql> SELECT name, voted_for FROM Voters WHERE voted_for = 4;
+---------------+-----------+
| name          | voted_for |
+---------------+-----------+
| Sarah Clark   |         4 |
| Daniel Nguyen |         4 |
+---------------+-----------+
2 rows in set (0,00 sec)

mysql> SELECT * FROM Voters LEFT JOIN Candidates On Voters.voted_for = Candidates.candidate_id;
+----------+------------------+------+-----------+--------------+-----------------+-------------------+----------------+
| voter_id | name             | age  | voted_for | candidate_id | name            | party_affiliation | position       |
+----------+------------------+------+-----------+--------------+-----------------+-------------------+----------------+
|        1 | Michael Adams    |   28 |         2 |            2 | Jane Smith      | Green Party       | Councilor      |
|        2 | Sarah Clark      |   35 |         4 |            4 | Robert Williams | Republican Party  | Governor       |
|        3 | David Lee        |   42 |         3 |            3 | Alice Johnson   | Democratic Party  | Senator        |
|        4 | Emma Garcia      |   31 |         1 |            1 | John Doe        | Independent       | Mayor          |
|        5 | Olivia Rodriguez |   26 |         2 |            2 | Jane Smith      | Green Party       | Councilor      |
|        6 | William Martinez |   39 |         5 |            5 | Emily Brown     | Libertarian Party | Congressperson |
|        7 | Sophia Hernandez |   45 |         3 |            3 | Alice Johnson   | Democratic Party  | Senator        |
|        8 | Daniel Nguyen    |   29 |         4 |            4 | Robert Williams | Republican Party  | Governor       |
|        9 | Ava Kim          |   33 |         1 |            1 | John Doe        | Independent       | Mayor          |
|       10 | James Jackson    |   37 |         5 |            5 | Emily Brown     | Libertarian Party | Congressperson |
+----------+------------------+------+-----------+--------------+-----------------+-------------------+----------------+
10 rows in set (0,00 sec)
