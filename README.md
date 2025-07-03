public class Student {
    int id;
    String name;
    int age;
    String course;

    public Student(int id, String name, int age, String course) {
        this.id = id;
        this.name = name;
        this.age = age;
        this.course = course;
    }

    public void display() {
        System.out.println("ID: " + id + ", Name: " + name + ", Age: " + age + ", Course: " + course);
    }
}
import java.util.ArrayList;

public class StudentService {
    ArrayList<Student> students = new ArrayList<>();

    public void addStudent(Student student) {
        students.add(student);
        System.out.println("Student added successfully.\n");
    }

    public void viewAllStudents() {
        if (students.isEmpty()) {
            System.out.println("No students found.");
        } else {
            for (Student s : students) {
                s.display();
            }
        }
        System.out.println();
    }

    public void removeStudentById(int id) {
        boolean removed = students.removeIf(s -> s.id == id);
        if (removed) {
            System.out.println("Student removed successfully.\n");
        } else {
            System.out.println("Student not found.\n");
        }
    }

    public void searchStudentById(int id) {
        for (Student s : students) {
            if (s.id == id) {
                s.display();
                return;
            }
        }
        System.out.println("Student not found.\n");
    }
}
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        StudentService service = new StudentService();
        int choice;

        do {
            System.out.println("\n===== Student Management System =====");
            System.out.println("1. Add Student");
            System.out.println("2. View All Students");
            System.out.println("3. Remove Student by ID");
            System.out.println("4. Search Student by ID");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter ID: ");
                    int id = sc.nextInt();
                    sc.nextLine(); // consume newline
                    System.out.print("Enter Name: ");
                    String name = sc.nextLine();
                    System.out.print("Enter Age: ");
                    int age = sc.nextInt();
                    sc.nextLine();
                    System.out.print("Enter Course: ");
                    String course = sc.nextLine();
                    service.addStudent(new Student(id, name, age, course));
                    break;
                case 2:
                    service.viewAllStudents();
                    break;
                case 3:
                    System.out.print("Enter Student ID to remove: ");
                    int removeId = sc.nextInt();
                    service.removeStudentById(removeId);
                    break;
                case 4:
                    System.out.print("Enter Student ID to search: ");
                    int searchId = sc.nextInt();
                    service.searchStudentById(searchId);
                    break;
                case 5:
                    System.out.println("Exiting the system. Goodbye!");
                    break;
                default:
                    System.out.println("Invalid choice. Try again.");
            }

        } while (choice != 5);
    }
}
