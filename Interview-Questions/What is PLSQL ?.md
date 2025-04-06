## ✅ 1. What is PL/SQL? How is it different from SQL?

### 🔷 What is PL/SQL?
**PL/SQL (Procedural Language/SQL)** is Oracle’s procedural extension to SQL. It combines the power of SQL with procedural programming features like:
- Variables
- Loops
- Conditions (IF, CASE)
- Functions and Procedures
- Exception Handling

It allows developers to write **modular, reusable, and efficient code blocks** for business logic and complex database operations.

---

### 🔷 What is SQL?
**SQL (Structured Query Language)** is a declarative language used to perform operations on data such as:
- Retrieving (`SELECT`)
- Modifying (`INSERT`, `UPDATE`, `DELETE`)
- Defining structures (`CREATE`, `ALTER`)

SQL cannot contain conditional logic or looping structures.

---

### 🔄 Key Differences Between SQL and PL/SQL

| Feature          | SQL                            | PL/SQL                                |
|------------------|--------------------------------|----------------------------------------|
| Type             | Declarative                    | Procedural                             |
| Execution        | One statement at a time        | Block of code (can contain many SQL statements) |
| Variables        | Not supported                  | Supported                              |
| Control Structures| Not available                 | Available (`IF`, `LOOP`, `WHILE`, etc.) |
| Error Handling   | Minimal                        | Robust error handling using `EXCEPTION` block |
| Use Cases        | Data access & manipulation     | Business logic, validations, transactions |

---

## 🚀 Example Use Case

### ✅ Task:
Give a **10% bonus** to all employees in the **SALES** department and **print** their updated salary.

---

### 🔸 SQL Example (Limited Logic)
  ```sql
  UPDATE employees
  SET salary = salary * 1.10
  WHERE department = 'SALES';
```
🧩 Limitation:
- Cannot perform row-by-row logic
- Cannot display output
- No exception handling

### 🔸 PL/SQL Example (Full Logic)
 ```PL/SQL
    DECLARE
     CURSOR c_sales_emp IS
        SELECT employee_id, salary FROM employees WHERE department = 'SALES';
     v_bonus_salary employees.salary%TYPE;
    BEGIN
       FOR emp IN c_sales_emp LOOP
          v_bonus_salary := emp.salary * 1.10;
          
          UPDATE employees
          SET salary = v_bonus_salary
          WHERE employee_id = emp.employee_id;
    
          DBMS_OUTPUT.PUT_LINE('Updated Salary for Emp ID ' || emp.employee_id || ': ' || v_bonus_salary);
       END LOOP;
    EXCEPTION
       WHEN OTHERS THEN
          DBMS_OUTPUT.PUT_LINE('Error: ' || SQLERRM);
    END;

```

🎯 Advantages of PL/SQL:
-  Looping through each employee
-  Performing row-level calculations
-  Printing messages using DBMS_OUTPUT
-  Exception handling

📌 Summary
  - Use SQL for simple data access or modifications.
  - Use PL/SQL for complex logic, conditions, loops, and modular code that encapsulates business rules.


