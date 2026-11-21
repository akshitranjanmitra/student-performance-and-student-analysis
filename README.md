
PROJECT DOCUMENTATION
Student Performance & Attendance Analysis
Python Data Analytics Project
Dataset
Dataset size stated in
source
Technology
college_student_performance_100.csv
100 records
Python with pandas
Repository
1. Introduction
github.com/akshatv312/hcltrainingstudentperformance
Student Performance & Attendance Analysis is a Python-based data analytics project designed to
examine academic scores and attendance for a college student dataset, maintained at
https://github.com/akshatv312/hcltrainingstudentperformance. The source identifies the input file as
college_student_performance_100.csv and states that it contains 100 records. The project uses
pandas for data handling and analysis without graphical plots.
2. Project Objectives
Load and inspect the student dataset
Clean the data by removing duplicate student records, standardizing department names, and
handling invalid or missing numeric values
Calculate a final score from mathematics, science, and English scores
Summarize student performance using average, highest, and lowest final scores
Evaluate grades and attendance status for the first 10 students
Classify overall performance using the average final score
3. Tools and Technologies
Programming language: Python
Data analysis library: pandas
Input format: CSV (comma-separated values)
Dataset: college_student_performance_100.csv
The supplied source names pandas as the library but does not show a complete environment setup or
package-version specification.
4. Dataset Description
The source identifies a 100-record college student dataset. The code references the following fields:
Student Performance & Attendance Analysis — Project Documentation
Page 1 of 6
Field
student_id
department
attendance_pct
math_score,
science_score,
english_score
Purpose indicated by the source
Student identifier, used when removing duplicate records and displaying report
card entries
Student department, standardized using title case
Attendance percentage, checked against the 0–100 range and 75% threshold
Subject scores checked against 0–100 and averaged to form final_score
5. Data Loading and Preprocessing
The code loads college_student_performance_100.csv with pd.read_csv(), prints --- Original
Dataset ---, Total Rows: {len(df)}, and df.head(), drops duplicate student_id rows (resetting
the index), and cleans department via .astype(str).str.strip().str.title().
# 1. LOAD DATASET
df = pd.read_csv("college_student_performance_100.csv")
print("--- Original Dataset ---")
print(f"Total Rows: {len(df)}")
print(df.head())
# Duplicate & department cleanup
df = df.drop_duplicates(subset=["student_id"]).reset_index(drop=True)
df["department"] = df["department"].astype(str).str.strip().str.title()
6. Data Cleaning and Handling Missing Values
Out-of-range values (< 0 or > 100) in attendance_pct, math_score, science_score, and
english_score are set to None, missing numeric entries are filled with
df.fillna(df.mean(numeric_only=True)), final_score is computed as the row-wise mean of the
three subject scores rounded to 2 decimals, and --- After Cleaning --- with Total Rows:
{len(df)} is printed.
df.loc[(df["attendance_pct"] < 0) | (df["attendance_pct"] > 100), "attendance_pct"] 
= None
df.loc[(df["math_score"] < 0) | (df["math_score"] > 100), "math_score"] = None
df.loc[(df["science_score"] < 0) | (df["science_score"] > 100), "science_score"] = 
None
df.loc[(df["english_score"] < 0) | (df["english_score"] > 100), "english_score"] = 
None
df = df.fillna(df.mean(numeric_only=True))
df["final_score"] = df[["math_score", "science_score", 
"english_score"]].mean(axis=1).round(2)
print("\n--- After Cleaning ---")
print(f"Total Rows: {len(df)}")
Student Performance & Attendance Analysis — Project Documentation
Page 2 of 6
7. Student Performance Analysis
The code converts final_score and attendance_pct to marks_list and attendance_list, sums
marks_list in a while i < len(marks_list) loop to get average, finds highest (max(marks_list))
and lowest (min(marks_list)), and prints Average Final Score, Highest Final Score, Lowest
Final Score, and Average Attendance (sum(attendance_list) / len(attendance_list)).
marks_list = df["final_score"].tolist()
attendance_list = df["attendance_pct"].tolist()
total = 0
i = 0
while i < len(marks_list):
total = total + marks_list[i]
i = i + 1
average = total / len(marks_list)
highest = max(marks_list)
lowest = min(marks_list)
print("\n--- Overall Analysis ---")
print(f"Average Final Score : {average:.2f}")
print(f"Highest Final Score : {highest}")
print(f"Lowest Final Score  : {lowest}")
print(f"Average Attendance  : {sum(attendance_list) / len(attendance_list):.2f}%")
8. Grade Calculation and Attendance Evaluation
A for j in range(10) loop builds the report card for the first 10 rows using
df['student_id'].iloc[j], assigning A+ (>=90), A (>=75), B (>=60), C (>=40), or Fail (<40), setting
status to Low Attendance! when attend < 75 and Good otherwise, and finally printing Overall
Performance: GOOD if average >= 60 or Overall Performance: NEEDS IMPROVEMENT otherwise.
Student Performance & Attendance Analysis — Project Documentation
Page 3 of 6
print()
j  ():
mark = marks_list[j]
attend = attendance_list[j]
mark >= :
grade = 
mark >= :
grade = 
mark >= :
grade = 
mark >= :
grade = 
:
grade = 
status =   attend <   
()
average >= :
()
:
()"\n--- Report Card (First 10 Students) --
"forinrange10if90"A+"elif75"A"elif60"B"elif40"C"else"Fail""Low 
Attendance!"if75else"Good"printf"{df['student_id'].iloc[j]} - Marks: {mark:.1f}, 
Grade: {grade}, Attendance: {attend:.1f}%, {status}"if60print"\nOverall 
Performance: GOOD"elseprint"\nOverall Performance: NEEDS IMPROVEMENT"
Student Performance & Attendance Analysis — Project Documentation
Page 4 of 6
9. Complete Python Source Code
import pandas  pd
df = pd.read_csv()
()
()
(df.head())
df = df.drop_duplicates(subset=[]).reset_index(drop=)
df[] = df[].astype().str.strip().str.title()
df.loc[(df[] < ) | (df[] > ), ] = 
df.loc[(df[] < ) | (df[] > ), ] = 
df.loc[(df[] < ) | (df[] > ), ] = 
df.loc[(df[] < ) | (df[] > ), ] = 
df = df.fillna(df.mean(numeric_only=))
df[] = df[[, , ]].mean(axis=).round()
()
()
marks_list = df[].tolist()
attendance_list = df[].tolist()
total = 
i = 
 i < (marks_list):
    total = total + marks_list[i]
    i = i + 
