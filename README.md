# VTB-test-task
Тестовое задание ВТБ
# SQL Задачи и решения

---
### 1) NULL, так как сравнение с NULL всегда даёт неизвестно  

---
### 2) Не выполняется, поле `order_code` не находится в `GROUP BY`  
---
### 3) Сотрудники, получающие ЗП больше, чем их руководителя

```sql

SELECT e.name

FROM employee e

JOIN employee chief ON e.chief_id = chief.id

WHERE e.salary > chief.salary;

```
---
### 4) Сотрудники с максимальной ЗП в своём отделе

```sql

SELECT e.*

FROM employee e

JOIN (

    SELECT department_id, MAX(salary) AS max_salary

    FROM employee

    GROUP BY department_id

) m ON e.department_id = m.department_id

   AND e.salary = m.max_salary;

```
---
### 5) Отделы, где ≤ 3 сотрудников

```sql

SELECT department_id

FROM employee

GROUP BY department_id

HAVING COUNT(*) <= 3;

```
---
### 6) Сотрудники без назначенного руководителя в том же отделе

```sql

SELECT e.*

FROM employee e

LEFT JOIN employee chief

  ON e.chief_id = chief.id

 AND e.department_id = chief.department_id

WHERE chief.id IS NULL;

```
---
### 7) Отдел с максимальной суммарной ЗП

```sql

SELECT department_id

FROM employee

GROUP BY department_id

ORDER BY SUM(salary) DESC

LIMIT 1;

```
---
### 8) Отделы без сотрудников
```sql

SELECT d.*

FROM department d

LEFT JOIN employee e ON d.id = e.department_id

WHERE e.id IS NULL;

```
---
### 9) Сотрудники, их ЗП и средняя ЗП по отделу
```sql

SELECT e.name,

       e.salary,

       avg_dept.avg_salary

FROM employee e

JOIN (

    SELECT department_id, AVG(salary) AS avg_salary

    FROM employee

    GROUP BY department_id

) avg_dept ON e.department_id = avg_dept.department_id;

```
---
