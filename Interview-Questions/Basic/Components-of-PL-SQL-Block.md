# ❓ Question 2: What are the Components of a PL/SQL Block?

---

## ✅ Answer:

A **PL/SQL block** is the basic unit of a PL/SQL program. Every block follows a defined structure that consists of up to **four sections**:

---

## 🧱 Components of a PL/SQL Block

| Section     | Description                                                                 |
|-------------|-----------------------------------------------------------------------------|
| `DECLARE`   | (Optional) Used to declare variables, constants, cursors, and exceptions.   |
| `BEGIN`     | (Mandatory) Contains the executable statements – this is the main logic.    |
| `EXCEPTION` | (Optional) Handles errors raised during execution in the BEGIN section.     |
| `END;`      | (Mandatory) Marks the end of the PL/SQL block.                              |

---

## 🔧 Syntax Template

```plsql
DECLARE
   -- Declarations (variables, constants, cursors, etc.)
BEGIN
   -- Executable statements (SQL and PL/SQL)
EXCEPTION
   -- Error handling statements
END;
```
## 📌 Example: Simple PL/SQL Block

```
DECLARE
   v_message VARCHAR2(50); -- Variable Declaration
BEGIN
   v_message := 'Welcome to PL/SQL!';
   DBMS_OUTPUT.PUT_LINE(v_message); -- Output Statement
EXCEPTION
   WHEN OTHERS THEN
      DBMS_OUTPUT.PUT_LINE('An error occurred: ' || SQLERRM);
END;

```

## 📝 Notes:
  * The DECLARE section is optional and can be omitted if no variables are needed.
  * The EXCEPTION block is useful for handling runtime errors gracefully.
  * Every block must start with BEGIN and end with END;

## 🎯 Real-World Use Case
  You use PL/SQL blocks to:
  * Write anonymous scripts
  * Create stored procedures and functions
  * Implement triggers
  * Handle business logic with error control
