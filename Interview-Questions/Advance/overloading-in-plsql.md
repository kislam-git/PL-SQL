
# 🔁 What is an Overloaded Procedure/Function in PL/SQL?

---

## ✅ Definition

**Overloading** in PL/SQL means creating **multiple procedures or functions** with the **same name** but **different parameter lists** (different number, types, or order of parameters).

PL/SQL determines which version to execute based on the **arguments passed** during the call.

---

## 🔍 Where is Overloading Allowed?

Overloading is supported:
- Inside **packages**
- In **object types**
- In **standalone functions/procedures** (in Oracle 11g and later)

---

## 🔧 Example: Overloaded Function in a Package

```plsql
CREATE OR REPLACE PACKAGE math_pkg IS
   FUNCTION add(x NUMBER, y NUMBER) RETURN NUMBER;
   FUNCTION add(x NUMBER, y NUMBER, z NUMBER) RETURN NUMBER;
END math_pkg;

CREATE OR REPLACE PACKAGE BODY math_pkg IS
   FUNCTION add(x NUMBER, y NUMBER) RETURN NUMBER IS
   BEGIN
      RETURN x + y;
   END;

   FUNCTION add(x NUMBER, y NUMBER, z NUMBER) RETURN NUMBER IS
   BEGIN
      RETURN x + y + z;
   END;
END math_pkg;
```

---

## 🚀 Usage

```plsql
DECLARE
   result1 NUMBER;
   result2 NUMBER;
BEGIN
   result1 := math_pkg.add(10, 20);       -- Calls 2-parameter version
   result2 := math_pkg.add(1, 2, 3);      -- Calls 3-parameter version

   DBMS_OUTPUT.PUT_LINE('Result 1: ' || result1);
   DBMS_OUTPUT.PUT_LINE('Result 2: ' || result2);
END;
```

---

## ⚠️ Rules for Overloading — Explained Simply

### ✅ 1. Must differ in **number**, **order**, or **datatype** of parameters

When you overload a function or procedure, each version must have **something different in the parameter list** so Oracle can tell which one to run.

### 🔸 Example 1: Different number of parameters

```plsql
-- Version 1
PROCEDURE greet(name VARCHAR2);

-- Version 2
PROCEDURE greet(first_name VARCHAR2, last_name VARCHAR2);
```

These are fine because they take a different **number** of parameters.

---

### 🔸 Example 2: Different datatype of parameters

```plsql
-- Version 1
PROCEDURE log_message(p_message VARCHAR2);

-- Version 2
PROCEDURE log_message(p_message CLOB);
```

Here, the **parameter types** are different — one takes `VARCHAR2`, the other takes `CLOB`. That's allowed.

---

### 🔸 Example 3: Different **order** of parameters

```plsql
-- Version 1
PROCEDURE add_item(id NUMBER, name VARCHAR2);

-- Version 2
PROCEDURE add_item(name VARCHAR2, id NUMBER);
```

These are okay too because even though both have 2 parameters, the **order** is different.

---

### 🚫 Not Allowed: Only return type is different

```plsql
-- Version 1
FUNCTION get_salary(emp_id NUMBER) RETURN NUMBER;

-- Version 2
FUNCTION get_salary(emp_id NUMBER) RETURN VARCHAR2;  -- ❌ Not allowed
```

This will **cause an error**, because Oracle can’t tell which version to use — the **parameter list is the same**, and Oracle **doesn’t look at the return type** to decide.

---

## 🎯 Why these rules?

Oracle must be able to decide **which version** of the function/procedure to call **just by looking at the parameters you pass**.

If two versions look the same (same parameter list), it gets confused — and that’s not allowed.

---


## 🧠 Real-World Use Case

A `log_message` procedure could be overloaded to accept:
- Just a message
- A message with a severity
- A message with severity and timestamp

```plsql
PROCEDURE log_message(p_msg VARCHAR2);
PROCEDURE log_message(p_msg VARCHAR2, p_level VARCHAR2);
PROCEDURE log_message(p_msg VARCHAR2, p_level VARCHAR2, p_time TIMESTAMP);
```

---

## ✅ Summary

| Feature               | Description                                     |
|------------------------|-------------------------------------------------|
| What is Overloading?  | Same name, different parameters                |
| Where is it used?     | Mainly in packages or object types             |
| Why use it?           | Simplifies usage and improves readability      |
| Key rule              | Return type alone cannot differentiate versions |

---

> 💡 Overloading in PL/SQL helps create flexible and developer-friendly interfaces.
```
