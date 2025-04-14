# cpp-student-records
#include <iostream>
#include <string>
#include <iomanip>
#include <algorithm>
#include <sstream>

using namespace std;

// Custom namespace for student utility functions
namespace StudentUtils {

    // Enum for grade levels
    enum GradeLevel {
        FRESHMAN = 1,
        SOPHOMORE,
        JUNIOR,
        SENIOR
    };

    // Type alias using 'using'
    using GPA = double;

    // Trims leading and trailing whitespace
    void trim(string &s) {
        s.erase(0, s.find_first_not_of(" \t\n\r"));
        s.erase(s.find_last_not_of(" \t\n\r") + 1);
    }

    // Converts a string to uppercase
    void formatName(string &name) {
        transform(name.begin(), name.end(), name.begin(), ::toupper);
    }

    // Converts enum to string representation
    string gradeLevelToString(GradeLevel level) {
        switch (level) {
            case FRESHMAN: return "Freshman";
            case SOPHOMORE: return "Sophomore";
            case JUNIOR: return "Junior";
            case SENIOR: return "Senior";
            default: return "Unknown";
        }
    }

    // Displays student information in formatted way
    void displayStudentInfo(const string &name, GradeLevel level, GPA gpa) {
        cout << "\nStudent Record:" << endl;
        cout << "Name: " << name << endl;
        cout << "Grade Level: " << gradeLevelToString(level) << endl;
        cout << fixed << setprecision(2); // Format GPA to 2 decimal places
        cout << "GPA: " << gpa << endl;
    }

} // namespace StudentUtils

int main() {
    string name;
    string input;
    int gradeInput = 0;
    StudentUtils::GPA gpa = 0.0;

    // Input section
    cout << "Enter student name: ";
    getline(cin, name);
    StudentUtils::trim(name);  // Trim spaces
    StudentUtils::formatName(name);  // Convert to uppercase

    // Grade level input with validation loop
    while (true) {
        cout << "Enter grade level (1=Freshman, 2=Sophomore, 3=Junior, 4=Senior): ";
        getline(cin, input);
        stringstream ss(input);
        if (ss >> gradeInput && (gradeInput >= 1 && gradeInput <= 4)) {
            break;
        }
        cout << "Invalid grade level. Please enter a number between 1 and 4.\n";
    }

    // GPA input with validation loop
    while (true) {
        cout << "Enter GPA (0.00 - 4.00): ";
        getline(cin, input);
        stringstream ss(input);
        if (ss >> gpa && (gpa >= 0.0 && gpa <= 4.0)) {
            break;
        }
        cout << "Invalid GPA. Please enter a number between 0.00 and 4.00.\n";
    }

    // Convert to enum
    StudentUtils::GradeLevel grade = static_cast<StudentUtils::GradeLevel>(gradeInput);

    // Output student record
    StudentUtils::displayStudentInfo(name, grade, gpa);

    return 0;
}
