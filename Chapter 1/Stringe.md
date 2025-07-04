# **شرح لمفهوم الـ Strings في C++**

في C++، **السلاسل النصية (Strings)** هي **تسلسل من الأحرف** يتم وضعه بين علامات اقتباس مزدوجة `" "`، مثل `"Hello"`.

### أنواع السلاسل النصية في C++

C++ تدعم **نوعين** من التمثيلات النصية:  
1️⃣ **String Type (كائن string في C++)**

- هو **كائن من الفئة (class)** `string`، وهي جزء من مكتبة **Standard Template Library (STL)**.
    
- يتم تعريفه باستخدام `#include <string>`.
    
- يتميز بأنه **ديناميكي**، أي يمكن تغيير طوله أثناء تنفيذ البرنامج.
    

📌 **مثال على استخدام string في C++**:

```cpp
#include <iostream>
#include <string>  // تضمين مكتبة string

using namespace std;

int main() {
    string str1 = "Hello";  // تعريف متغير نصي
    cout << str1 << endl;   // طباعة النص
    cout << "First character: " << str1[0] << endl; // الوصول لأول حرف
    cout << "Second character: " << str1[1] << endl; // الوصول للحرف الثاني
    return 0;
}
```

💡 **ملاحظات هامة:**

- الحروف داخل السلسلة تبدأ من **الموضع 0**، فمثلًا `"Hello"` يكون:
    
    - `H` في الموضع `0`
        
    - `e` في الموضع `1`
        
    - `l` في الموضع `2`
        
    - `l` في الموضع `3`
        
    - `o` في الموضع `4`
        

### تضمين مكتبة

للاستفادة من **وظائف السلاسل النصية** في C++، يجب تضمين مكتبة `<string>`، والتي توفر **وظائف جاهزة** مثل:

- `length()` أو `size()` → لحساب عدد الأحرف
    
- `append()` → لإضافة نص آخر
    
- `substr()` → لاستخراج جزء معين من النص
    
- `find()` → للبحث عن جزء معين داخل النص
    
---
# **شرح C-Strings (Character Arrays) في C++**

💡 **ما هي C-Strings؟**  
في C++، **C-strings** هي **مصفوفة من الأحرف** (**Character Array**) يتم إنهاؤها برمز **null character (`'\0'`)**، وهو **يمثل نهاية السلسلة النصية**.

🛑 **الفرق الأساسي بين `string` و `C-string`:**

|النوع|المرونة|طريقة التخزين|إنهاء النص|
|---|---|---|---|
|**`string` (كائن من فئة `string`)**|**ديناميكي** (يمكن تغيير حجمه)|يتم تخزينه وإدارته تلقائيًا|لا يحتاج إلى `'\0'` لأنه يتم التعامل معه ككائن|
|**C-string (مصفوفة أحرف)**|**ثابت الطول** (لا يمكن تغيير حجمه بعد تعريفه)|يتم تخزينه كمصفوفة أحرف|يجب أن ينتهي دائمًا بـ `'\0'`|

---

### **تعريف C-Strings**

C-string عبارة عن **مصفوفة من الأحرف** يتم إنهاؤها تلقائيًا برمز **`'\0'`**.  
مثال:

```cpp
#include <iostream>
using namespace std;

int main() {
    char str1[] = "Hello";  // يتم تلقائيًا إضافة '\0' في النهاية
    char str2[] = {'H', 'e', 'l', 'l', 'o', '\0'};  // نفس الشيء لكن بإضافة '\0' يدويًا

    cout << "str1: " << str1 << endl;
    cout << "str2: " << str2 << endl;

    return 0;
}
```

✅ **ملاحظات:**

- عند تعريف C-string باستخدام **علامات الاقتباس** `"Hello"`، يضيف المترجم تلقائيًا `'\0'` في النهاية.
    
- إذا حددت الأحرف داخل `{}`، **يجب عليك إضافة `'\0'` يدويًا** وإلا فلن يتم التعرف على نهاية النص.
    

---

### **استخدام مكتبة `<cstring>`**

توفر **مكتبة `<cstring>`** مجموعة من **الدوال المخصصة للتعامل مع C-strings**، مثل:

|الدالة|الوظيفة|
|---|---|
|`strlen(str)`|حساب طول النص بدون `'\0'`|
|`strcpy(dest, src)`|نسخ النص من `src` إلى `dest`|
|`strcat(dest, src)`|دمج النص `src` مع `dest`|
|`strcmp(str1, str2)`|مقارنة نصين (`0` إذا كانا متطابقين)|

📌 **مثال عملي على دوال `<cstring>`:**

```cpp
#include <iostream>
#include <cstring>  // تضمين مكتبة التعامل مع C-strings

using namespace std;

int main() {
    char str1[20] = "Hello";
    char str2[20] = " World";

    strcat(str1, str2); // دمج النصوص
    cout << "Merged string: " << str1 << endl; 

    cout << "Length: " << strlen(str1) << endl; // حساب الطول

    return 0;
}
```

