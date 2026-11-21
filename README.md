PROJECT DOCUMENTATION
Student Performance & Attendance Analysis
Python Data Analytics Project
Dataset
Dataset Size
Technology
Repository
college_student_performance_100.csv
100 records (6 columns)
Python with 
pandas (no graphs or plotting libraries)
https://github.com/akshitranjanmitra/student-performance-and-student
analysis.git
1. Introduction
Student Performance & Attendance Analysis is a Python-based data analytics project designed to
examine academic scores and attendance for a college student dataset. The project uses
college_student_performance_100.csv containing 100 student records and relies on 
data loading, cleaning, validation, and tabular statistical reporting without graphs.
2. Project Objectives
pandas for
Load and inspect the 100-record student dataset from 
college_student_performance_100.csv .
Clean the data by removing duplicate 
student_id entries, standardizing 
department names, and
handling out-of-range (<0 or >100) or missing numeric values.
Calculate a composite 
final_score from 
math_score , 
science_score , and 
english_score .
Summarize overall student performance using average, highest, and lowest final scores along with
mean attendance percentage.
Evaluate grades (
A+ , A, B, C, 
Fail ) and attendance eligibility status (<75% flagged as 
Attendance! ) for the first 10 students.
Classify overall cohort performance as 
GOOD (average ≥60) or 
Low
NEEDS IMPROVEMENT (average
<60).
3. Tools and Technologies
Programming language: Python 3.9+
Data analysis library: 
pandas
Input format: CSV (
college_student_performance_100.csv )
Source repository: 
analysis.git
https://github.com/akshitranjanmitra/student-performance-and-student
Visualization policy: Text and table outputs only (no graphs or chart libraries)
Student Performance & Attendance Analysis — Project Documentation
Page 1 of 3
4. Dataset Description
The dataset 
college_student_performance_100.csv contains 100 records (
STU101
STU200 )
across four departments (Computer Science, Electronics, Mechanical, Commerce), including 2
missing values in 
attendance_pct and 2 missing values in 
science_score .
Field
student_id
department
attendance_pct
math_score
science_score
Purpose and Validation in Analysis
Unique student identifier used when deduplicating records and printing student report
cards.
Academic department normalized with
.astype(str).str.strip().str.title() .
Class attendance percentage; checked against 0–100 bounds, mean-imputed for
missing values, and evaluated against the 75.0% threshold.
final_score .
Mathematics exam score (0–100); validated, mean-imputed if missing, and averaged
into 
Science exam score (0–100); validated, mean-imputed if missing, and averaged into
final_score .
english_score
English exam score (0–100); validated, mean-imputed if missing, and averaged into
final_score .
5. Data Loading and Preprocessing
The script loads 
college_student_performance_100.csv via
pd.read_csv("college_student_performance_100.csv") , displays the initial row count and
preview rows, removes duplicate 
student_id entries with a reset index, and standardizes
department labels.
6. Data Cleaning and Handling Missing Values
Values below 0 or above 
100 in 
attendance_pct , 
english_score are set to 
None (
math_score , 
science_score , and
NaN ). Missing numeric entries are then filled using column means
(d
f.fillna(df.mean(numeric_only=True)) ), and 
final_score is computed as the 3-subject
average rounded to 2 decimal places.
7. Student Performance Analysis, Grade Calculation & Attendance Evaluation
Using a 
while loop over 
final_score , the script computes the cohort average (
(10
0.0 ), and lowest (
55.43 ) scores alongside average attendance (
77.57 ), highest
77.64% ). A 
for loop over the
first 10 students assigns grades (
A+ : ≥90, A: ≥75, B: ≥60, C: ≥40, 
Fail : <40) and attendance flags
(<75% as 
Low Attendance! ), concluding with 
Overall Performance: GOOD .
Student Performance & Attendance Analysis — Project Documentation
Page 2 of 3
import pandas as pd
df = pd.read_csv("college_student_performance_100.csv")
df = df.drop_duplicates(subset=["student_id"]).reset_index(drop=True)
df["department"] = df["department"].astype(str).str.strip().str.title()
for col in ["attendance_pct", "math_score", "science_score", "english_score"]:
df.loc[(df[col] < 0) | (df[col] > 100), col] = None
df = df.fillna(df.mean(numeric_only=True))
df["final_score"] = df[["math_score", "science_score", 
"english_score"]].mean(axis=1).round(2)
marks_list = df["final_score"].tolist()
attendance_list = df["attendance_pct"].tolist()
total = 0
i = 0
while i < len(marks_list):
total = total + marks_list[i]
i = i + 1
average = total / len(marks_list)
print(f"Average Final Score: {average:.2f} | Highest: {max(marks_list)} | Lowest: 
{min(marks_list)}")
print(f"Average Attendance : {sum(attendance_list) / len(attendance_list):.2f}%")
print("Overall Performance: GOOD" if average >= 60 else "Overall Performance: NEEDS 
IMPROVEMENT")
Student Performance & Attendance Analysis — Project Documentation
Page 3 of 3
