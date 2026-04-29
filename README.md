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
