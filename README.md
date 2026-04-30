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


    def search_student(students):
    keyword = input("Enter name to search: ")
    found = False

    for s in students:
        if keyword.lower() in s['name'].lower():
            print(f"Found: ID: {s['id']} | Name: {s['name']} | Course: {s['course']}")
            found = True

    if not found:
        print("No student found.\n")


def delete_student(students):
    sid = input("Enter ID to delete: ")
    new_list = [s for s in students if s['id'] != sid]

    if len(new_list) == len(students):
        print("Student not found.\n")
    else:
        save_students(new_list)
        print("Student deleted successfully!\n")
    return new_list


    def main():
    students = load_students()

    while True:
        print("===== Student Information System =====")
        print("1. Add Student")
        print("2. View Students")
        print("3. Search Student")
        print("4. Delete Student")
        print("5. Exit")

        choice = input("Enter choice: ")

        if choice == "1":
            add_student(students)
        elif choice == "2":
            view_students(students)
        elif choice == "3":
            search_student(students)
        elif choice == "4":
            students = delete_student(students)
        elif choice == "5":
            print("Exiting program...")
            break
        else:
            print("Invalid input. Try again.\n")
# Run program
main()

