
```C++
#include <iostream>
#include <fstream>
#include <cstring>
using namespace std;

// تعريف بنية الطالب
struct Student {
    int id;
    char firstName[20];
    char lastName[20];
    float gpa;
};

// إنشاء ملف ثنائي students.dat من ملف students.txt
void createRandomAccessFile() {
    ifstream txtFile("students.txt");
    fstream binFile("students.dat", ios::out | ios::binary);

    Student s;
    while (txtFile >> s.id >> s.firstName >> s.lastName >> s.gpa) {
        long position = (s.id - 1) * sizeof(Student); // الموقع حسب ID
        binFile.seekp(position);
        binFile.write((char*)&s, sizeof(Student));  // ← الطريقة المطلوبة
    }

    txtFile.close();
    binFile.close();
    cout << "✅ تم إنشاء الملف الثنائي باستخدام Random Access.\n";
}

// قراءة وعرض كل الطلاب من الملف الثنائي
void readAllStudents() {
    ifstream binFile("students.dat", ios::in | ios::binary);
    Student s;
    cout << "\n📚 كل الطلاب في students.dat:\n";

    while (binFile.read((char*)&s, sizeof(Student))) {
        cout << "ID: " << s.id
             << ", Name: " << s.firstName << " " << s.lastName
             << ", GPA: " << s.gpa << endl;
    }

    binFile.close();
}

// عرض بيانات طالب معين حسب ID
void readStudentByID(int id) {
    ifstream binFile("students.dat", ios::in | ios::binary);
    Student s;
    long position = (id - 1) * sizeof(Student);
    binFile.seekg(position);
    binFile.read((char*)&s, sizeof(Student));

    if (binFile) {
        cout << "\n🔍 بيانات الطالب ID " << id << ":\n";
        cout << "Name: " << s.firstName << " " << s.lastName << ", GPA: " << s.gpa << endl;
    } else {
        cout << "\n⚠️ لا يوجد طالب بهذا الرقم.\n";
    }

    binFile.close();
}

// تحديث معدل GPA لطالب معين باستخدام ID
void updateGPAByID(int id, float newGPA) {
    fstream binFile("students.dat", ios::in | ios::out | ios::binary);
    Student s;
    long position = (id - 1) * sizeof(Student);
    binFile.seekg(position);
    binFile.read((char*)&s, sizeof(Student));

    if (binFile) {
        s.gpa = newGPA;
        binFile.seekp(position);
        binFile.write((char*)&s, sizeof(Student));
        cout << "\n✅ تم تحديث المعدل للطالب ID " << id << ".\n";
    } else {
        cout << "\n⚠️ لا يمكن تحديث: الطالب غير موجود.\n";
    }

    binFile.close();
}

// حساب حجم الملف students.dat
void showFileSize() {
    ifstream file("students.dat", ios::binary | ios::ate);
    cout << "\n📦 حجم الملف students.dat: " << file.tellg() << " بايت.\n";
    file.close();
}

// حذف طالب باستخدام ID (إعادة تعيين السجل)
void deleteStudentByID(int id) {
    fstream binFile("students.dat", ios::in | ios::out | ios::binary);
    Student empty = {0, "", "", 0.0}; // سجل فارغ
    long position = (id - 1) * sizeof(Student);
    binFile.seekp(position);
    binFile.write((char*)&empty, sizeof(Student));
    binFile.close();
    cout << "\n🗑️ تم حذف الطالب ID " << id << " (تعيين السجل كفارغ).\n";
}

// الدالة الرئيسية
int main() {
    createRandomAccessFile();
    readAllStudents();

    readStudentByID(2);
    updateGPAByID(2, 4.0);
    readStudentByID(2);

    showFileSize();

    deleteStudentByID(3);
    readAllStudents();

    return 0;
}
```
## ✅ **تعريف هيكل الطالب `Student`**

```cpp
#include <iostream>
#include <fstream>
#include <cstring>
using namespace std;

struct Student {
    int id;
    char firstName[20];
    char lastName[20];
    float gpa;
};
```

> 🔸 نستخدم `char[]` بدلاً من `string` لأنه أكثر توافقًا مع الملفات الثنائية (binary files).

