A simple Python-based Student Grade Management System to add, view, calculate grades and generate report cards. Made for students in Pydroid 3.# Student Grade Management System - Pro Version

students = {}

def calculate_grade(avg):
    if avg >= 90:
        return "A+"
    elif avg >= 80:
        return "A"
    elif avg >= 70:
        return "B"
    elif avg >= 60:
        return "C"
    elif avg >= 50:
        return "D"
    else:
        return "F - Fail"

print("===== STUDENT GRADE MANAGEMENT SYSTEM =====")

while True:
    print("\n1. Add Student")
    print("2. View All Students")
    print("3. Search Student")
    print("4. Delete Student")
    print("5. Save to File & Exit")

    choice = input("Enter choice (1-5): ")

    if choice == "1":
        name = input("Enter student name: ")
        roll = input("Enter roll no: ")
        print("Enter marks for 3 subjects (out of 100):")
        try:
            m1 = int(input(" Subject 1: "))
            m2 = int(input(" Subject 2: "))
            m3 = int(input(" Subject 3: "))

            total = m1 + m2 + m3
            avg = total / 3
            grade = calculate_grade(avg)

            students[roll] = {
                "name": name,
                "marks": [m1, m2, m3],
                "total": total,
                "avg": round(avg, 2),
                "grade": grade
            }
            print(f"✅ Student {name} Added! Grade: {grade}")
        except:
            print("❌ Marks should be numbers!")

    elif choice == "2":
        if not students:
            print("No students yet!")
        else:
            print("\n--- All Students Report ---")
            for roll, data in students.items():
                print(f"Roll: {roll} | Name: {data['name']} | Total: {data['total']}/300 | Avg: {data['avg']} | Grade: {data['grade']}")

    elif choice == "3":
        roll = input("Enter roll no to search: ")
        if roll in students:
            d = students[roll]
            print(f"\nFound: {d['name']} - Marks: {d['marks']} - Avg: {d['avg']} - Grade: {d['grade']}")
        else:
            print("Not Found!")

    elif choice == "4":
        roll = input("Enter roll no to delete: ")
        if roll in students:
            del students[roll]
            print("Deleted!")
        else:
            print("Not Found!")

    elif choice == "5":
        # Save to file for proof
        with open("students_record.txt", "w") as f:
            for roll, data in students.items():
                f.write(f"{roll} - {data['name']} - {data['avg']} - {data['grade']}\n")
        print("Record saved to students_record.txt")
        print("Thanks! Bye!")
        break
