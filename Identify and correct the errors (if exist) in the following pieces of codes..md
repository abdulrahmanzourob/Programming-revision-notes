## 📁 أولاً: التعامل مع الملفات (File Handling)

### ✍️ كتابة بيانات إلى ملف باستخدام `write()`:

1. `int score[] = {50, 80, 100, 90}; outFile.write(score, sizeof(score));`
***Solution and explain :*** [char(score)](Explain2/char(score).md)
    
2. `int x; outFile.write(&x, sizeof(x));`
***Solution and explain :*** [(&x](Explain2/(&x.md)
    
3. `char letter[] = {'L', 'M', 'N', 'O'}; file.write((char*)&letter, sizeof(letter));`
***Solution and explain :*** [(char)&letter](Explain2/(char)&letter.md)
    
4. `char L = 'Z'; file.write(L, sizeof(L));`
***Solution***
```C++
file.write((char*)&L, sizeof(L));
```

    
5. `int num; outFile.write(&num, sizeof(num));`
***Solution***
```C++
outFile.write((char*)&num, sizeof(num));
```

---

### 📂 فتح الملفات:

1. `outFile.open("student.dat", ios::binary); // Opening a file for writing at end-of-file in binary mode`
***Solution and explain :*** [ios;app](Explain2/ios;app.md)
2. 
```C++
string fileName;
cout << "Enter the input file name: ";
cin >> fileName;
infile.open(fileName);
```
***Solution and explain :*** [c_str()](Explain2/c_str().md)

---

### 📌 تحريك مؤشر القراءة:

1. `inFile.seekg(50L, ios::end);`
***Solution and explain :*** [seekg](Explain2/seekg.md)
---

## 📁 ثانياً: السلاسل النصية (Strings & Character Arrays)

### ⚠️ محاولات إسناد String إلى مصفوفة `char`:

1. `char Name[26]; Name = " Mahmoud ";`
***Solution***
```C++
strcpy(Name, "Mahmoud");
```
    
2. 
```C++
char str1[20], str2[20] = "A string";
str1 = str2;
```
***Solution***
```C++
strcpy(str1, str2);
```
    
3. `char str[20]; cout << str.length();`
***Solution***
```C++
cout << strlen(str);  
```

---

### ✅ استخدام `string` مع `strlen`:

1. `string str1 = "Hello "; cout << strlen(str1);`
_(لاحظ أن `strlen()` تعمل فقط على `char[]` وليس على `string` مباشرة)_

***Solution***
```C++
cout << str1.length();
```

---

## 📁 ثالثاً: الإدخال (Input)

1. `cin.get() >> v1 >> v2;`
***Solution and explain :*** [cin.get()](Explain2/cin.get().md)
    
2. `Assume that Part is a variable of struct type (ParttID, ParttName, QTY)`
```C++
cin >> Part;
```
***Solution***
```C++
cin >> Part.PartID >> Part.PartName >> Part.QTY;
```


---

## 📁 رابعاً: الإخراج (Output)

1. `cout << "Welcome " + "Friends";`
***Solution***
```C++
cout << string("Welcome ") + "Friends";

cout << "Welcome " << "Friends";
```
---

## 📁 خامساً: التعداد (Enumerations) و الـ Struct

1. `enum GPA {'A', 'B', 'C', 'D', 'F'};`
***Solution***
```C++
enum GPA {A, B, C, D, F};
```
    
2. `Assume that popularSport; is a variable of an enumerated type sports`
`popularSport++;` 
***Solution***
```C++
popularSport = static_cast<sports>(static_cast<int>(popularSport) + 1);
```


[name of file](../Explain2/path)