---

## ✅ 1. **إنشاء ملف ثنائي `students.dat` حسب رقم الـ ID كموقع تخزين**

```cpp
void createRandomAccessFile() {
    ifstream txtFile("students.txt");
    fstream binFile("students.dat", ios::out | ios::binary);
    
    Student s;
    while (txtFile >> s.id >> s.firstName >> s.lastName >> s.gpa) {
        long position = (s.id - 1) * sizeof(Student); // الموقع بناءً على ID
        binFile.seekp(position);
        binFile.write((char*)&s, sizeof(Student));
    }

    txtFile.close();
    binFile.close();
    cout << "Binary file created using random access.\n";
}
```

---

## ✅ 2. **قراءة وطباعة جميع بيانات الطلاب من `students.dat`**

```cpp
void readAllStudents() {
    ifstream binFile("students.dat", ios::binary);
    
    Student s;
    int index = 0;
    while (binFile.read((char*)&s, sizeof(Student))) {
        if (s.id != 0) { // 0 = يعتبر محذوف
            cout << "ID: " << s.id
                 << ", Name: " << s.firstName << " " << s.lastName
                 << ", GPA: " << s.gpa << endl;
        }
        index++;
    }

    binFile.close();
}
```

---

## ✅ 3. **عرض بيانات طالب باستخدام الـ ID**

```cpp
void readStudentByID(int id) {
    ifstream file("students.dat", ios::binary);

    long pos = (id - 1) * sizeof(Student);
    file.seekg(pos);

    Student s;
    binFile.read((char*)&s, sizeof(Student));

    if (s.id != 0)
        cout << "ID: " << s.id << ", Name: " << s.firstName << " " << s.lastName << ", GPA: " << s.gpa << endl;
    else
        cout << "No student found with ID " << id << endl;

    file.close();
}
```

---

## ✅ 4. **تحديث المعدل GPA لطالب معين باستخدام ID**

```cpp
void updateGPAByID(int id, float newGPA) {
    fstream file("students.dat", ios::in | ios::out | ios::binary);

    long pos = (id - 1) * sizeof(Student);
    file.seekg(pos);

    Student s;
    binFile.read((char*)&s, sizeof(Student));

    if (s.id != 0) {
        s.gpa = newGPA;
        file.seekp(pos);
        binFile.write((char*)&s, sizeof(Student));
        cout << "GPA updated successfully.\n";
    } else {
        cout << "No student found with ID " << id << endl;
    }

    file.close();
}
```

---

## ✅ 5. **عرض حجم الملف `students.dat` بالبايت**

```cpp
void displayFileSize() {
    ifstream file("students.dat", ios::binary | ios::ate); // ios::ate = انتقل لنهاية الملف مباشر

    cout << "Size of students.dat: " << file.tellg() << " bytes" << endl;

    file.close();
}
```

---

## ✅ 6. حذف طالب باستخدام ID (إعادة تعيين السجل)

```C++
void deleteStudentByID(int id) {
    fstream binFile("students.dat", ios::in | ios::out | ios::binary);
    Student empty = {0, "", "", 0.0}; // سجل فارغ
    long position = (id - 1) * sizeof(Student);
    binFile.seekp(position);
    binFile.write((char*)&empty, sizeof(Student));
    binFile.close();
    cout << "\n Student with ID " << id << " has been deleted (record set to empty).\n";
}
```

---

## ✅ دالة `main()` لتجربة الوظائف:

```cpp
int main() {
    createRandomAccessFile();
    cout << "\nAll students:\n";
    readAllStudents();

    cout << "\nStudent with ID 2:\n";
    readStudentByID(2);

    cout << "\nUpdating GPA of student with ID 2 to 3.9...\n";
    updateGPAByID(2, 3.9);

    cout << "\nStudent with ID 2 after update:\n";
    readStudentByID(2);

    cout << "\nFile size:\n";
    displayFileSize();

    return 0;
}
```

---

## هل تريد إضافة:

- حذف طالب باستخدام ID؟
    
- إعادة كتابة البيانات إلى `students.txt`؟
    
- قائمة الطلاب بترتيب معين؟
    

أخبرني وسأضيفها لك مباشرة.