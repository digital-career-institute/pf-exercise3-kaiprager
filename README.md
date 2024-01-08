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
