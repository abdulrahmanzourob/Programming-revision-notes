### **1. برنامج لتحويل أول حرف من كل كلمة إلى حرف كبير (Capital)**

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str;
    cout << "Enter a string: ";
    getline(cin, str);

    bool capitalize = true;
    for (int i = 0; i < str.length(); i++) {
        if (str[i] == ' ') {
            capitalize = true; // الكلمة التالية تبدأ بعد فراغ
        } else if (capitalize && isalpha(str[i])) {
            str[i] = toupper(str[i]);
            capitalize = false;
        }
    }

    cout << "Capitalized string: " << str << endl;
    return 0;
}
```


## **1. برنامج تحويل أول حرف من كل كلمة إلى حرف كبير**

### ✅ الهدف:

تحويل أول حرف من كل كلمة في الجملة إلى **حرف كبير (capital)**، والكلمات مفصولة بمسافة واحدة فقط.

### 🔍 شرح الكود:

```cpp
bool capitalize = true;
```

- متغير يستخدم لتحديد متى يجب أن نقوم بتحويل الحرف إلى حرف كبير.
    

```cpp
for (int i = 0; i < str.length(); i++) {
```

- حلقة تمر على كل حرف في السلسلة.
    

```cpp
if (str[i] == ' ') capitalize = true;
```

- إذا وجدنا فراغًا، نحدد أن الكلمة التالية يجب أن يبدأ أول حرف منها بحرف كبير.
    

```cpp
else if (capitalize && isalpha(str[i])) {
    str[i] = toupper(str[i]);
    capitalize = false;
}
```

- إذا كنا في بداية كلمة (`capitalize = true`) وكان الحرف حرفًا (وليس رقمًا أو رمزا)، نقوم بتحويله إلى حرف كبير.
    


---

### **2. برنامج لحساب عدد الحروف المتحركة (vowels) في السلسلة**

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string str;
    cout << "Enter a string: ";
    getline(cin, str);

    int vowelCount = 0;
    for (char c : str) {
        c = tolower(c);
        if (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u') {
            vowelCount++;
        }
    }

    cout << "Number of vowels: " << vowelCount << endl;
    return 0;
}
```

## **2. برنامج عد الحروف المتحركة (vowels)**

### ✅ الهدف:

عد عدد الحروف المتحركة في سلسلة. الحروف المتحركة هي: `a, e, i, o, u`.

### 🔍 شرح الكود:

```cpp
for (char c : str) {
    c = tolower(c);
```

- تمر على كل حرف في السلسلة وتحوله إلى حرف صغير لتسهيل المقارنة.
    

```cpp
if (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u')
    vowelCount++;
```

- إذا كان الحرف أحد الحروف المتحركة، نزيد العداد `vowelCount`.
    

---

### **3. برنامج لطباعة كل الكلمات التي تبدأ بحرف معين**

```cpp
#include <iostream>
#include <string>
#include <sstream>
using namespace std;

int main() {
    string str;
    char target;
    cout << "Enter a string: ";
    getline(cin, str);

    cout << "Enter the starting character: ";
    cin >> target;
    target = tolower(target);

    stringstream ss(str);
    string word;

    cout << "Words starting with '" << target << "':" << endl;
    while (ss >> word) {
        if (tolower(word[0]) == target) {
            cout << word << endl;
        }
    }

    return 0;
}
```

---

هل ترغب أن أجمع هذه البرامج في ملف واحد وتُعرض للمستخدم في شكل قائمة خيارات؟