import csv
import os

FILE_NAME = "student.csv"

if not os.path.exists(FILE_NAME):
    with open(FILE_NAME, "w", newline="") as file:
        writer = csv.writer(file)
        writer.writerow(["Roll", "Name", "Marks"])

def add_student():
    roll = input("Enter roll Number: ")
    name = input("Enter stundent Name: ")
    marks = input("Enter student Marks: ")

    with open(FILE_NAME, "a", newline="") as file:
        writer = csv.writer(file)
        writer.writerow([roll, name, marks])

    print("\nStudent added successfully!\n") 

def display_students():
    with open(FILE_NAME, "r") as file:
        reader = csv.reader(file)
        data = list(reader)

        if len(data) <= 1:
            print("\nNo student records found!\n")
            return
        
        print("\n--- All Students ---")
        print("{:<10} {:<20} {:<10}".format("Roll", "Name", "Marks"))
        print("-" * 40)

        for row in data[1:]:
            print("{:<10} {:<20} {:<10}".format(row[0], row[1], row[2]))
        print()

def search_student():
    roll = input("Enter Roll Number to search: ")
    found = False

    with open(FILE_NAME, "r") as file:
        reader = csv.reader(file)
        for row in reader:
            if row[0] == roll:
                found = True
                print("\nStudent Found!")
                print(f"Roll: {row[0]}, Name: {row[1]}, Marks: {row[2]}\n")
                break

    if not found:
        print("\nStudent not found!\n")

def update_student():
    roll = input("Enter Roll Number to update: ")
    updated = False

    rows = []
    with open(FILE_NAME, "r") as file:
        reader = csv.reader(file)
        for row in reader:
            if row[0] == roll:
                print("\nCurrent Data:")
                print(f"Name: {row[1]}, Marks: {row[2]}")
                row[1] = input("Enter New Name: ")
                row[2] = input("Enter New Marks: ")
                updated = True
            rows.append(row)

    if updated:
        with open(FILE_NAME, "w", newline="") as file:
            writer = csv.writer(file)
            writer.writerows(rows)
        print("\nStudent updated successfully!\n")
    else:
        print("\nStudent not found!\n")


def delete_student():
    roll = input("Enter Roll Number to delete: ")
    deleted = False

    rows = []
    with open(FILE_NAME, "r") as file:
        reader = csv.reader(file)
        for row in reader:
            if row[0] == roll:
                deleted = True
                continue
            rows.append(row)

    if deleted:
        with open(FILE_NAME, "w", newline="") as file:
            writer = csv.writer(file)
            writer.writerows(rows)
        print("\nStudent deleted successfully!\n")
    else:
        print("\nStudent not found!\n")

def menu():
    while True:
          print("===== Student Management System =====")
          print("1. Add Student")
          print("3. Search Student")
          print("4. Update Student")
          print("5. Delete Student")
          print("6. Exit")
          choice = input("Enter your choice: ")

          if choice == "1":
              add_student()
          elif choice == "2":
              display_students()
          elif choice == "3":
              search_student()
          elif choice == "4":
              update_student()
          elif choice == "5":
              delete_student()
          elif choice == "6":
               print("Exiting...")
               break
          else:
            print("Invalid choice! Try again.\n")


menu()
