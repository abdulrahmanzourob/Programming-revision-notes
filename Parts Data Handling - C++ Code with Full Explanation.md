
# Code

``` C++
#include <iostream>
#include <fstream>
using namespace std;

// تعريف بنية تمثل جزء من القطع
struct Part {
    int partNo;
    char partName[20];
    int marks;
    int quantity;
    char description[50];
};

// 1️⃣ إنشاء ملف ثنائي من ملف نصي
void createBinaryFile() {
    ifstream fin("PartData.txt"); // فتح الملف النصي
    ofstream fout("Part.dat", ios::binary); // إنشاء الملف الثنائي

    Part p;
    // قراءة البيانات من الملف النصي وكتابتها كـ binary
   while(fin >> p.partNo >> p.partName >> p.marks >> p.quantity) {
        fin.ignore(); // Ignore the newline character after quantity
        fin.getline(p.description, 50); // Read the description line

        fout.write((char*)&p, sizeof(p));
    }
    fin.close();
    fout.close();
}

// 2️⃣ قراءة البيانات من الملف الثنائي
void readBinaryFile() {
    ifstream fin("Part.dat", ios::binary);
    Part p;
    while (fin.read((char*)&p, sizeof(p))) {
        cout << "Part No: " << p.partNo << "\n";
        cout << "Name: " << p.partName << "\n";
        cout << "Marks: " << p.marks << "\n";
        cout << "Quantity: " << p.quantity << "\n";
        cout << "Description: " << p.description << "\n";
        cout << "--------------------------\n";
    }
    fin.close();
}

// 3️⃣ تحريك مؤشر القراءة إلى البايت رقم 100
void moveGetPointer() {
    ifstream fin("Part.dat", ios::binary);
    fin.seekg(100, ios::beg); // الانتقال للبايت رقم 100 من البداية

    Part p;
    if (fin.read((char*)&p, sizeof(p))) {
        cout << "From byte 100: " << p.partName << "\n";
    } else {
        cout << "No record at byte 100\n";
    }
    fin.close();
}

// 4️⃣ تحريك مؤشر الكتابة لنهاية الملف (لإضافة سجل جديد)
void movePutPointer() {
    ofstream fout("Part.dat", ios::binary | ios::app); // فتح الملف للإضافة في النهاية
    Part p = {104, "Washer", 8, 300, "FlatWasher"}; // سجل جديد
    fout.write((char*)&p, sizeof(p));
    fout.close();
}

// الدالة الرئيسية لتنفيذ الخطوات السابقة
int main() {
    cout << "Creating binary file from PartData.txt...\n";
    createBinaryFile();

    cout << "\nReading data from Part.dat...\n";
    readBinaryFile();

    cout << "\nMoving get pointer to byte 100...\n";
    moveGetPointer();

    cout << "\nAdding new record at end of file...\n";
    movePutPointer();

    cout << "\nReading updated data from Part.dat...\n";
    readBinaryFile();

    return 0;
}
```

---

### 📁 بيانات الملف النصي `PartData.txt` (مثال):

```txt
101 Screw 10 200 SmallScrew
102 Bolt 15 100 HeavyBolt
103 Nut 5  500 RoundNut
```

---

### ✅ أولًا: نحتاج هيكل (Structure) يمثل كل جزء (Part)

```cpp
#include <iostream>
#include <fstream>  // For file handling
using namespace std;

struct Part {
    int partNo;
    char partName[20];
    int marks;
    int quantity;
    char description[50];
};
```

> نستخدم `char[]` بدل `string` لأن الملفات الثنائية تحتاج نوع بيانات ثابت الطول.

---

# 🧩 1) إنشاء ملف ثنائي "Part.dat" عن طريق القراءة من "PartData.txt"

```C++
void createBinaryFile() {
    ifstream fin("PartData.txt");          // فتح الملف النصي للقراءة
    ofstream fout("Part.dat", ios::binary); // فتح الملف الثنائي للكتابة بالوضع الثنائي

    Part p;
    while (fin >> p.partNo >> p.partName >> p.marks >> p.quantity >> p.description) {
        fout.write((char*)&p, sizeof(p));  // الكتابة في الملف الثنائي
    }

    fin.close();
    fout.close();
}
```

---
#### 🟦 فتح الملف النصي للقراءة

```cpp
ifstream fin("PartData.txt");
```

- `ifstream` ← اختصار لـ **input file stream**، تُستخدم لقراءة الملفات النصية.
- بيتم فتح الملف `"PartData.txt"` بهدف القراءة فقط.

---

#### 🟨 فتح الملف الثنائي للكتابة

```cpp
ofstream fout("Part.dat", ios::binary);
```

- `ofstream` ← **output file stream**، تُستخدم للكتابة داخل الملفات.
    
- `"Part.dat"` ← اسم الملف اللي هيتم إنشاؤه أو الكتابة فيه.
    
- `ios::binary` ← بيخلي الكتابة تتم بطريقة ثنائية (binary)، مش كنصوص.
    

----

#### 🟩 تعريف متغير من نوع `Part`

```cpp
Part p;
```

- هنا بيتم تعريف متغير `p` من نوع `Part`.
    
- **ملاحظة مهمة**: لازم يكون فيه تعريف مسبق لـ `struct Part`، وده شكله المتوقع:
    

