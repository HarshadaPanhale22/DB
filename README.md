3.  Design and develop SQL queries for any suitable database application using SQL DML statements
   
    -- Step 1: Create a Database
CREATE DATABASE InstituteDB;

-- Step 2: Use the Database
USE InstituteDB;

-- Step 3: Create a Table
CREATE TABLE StudentRecord (
    Student_ID INT PRIMARY KEY,
    Name VARCHAR(50),
    Course VARCHAR(50),
    Marks INT
);

-- Step 4: Insert Records (INSERT Command)
INSERT INTO StudentRecord (Student_ID, Name, Course, Marks)
VALUES 
(1, 'Amit', 'Computer Science', 85),
(2, 'Priya', 'Information Tech', 78),
(3, 'Rahul', 'Computer Science', 90),
(4, 'Harshada', 'Electronics', 88);

-- Step 5: Display All Records (SELECT Command)
SELECT * FROM StudentRecord;

-- Step 6: Update Record (Change Marks)
UPDATE StudentRecord
SET Marks = 95
WHERE Student_ID = 3;

-- Step 7: Change Name (UPDATE Command)
UPDATE StudentRecord
SET Name = 'Rohit'
WHERE Student_ID = 1;

-- Step 8: Delete a Record (DELETE Command)
DELETE FROM StudentRecord
WHERE Student_ID = 2;

-- Step 9: Display Final Records
SELECT * FROM StudentRecord;

-- Step 10: Display Students with Marks greater than 70
SELECT * FROM StudentRecord WHERE Marks > 70;

-- Step 11: Sort students by Marks in descending order (highest first)
SELECT * FROM StudentRecord
ORDER BY Marks DESC;

-- Step 12: Sort only student names by Marks in descending order
SELECT Name FROM StudentRecord
ORDER BY Marks DESC;



4.
