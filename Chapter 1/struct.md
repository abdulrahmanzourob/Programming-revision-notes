### **🔹 شرح مفصل عن `struct` في C++**

### **1. `structs` (Records)**

- `struct` هو **بنية بيانات** (Data Structure) تسمح لك بتجميع عدة **متغيرات مختلفة الأنواع** في كيان واحد.
- يستخدم عادةً لتمثيل الكيانات الحقيقية مثل **طالب، سيارة، كتاب، موظف**، حيث يحتاج كل كيان إلى مجموعة من البيانات.
- يشبه `class`، ولكن الفرق الأساسي هو أن جميع أعضائه افتراضيًا **public**، بينما في `class` تكون افتراضيًا **private**.

#### **🔹 مثال على تعريف `struct`**

```cpp
#include <iostream>
using namespace std;

struct Student {
    string name;
    int age;
    float grade;
};
```

هنا، لدينا `struct` باسم `Student` يحتوي على **ثلاثة أعضاء**:

- `name`: اسم الطالب من نوع `string`
- `age`: عمر الطالب من نوع `int`
- `grade`: تقدير الطالب من نوع `float`

---

### **2. Accessing struct Members**

- يتم الوصول إلى أعضاء `struct` باستخدام **نقطة `.`** إذا كنا نتعامل مع كائن مباشر.
- إذا كنا نتعامل مع مؤشر إلى `struct`، نستخدم **السهم `->`**.

#### **🔹 مثال**

```cpp
Student s1; // تعريف كائن من struct
s1.name = "Ali";
s1.age = 20;
s1.grade = 90.5;

cout << "Name: " << s1.name << endl;
cout << "Age: " << s1.age << endl;
cout << "Grade: " << s1.grade << endl;
```

#### **🔹 عند استخدام مؤشر إلى `struct`**[مؤشر إلى struct](مؤشر%20إلى%20struct.md)

```cpp
Student *ptr = &s1;  // مؤشر يشير إلى كائن s1
ptr->age = 21;       // تعديل قيمة باستخدام السهم `->`
cout << ptr->age;    // طباعة العمر الجديد
```

---

### **3. Initializing Structure Members**

**🔹 طرق تهيئة كائن من `struct` عند إنشائه**

1. **التهيئة اليدوية بعد التعريف**
2. **التهيئة باستخدام `{}` عند التعريف**
3. **استخدام `C++11` وتهيئة حديثة**

#### **🔹 مثال**

```cpp
Student s1 = {"Ahmed", 22, 88.5};  // الطريقة التقليدية
Student s2{"Sara", 19, 95.0};      // الطريقة الحديثة (C++11)
```

---

### **4. Comparison (Relational Operators)**

- لا يمكن مقارنة `struct` باستخدام **`==` أو `<` أو `>`** مباشرةً.
- يجب مقارنة **كل عضو على حدة**.

#### **🔹 مثال**

```cpp
if (s1.age == s2.age) {
    cout << "Both students are of the same age!" << endl;
} else {
    cout << "They have different ages." << endl;
}
```

---

### **5. Input/Output with struct**

- يمكننا استخدام `cin` و `cout` لإدخال وإخراج البيانات.
- يفضل استخدام **دالة منفصلة** لطباعة البيانات.

#### **🔹 مثال**

```cpp
void printStudent(Student s) {
    cout << "Name: " << s.name << ", Age: " << s.age << ", Grade: " << s.grade << endl;
}

int main() {
    Student s1;
    cout << "Enter name, age, and grade: ";
    cin >> s1.name >> s1.age >> s1.grade;
    printStudent(s1);
}
```

---

### **6. struct Variables and Functions**
[طرق تمرير struct](طرق%20تمرير%20struct.md)
- يمكن تمرير `struct` إلى الدوال بثلاث طرق:
    1. **بالقيمة (`by value`)** ← يتم نسخ البيانات (استهلاك أكبر للذاكرة).
    2. **بالإشارة (`by reference`)** ← لا يتم نسخ البيانات، توفير للذاكرة.
    3. **كمؤشر (`by pointer`)** ← أيضًا لا يتم النسخ، لكن يجب التعامل مع المؤشرات.