🔹 **مخرجات البرنامج:**

```
Merged string: Hello World
Length: 11
```

---

### **ملحوظات هامة عن C-strings**

1️⃣ **C-strings ذات حجم ثابت** → لا يمكن تغيير طولها بعد تعريفها.  
2️⃣ **يجب أن تنتهي دائمًا بـ `'\0'`** → وإلا ستؤدي إلى أخطاء عند معالجتها.  
3️⃣ **عند نسخ النصوص أو دمجها، تأكد من وجود مساحة كافية** → تجنب الكتابة خارج حدود المصفوفة.

---

# 📝 طرق إنشاء النصوص (`string`) في C++**

📌 **1. إنشاء نص فارغ (Empty String)**

- عند تعريف `string` بدون تهيئة، يتم إنشاؤه كنص فارغ (`""`).
    
    ```cpp
    string s1; // s1 = ""
    ```
    

📌 **2. إنشاء نص بقيمة (`String Constant`)**

- يمكن تعيين قيمة مباشرة للنص أثناء التهيئة.
    
    ```cpp
    string s2 = "Hello";
    ```
    

📌 **3. إنشاء نص من نص آخر (`Copy Constructor`)**

- يمكن إنشاء نص جديد بنفس محتوى نص موجود مسبقًا.
    
    ```cpp
    string s3(s2); // s3 = نفس محتوى s2
    ```
    

🔹 **ملحوظات:**

- جميع الطرق تعتمد على **المكتبة `<string>`**، لذا يجب تضمينها في البرنامج.
    
- النصوص في C++ **ديناميكية**، أي يمكن تغيير طولها أثناء التشغيل.
    
---
### 📝 إنشاء النصوص (`string`) باستخراج جزء منها في C++**

📌 **1. إنشاء نص يحتوي على جزء من نص آخر**

- يمكن إنشاء `string` جديد يحتوي على **عدد معين من الأحرف** من نص آخر، بدءًا من موقع معين.
    
    ```cpp
    string str(other_string, position, count);
    ```
    
- **إذا لم يتم تحديد `count`**، فسيتم نسخ جميع الأحرف **من `position` حتى نهاية النص**.
    

---

### **📌 أمثلة عملية**

#### ✅ **مثال 1: استخراج عدد محدد من الأحرف**

```cpp
string s2("abcdef");  
string s4(s2, 3, 2); // يبدأ من index = 3 ويأخذ حرفين  
cout << s4 << endl;  // النتيجة: "de"
```

#### ✅ **مثال 2: استخراج جميع الأحرف من موقع معين حتى النهاية**

```cpp
string s5(s2, 1); // يبدأ من index = 1 ويأخذ باقي الأحرف  
cout << s5 << endl;  // النتيجة: "bcdef"
```

---

### **📌 أمثلة باستخدام جمل أطول**

#### ✅ **مثال 3: استخراج كلمات من جملة طويلة**

```cpp
string Str1 = "YOU ARE WELCOME!";

string Str2(Str1, 8, 7); // يبدأ من index = 8 ويأخذ 7 أحرف
cout << Str2 << endl;  // النتيجة: "WELCOME"

string Str3(Str1, 8);  // يبدأ من index = 8 ويأخذ باقي الأحرف
cout << Str3 << endl;  // النتيجة: "WELCOME!"

string Str5("YOU ARE WELCOME!", 8, 7);  
cout << Str5 << endl;  // النتيجة: "WELCOME"

string Str4("YOU ARE WELCOME!", 3);  
cout << Str4 << endl;  // النتيجة: "YOU"
```

---

### **📌 ملخص استخدام `string(other_string, position, count)`**

|الكود|النتيجة|
|---|---|
|`string s4(s2, 3, 2);`|`"de"`|
|`string s5(s2, 1);`|`"bcdef"`|
|`string Str2(Str1, 8, 7);`|`"WELCOME"`|
|`string Str3(Str1, 8);`|`"WELCOME!"`|
|`string Str5("YOU ARE WELCOME!", 8, 7);`|`"WELCOME"`|
|`string Str4("YOU ARE WELCOME!", 3);`|`"YOU"`|

---

## 📝 **ملخص العمليات على النصوص (`string`) في C++**

### **📌 1. الإسناد (`=`)**

يمكن تعيين قيمة متغير `string` لمتغير آخر باستخدام `=`، حيث يتم **نسخ** محتوى النص.

```cpp
string s1;
string s2 = "Hello";
s1 = s2; // الآن s1 تحتوي على "Hello"
```

---

### **📌 2. دمج النصوص (`Concatenation +`)**

يمكن دمج (`concatenate`) نصين باستخدام `+`، ولكن **يجب أن يكون أحد العوامل على الأقل من نوع `string`**.

