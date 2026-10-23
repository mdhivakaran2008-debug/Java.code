# Java.code
import java.util.Scanner;

class Student {
    int id;
    String name;
    int age;
    String department;
    double marks;

    Student(int id, String name, int age, String department, double marks) {
        this.id = id;
        this.name = name;
        this.age = age;
        this.department = department;
        this.marks = marks;
    }

    void display() {
        System.out.printf("%-5d %-20s %-5d %-15s %.2f%n",
                id, name, age, department, marks);
    }
}

public class Main {

    static Scanner sc = new Scanner(System.in);
    static Student[] students = new Student[100];
    static int count = 0;

    static void addStudent() {
        System.out.print("Enter Student ID: ");
        int id = sc.nextInt();
        sc.nextLine();

        System.out.print("Enter Student Name: ");
        String name = sc.nextLine();

        System.out.print("Enter Age: ");
        int age = sc.nextInt();
        sc.nextLine();

        System.out.print("Enter Department: ");
        String department = sc.nextLine();

        System.out.print("Enter Marks: ");
        double marks = sc.nextDouble();

        students[count] = new Student(id, name, age, department, marks);
        count++;

        System.out.println("Student added successfully!");
    }

    static void displayStudents() {
        if (count == 0) {
            System.out.println("No student records found.");
            return;
        }

        System.out.println("\n--------------------------------------------------------------");
        System.out.printf("%-5s %-20s %-5s %-15s %s%n",
                "ID", "Name", "Age", "Department", "Marks");
        System.out.println("--------------------------------------------------------------");

        for (int i = 0; i < count; i++) {
            students[i].display();
        }
    }

    static void searchStudent() {
        System.out.print("Enter Student ID to search: ");
        int id = sc.nextInt();

        for (int i = 0; i < count; i++) {
            if (students[i].id == id) {
                System.out.println("\nStudent Found:");
                System.out.println("ID: " + students[i].id);
                System.out.println("Name: " + students[i].name);
                System.out.println("Age: " + students[i].age);
                System.out.println("Department: " + students[i].department);
                System.out.println("Marks: " + students[i].marks);
                return;
            }
        }

        System.out.println("Student not found.");
    }

    static void updateStudent() {
        System.out.print("Enter Student ID to update: ");
        int id = sc.nextInt();
        sc.nextLine();

        for (int i = 0; i < count; i++) {
            if (students[i].id == id) {

                System.out.print("Enter new name: ");
                students[i].name = sc.nextLine();

                System.out.print("Enter new age: ");
                students[i].age = sc.nextInt();
                sc.nextLine();

                System.out.print("Enter new department: ");
                students[i].department = sc.nextLine();

                System.out.print("Enter new marks: ");
                students[i].marks = sc.nextDouble();

                System.out.println("Student details updated successfully!");
                return;
            }
        }

        System.out.println("Student not found.");
    }

    static void deleteStudent() {
        System.out.print("Enter Student ID to delete: ");
        int id = sc.nextInt();

        for (int i = 0; i < count; i++) {
            if (students[i].id == id) {

                for (int j = i; j < count - 1; j++) {
                    students[j] = students[j + 1];
                }

                students[count - 1] = null;
                count--;

                System.out.println("Student deleted successfully!");
                return;
            }
        }

        System.out.println("Student not found.");
    }

    static void sortByMarks() {
        for (int i = 0; i < count - 1; i++) {
            for (int j = 0; j < count - i - 1; j++) {

                if (students[j].marks < students[j + 1].marks) {
                    Student temp = students[j];
                    students[j] = students[j + 1];
                    students[j + 1] = temp;
                }
            }
        }

        System.out.println("Students sorted by marks.");
        displayStudents();
    }

    static void calculateAverage() {
        if (count == 0) {
            System.out.println("No student records available.");
            return;
        }

        double total = 0;

        for (int i = 0; i < count; i++) {
            total += students[i].marks;
        }

        double average = total / count;

        System.out.printf("Average Marks = %.2f%n", average);
    }

    public static void main(String[] args) {

        int choice;

        do {
            System.out.println("\n===== STUDENT MANAGEMENT SYSTEM =====");
            System.out.println("1. Add Student");
            System.out.println("2. Display Students");
            System.out.println("3. Search Student");
            System.out.println("4. Update Student");
            System.out.println("5. Delete Student");
            System.out.println("6. Sort by Marks");
            System.out.println("7. Calculate Average");
            System.out.println("8. Exit");
            System.out.print("Enter your choice: ");

            choice = sc.nextInt();

            switch (choice) {
                case 1:
                    addStudent();
                    break;

                case 2:
                    displayStudents();
                    break;

                case 3:
                    searchStudent();
                    break;

                case 4:
                    updateStudent();
                    break;

                case 5:
                    deleteStudent();
                    break;

                case 6:
                    sortByMarks();
                    break;

                case 7:
                    calculateAverage();
                    break;

                case 8:
                    System.out.println("Program exited successfully.");
                    break;

                default:
                    System.out.println("Invalid choice!");
            }

        } while (choice != 8);

        sc.close();
    }
}