average = total / (marks_list)
highest = (marks_list)
lowest = (marks_list)
()
()
()
()
()
()
 j  ():
    mark = marks_list[j]
    attend = attendance_list[j]
     mark >= :
        grade = 
     mark >= :
        grade = 
     mark >= :
grade=
Student Performance & Attendance Analysis — Project Documentation Page 5 of 6
as# 1. LOAD DATASET"college_student_performance_100.csv"print"--- Original Dataset ---"printf"Total Rows: {len(df)}"print# 2. DATA 
CLEANING"student_id"True"department""department"str"attendance_pct"0"attendance_pct
"100"attendance_pct"None"math_score"0"math_score"100"math_score"None"science_score"
0"science_score"100"science_score"None"english_score"0"english_score"100"english_sc
ore"NoneTrue"final_score""math_score""science_score""english_score"12print"\n--- 
After Cleaning ---"printf"Total Rows: {len(df)}"# 3. 
ANALYSIS"final_score""attendance_pct"00whilelen1lenmaxminprint"\n--- Overall 
Analysis ---"printf"Average Final Score : {average:.2f}"printf"Highest Final Score 
: {highest}"printf"Lowest Final Score  : {lowest}"printf"Average Attendance  : 
{sum(attendance_list) / len(attendance_list):.2f}%"# 4. GRADE + ATTENDANCEprint"\n--- Report Card (First 10 Students) --
"forinrange10if90"A+"elif75"A"elif60"B"elif40"C"else"Fail""Low 
Attendance!"if75else"Good"printf"{df['student_id'].iloc[j]} - Marks: {mark:.1f}, 
Grade: {grade}, Attendance: {attend:.1f}%, {status}"# 5. FINAL 
RESULTif60print"\nOverall Performance: GOOD"elseprint"\nOverall Performance: NEEDS 
IMPROVEMENT"
Student Performance & Attendance Analysis — Project Documentation
Page 6 of 6
