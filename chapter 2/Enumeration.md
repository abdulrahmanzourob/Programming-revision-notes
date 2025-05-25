### 📌 **ملخص Enumeration في C++**

#### 🔹 **ما هو `enum`؟**

- `enum` هو **نوع بيانات مخصص** يحتوي على مجموعة **قيم ثابتة عددية صحيحة**.
    
- يسمح باستخدام **أسماء ذات معنى** بدلاً من الأرقام، مما يجعل الكود **أوضح وأسهل في الصيانة**.
    
- كل عنصر داخل `enum` يسمى **مُعدِّد (Enumerator)** وهو **ثابت (constant)**.
    

#### 🔹 **القواعد الأساسية لـ `enum`**

✅ يتم تعريف `enum` باستخدام **الكلمة المحجوزة** `enum`.  
✅ القيم الافتراضية تبدأ من **0** وتزداد تلقائيًا.  
✅ يمكن تخصيص القيم يدويًا عند التعريف.  
✅ لا يمكن **إعادة تعريف `enum` بنفس الاسم في نفس النطاق (scope)**.  
✅ يمكن أن يحتوي `enum` على **ما يصل إلى 256 قيمة**.

#### 🔹 **الصياغة العامة (`Syntax`)**

```cpp
enum typeName { value1, value2, value3, ... };
```

#### 🔹 **أمثلة على `enum`**

✅ **استخدام القيم الافتراضية:**

```cpp
enum Days { SUNDAY, MONDAY, TUESDAY };  
// SUNDAY = 0, MONDAY = 1, TUESDAY = 2
```

✅ **تخصيص القيم يدويًا:**

```cpp
enum Status { ERROR = -1, OK = 1, WARNING = 2 };
// ERROR = -1, OK = 1, WARNING = 2
```

✅ **مثال باستخدام `switch` مع `enum`:**

```cpp
enum TrafficLight { RED, YELLOW, GREEN };

TrafficLight signal = RED;

switch (signal) {
    case RED: cout << "Stop!"; break;
    case YELLOW: cout << "Get Ready!"; break;
    case GREEN: cout << "Go!"; break;
}
```

✅ **تعريف `enum` بقيم مخصصة:**

```cpp
enum season { spring = 0, summer = 4, autumn = 8, winter = 12 };
// spring = 0, summer = 4, autumn = 8, winter = 12
```

#### 🔹 **🛠️ الأخطاء الشائعة**

❌ **إعادة تعريف `enum` بنفس الاسم يؤدي إلى خطأ:**

```cpp
enum color { red, green, blue };  // ✅ صحيح
enum color { red=1, green, blue };  // ❌ خطأ: لا يمكن إعادة تعريف نفس `enum`
```

---

### 📌 **أخطاء شائعة عند استخدام `enum` في C++**

#### ❌ **أخطاء في تعريف `enum`**

1️⃣ **استخدام علامات الاقتباس (' ') مع القيم:**

```cpp
enum grades {'A', 'B', 'C', 'D', 'F'}; // ❌ خطأ
```

🔴 **السبب:**

- `enum` يقبل **المعرفات (Identifiers)** فقط، وليس القيم الحرفية (`'A'`, `'B'`، إلخ).
    

✅ **التصحيح الصحيح:**

```cpp
enum grades {A, B, C, D, F}; // ✅ صحيح
```

---

2️⃣ **استخدام أرقام أو رموز غير صالحة كمعرفات:**

```cpp
enum places {1ST, 2ND, 3RD, 4TH}; // ❌ خطأ
```

🔴 **السبب:**

- لا يمكن أن يبدأ **المعرف برقم**.
    
- لا يمكن استخدام رموز خاصة (`ST`, `ND`, `RD`, إلخ) داخل الأسماء.
    

✅ **التصحيح الصحيح:**

```cpp
enum places {FIRST, SECOND, THIRD, FOURTH}; // ✅ صحيح
```

---

3️⃣ **استخدام نفس القيمة في أكثر من `enum` داخل نفس `block`:**

