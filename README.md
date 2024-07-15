# CodeAlpha_Project_CGPA-Calculator
#include <iostream>
#include <vector>
#include <string>

using namespace std;

class Course {
public:
    string name;
    int creditHours;
    char grade;

    Course(string n, int ch, char g) {
        name = n;
        creditHours = ch;
        grade = g;
    }

    int gradeToPoint() {
        switch (grade) {
        case 'A': return 4;
        case 'B': return 3;
        case 'C': return 2;
        case 'D': return 1;
        case 'F': return 0;
        default: return 0;
        }
    }
};

class Semester {
public:
    vector<Course> courses;

    void addCourse(Course c) {
        courses.push_back(c);
    }

    double calculateGPA() {
        int totalCreditHours = 0;
        int totalPoints = 0;

        for (Course c : courses) {
            totalCreditHours += c.creditHours;
            totalPoints += c.gradeToPoint() * c.creditHours;
        }

        return static_cast<double>(totalPoints) / totalCreditHours;
    }
};

class Student {
public:
    vector<Semester> semesters;

    void addSemester(Semester s) {
        semesters.push_back(s);
    }

    double calculateCGPA() {
        int totalCreditHours = 0;
        int totalPoints = 0;

        for (Semester s : semesters) {
            for (Course c : s.courses) {
                totalCreditHours += c.creditHours;
                totalPoints += c.gradeToPoint() * c.creditHours;
            }
        }

        return static_cast<double>(totalPoints) / totalCreditHours;
    }
};

int main() {
    Student student;

    int numberOfSemesters;
    cout << "Enter the number of semesters: ";
    cin >> numberOfSemesters;

    for (int i = 0; i < numberOfSemesters; i++) {
        Semester semester;
        int numberOfCourses;

        cout << "\nEnter the number of courses for semester " << i + 1 << ": ";
        cin >> numberOfCourses;

        for (int j = 0; j < numberOfCourses; j++) {
            string courseName;
            int creditHours;
            char grade;

            cout << "Enter the course name: ";
            cin >> courseName;
            cout << "Enter the credit hours for " << courseName << ": ";
            cin >> creditHours;
            cout << "Enter the grade (A, B, C, D, F) for " << courseName << ": ";
            cin >> grade;

            semester.addCourse(Course(courseName, creditHours, grade));
        }

        student.addSemester(semester);
        double gpa = semester.calculateGPA();
        cout << "The GPA for semester " << i + 1 << " is: " << gpa << endl;
    }

    double cgpa = student.calculateCGPA();
    cout << "\nThe overall CGPA is: " << cgpa << endl;

    return 0;
}

