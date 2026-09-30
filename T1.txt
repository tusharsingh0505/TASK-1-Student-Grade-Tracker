import java.util.ArrayList;
import java.util.Scanner;

class Student {
    private String name;
    private ArrayList<Double> grades;

    public Student(String name) {
        this.name = name;
        this.grades = new ArrayList<>();
    }

    public void addGrade(double grade) {
        grades.add(grade);
    }

    public double getAverage() {
        if (grades.isEmpty()) {
            return 0;
        }

        double sum = 0;

        for (double grade : grades) {
            sum += grade;
        }

        return sum / grades.size();
    }

    public double getHighest() {
        if (grades.isEmpty()) {
            return 0;
        }

        double highest = grades.get(0);

        for (double grade : grades) {
            if (grade > highest) {
                highest = grade;
            }
        }

        return highest;
    }

    public double getLowest() {
        if (grades.isEmpty()) {
            return 0;
        }

        double lowest = grades.get(0);

        for (double grade : grades) {
            if (grade < lowest) {
                lowest = grade;
            }
        }

        return lowest;
    }

    public String getName() {
        return name;
    }

    public ArrayList<Double> getGrades() {
        return grades;
    }
}

public class StudentGradeTracker {

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        ArrayList<Student> students = new ArrayList<>();

        System.out.println("=================================");
        System.out.println("       STUDENT GRADE TRACKER");
        System.out.println("=================================");

        System.out.print("Enter number of students: ");
        int numberOfStudents = scanner.nextInt();
        scanner.nextLine();

        for (int i = 0; i < numberOfStudents; i++) {

            System.out.println("\nStudent " + (i + 1));

            System.out.print("Enter student name: ");
            String name = scanner.nextLine();

            Student student = new Student(name);

            System.out.print("Enter number of subjects: ");
            int subjects = scanner.nextInt();

            for (int j = 0; j < subjects; j++) {

                double grade;

                do {
                    System.out.print("Enter grade for subject "
                            + (j + 1) + " (0-100): ");
                    grade = scanner.nextDouble();

                    if (grade < 0 || grade > 100) {
                        System.out.println(
                                "Invalid grade! Enter between 0 and 100."
                        );
                    }

                } while (grade < 0 || grade > 100);

                student.addGrade(grade);
            }

            scanner.nextLine();
            students.add(student);
        }

        System.out.println("\n\n=================================");
        System.out.println("        STUDENT SUMMARY");
        System.out.println("=================================");

        for (Student student : students) {

            System.out.println("\nStudent Name: " + student.getName());
            System.out.println("Grades: " + student.getGrades());

            System.out.printf("Average: %.2f%n",
                    student.getAverage());

            System.out.printf("Highest: %.2f%n",
                    student.getHighest());

            System.out.printf("Lowest: %.2f%n",
                    student.getLowest());

            double average = student.getAverage();

            String result;

            if (average >= 90) {
                result = "A";
            } else if (average >= 80) {
                result = "B";
            } else if (average >= 70) {
                result = "C";
            } else if (average >= 60) {
                result = "D";
            } else if (average >= 50) {
                result = "E";
            } else {
                result = "F";
            }

            System.out.println("Grade: " + result);
        }

        scanner.close();

        System.out.println("\n=================================");
        System.out.println("       PROGRAM COMPLETED");
        System.out.println("=================================");
    }
}
