## **C-Strings ومعالجة النصوص في C++**

### **1. ما هي C-Strings؟**

في لغة C++، هناك نوعان رئيسيان من النصوص (Strings):

- **C-Strings** وهي الطريقة القديمة المستخدمة في لغة C، حيث يتم تمثيل النصوص كمصفوفة من الأحرف تنتهي بالقيمة `'\0'` (null character).
    
- **std::string** وهي الطريقة الحديثة المقدمة في C++، والتي توفر وظائف متقدمة وأسهل في التعامل.
    

### **2. تعريف C-Strings**

C-String هي مصفوفة من الأحرف تنتهي دائمًا بالرمز `'\0'` (null character) للإشارة إلى نهاية النص. مثال على تعريف C-String:

```cpp
#include <iostream>

int main() {
    char text[] = "Hello";
    std::cout << text << std::endl; // طباعة النص
    return 0;
}
```

في هذا المثال:

- يتم تخزين النص `"Hello"` في مصفوفة من الأحرف.
    
- يتم تخصيص حرف `'\0'` تلقائيًا في النهاية.
    

### **3. تعريف C-String باستخدام المؤشر `char*`**

يمكنك تعريف C-String باستخدام مؤشر `char*` كما يلي:

```cpp
#include <iostream>

int main() {
    char* text = (char*)"Hello";
    std::cout << text << std::endl;
    return 0;
}
```

⚠ **ملاحظة**: منذ C++11، استخدام `(char*)` لتحويل النصوص النصية المباشرة يعتبر غير آمن، ومن الأفضل استخدام `const char*` كما يلي:

```cpp
const char* text = "Hello";
```

### **4. إدخال وإخراج C-Strings**

#### **الإدخال باستخدام `cin`**

```cpp
#include <iostream>

int main() {
    char name[20];
    std::cout << "Enter your name: ";
    std::cin >> name;
    std::cout << "Hello, " << name << "!" << std::endl;
    return 0;
}
```

⚠ **مشكلة `cin` مع C-Strings**:

- `cin` لا يأخذ إلا كلمة واحدة ويتوقف عند المسافة.
    

#### **إدخال سطر كامل باستخدام `cin.getline`**

لحل المشكلة السابقة يمكن استخدام `cin.getline`:

```cpp
#include <iostream>

int main() {
    char name[50];
    std::cout << "Enter your full name: ";
    std::cin.getline(name, 50);
    std::cout << "Hello, " << name << "!" << std::endl;
    return 0;
}
```

### **5. دوال التعامل مع C-Strings**

C++ توفر مجموعة من الدوال داخل مكتبة `<cstring>` لمعالجة النصوص.

#### **(1) `strlen` - إيجاد طول النص**

```cpp
#include <iostream>
#include <cstring>

int main() {
    char text[] = "Hello, World!";
    std::cout << "Length: " << strlen(text) << std::endl;
    return 0;
}
```

✦ **`strlen` لا يحسب `'\0'` ضمن الطول.**

#### **(2) `strcpy` - نسخ النصوص**

```cpp
#include <iostream>
#include <cstring>

int main() {
    char source[] = "Hello";
    char destination[10];
    
    strcpy(destination, source);
    
    std::cout << "Copied String: " << destination << std::endl;
    return 0;
}
```

⚠ **تحذير**: تأكد أن `destination` لديه مساحة كافية لتجنب تجاوز الحدود.

#### **(3) `strncpy` - نسخ النصوص بأمان**

```cpp
#include <iostream>
#include <cstring>

int main() {
    char source[] = "Hello";
    char destination[10];

    strncpy(destination, source, sizeof(destination) - 1);
    destination[sizeof(destination) - 1] = '\0'; // ضمان انتهاء النص بـ '\0'

    std::cout << "Copied String: " << destination << std::endl;
    return 0;
}
```

✦ `strncpy` ينسخ عدد محدد من الأحرف لمنع التجاوز.

#### **(4) `strcmp` - مقارنة النصوص**

```cpp
#include <iostream>
#include <cstring>

int main() {
    char str1[] = "apple";
    char str2[] = "banana";

    if (strcmp(str1, str2) == 0)
        std::cout << "Strings are equal" << std::endl;
    else if (strcmp(str1, str2) < 0)
        std::cout << "str1 is less than str2" << std::endl;
    else
        std::cout << "str1 is greater than str2" << std::endl;

    return 0;
}
```

✦ `strcmp` يقارن النصوص وفقًا للترتيب القاموسي.

#### **(5) `strcat` - دمج النصوص**

```cpp
#include <iostream>
#include <cstring>

int main() {
    char str1[20] = "Hello, ";
    char str2[] = "World!";
    
    strcat(str1, str2);

    std::cout << "Concatenated String: " << str1 << std::endl;
    return 0;
}
```

⚠ **يجب التأكد من وجود مساحة كافية في `str1` لاستيعاب `str2`.**

#### **(6) `strchr` - البحث عن حرف**

```cpp
#include <iostream>
#include <cstring>

int main() {
    char text[] = "Hello, World!";
    char* result = strchr(text, 'W');

    if (result != nullptr)
        std::cout << "Character found at position: " << (result - text) << std::endl;
    else
        std::cout << "Character not found" << std::endl;

    return 0;
}
```

✦ `strchr` يعيد مؤشرًا إلى أول تكرار للحرف في النص.

#### **(7) `strstr` - البحث عن نص فرعي**

```cpp
#include <iostream>
#include <cstring>

int main() {
    char text[] = "Hello, World!";
    char* result = strstr(text, "World");

    if (result != nullptr)
        std::cout << "Substring found at position: " << (result - text) << std::endl;
    else
        std::cout << "Substring not found" << std::endl;

    return 0;
}
```

✦ `strstr` يبحث عن نص فرعي داخل النص الأصلي.

### **6. استخدام `std::string` بدلاً من C-Strings**

نظرًا لتعقيدات التعامل مع C-Strings، يفضل استخدام `std::string`:

```cpp
#include <iostream>
#include <string>

int main() {
    std::string str1 = "Hello";
    std::string str2 = "World";

    std::string result = str1 + ", " + str2 + "!";
    std::cout << result << std::endl;

    return 0;
}
```

✦ `std::string` يسهل التعامل مع النصوص ويقلل الأخطاء.

### **الخلاصة**

- **C-Strings** عبارة عن مصفوفة من الأحرف تنتهي بـ `'\0'`.
    
- **يجب الحذر من تجاوز سعة المصفوفة عند النسخ أو الدمج**.
    
- **مكتبة `<cstring>` توفر دوال قوية لمعالجة C-Strings**.
    
- **يفضل استخدام `std::string` في C++ لتجنب مشاكل الذاكرة والتعامل اليدوي مع النصوص**.
    

🚀 **باستخدام هذه الدوال والمفاهيم، يمكنك التعامل مع النصوص في C++ بكفاءة!**