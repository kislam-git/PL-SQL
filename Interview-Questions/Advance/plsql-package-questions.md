# 📦 Oracle PL/SQL Package Interview Questions and Answers

This document contains essential PL/SQL **package-related interview questions** with clear and concise answers. Ideal for both beginners and intermediate Oracle developers preparing for technical interviews.

---

## ❓ 1. What is a PL/SQL package? What are its components?

### ✅ Answer:

A **PL/SQL package** is a **named collection** of related procedures, functions, variables, cursors, and types stored together as a single unit. Packages help modularize and organize code for reuse and better maintenance.

**Components of a Package:**
- **Package Specification**: Declares public elements — procedures, functions, variables, etc.
- **Package Body**: Implements the logic for the items declared in the specification.

```plsql
-- Specification
CREATE OR REPLACE PACKAGE emp_pkg IS
   PROCEDURE show_salary(p_emp_id NUMBER);
END emp_pkg;

-- Body
CREATE OR REPLACE PACKAGE BODY emp_pkg IS
   PROCEDURE show_salary(p_emp_id NUMBER) IS
      v_salary employees.salary%TYPE;
   BEGIN
      SELECT salary INTO v_salary FROM employees WHERE employee_id = p_emp_id;
      DBMS_OUTPUT.PUT_LINE('Salary: ' || v_salary);
   END;
END emp_pkg;
```

---

## ❓ 2. What are the advantages of using packages in PL/SQL?

### ✅ Answer:

- ✅ **Modularity**: Related code is grouped in one logical unit.
- ✅ **Encapsulation**: Hide private logic inside the package body.
- ✅ **Reusability**: Public elements can be used across multiple programs.
- ✅ **Better Performance**: Loaded once into memory per session.
- ✅ **Supports Overloading**: Allows same-name procedures/functions with different parameters.

---

## ❓ 3. What is the difference between a package specification and a package body?

### ✅ Answer:

| Feature              | Package Specification                    | Package Body                                |
|----------------------|------------------------------------------|----------------------------------------------|
| Purpose              | Declares public elements (interface)     | Implements the logic of declared elements    |
| Required?            | Always                                   | Optional if no procedures/functions declared |
| Visibility           | Visible to external programs             | Hidden (private logic)                       |

---

## ❓ 4. Can you overload procedures/functions inside a package?

### ✅ Answer:

Yes, PL/SQL allows **overloading** of procedures/functions within a package — you can use the same name with different parameter lists.

```plsql
CREATE OR REPLACE PACKAGE math_pkg IS
   FUNCTION add(x NUMBER, y NUMBER) RETURN NUMBER;
   FUNCTION add(x NUMBER, y NUMBER, z NUMBER) RETURN NUMBER;
END;
```

---

## ❓ 5. What is package initialization and when does it happen?

### ✅ Answer:

The **initialization section** of a package is a block that runs **only once per session**, the first time the package is referenced.

```plsql
CREATE OR REPLACE PACKAGE BODY init_demo IS
   v_loaded_date DATE;

   PROCEDURE show_time IS
   BEGIN
      DBMS_OUTPUT.PUT_LINE('Loaded at: ' || v_loaded_date);
   END;

BEGIN
   v_loaded_date := SYSDATE; -- Initialization section
END;
```

---

## ❓ 6. What are public and private elements in a PL/SQL package?

### ✅ Answer:

- **Public Elements**: Declared in the **specification**, accessible from outside.
- **Private Elements**: Declared only in the **body**, not visible outside the package.

Private elements help in **hiding internal logic** and exposing only necessary functionality.

---

## ❓ 7. Can you have a package without a body?

### ✅ Answer:

Yes, if the **specification only contains constants, variables, types**, and does **not declare any procedures or functions**, a **body is not required**.

```plsql
CREATE OR REPLACE PACKAGE app_constants IS
   c_tax_rate CONSTANT NUMBER := 0.18;
END;
```

---

## ❓ 8. How do you call a procedure or function from a package?

### ✅ Answer:

You can call procedures/functions using the `package_name.procedure_name` or `package_name.function_name` syntax.

```plsql
BEGIN
   emp_pkg.show_salary(101); -- Procedure
END;

DECLARE
   v_sum NUMBER;
BEGIN
   v_sum := math_pkg.add(10, 20); -- Function
   DBMS_OUTPUT.PUT_LINE('Sum: ' || v_sum);
END;
```

---

## ❓ 9. What happens when you recompile a package body?

### ✅ Answer:

- Recompiling the **package body** does **not** invalidate dependent objects.
- But if the **specification changes**, then all dependent objects (procedures, functions, views, etc.) are **invalidated** and require recompilation.

---

## ❓ 10. Can you handle exceptions in a PL/SQL package?

### ✅ Answer:

Yes. Exceptions can be handled:
- Inside **individual procedures/functions** within the body.
- Inside the **initialization section** of the package.

```plsql
CREATE OR REPLACE PACKAGE BODY demo_pkg IS
   PROCEDURE test_proc IS
   BEGIN
      -- logic
   EXCEPTION
      WHEN OTHERS THEN
         DBMS_OUTPUT.PUT_LINE('Handled in procedure.');
   END;

BEGIN
   DBMS_OUTPUT.PUT_LINE('Package loaded.');
EXCEPTION
   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('Init error: ' || SQLERRM);
END;
```

---

## ✅ Summary

PL/SQL packages are powerful for:
- Structuring code cleanly
- Reusing logic
- Improving performance
- Supporting object-oriented practices (like encapsulation and overloading)

---