```cpp
struct Part {
    int partNo;
    string partName;
    int marks;
    int quantity;
    string description;
};
```

> ⚠️ **تحذير**: لا يمكن استخدام `string` داخل الكتابة الثنائية المباشرة بهذه الطريقة. لازم تستخدم `char arrays` بدلًا من `string` علشان تضمن الكتابة بشكل صحيح للملف الثنائي.

---

#### 🔄 حلقة القراءة من الملف النصي والكتابة في الملف الثنائي

```cpp
while (fin >> p.partNo >> p.partName >> p.marks >> p.quantity >> p.description) {
    fout.write((char*)&p, sizeof(p));
}
```

### 1. `fin >> ...`

- بيقرأ البيانات من السطر الحالي في الملف النصي، وبيحطها في متغير `p`.
    
- كل مرة يقرأ فيها سطر جديد، بيملا أعضاء `p` بالقيم.
    

### 2. `fout.write((char*)&p, sizeof(p));`

- `&p` ← عنوان المتغير `p` (بداية البيانات).
    
- `(char*)&p` ← بنحوّل العنوان لنوع `char*` لأن دالة `write()` بتحتاج `char*`.
    
- `sizeof(p)` ← عدد البايتات اللي بيشغلها `p` في الذاكرة.
    
- `write()` ← تكتب البايتات دي كلها في الملف الثنائي.
    

> ⚠️ **مرة تانية**: لو `Part` يحتوي على `string`، الكتابة كده مش هتكون صحيحة. استخدم `char partName[50];` بدلًا من `string partName;`.

---

#### ✅ إغلاق الملفات

```cpp
fin.close();
fout.close();
```

- بيتم إغلاق الملفين بعد الانتهاء لحفظ البيانات وتحرير الموارد.
    

###### 📌 ملخص الفرق بين `fin` و `fout`

|الكائن|النوع|الوظيفة|الملف المستخدم|
|---|---|---|---|
|`fin`|`ifstream`|قراءة من ملف نصي|`"PartData.txt"`|
|`fout`|`ofstream`|كتابة في ملف ثنائي|`"Part.dat"`|

---

# 🧩 2) قراءة البيانات من الملف الثنائي "Part.dat" وإخراجها

```cpp
void readBinaryFile() {
    ifstream fin("Part.dat", ios::binary); // فتح الملف الثنائي للقراءة

    Part p;
    while (fin.read((char*)&p, sizeof(p))) {
        cout << "Part No: " << p.partNo << "\n";
        cout << "Name: " << p.partName << "\n";
        cout << "Marks: " << p.marks << "\n";
        cout << "Quantity: " << p.quantity << "\n";
        cout << "Description: " << p.description << "\n";
        cout << "---
        -----------------------\n";
    }

    fin.close();
}
```

### ✅ شرح:

- نستخدم `read()` لقراءة كل كائن `Part`.
    
- نطبع بياناته على الشاشة.


---

# 🧩 3) تحريك مؤشر القراءة (get pointer) إلى البايت رقم 100

```cpp
void moveGetPointer() {
    ifstream fin("Part.dat", ios::binary);
    fin.seekg(100, ios::beg);  // الانتقال إلى البايت رقم 100 من بداية الملف

    Part p;
    if (fin.read((char*)&p, sizeof(p))) {
        cout << "From byte 100: " << p.partName << "\n";
    } else {
        cout << "No record at byte 100\n";
    }

    fin.close();
}
```

### ✅ شرح:

- `seekg`: تحريك مؤشر القراءة.
    
- نحاول نقرأ سجل يبدأ من البايت رقم 100.

### 📌 دوال التحكم في موقع المؤشر:

| الدالة    | الغرض                            |
| --------- | -------------------------------- |
| `seekg()` | تغيير موقع القراءة (get pointer) |
| `seekp()` | تغيير موقع الكتابة (put pointer) |
| `tellg()` | معرفة موقع القراءة الحالي        |
| `tellp()` | معرفة موقع الكتابة الحالي        |

---

# 🧩 4) تحريك مؤشر الكتابة (put pointer) إلى نهاية الملف

```cpp
void movePutPointer() {
    ofstream fout("Part.dat", ios::binary | ios::app); // ios::app يعني نهاية الملف
    Part p = {104, "Washer", 8, 300, "FlatWasher"}; // البيانات اللي هحطها

    fout.write((char*)&p, sizeof(p)); // إضافة سجل جديد في نهاية الملف

    fout.close();
}
```

### ✅ شرح:

- `ios::app` يحرك المؤشر إلى آخر الملف تلقائيًا.
- `seekp()` تغيير موقع الكتابة (put pointer)
- كتبنا سجل جديد في نهاية الملف.

---

# الدالة الرئيسية لتنفيذ الخطوات السابقة

```C++
int main() {
    cout << "Creating binary file from PartData.txt...\n";
    createBinaryFile();

    cout << "\nReading data from Part.dat...\n";
    readBinaryFile();

    cout << "\nMoving get pointer to byte 100...\n";
    moveGetPointer();

    cout << "\nAdding new record at end of file...\n";
    movePutPointer();

    cout << "\nReading updated data from Part.dat...\n";
    readBinaryFile();

    return 0;
}
```