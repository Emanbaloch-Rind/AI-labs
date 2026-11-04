# Lab 01: Knowledge-Based Systems

## Exercise 1: Degree Honors Rule

### Task
Add a new rule to UNIVERSITY_KB["rules"] for students completing their degree program.

### Condition
- CGPA must be greater than or equal to 3.70.
- Disciplinary warnings must be equal to 0.

### Expected Status
Graduated with Magna Cum Laude Honors.
```python
{ "id": "RULE_07",
    "conditions": {
        "cgpa_min": 3.70,
        "disciplinary_warnings": 0
    },
    "condition_type": "degree_honors",
    "grade": "A",
    "status": "Graduated with Magna Cum Laude Honors",
    "action": "Eligible for Magna Cum Laude Degree Honors."
},

```
Adding above lines to KB to achive the first execute
## Exercise 2: Tracing Forward Chaining

### Task
Modify evaluate_student() to print each evaluated rule condition as the loop runs.

### Purpose
To understand how the system checks rules one by one and makes logical decisions.
# STEP 2: INFERENCE ENGINE
```python
def evaluate_student(student_record, kb):
print(f"\n--- EVALUATING STUDENT: {student_record['student_name']} ---")

    # Check Rule 1: Attendance
    print("\nChecking Attendance Rule...")

    if student_record["attendance"] < 75:

        print("Attendance condition: TRUE")

        attendance_rule = next(r for r in kb["rules"] if r["condition_type"] == "attendance_below")

        print("Rule matched:", attendance_rule["id"])

        return {
            "rule_id": attendance_rule["id"],
            "grade": attendance_rule["grade"],
            "status": attendance_rule["status"],
            "action": attendance_rule["action"]
        }

    else:
        print("Attendance condition: FALSE")


    # Check Rule 07: Degree Honors
    print("\nChecking Degree Honors Rule...")

    if student_record.get("cgpa", 0) >= 3.70 and student_record.get("disciplinary_warnings", -1) == 0:

        print("Degree Honors condition: TRUE")

        honors_rule = next(r for r in kb["rules"] if r["condition_type"] == "degree_honors")

        print("Rule matched:", honors_rule["id"])

        return {
            "rule_id": honors_rule["id"],
            "grade": honors_rule["grade"],
            "status": honors_rule["status"],
            "action": honors_rule["action"]
        }

    else:
        print("Degree Honors condition: FALSE")


    # Check Grade Spectrum Rules
    print("\nChecking Marks Range Rules...")

    marks = student_record["total_marks"]

    for rule in kb["rules"]:

        if rule["condition_type"] == "marks_range":

            print("Checking rule:", rule["id"])

            if rule["conditions"]["marks_min"] <= marks <= rule["conditions"]["marks_max"]:

                print("Marks condition: TRUE")
                print("Rule matched:", rule["id"])

                return {
                    "rule_id": rule["id"],
                    "grade": rule["grade"],
                    "status": rule["status"],
                    "action": rule["action"]
                }

            else:
                print("Marks condition: FALSE")


    print("No matching rule found.")

    return {
        "rule_id": "UNKNOWN",
        "grade": "N/A",
        "status": "Invalid Score Entry",
        "action": "Verify submitted marks with the exam department."
    }

```
