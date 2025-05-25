## 🟢 **General Questions about Binary Files**

### a) What are the advantages of Binary Files?

- Faster read/write operations compared to text files.
    
- Less memory/storage usage as data is stored in raw format.
    
- Supports random access using file pointers.
    
- Suitable for storing structured data like objects and records.
    

### b) What are the differences between Text and Binary Files?

|Feature|Text Files|Binary Files|
|---|---|---|
|Format|Human-readable|Machine-readable|
|Size|Larger|Smaller|
|Processing|Slower|Faster|
|Editing|Editable with text editors|Not readable or editable with normal editors|
|Use Case|For documents and readable data|For structured data like records, media|

---

## 🟦 **Parts Data Handling**

**Given**: Text file `PartData.txt` contains data in the following format:  
`PartNo PartName Marks10 Quantity Description`

### Tasks:

1. Create a **binary file** `Part.dat` that reads from `PartData.txt`.
    
2. Read and output the data from `Part.dat`.
    
3. Move the **get pointer** to Byte No. 100 from the beginning of the file.
    
4. Move the **put pointer** to the **end** of the file.
    
### Solution : [Parts Data Handling - C++ Code with Full Explanation](Parts%20Data%20Handling%20-%20C++%20Code%20with%20Full%20Explanation.md)

---

## 🟩 **Student Data - Random Access Binary File**

**Given**: Text file `students.txt` contains data:  
`ID FirstName LastName GPA`

### Tasks:

1. Create a **random access binary file** `students.dat` so that each student's data is written at the location specified by their **ID**.
    
2. Read and output all the data from `students.dat`.
    
3. Output the data of a **certain student** using their ID.
    
4. **Update** the **GPA** of a certain student using their ID.
    
5. Output the **size** of the file `students.dat`.
    

---

## 🟨 **Student Data with Deletion Operation**

(Same file format: `ID FirstName LastName GPA`)

### Additional Task:

6. **Delete** a student using their ID (for example, by overwriting their record with a blank/empty record or marking as deleted).
    

---

## 🟥 **Employee Data Handling**

**Given**: Text file `employee.txt` contains data:  
`EmpID Marks10 EmpName DeptID Salary`

### Tasks:

1. Create a binary file `employee.dat` that reads from `employee.txt`.
    
2. Read and output the data from `employee.dat`.
    
3. Move the **get pointer** to Byte No. 500 from the beginning of the file.
    
4. Move the **put pointer** to the **end** of the file.
    

---

هل ترغب أن أكتب لك الأكواد بلغة ++C الخاصة بكل سؤال أيضًا؟