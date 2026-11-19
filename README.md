# -OOPS-EXP.8
C++ program using STL containers ( vector , map , unordered map ) and algorithms (sort , find if , transform )  to process a student marks dataset 

#include <iostream>
#include <vector>
#include <map>
#include <unordered_map>
#include <algorithm>

using namespace std;
struct Student { int id; string name; int marks; };

int main() {
    vector<Student> students = { {101, "Kinjal", 91}, {102, "Priya", 85}, {103, "Rahul", 62}, {104, "Ananya", 90}, {105, "Vikram", 74} };
    // 1. transform
    transform(students.begin(), students.end(), students.begin(), [](auto s) {
        s.marks = min(100, s.marks + 5); return s;
    });
    
    // 2. sort
    sort(students.begin(), students.end(), [](auto& a, auto& b) { return a.marks > b.marks; });
    
    // 3. find_if
    auto it = find_if(students.begin(), students.end(), [](auto& s) { return s.marks >= 90; });
    if (it != students.end()) cout << "Top Scorer (>=90): " << it->name << " (" << it->marks << ")\n";
    
    // 4. map & unordered_map
    map<int, string> idMap;
    unordered_map<string, int> nameMap;
    for (auto& s : students) { idMap[s.id] = s.name; nameMap[s.name] = s.marks; }

    cout << "Priya's Marks (from unordered_map): " << nameMap["Priya"] << "\n";
    return 0;
}
