الكود التالي:

```cpp
string fileName;
cout << "Enter the input file name: ";
cin >> fileName;
infile.open(fileName);
```

يبدو **نحويًا صحيحًا**، ولكن فيه **نقطة خطأ منطقية أو تصميمية** قد تسبب مشاكل عند التنفيذ.

---

## ✅ ما الذي يفعله الكود؟

- يطلب من المستخدم إدخال اسم ملف.
    
- يفتح الملف بهذا الاسم لاستخدامه كملف إدخال (`ifstream infile` يجب أن تكون مُعلنة سابقًا).
    

---

## ❌ الخطأ أو المشكلة:

### 1. `fileName` هو متغير من النوع `string`، بينما `ifstream::open()` يتطلب:

- `const char*` (أي سلسلة نصية C-style)
---
###  ✅ التصحيح

```cpp
infile.open(fileName.c_str()); // تحويل string إلى const char*
```
