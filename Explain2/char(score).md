

```cpp
int score[] = {50, 80, 100, 90};
outFile.write(score, sizeof(score));  // ❌
```

---

### 🔧 التصحيح باستخدام نفس طريقتك (`(char*)&`):

نطبق نفس الفكرة، لكن على المصفوفة `score`:

```cpp
int score[] = {50, 80, 100, 90};
outFile.write((char*)&score, sizeof(score));  // ✅
```

أو الأفضل توضيحًا:

```cpp
outFile.write((char*)score, sizeof(score));
```

---

### ✅ الشرح:

- `score` هو اسم مصفوفة، أي أنه بمثابة **مؤشر لأول عنصر**.
    
- `(char*)score` أو `(char*)&score[0]` يقوم بتحويل العنوان من نوع `int*` إلى `char*`، وهو المطلوب لدالة `write`.
    
- `sizeof(score)` يعطي **حجم كامل المصفوفة بالبايتات**، أي `عدد العناصر × حجم كل عنصر`.
    

---

### 📌 مثال كامل:

```cpp
#include <fstream>
using namespace std;

int main() {
    ofstream outFile("data.bin", ios::binary);
    
    int score[] = {50, 80, 100, 90};
    
    outFile.write((char*)score, sizeof(score));
    
    outFile.close();
    return 0;
}
```

---

### ❗ ملاحظات مهمة:

- تأكد دائمًا من فتح الملف بوضع `ios::binary` عند الكتابة الثنائية.
    
- استخدم نفس الحجم عند القراءة لاحقًا حتى تسترجع البيانات بشكل صحيح.
    
- هذه الطريقة تعمل فقط مع **أنواع البيانات البسيطة (Plain Old Data)**، وليست آمنة مع أنواع تحتوي مؤشرات أو ديناميكية.
    

---

هل تحب أشرح كيف تقرأ نفس البيانات باستخدام `ifstream.read()`؟