```cpp
enum mathStudent {JOHN, BILL, CINDY, LISA, RON};
enum compStudent {SUSAN, CATHY, JOHN, WILLIAM}; // ❌ خطأ
```

🔴 **السبب:**

- `JOHN` تم استخدامه مسبقًا في `mathStudent`، لذلك لا يمكن استخدامه مجددًا في `compStudent` داخل نفس النطاق (`block`).
    

✅ **التصحيح الصحيح:**  
✔️ **تغيير الاسم في `compStudent`:**

```cpp
enum mathStudent {JOHN, BILL, CINDY, LISA, RON};
enum compStudent {SUSAN, CATHY, JONATHAN, WILLIAM}; // ✅ صحيح
```

✔️ **أو وضع `enum` في نطاقات (`namespace` أو `struct`) مختلفة:**

```cpp
namespace Math {
    enum Student { JOHN, BILL, CINDY, LISA, RON };
}

namespace Comp {
    enum Student { SUSAN, CATHY, JOHN, WILLIAM }; // ✅ صحيح داخل نطاق مختلف
}
```

---

## 📌 **ملخص العمليات على `enum` في C++**

#### ❌ **العمليات الحسابية غير مسموحة مباشرة على `enum`**

🚫 لا يمكن استخدام `+`, `-`, `*`, `/`, `++`, `--` مباشرة مع `enum`.

```cpp
popularSport++;          // ❌ خطأ
popularSport = popularSport + 2;  // ❌ خطأ
```

#### ✅ **الحل: استخدام `static_cast`**

✔️ يمكن **تحويل `enum` إلى `int`** وإجراء العمليات ثم تحويله مرة أخرى إلى `enum`:

```cpp
popularSport = static_cast<sports>(popularSport + 1);  // ✅ صحيح
```

🔹 **التقدم في القائمة:**

```cpp
popularSport = FOOTBALL;  // القيمة = 1
popularSport = static_cast<sports>(popularSport + 1);  // الآن HOCKEY (القيمة = 2)
```

🔹 **التراجع في القائمة:**

```cpp
popularSport = FOOTBALL;  // القيمة = 1
popularSport = static_cast<sports>(popularSport - 1);  // الآن BASKETBALL (القيمة = 0)
```

### ✅ **ملخص سريع**

✔️ `enum` لا يدعم العمليات الحسابية مباشرة.  
✔️ يجب استخدام `static_cast` للتحويل إلى عدد صحيح قبل العمليات الرياضية.  
✔️ يمكن **الانتقال إلى القيمة التالية أو السابقة** باستخدام `+1` أو `-1`.

---

## 📌 **إدخال وإخراج القيم في `enum` في C++**

#### ❌ **`enum` لا يدعم الإدخال/الإخراج مباشرة**

🚫 لا يمكن استخدام `cin` أو `cout` مباشرة مع `enum` لأنه ليس من الأنواع المدمجة (`int`, `char`, `double`, إلخ).

```cpp
enum courses {ALGEBRA, BASIC, PASCAL, CPP, PHILOSOPHY, ANALYSIS, CHEMISTRY, HISTORY};
courses registered;

cin >> registered;  // ❌ خطأ - لا يمكن الإدخال مباشرة
cout << registered; // ❌ خطأ - لا يمكن الإخراج مباشرة
```

#### ✅ **الحل: تحويل `enum` إلى عدد صحيح والعكس**

✔️ **لإدخال قيمة، نقوم بقراءتها كعدد صحيح ثم تحويلها إلى `enum`**:

```cpp
int input;
cin >> input;
registered = static_cast<courses>(input);  // ✅ تحويل الرقم إلى enum
```

✔️ **لإخراج قيمة `enum`، نحولها إلى عدد صحيح**:

```cpp
cout << static_cast<int>(registered);  // ✅ طباعة القيمة كعدد صحيح
```

### ✅ **ملخص سريع**

✔️ لا يمكن استخدام `cin` و `cout` مباشرة مع `enum`.  
✔️ **الحل:** استخدام `static_cast<int>()` للتحويل بين `enum` و `int`.