#### **🔹 تمرير `struct` بالإشارة (`&`)**

```cpp
void modifyStudent(Student &s) {
    s.grade += 5; // رفع التقدير بمقدار 5
}
```

---

### **7. Returning Structure Variables**

- يمكن أن تعيد الدالة كائنًا من نوع `struct`.
- يفضل الإرجاع بالإشارة (`const &`) لتوفير الذاكرة.

``` cpp
#include <iostream>
using namespace std;

struct Student {
    string name;
    int age;
    float grade;
};

const Student& getStudent() {
    static Student s = {"Omar", 21, 92.0};  // كائن ثابت في الذاكرة
    return s;
}

int main() {
    const Student &s = getStudent();  // استقبال المرجع
    cout << s.name << " - " << s.age << " - " << s.grade << endl;
    return 0;
}

```

#### **🔹 مثال**

```cpp
Student createStudent() {
    return {"Omar", 21, 92.0};
}

int main() {
    Student s = createStudent();
    cout << s.name << " - " << s.age << " - " << s.grade;
}
```

---

### **8. Arrays versus structs**

**المصفوفات (`arrays`)**:

- تحتوي على **عناصر من نفس النوع**.
- لا يمكن تخزين بيانات مختلفة في عنصر واحد.

**الهياكل (`struct`)**:

- يمكنها تخزين **أنواع بيانات مختلفة** في نفس الكيان.
- أكثر مرونة عند التعامل مع البيانات المنظمة.

---

### **9. Array of Structures**
[Array of Structures](Array%20of%20Structures.md)
- يمكن إنشاء **مصفوفة من `struct`** لتخزين بيانات متعددة.

#### **🔹 مثال**

```cpp
Student students[3] = {
    {"Ali", 20, 90.5},
    {"Mona", 21, 85.7},
    {"Khaled", 22, 78.9}
};

cout << students[0].name; // طباعة اسم الطالب الأول
```

---

### **10. Array in struct**

- يمكن أن تحتوي `struct` على **مصفوفة** كأحد أعضائها.

#### **🔹 مثال**

```cpp
struct Classroom {
    string students[5]; // مصفوفة داخل struct
};

Classroom c1 = {{"Ali", "Mona", "Khaled", "Sara", "Omar"}};
cout << c1.students[2]; // طباعة "Khaled"
```

---

### **11. Nested Structures (structs within a struct)**

- يمكن أن يحتوي `struct` على `struct` آخر بداخله.

#### **🔹 مثال**

```cpp
struct Address {
    string city;
    int postalCode;
};

struct Person {
    string name;
    Address address; // struct داخل struct
};

Person p1 = {"Omar", {"Cairo", 12345}};
cout << p1.address.city; // طباعة "Cairo"
```

---

### **12. Initializing Nested Structures**

- عند تهيئة `struct` المتداخل، يجب تحديد القيم لكل `struct` داخلي.

#### **🔹 مثال**

```cpp
Person p2 = {"Ali", {"Alexandria", 54321}};
```

---

### **13. Complex Nested Structures**

- يمكن تضمين `struct` داخل `struct` بشكل متكرر.

#### **🔹 مثال عملي متقدم**

```cpp
struct Date {
    int day;
    int month;
    int year;
};

struct Student {
    string name;
    Date birthdate; // struct داخل struct
};

Student s1 = {"Ahmed", {12, 5, 2002}};
cout << s1.name << " was born on " << s1.birthdate.day << "/" << s1.birthdate.month << "/" << s1.birthdate.year << endl;
```

---

### **💡 ملخص**

✅ `struct` طريقة قوية لتنظيم البيانات في C++.  
✅ يمكن استخدامها مع الدوال، المصفوفات، والمؤشرات.  
✅ يمكن أن تحتوي `struct` على `struct` آخر (تداخل `nested struct`).  
✅ يفضل التمرير بالإشارة (`&`) لتوفير الذاكرة عند التعامل مع الدوال.