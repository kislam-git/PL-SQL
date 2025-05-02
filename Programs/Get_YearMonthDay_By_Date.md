# 📆 Oracle PL/SQL Function – Calculate Year, Month, and Day Difference Between Two Dates

![Oracle](https://img.shields.io/badge/Oracle-PL%2FSQL-red.svg)
![Status](https://img.shields.io/badge/status-stable-brightgreen.svg)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

This repository contains a PL/SQL function that calculates the **difference between two dates** in **Years, Months, and Days**. It's useful for applications like age calculation, service duration, or general reporting.

---

## 🚀 Features

- Calculates exact difference in `Years`, `Months`, and `Days`
- Returns a readable string like: `2 Years, 3 Months, 10 Days`
- Works with any valid Oracle `DATE` input
- Simple to integrate into any PL/SQL-based application

---

## 🧩 Function Definition

```sql
CREATE OR REPLACE FUNCTION get_date_difference(
    start_date IN DATE,
    end_date   IN DATE
) RETURN VARCHAR2
IS
    years_diff   NUMBER;
    months_diff  NUMBER;
    days_diff    NUMBER;
BEGIN
    years_diff := TRUNC(MONTHS_BETWEEN(end_date, start_date) / 12);
    months_diff := TRUNC(MOD(MONTHS_BETWEEN(end_date, start_date), 12));
    days_diff := TRUNC(end_date - ADD_MONTHS(start_date, TRUNC(MONTHS_BETWEEN(end_date, start_date))));
    
    RETURN years_diff || ' Years, ' || months_diff || ' Months, ' || days_diff || ' Days';
END;
/
````

---

## 🧪 How to Use

1. Open Oracle SQL Developer or any SQL interface.
2. Run the function code above to create it in your schema.
3. Call the function using SQL like below.

---

## 📥 Example Query

```sql
SELECT get_date_difference(
    TO_DATE('05-JUN-2023', 'DD-MON-YYYY'), 
    SYSDATE
) AS difference
FROM dual;
```

---

## 📤 Example Output

```text
1 Years, 10 Months, 27 Days
```

---
