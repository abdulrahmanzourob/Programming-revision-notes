الكود التالي يحتوي على **خطأ برمجي** بسيط في النوع (Type Error). دعنا نشرح السبب وكيف نصححه:

---

## ✅ الكود:

```cpp
int x;
outFile.write(&x, sizeof(x));
```

---

## ❌ الخطأ:

دالة `write` في C++ لديها الصيغة التالية:

```cpp
ostream& write(const char* buffer, streamsize size);
```

لكن في السطر:

```cpp
outFile.write(&x, sizeof(x));
```

- `&x` هو مؤشر من نوع `int*`، **لكن write تحتاج إلى مؤشر من نوع `char*` أو `const char*`**.
    
- النتيجة: ❌ **Type mismatch** – محاولة تمرير `int*` بدلًا من `char*`.
    

---

## ✅ التصحيح:

نحتاج إلى تحويل العنوان إلى `char*` باستخدام **casting**:

```cpp
outFile.write((char*)&x, sizeof(x));
```

---

## ✅ شرح التصحيح:

- `(char*)&x` يحوّل عنوان المتغير `x` إلى نوع `char*`.
    
- `sizeof(x)` يحسب عدد البايتات التي يحتاجها `x` (عادة 4 بايت على الأنظمة الحديثة).
    

---

## 💡 مثال كامل:

```cpp
#include <fstream>
using namespace std;

int main() {
    ofstream outFile("output.bin", ios::binary);
    int x = 123;
    outFile.write((char*)&x, sizeof(x));
    outFile.close();
    return 0;
}
```

---

## ✅ متى نستخدم هذه الطريقة؟

عند كتابة بيانات **ثنائية (binary)** إلى الملف مثل:

- متغيرات فردية (`int`, `float`, `double`, `struct`, ...)
    
- مصفوفات أو كائنات كاملة دفعة واحدة
    

---

هل تحب أيضًا مثال على **قراءة هذا المتغير** مرة أخرى من الملف؟