الكود:

```cpp
inFile.seekg(50L, ios::end);
```

---

## شرح الكود:

- `seekg` هي دالة تستخدم لتحريك مؤشر القراءة (get pointer) في ملف إدخال (`ifstream` أو `fstream`).
    
- الوسيط الأول `50L` هو عدد البايتات التي سيتم تحريك المؤشر بها.
    
- الوسيط الثاني `ios::end` يعني أن التحريك يتم **بالنسبة لنهاية الملف**.
    

---

## ❌ هل هذا الكود صحيح؟

من الناحية النحوية، الكود **صحيح**.

لكن عمليًا، تحريك المؤشر بـ `50` بايت **بعد نهاية الملف** هو **غير منطقي**.

---

## ماذا يعني؟

- `seekg(50L, ios::end)` يحرك مؤشر القراءة **إلى ما بعد نهاية الملف بمقدار 50 بايت**.
    
- هذا يجعل مؤشر القراءة يشير إلى موقع غير موجود في الملف (خارج حدوده).
    
- هذا قد يؤدي إلى فشل عمليات القراءة أو تعطي نتائج غير متوقعة.
    

---

## ✅ الاستخدام الصحيح:

إذا تريد تحريك المؤشر **إلى 50 بايت قبل نهاية الملف**، استخدم قيمة سالبة:

```cpp
inFile.seekg(-50L, ios::end);
```

---

## ملخص:

|الكود|النتيجة|
|---|---|
|`inFile.seekg(50L, ios::end);`|المؤشر بعد نهاية الملف (غير صحيح عمليًا)|
|`inFile.seekg(-50L, ios::end);`|المؤشر يقع قبل نهاية الملف بـ 50 بايت (صحيح)|

