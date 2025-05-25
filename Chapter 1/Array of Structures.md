# **📌 المصفوفات من `struct` في C++ (Array of Structures)**

في C++، يمكن استخدام **المصفوفات (`arrays`)** مع **الهياكل (`struct`)** لتخزين بيانات متعددة **من نفس النوع** بطريقة منظمة وفعالة. تُستخدم هذه التقنية كثيرًا عندما يكون لدينا **عدة كائنات** تحتوي على نفس مجموعة البيانات، مثل قائمة **طلاب، موظفين، سيارات، منتجات...** إلخ.

---

## **📌 لماذا نستخدم مصفوفة من `struct`؟**

بدلاً من إنشاء كائن منفصل لكل طالب، يمكننا استخدام **مصفوفة من `struct`** لتسهيل التعامل مع البيانات.

### **❌ بدون استخدام المصفوفة**

```cpp
struct Student {
    string name;
    int age;
    float grade;
};

int main() {
    Student student1 = {"Ali", 20, 90.5};
    Student student2 = {"Mona", 21, 85.7};
    Student student3 = {"Khaled", 22, 78.9};

    cout << student1.name << endl;
    cout << student2.name << endl;
    cout << student3.name << endl;
    
    return 0;
}
```

🔹 **المشكلة؟**

- الكود غير مرن! إذا أردت تخزين **100 طالب**، ستحتاج إلى إنشاء **100 كائن** يدويًا 😵‍💫.

---

## **📌 الحل: استخدام مصفوفة من `struct`**

```cpp
#include <iostream>
using namespace std;

struct Student {
    string name;
    int age;
    float grade;
};

int main() {
    // مصفوفة من 3 طلاب
    Student students[3] = {
        {"Ali", 20, 90.5},
        {"Mona", 21, 85.7},
        {"Khaled", 22, 78.9}
    };

    // طباعة بيانات الطالب الأول
    cout << "Student 1: " << students[0].name << ", Age: " << students[0].age << ", Grade: " << students[0].grade << endl;

    return 0;
}
```

📌 **الإخراج المتوقع:**

```
Student 1: Ali, Age: 20, Grade: 90.5
```

🔹 **المميزات؟**

- **كود أقصر وأكثر ترتيبًا.**
- **يمكننا تخزين عدد غير محدود من الكائنات بسهولة.**

---

## **📌 الوصول إلى بيانات الطلاب في المصفوفة**

يمكنك الوصول إلى **أي عنصر** في المصفوفة باستخدام **الفهرس (`index`)**.

```cpp
cout << students[1].name;  // طباعة اسم الطالب الثاني "Mona"
students[2].grade = 80.5;  // تعديل درجة الطالب الثالث "Khaled"
```

---

## **📌 إدخال بيانات المصفوفة من المستخدم**

يمكنك استخدام **`for` loop** لإدخال البيانات يدويًا.

```cpp
#include <iostream>
using namespace std;

struct Student {
    string name;
    int age;
    float grade;
};

int main() {
    const int SIZE = 3; // عدد الطلاب
    Student students[SIZE];

    // إدخال بيانات الطلاب
    for (int i = 0; i < SIZE; i++) {
        cout << "Enter name, age, and grade for student " << i + 1 << ": ";
        cin >> students[i].name >> students[i].age >> students[i].grade;
    }

    // طباعة بيانات الطلاب
    cout << "\nStudent Details:\n";
    for (int i = 0; i < SIZE; i++) {
        cout << students[i].name << " - Age: " << students[i].age << " - Grade: " << students[i].grade << endl;
    }

    return 0;
}
```

📌 **الإخراج المتوقع (إذا أدخل المستخدم بيانات معينة):**

```
Enter name, age, and grade for student 1: Ali 20 90.5
Enter name, age, and grade for student 2: Mona 21 85.7
Enter name, age, and grade for student 3: Khaled 22 78.9

Student Details:
Ali - Age: 20 - Grade: 90.5
Mona - Age: 21 - Grade: 85.7
Khaled - Age: 22 - Grade: 78.9
```