✅ **مثال صحيح:**

```cpp
string s1("abc");
string s2("def");
string s3;
s3 = s1 + s2;  
cout << s3 << endl;  // النتيجة: "abcdef"
```

✅ **مثال آخر مع `cout`:**

```cpp
string s("Good morning ");
cout << s + "mister X" + '!' << endl;  // النتيجة: "Good morning mister X!"
```

❌ **خطأ شائع:**

```cpp
cout << "Good morning " + "mister X"; // ❌ خطأ! لأن كلا المعاملين نصيان عاديان وليس كائن `string`
```

🔹 **السبب:** لا يمكن دمج (`+`) سلسلتين نصيتين (`""`) مباشرة، ولكن يمكن تجاوز المشكلة بجعل أحدهما `string`:

```cpp
cout << string("Good morning ") + "mister X"; // ✅ صحيح
```

---

### **📌 ملخص سريع للعمليات على `string`**

|العملية|الوصف|مثال|
|---|---|---|
|`=`|نسخ محتوى `string` إلى متغير آخر|`s1 = s2;`|
|`+`|دمج (`concatenate`) نصوص|`s3 = s1 + s2;`|
|`"text" + "text"`|❌ غير مسموح|`cout << "Hello" + "World"; // خطأ!`|

---

### **📌 1. الإضافة (`Append +=`)**

يمكنك إضافة (`append`) محتوى `string` آخر إلى النص الأصلي باستخدام `+=`.

✅ **مثال:**

```cpp
string s1("abc");
string s2("def");
s1 += s2;  
cout << s1 << endl;  // النتيجة: "abcdef"
```

📌 **الملاحظة:** العملية **تعدل النص الأول (`s1`)** بإضافة محتوى `s2` إليه.

---

### **📌 2. الفهرسة (`Indexing []`)**

يمكن الوصول إلى **أحرف النصوص** أو تعديلها باستخدام `[]`، حيث أن الفهرسة تبدأ من **الصفر (`0`)**.

✅ **مثال على قراءة قيمة حرف معين:**

```cpp
string s("def");
char c = s[2];  
cout << c << endl;  // النتيجة: 'f'
```

✅ **مثال على تعديل النص باستخدام الفهرسة:**

```cpp
s[0] = s[1];  
cout << s << endl;  // النتيجة: "eef"
```

📌 **الملاحظة:** يتم تغيير **الحرف الأول (`s[0]`) ليصبح مثل الحرف الثاني (`s[1]`)**.

---

### **📌 ملخص سريع للعمليات**

|العملية|الوصف|مثال|النتيجة|
|---|---|---|---|
|`+=`|إلحاق (`append`) نص إلى متغير `string`|`s1 += s2;`|`s1` يحتوي على `"abcdef"`|
|`[]`|الوصول إلى حرف معين في النص|`char c = s[2];`|`c = 'f'`|
|`[]`|تعديل حرف معين في النص|`s[0] = s[1];`|`s = "eef"`|

---
# 📝 **ملخص الدوال الخاصة بالنصوص (`string`) في C++**

### **📌 1. إرجاع طول النص (`length()` و `size()`)**

🔹 **الدالتان `length()` و `size()` متطابقتان تمامًا** وتُرجعان طول النص بعدد الأحرف.

✅ **مثال:**

```cpp
string S = "Hello";
cout << S.length() << endl;  // النتيجة: 5
cout << S.size() << endl;    // النتيجة: 5 (نفس `length()`)
```

---

### **📌 2. مسح محتوى النص (`clear()`)**

🔹 **الدالة `clear()` تقوم بحذف جميع الأحرف في النص، مما يجعله نصًا فارغًا (`""`).**  
✅ **مثال:**

```cpp
string S = "Hello";
S.clear();  
cout << "Length: " << S.length() << endl;  // النتيجة: 0
```

---

### **📌 3. التحقق مما إذا كان النص فارغًا (`empty()`)**

🔹 **الدالة `empty()` تُرجع `true` إذا كان النص فارغًا، و`false` خلاف ذلك.**

✅ **مثال:**

```cpp
string S = "";
if (S.empty()) {
    cout << "The string is empty!" << endl;
}
```

🔹 **بعد استخدام `clear()` يصبح النص فارغًا أيضًا، لذا `empty()` ستُرجع `true` في هذه الحالة.**

---

### **📌 ملخص سريع للدوال**

|الدالة|الوصف|مثال|النتيجة|
|---|---|---|---|
|`length()`|تُرجع عدد الأحرف في النص|`S.length()`|`5`|
|`size()`|نفس `length()`|`S.size()`|`5`|
|`clear()`|تحذف محتوى النص|`S.clear();`|`S = ""`|
|`empty()`|تُرجع `true` إذا كان النص فارغًا، و`false` خلاف ذلك|`S.empty()`|`true` إذا كان `S = ""`|

---

