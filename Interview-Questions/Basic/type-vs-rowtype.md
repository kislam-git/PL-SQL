
# ❓ What is the Difference Between `%TYPE` and `%ROWTYPE` in PL/SQL?

---

## ✅ Answer:

In PL/SQL, `%TYPE` and `%ROWTYPE` are **attribute declarations** used to define variables based on the **data types of database columns** or **entire rows**.

They ensure **data consistency**, reduce hardcoding, and automatically adapt to changes in table structures.

---

## 🔍 %TYPE

- Declares a variable with the **same data type** as a **single column** or another variable.
- Helps avoid manual datatype declarations.

```plsql
DECLARE
   v_salary employees.salary%TYPE;
```

✔️ `v_salary` has the **same data type** as the `salary` column in the `employees` table.

---

## 🔍 %ROWTYPE

- Declares a **record variable** that holds **an entire row** from a table or cursor.
- Each field in the record corresponds to a column in the row.

```plsql
DECLARE
   v_emp_record employees%ROWTYPE;
```

✔️ `v_emp_record` contains fields like:
- `v_emp_record.employee_id`
- `v_emp_record.first_name`
- `v_emp_record.salary`  
... and all other columns of the `employees` table.

---

## 🆚 Key Differences

| Feature       | `%TYPE`                                  | `%ROWTYPE`                                   |
|---------------|-------------------------------------------|----------------------------------------------|
| Scope         | Refers to a **single column**             | Refers to an **entire row**                  |
| Use Case      | Declare individual variables              | Declare a record with multiple columns       |
| Syntax        | `var_name table.column%TYPE`              | `record_name table_name%ROWTYPE`             |
| Example       | `v_name employees.first_name%TYPE`        | `v_emp employees%ROWTYPE`                    |

---

## 🧠 When to Use

- Use **%TYPE** when you want to work with a **single column value**, like salary or name.
- Use **%ROWTYPE** when you need to **fetch or store a full row**, such as inside a SELECT * INTO operation.

---

## 🎯 Real-World Use Case

```plsql
DECLARE
   v_dept_id   departments.department_id%TYPE;
   v_dept_row  departments%ROWTYPE;
BEGIN
   -- Fetch a single column using %TYPE
   SELECT department_id INTO v_dept_id
   FROM departments
   WHERE department_name = 'HR';

   -- Fetch an entire row using %ROWTYPE
   SELECT * INTO v_dept_row
   FROM departments
   WHERE department_id = v_dept_id;

   DBMS_OUTPUT.PUT_LINE('Department Name: ' || v_dept_row.department_name);
END;
```

---

✅ Summary:
- `%TYPE` = Single column’s datatype  
- `%ROWTYPE` = Entire row structure  
- Both are great for **maintainability** and **consistency** in PL/SQL code

```
