Student Result Management System

# Project Overview

This project is a Student Result Management System built using SQL.
It helps in managing student details, courses, semesters, grades, and calculating GPA based on marks.

The database is designed to handle:

Student Information

Course Details

Semester Records

Grades & GPA Calculation


---

# Database Schema

1. Students Table

Stores student personal information.

CREATE TABLE Students(
   student_id INT AUTO_INCREMENT PRIMARY KEY,
   name VARCHAR(100),
   dob INT,
   department VARCHAR(100)
);

2. Course Table

Stores courses offered with credits.

CREATE TABLE Course(
  course_id INT PRIMARY KEY,
  course_name VARCHAR(100),
  credits INT
);

3. Semesters Table

Stores semester details.

CREATE TABLE Semesters(
  semester_id INT PRIMARY KEY,
  semester_name VARCHAR(100)
);

4. Grades Table

(Assumed from triggers and GPA calculation – to store marks, grade, GPA).

CREATE TABLE Grades(
  grade_id INT AUTO_INCREMENT PRIMARY KEY,
  student_id INT,
  course_id INT,
  semester_id INT,
  marks INT,
  grade VARCHAR(2),
  gpa FLOAT,
  FOREIGN KEY(student_id) REFERENCES Students(student_id),
  FOREIGN KEY(course_id) REFERENCES Course(course_id),
  FOREIGN KEY(semester_id) REFERENCES Semesters(semester_id)
);


---

# Features Implemented

Trigger for Grade Assignment
Automatically assigns grade & GPA based on marks before inserting into Grades.

GPA Calculation Query
Calculates Semester GPA using weighted average of credits.


Example GPA Calculation:

SELECT 
    s.student_id,
    s.name,
    sem.semester_id,
    ROUND(SUM(g.gpa * c.credits) / SUM(c.credits),2) AS Semester_GPA
FROM Grades g
JOIN Students s ON g.student_id = s.student_id
JOIN Course c ON g.course_id = c.course_id
JOIN Semesters sem ON g.semester_id = sem.semester_id
GROUP BY s.student_id, s.name, sem.semester_id;


---

3. Run all the SQL scripts in order:

Create Students, Course, Semesters, and Grades tables.

Add the Trigger for grade calculation.

Insert sample data.

Run GPA calculation queries.



---

# Example Output

Student ID	Name	Semester	GPA

1	Anjali
