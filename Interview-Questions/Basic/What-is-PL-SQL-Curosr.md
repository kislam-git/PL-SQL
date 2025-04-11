# ❓ Question 3: What is a Cursor in PL/SQL?

---

## ✅ Answer:

In **PL/SQL**, a **cursor** is a pointer to the result set of a SQL query. It allows row-by-row processing of query results.

When you execute a `SELECT` statement that returns **more than one row**, you need a cursor to **fetch and process each row individually**.

---

## 🧠 Types of Cursors

| Type             | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| **Implicit Cursor** | Automatically created by Oracle for single-row queries like `SELECT INTO`. |
| **Explicit Cursor** | Declared by the programmer for queries that return multiple rows.          |

---

## 🔹 Implicit Cursor Example

```plsql
DECLARE
   v_name employees.first_name%TYPE;
BEGIN
   SELECT first_name INTO v_name
   FROM employees
   WHERE employee_id = 100;

   DBMS_OUTPUT.PUT_LINE('Employee Name: ' || v_name);
END;
```
### ✅ Used when the query is guaranteed to return only one row.
### ⚠️ Throws TOO_MANY_ROWS if more than one row is returned.

```
DECLARE
   CURSOR emp_cursor IS
      SELECT employee_id, first_name FROM employees WHERE department_id = 10;

   v_id employees.employee_id%TYPE;
   v_name employees.first_name%TYPE;
BEGIN
   OPEN emp_cursor;
   LOOP
      FETCH emp_cursor INTO v_id, v_name;
      EXIT WHEN emp_cursor%NOTFOUND;

      DBMS_OUTPUT.PUT_LINE('ID: ' || v_id || ' - Name: ' || v_name);
   END LOOP;
   CLOSE emp_cursor;
END;

```

### ✅ Used when:
*  You expect multiple rows
*  You need fine-grained control over fetching and processing

## 🛠 Cursor Attributes
| Attribute        | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| **cursor_name%FOUND** | Returns TRUE if the last fetch returned a row. |
| **cursor_name%NOTFOUND** | TRUE if the last fetch did not return a row.          |
| **cursor_name%ROWCOUNT** | Number of rows fetched so far.          |
| **cursor_name%ISOPEN** | TRUE if the cursor is open.          |

## 🎯 Real-World Use Case
* Generating reports by iterating through result sets
* Performing complex logic per record
* Bulk data manipulation with cursor loops

## ✅ Summary
* Use implicit cursors for single-row queries.
* Use explicit cursors for multi-row queries.
* Cursors give row-by-row control in PL/SQL.
