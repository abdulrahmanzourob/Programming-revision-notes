### الجملة:

**Write function transfers a given number of bytes from memory to a file.**

### الترجمة:

**دالة `write` تنقل عددًا معينًا من البايتات من الذاكرة إلى ملف.**

---

### ✅ الجملة **صحيحة**.

---

### 📘 الشرح:

#### ما هي دالة `write` في C++؟

عند العمل مع **الملفات الثنائية (binary files)** في C++، نستخدم الدالة `write()` التابعة لكائنات `ofstream` أو `fstream` لكتابة **بيانات خام (raw data)** مباشرةً إلى ملف.

---

### 📌 الشكل العام:

```cpp
ofstream file("data.bin", ios::binary);
file.write(reinterpret_cast<char*>(pointer), number_of_bytes);
```

- `pointer`: يشير إلى موقع في الذاكرة يحتوي على البيانات.
    
- `number_of_bytes`: عدد البايتات التي سيتم نقلها.
    
- `reinterpret_cast<char*>`: لأن `write` تتعامل مع البيانات كـ C-strings أو raw bytes، نحتاج لتحويل المؤشر إلى نوع `char*`.
    

---

### 🧠 مثال عملي:

```cpp
int num = 123;
ofstream outFile("output.bin", ios::binary);
outFile.write(reinterpret_cast<char*>(&num), sizeof(num));
outFile.close();
```

- هذا المثال ينقل **4 بايت** (حجم `int`) من الذاكرة إلى الملف.
    

---

### 💡 الخلاصة:

- `write()` تنقل **عددًا محددًا من البايتات** من **الذاكرة الرئيسية (RAM)** إلى **ملف**.
    
- تُستخدم غالبًا مع **الملفات الثنائية**.
    
- لذلك الجملة **صحيحة** ✅.
    

هل تحب أشرح أيضًا دالة `read()` المقابلة لها؟