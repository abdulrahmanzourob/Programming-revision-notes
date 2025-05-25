### الجملة:

**When specifying a file at runtime, the argument to `open()` must be a C-string.**

### الترجمة:

**عند تحديد اسم الملف أثناء وقت التشغيل (runtime)، يجب أن يكون الوسيط المرسل إلى الدالة `open()` عبارة عن سلسلة C (C-string).**

---

### ✅ الجملة **صحيحة**.

---

### 📘 الشرح:

#### ما المقصود بـ **C-string**؟

هي **مصفوفة من الأحرف** منتهية بالرمز null (`'\0'`)، مثل:

```cpp
char filename[] = "data.txt";
```

---

### 📌 استخدام `open()` مع ملفات في C++:

عند استخدام `fstream`, `ifstream`, أو `ofstream` لفتح ملف، يمكننا استخدام الدالة `.open()`.

مثال:

```cpp
fstream file;
file.open("myfile.txt", ios::in | ios::out);
```

ولكن إذا أردت تحديد اسم الملف **خلال وقت التشغيل**، فإن الدالة `open()` تتطلب **C-string**، أي:

```cpp
string name;
cin >> name;
file.open(name.c_str());  // تحويل string إلى C-string
```

---

### ⚠️ لماذا نحتاج تحويل `string` إلى `C-string`؟

الدالة `open()` تقبل:

```cpp
void open(const char* filename, ios_base::openmode mode = ios_base::in);
```

لاحظ أن `filename` من النوع `const char*` وليس `string`.

لذلك يجب استخدام `c_str()` لتحويل `string` إلى C-string.

---

### 🧠 مثال عملي:

```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
    string filename;
    cout << "Enter filename: ";
    cin >> filename;

    ifstream file;
    file.open(filename.c_str());  // ✅ تحويل string إلى C-string

    if (!file) {
        cout << "File couldn't be opened.\n";
    } else {
        cout << "File opened successfully.\n";
    }
    return 0;
}
```

---

### 💡 الخلاصة:

- دالة `open()` تتطلب C-string (`const char*`) كوسيط.
    
- إذا كنت تستخدم `std::string`، يجب تحويله باستخدام `.c_str()`.
    
- إذًا الجملة **صحيحة** ✅.
    

هل تحب أرسل لك مقارنة بين `C-string` و `std::string`؟