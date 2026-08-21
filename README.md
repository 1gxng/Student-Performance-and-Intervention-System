# Student-Performance-and-Intervention-System

# Team Contribution
The program contributers were: **FCC Group 2**:

| Member | Student Number |
|---|---|
| Eugene Mwangangi | 224381 |
| Kennedy Odunga | —  |
| Horace Ouma Otieno | 169702 |
| Mulei Mutuku | 230016 |
| Kiprop Amos | 225346  |

## 1. Problem Statement

This simple student performance management system that can evaluate academic performance and identify students who may require academic intervention. The system must process student academic records, validate the information provided, calculate weighted final marks, assign grades, analyse overall class performance, and identify students requiring additional academic support.

The solution is implemented as a **menu-driven Python program**. The program stores student records using a list of dictionaries and provides separate functions for validation, performance analysis, intervention identification, and student searching.

The system is designed to ensure that invalid data does not affect the calculation of academic performance statistics.

---

## 2. Objectives

The main objectives of the Student Performance and Intervention System are to:

1. Store student records using an appropriate Python data structure.
2. Validate each student record against the specified validation rules.
3. Separate valid student records from invalid records and provide reasons for invalidity.
4. Calculate each valid student's weighted final mark.
5. Assign students grades based on their final marks.
6. Identify students who require academic intervention.
7. Calculate and display class-level performance statistics.
8. Identify the highest and lowest final marks.
9. Count the number of students in each grade category.
10. Allow users to search for individual students using their Student ID.
11. Provide a simple, menu-driven interface for accessing the system's functions.

---

## 3. Data Structure

The student records are stored using a **list of dictionaries**.

Each dictionary represents one student and contains the following fields:

- `student_id`
- `programme`
- `assignment_mark`
- `cat_mark`
- `exam_mark`
- `attendance_pct`
- `submitted_project`

For example:

```python
{
    "student_id": "ST001",
    "programme": "MSc IT",
    "assignment_mark": 52,
    "cat_mark": 49,
    "exam_mark": 49,
    "attendance_pct": 64,
    "submitted_project": True
}
```

This structure is appropriate because the list allows multiple student records to be stored, while dictionaries allow each student's attributes to be accessed using meaningful field names.

---

## 4. Validation Rules

Before academic performance is analysed, every student record is validated.

The system applies the following rules:

1. `Student ID:` The program ensures Student ID provided, otherwise, a missing Student ID causes the record to be classified as invalid.

2. `Programme:`A programe must be provided for every student e.g (- MSc IT or MSc AI)

3. `Marks and Attendance:` Assignment, CAT, examination and attendance field values are a must and should; *be numeric values and be between 0 and 100 inclusive*. Also 

4. `Project Submission:` The project-submission status must be a Boolean value: True or False

* Invalid Record Reporting: When a record fails one or more validation rules, the system records the reason for invalidity. This makes it easy for users to identify and correct problematic records.

---

# 5. Main Functions

## 5.1 `validate_records()`

The `validate_records()` function validates all student records and separates them into valid and invalid records.
The function check the following:

1. Checks whether Student ID is provided.
2. Checks whether the programme is provided.
3. Checks whether project submission is Boolean.
4. Validates assignment, CAT, examination and attendance values.
5. Stores valid records in `valid_students`.
6. Stores invalid records in `invalid_records`.
7. Records the reason for each invalid record.

The function returns two lists; valid_students, invalid_records
This allows the rest of the program to work only with valid records when calculating performance.

---

## 5.2 `display_valid_students()`
Displays all student records that have passed the validation process.
If valid records exist, they are displayed to the user. If no valid records are available, the system displays an appropriate message.

This function supports **Menu Option 1: View Valid Students**.

---

## 5.3 `display_invalid_records()`
Displays records that failed validation together with the reasons for failure.

For each invalid record, the system displays the Student ID and validation reason.

This supports **Menu Option 2: View Invalid Records**.

---

## 5.4 `calculate_final_mark()`
Calculates the weighted final mark for every valid student.

The university's weighting scheme is:

```text
Assignment       = 20%
CAT              = 20%
Examination      = 60%
```
The result is rounded to two decimal places and added to the student's record.

---

## 5.5 `grade_final_mark()`
Assigns a grade to each valid student according to the university's grading scale.

| Final Mark | Grade |
|---:|:---:|
| ≥ 70 | A |
| 60 – <70 | B |
| 50 – <60 | C |
| 40 – <50 | D |
| <40 | E |

The grade is stored in each student record.

---

## 5.6 `_calculate_class_statistics()`

Calculates the main numerical indicators of class performance.

The function calculates:

- Class average
- Highest final mark
- Lowest final mark
- Number of valid students
- Individual final marks

The class average is calculated as: `Sum of Final Marks / Number of Valid Students`

The final outputs are rounded to two decimal places.

---

## 5.7 `count_students_in_every_grade()`

Counts the number of students receiving each grade: A , B, C, D, E
The output provides the overall grade distribution of the valid students.

---

## 5.8 `display_perfomance()`

Displays the overall class performance summary.
The function combines the statistical calculations and grade distribution and displays:

```text
Class Performance Summary
-------------------------
Class Average
Highest Mark
Lowest Mark
Total Students
Grades Summary
```

This supports **Menu Option 3: Analyse Class Performance**.

---

# 6. Intervention Analysis

## `view_intervention_list()`

The intervention function identifies students who may require academic support.

A student is flagged when **at least one** of the following conditions is satisfied:

* *Condition 1: Low Final Mark*: If final_mark < 50

* *Condition 2: Low Attendance:* If attendance_pct < 75

* *Condition 3: Project Not Submitted:* submitted_project is False

The function evaluates all three conditions independently. Therefore, a student can have more than one intervention reason.

This provides academic staff with more useful information than simply identifying a student as requiring intervention.

---

# 7. Student Search

## `search_for_student()`

The search function allows the user to retrieve the details of an individual student.

The user enters the numeric portion of the Student ID, for example:`001`

The function then searches through the student records.

If the student exists, the system displays their details.

If no matching record exists, the system displays: `Student not found`

The user inputs: `#` to leave the student-search section and return to the main menu.

---

# 8. Menu-Driven System

The system provides six menu options:

```text
1. View Valid Students
2. View Invalid Records
3. Analyse Class Performance
4. View Intervention List
5. Search for a Student
6. Exit
```

The menu is implemented using a `while True` loop, which keeps the system running until the user selects option 6.

### Menu Functionality

| Option | Function | Purpose |
|---:|---|---|
| 1 | `display_valid_students()` | Display validated student records |
| 2 | `display_invalid_records()` | Display invalid records and reasons |
| 3 | `display_perfomance()` | Analyse overall class performance |
| 4 | `view_intervention_list()` | Identify students requiring intervention |
| 5 | `search_for_student()` | Search for an individual student |
| 6 | Exit | Terminate the program |

Invalid menu selections produce an error message and return the user to the menu.

---


# 9. Running Instructions

### Step 1: Open the Python environment

The program can be run using:

- Google Colab
- VS Code
- Python IDLE
- PyCharm
- GitHub Codespaces
- Python Command Prompt/Terminal

### Step 2: Load the program

Copy the Python code into a Python file or notebook.

For a `.py` file, save it as:

```text
main.py
```

### Step 3: Run the program

From a terminal, use:

```bash
python main.py
```

### Step 4: Select an operation

When the menu appears, enter a number from **1 to 6**.
For example:

```text
Please make a selection from the menu: 3
```

The program will display the class performance analysis.

### Step 5: Exit

Select:

```text
6
```

to terminate the program.

---

