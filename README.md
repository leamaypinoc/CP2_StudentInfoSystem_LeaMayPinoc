import os

FILE_NAME = "students.txt"


def load_students():
    students = []
    if os.path.exists(FILE_NAME):
        with open(FILE_NAME, "r") as file:
            for line in file:
                data = line.strip().split("|")
                if len(data) == 3:
                    students.append({
                        "id": data[0],
                        "name": data[1],
                        "course": data[2]
                    })
    return students

def save_students(students):
    with open(FILE_NAME, "w") as file:
        for s in students:
            file.write(f"{s['id']}|{s['name']}|{s['course']}\n")

def add_student(students):
    print("\n--- Add Student ---")
    sid = input("Enter ID: ")
    name = input("Enter Name: ")
    course = input("Enter Course: ")

    students.append({
        "id": sid,
        "name": name,
        "course": course
    })

    save_students(students)
    print("Student added successfully!\n")

    
def view_students(students):
    print("\n--- Student List ---")
    if not students:
        print("No students found.\n")
        return

    for s in students:
        print(f"ID: {s['id']} | Name: {s['name']} | Course: {s['course']}")
    print()


    