---

## **📌 تمرير مصفوفة `struct` إلى دالة**

يمكننا تمرير **مصفوفة من `struct`** إلى **دالة** لمعالجة البيانات.

### **🔹 مثال: دالة لطباعة بيانات الطلاب**

```cpp
#include <iostream>
using namespace std;

struct Student {
    string name;
    int age;
    float grade;
};

// دالة لطباعة بيانات جميع الطلاب
void printStudents(Student students[], int size) {
    for (int i = 0; i < size; i++) {
        cout << students[i].name << " - Age: " << students[i].age << " - Grade: " << students[i].grade << endl;
    }
}

int main() {
    Student students[3] = {
        {"Ali", 20, 90.5},
        {"Mona", 21, 85.7},
        {"Khaled", 22, 78.9}
    };

    printStudents(students, 3); // تمرير المصفوفة إلى الدالة

    return 0;
}
```

📌 **الإخراج المتوقع:**

```
Ali - Age: 20 - Grade: 90.5
Mona - Age: 21 - Grade: 85.7
Khaled - Age: 22 - Grade: 78.9
```

---

## **📌 استخدام المؤشرات مع المصفوفة من `struct`**

يمكنك استخدام **المؤشرات (`pointers`)** للوصول إلى المصفوفة بنفس الطريقة.

### **🔹 مثال: الوصول إلى بيانات الطلاب باستخدام مؤشر**

```cpp
#include <iostream>
using namespace std;

struct Student {
    string name;
    int age;
    float grade;
};

int main() {
    Student students[3] = {
        {"Ali", 20, 90.5},
        {"Mona", 21, 85.7},
        {"Khaled", 22, 78.9}
    };

    Student *ptr = students;  // تعيين المؤشر إلى أول عنصر في المصفوفة

    // طباعة بيانات الطلاب باستخدام المؤشر
    for (int i = 0; i < 3; i++) {
        cout << (ptr + i)->name << " - Age: " << (ptr + i)->age << " - Grade: " << (ptr + i)->grade << endl;
    }

    return 0;
}
```

📌 **الإخراج المتوقع:**

```
Ali - Age: 20 - Grade: 90.5
Mona - Age: 21 - Grade: 85.7
Khaled - Age: 22 - Grade: 78.9
```

🔹 **المؤشر `ptr` يشير إلى أول عنصر في المصفوفة (`students[0]`). عند التحرك `(ptr + i)`, نحصل على العنصر التالي وهكذا.**

---

## **📌 مقارنة بين `struct` عادية ومصفوفة من `struct`**

|**الميزة**|**هيكل واحد (`Single struct`)**|**مصفوفة من `struct` (`Array of struct`)**|
|---|---|---|
|**التخزين**|يخزن **كائنًا واحدًا** فقط|يخزن **عدة كائنات** بسهولة|
|**الوصول**|باستخدام `.` (`student.name`)|باستخدام **`[]`** (`students[i].name`)|
|**المرونة**|ثابت|ديناميكي ويمكن تعديله بسهولة|
|**الإدخال**|لكل كائن يدويًا|يمكن استخدام `for loop` للإدخال|

---

## **📌 الخلاصة**

✔️ **المصفوفة من `struct`** تُستخدم لتخزين عدة كائنات متشابهة بسهولة.  
✔️ يمكننا الوصول إلى العناصر باستخدام **الفهارس (`index`)** أو **المؤشرات (`pointers`)**.  
✔️ يمكن تمرير **المصفوفة إلى الدوال** لمعالجة البيانات.  
✔️ **`for loop`** يجعل إدخال البيانات وعرضها أكثر كفاءة.

🚀 **مثالية لإدارة بيانات مثل: الطلاب، المنتجات، الموظفين...**