## 🟦 أولًا: **البحث Search**

|   # | Statement                                                  | True/False | Explanation                                                                 | More explanation                                              |
| --: | ---------------------------------------------------------- | ---------- | --------------------------------------------------------------------------- | ------------------------------------------------------------- |
|   1 | Sequential Search is inefficient for large lists.          | ✅ **True** | لأنه يفحص كل عنصر حتى يجد الهدف، وبالتالي بطيء في القوائم الكبيرة (`O(n)`). | [Sequential Search is inefficient for large lists.](explain/Sequential%20Search%20is%20inefficient%20for%20large%20lists..md)         |
|  21 | A binary search of a list assumes that the list is sorted. | ✅ **True** | Binary Search لا يعمل إلا على القوائم المرتبة.                              | [A binary search of a list assumes that the list is sorted](explain/A%20binary%20search%20of%20a%20list%20assumes%20that%20the%20list%20is%20sorted.md) |

---

## 🟦 ثانيًا: **ملفات (File Handling)**

|   # | Statement                                                                                   | True/False  | Explanation                                                                   | More explanation                                                                                                                                                                      |
| --: | ------------------------------------------------------------------------------------------- | ----------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|   2 | Write function transfers a given number of bytes from memory to a file.                     | ✅ **True**  | هذا هو دور دالة الكتابة في الملفات الثنائية (binary files).                   | [Write function transfers a given number of bytes from memory to a file.](explain/Write%20function%20transfers%20a%20given%20number%20of%20bytes%20from%20memory%20to%20a%20file..md) |
|   3 | fstream may be used for both input and output streams.                                      | ✅ **True**  | يمكن استخدام `fstream` مع `ios::in` و `ios::out`.                             |                                                                                                                                                                                       |
|   4 | fstream may be used only for input.                                                         | ❌ **False** | `ifstream` فقط للقراءة، أما `fstream` فلكلا الاتجاهين (read/write).           |                                                                                                                                                                                       |
|   5 | When specifying a file at runtime, the argument to `open()` must be a C-string.             | ✅ **True**  | دالة `open()` في C++ تتطلب `const char*` (C-string).                          | [Write function transfers a given number of bytes from memory to a file.](explain/Write%20function%20transfers%20a%20given%20number%20of%20bytes%20from%20memory%20to%20a%20file..md) |
|   6 | Random file access is associated with a file pointer.                                       | ✅ **True**  | نستخدم المؤشر لتحديد مكان القراءة أو الكتابة داخل الملف.                      | [Random file access is associated with a file pointer.](explain/Random%20file%20access%20is%20associated%20with%20a%20file%20pointer..md)                                             |
|   7 | File pointer is different from the pointers we have used in arrays.                         | ✅ **True**  | مؤشرات الملفات تتحكم في موقع القراءة/الكتابة، وليست مؤشرات بيانات في الذاكرة. | [File pointer is different from the pointers we have used in arrays.](explain/File%20pointer%20is%20different%20from%20the%20pointers%20we%20have%20used%20in%20arrays..md)           |
|   8 | By default, a file is opened as a text file.                                                | ✅ **True**  | يجب تحديد `ios::binary` لفتح الملف كملف ثنائي.                                | [By default, a file is opened as a text file](explain/By%20default,%20a%20file%20is%20opened%20as%20a%20text%20file.md)                                                               |
|   9 | Binary file access is faster and more compact than text file access.                        | ✅ **True**  | الملفات الثنائية لا تحتوي على تنسيقات، لذا أسرع وأكثر ضغطًا.                  | [Binary file access is faster and more compact than text file access.](explain/Binary%20file%20access%20is%20faster%20and%20more%20compact%20than%20text%20file%20access..md)         |
|  10 | Data in a text file is called formatted data, while in a binary file it is called raw data. | ✅ **True**  | الملفات النصية تنسق البيانات (مثل تحويل الأرقام إلى نصوص).                    |                                                                                                                                                                                       |

---

## 🟦 ثالثًا: **السلاسل النصية (Strings and C-strings)**

|   # | Statement                                                                        | True/False | Explanation                                                              | More explanation                                                                     |
| --: | -------------------------------------------------------------------------------- | ---------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
|  11 | The one place C++ allows aggregate operations on arrays is the I/O of C-strings. | ✅ **True** | يمكن استخدام `cin` و `cout` مباشرة مع C-strings، بخلاف المصفوفات الأخرى. | [The one place C++ allows aggregate operations on arrays is the I-O of C-strings.](explain/The%20one%20place%20C++%20allows%20aggregate%20operations%20on%20arrays%20is%20the%20I-O%20of%20C-strings..md) |
|  12 | C-string is a one-dimensional array of characters terminated by `'\0'`.          | ✅ **True** | هذا هو تعريف الـ C-string.                                               |                                                                                      |
|  13 | getline() function discards the terminating character.                           | ✅ **True** | `getline()` تحذف نهاية السطر (`\n`) ولكن تبقي باقي السطر.                | [getline() function discards the terminating character.](explain/getline()%20function%20discards%20the%20terminating%20character..md)                           |
|  14 | >> cannot be used to read strings that contain blanks.                           | ✅ **True** | `cin >>` يتوقف عند أول فراغ أو تبويب.                                    |                                                                                      |
|  15 | Null character is less than any other character in the char data set.            | ✅ **True** | القيمة ASCII للـ `'\0'` هي 0، وهي أقل من أي حرف آخر.                     |                                                                                      |

---

## 🟦 رابعًا: **الاستدعاء الذاتي Recursion**

|   # | Statement                                                                            | True/False  | Explanation                                                  | More explanation                                                                         |
| --: | ------------------------------------------------------------------------------------ | ----------- | ------------------------------------------------------------ | ---------------------------------------------------------------------------------------- |
|  16 | When a function calls itself, a new copy of that function is run.                    | ✅ **True**  | كل استدعاء ذاتي يتم وضعه في Stack جديد.                      | [When a function calls itself, a new copy of that function is run.](explain/When%20a%20function%20calls%20itself,%20a%20new%20copy%20of%20that%20function%20is%20run..md)                    |
|  17 | Every recursive definition must have one (or more) base cases.                       | ✅ **True**  | بدون base case سيحدث infinite recursion.                     | [Every recursive definition must have one (or more) base cases.](explain/Every%20recursive%20definition%20must%20have%20one%20(or%20more)%20base%20cases..md)                       |
|  18 | Every recursive definition must have only one base case.                             | ❌ **False** | يمكن أن يكون هناك أكثر من base case.                         |                                                                                          |
|  19 | The base case for which an answer is explicitly known can be stated non-recursively. | ✅ **True**  | في الـ base case، لا حاجة لاستدعاء ذاتي.                     | [The base case for which an answer is explicitly known can be stated non-recursively.](explain/The%20base%20case%20for%20which%20an%20answer%20is%20explicitly%20known%20can%20be%20stated%20non-recursively..md) |
|  20 | The base case for which an answer is explicitly known can be stated recursively.     | ❌ **False** | الـ base case لا يُستخدم فيه recursion، بل هو نهاية التكرار. |                                                                                          |

---

## ✅ تقسيم العبارات حسب المواضيع:

|القسم|العبارات|
|---|---|
|البحث Search|1, 21|
|الملفات File Handling|2, 3, 4, 5, 6, 7, 8, 9, 10|
|السلاسل النصية Strings|11, 12, 13, 14, 15|
|الاستدعاء الذاتي Recursion|16, 17, 18, 19, 20|
نن
