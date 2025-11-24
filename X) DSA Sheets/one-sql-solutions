# MySQL Sequential Practice Sheet

**(Run from top → bottom; each step builds on previous ones)**

> **Instructions:** Execute queries in order. Dependencies are explicitly stated.

---

# 1 — Setup: Database & Base Tables

### **1. Create database and switch to it**

```sql
CREATE DATABASE IF NOT EXISTS office;
USE office;
```

### **2. Create department table**

```sql
CREATE TABLE department (
  dept_id INT AUTO_INCREMENT PRIMARY KEY,
  dept_name VARCHAR(100) NOT NULL
);

INSERT INTO department (dept_name) VALUES ('HR'),('Sales'),('Engineering'),('Finance');
```

### **3. Create employee table**

```sql
CREATE TABLE employee (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100),
  salary DECIMAL(12,2),
  manager_id INT NULL,
  dept_id INT,
  job_role VARCHAR(100),
  hire_date DATE,
  is_deleted TINYINT(1) DEFAULT 0,
  UNIQUE KEY uk_emp_name (name),
  FOREIGN KEY (dept_id) REFERENCES department(dept_id),
  FOREIGN KEY (manager_id) REFERENCES employee(id)
);
```

### **4. Insert sample data**

```sql
INSERT INTO employee (name,salary,manager_id,dept_id,job_role,hire_date)
VALUES
('Aman',50000,NULL,1,'HR Executive','2024-01-10'),
('Arun',70000,1,2,'Sales Exec','2023-11-05'),
('Anita',90000,1,3,'Engineer','2022-08-20'),
('Bob',60000,2,2,'Sales Exec','2025-02-15'),
('Charlie',45000,3,3,'Engineer','2021-06-12'),
('David',120000,NULL,4,'CFO','2020-03-01'),
('Eve',70000,6,4,'Accountant','2022-12-01'),
('Frank',70000,6,4,'Accountant','2022-12-01'),
('Gopal',30000,3,3,'Intern',NULL),
('Hira',85000,3,3,'Engineer','2023-05-18');
```

---

# 2 — Table Copying / Cloning

### **5. Create employee_copy (structure only)**

```sql
CREATE TABLE employee_copy LIKE employee;
```

### **6. Create employee_copy2 (structure + data)**

```sql
CREATE TABLE employee_copy2 AS SELECT * FROM employee;
```

### **7. Salary audit table**

```sql
CREATE TABLE salary_audit (
  audit_id INT AUTO_INCREMENT PRIMARY KEY,
  emp_id INT,
  old_salary DECIMAL(12,2),
  new_salary DECIMAL(12,2),
  changed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

# 3 — Basic SELECT / Filtering

### **8. Names beginning with A**

```sql
SELECT * FROM employee WHERE name LIKE 'A%';
```

### **9. Names containing substring**

```sql
SELECT * FROM employee WHERE name LIKE '%an%';
```

### **10. NULL values**

```sql
SELECT * FROM employee WHERE hire_date IS NULL;
```

### **11. Replace NULL with default**

```sql
SELECT id, name, COALESCE(hire_date, '2000-01-01') AS hire_date_display
FROM employee;
```

---

# 4 — Sorting, Pagination, Position Fetch

### **12. First 10 employees**

```sql
SELECT * FROM employee ORDER BY id LIMIT 10;
```

### **13. Last 5 employees**

```sql
SELECT * FROM (
  SELECT * FROM employee ORDER BY id DESC LIMIT 5
) t ORDER BY id;
```

### **14. 8th employee**

```sql
SELECT * FROM employee ORDER BY id LIMIT 1 OFFSET 7;
```

### **15. Pagination**

```sql
SET @page = 2; SET @size = 5;
SELECT * FROM employee ORDER BY id LIMIT @size OFFSET (@page-1)*@size;
```

### **16. Alternate rows**

```sql
SELECT * FROM (
  SELECT e.*, ROW_NUMBER() OVER (ORDER BY id) rn
  FROM employee e
) t WHERE MOD(rn,2)=1;
```

---

# 5 — Aggregation & Grouping

### **17. Salary stats per department**

```sql
SELECT d.dept_name, COUNT(e.id) cnt, AVG(salary) avg_sal, MIN(salary) min_sal,
       MAX(salary) max_sal, SUM(salary) sum_sal
FROM department d
LEFT JOIN employee e ON d.dept_id = e.dept_id
GROUP BY d.dept_name;
```

### **18. Department headcount**

```sql
SELECT dept_id, COUNT(*) cnt FROM employee GROUP BY dept_id;
```

### **19. Departments with headcount < 3**

```sql
SELECT dept_id, COUNT(*) cnt FROM employee GROUP BY dept_id HAVING cnt < 3;
```

### **20. % salary contribution by employee**

```sql
SELECT e.id, e.name, e.salary,
  ROUND(e.salary / SUM(e.salary) OVER (PARTITION BY e.dept_id) * 100,2)
  AS pct_of_dept
FROM employee e;
```

---

# 6 — Ranking & Window Functions (MySQL 8+)

### **21. Top 3 salaries per department**

```sql
SELECT * FROM (
  SELECT e.*, ROW_NUMBER() OVER (PARTITION BY dept_id ORDER BY salary DESC) rn
  FROM employee e
) t WHERE rn <= 3;
```

### **22. Running salary total**

```sql
SELECT id, name, hire_date, salary,
  SUM(salary) OVER (ORDER BY hire_date
  ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS running_total
FROM employee;
```

### **23. LAG / LEAD**

```sql
SELECT id, name, salary,
  LAG(salary) OVER (ORDER BY hire_date) AS prev_salary,
  LEAD(salary) OVER (ORDER BY hire_date) AS next_salary
FROM employee;
```

---

# 7 — Second / Third Highest Salary

### **24. Second highest salary**

```sql
SELECT MAX(salary)
FROM employee
WHERE salary < (SELECT MAX(salary) FROM employee);
```

### **25. Third highest salary**

```sql
SELECT MAX(salary)
FROM employee
WHERE salary < (
  SELECT MAX(salary) FROM employee
  WHERE salary < (SELECT MAX(salary) FROM employee)
);
```

### **26–27. Using LIMIT and ranking**

```sql
SELECT DISTINCT salary FROM employee ORDER BY salary DESC LIMIT 1 OFFSET 1; -- second
SELECT DISTINCT salary FROM employee ORDER BY salary DESC LIMIT 1 OFFSET 2; -- third
```

Using window:

```sql
SELECT salary FROM (
  SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) rnk
  FROM employee
) t WHERE rnk IN (2,3);
```

---

# 8 — Joins

### **28. INNER JOIN**

```sql
SELECT e.*, d.dept_name
FROM employee e JOIN department d ON e.dept_id = d.dept_id;
```

### **29. LEFT JOIN**

```sql
SELECT e.*, d.dept_name
FROM employee e LEFT JOIN department d ON e.dept_id = d.dept_id
WHERE d.dept_id IS NULL;
```

### **30. RIGHT JOIN**

```sql
SELECT e.*, d.dept_name
FROM employee e RIGHT JOIN department d ON e.dept_id = d.dept_id;
```

### **31. FULL OUTER JOIN (simulated)**

```sql
SELECT e.*, d.dept_name
FROM employee e LEFT JOIN department d ON e.dept_id = d.dept_id
UNION
SELECT e.*, d.dept_name
FROM employee e RIGHT JOIN department d ON e.dept_id = d.dept_id;
```

### **32. CROSS JOIN**

```sql
SELECT e.name, d.dept_name
FROM employee e CROSS JOIN department d
LIMIT 10;
```

### **33. SELF JOIN (manager mapping)**

```sql
SELECT e.id, e.name, m.name AS manager_name
FROM employee e LEFT JOIN employee m ON e.manager_id = m.id;
```

---

# 9 — Set Operations

### **35. Intersection**

```sql
SELECT e.*
FROM employee e
INNER JOIN employee_copy2 c
ON e.name=c.name AND e.salary=c.salary;
```

### **36. Difference**

```sql
SELECT c.*
FROM employee_copy2 c
LEFT JOIN employee e
ON e.name=c.name AND e.salary=c.salary
WHERE e.id IS NULL;
```

### **37. UNION vs UNION ALL**

```sql
SELECT name FROM employee
UNION
SELECT name FROM employee_copy2;

SELECT name FROM employee
UNION ALL
SELECT name FROM employee_copy2;
```

---

# 10 — Duplicate Detection & Removal

### **38. Find duplicates**

```sql
SELECT name, salary, COUNT(*) cnt
FROM employee
GROUP BY name, salary
HAVING cnt > 1;
```

### **39. Remove duplicates**

```sql
CREATE TABLE tmp_employee AS SELECT * FROM employee GROUP BY name,salary;
TRUNCATE TABLE employee;
INSERT INTO employee SELECT * FROM tmp_employee;
DROP TABLE tmp_employee;
```

### **40. Case-insensitive duplicates**

```sql
SELECT LOWER(name) lname, COUNT(*) cnt
FROM employee
GROUP BY lname HAVING cnt > 1;
```

---

# 11 — Cleanup & Transforms

### **41. Normalize casing**

```sql
UPDATE employee SET name = UPPER(name);
```

### **42. Missing ID sequence**

```sql
SELECT t1.id+1 AS start_missing
FROM employee t1
LEFT JOIN employee t2 ON t1.id + 1 = t2.id
WHERE t2.id IS NULL
ORDER BY t1.id;
```

### **43. Soft-delete**

```sql
UPDATE employee SET is_deleted = 1 WHERE id = 3;
UPDATE employee SET is_deleted = 0 WHERE id = 3;
```

---

# 12 — DML (Advanced)

### **44. UPSERT**

```sql
INSERT INTO employee (id,name,salary,dept_id)
VALUES (2,'Arun',75000,2)
ON DUPLICATE KEY UPDATE salary=VALUES(salary);
```

### **45. Update salaries by percentage**

```sql
UPDATE employee SET salary = salary * 1.10 WHERE dept_id = 3;
```

### **46–48. Delete / Truncate / Drop**

```sql
DELETE FROM employee WHERE id > 6;
TRUNCATE TABLE employee;
DROP TABLE IF EXISTS employee;
```

---

# 13 — Manager Analytics

### **49. Manager report counts**

```sql
SELECT m.id,m.name,COUNT(e.id) reports
FROM employee m LEFT JOIN employee e ON m.id = e.manager_id
GROUP BY m.id, m.name;
```

### **50. Managers by team salary**

```sql
SELECT m.id, m.name, SUM(e.salary) team_salary
FROM employee m JOIN employee e ON m.id = e.manager_id
GROUP BY m.id,m.name
ORDER BY team_salary DESC;
```

### **51. Employees without managers**

```sql
SELECT * FROM employee WHERE manager_id IS NULL;
```

---

# 14 — Window Functions (Business)

### **52. Rank employees by salary**

```sql
SELECT id,name,salary,
  RANK() OVER (ORDER BY salary DESC) rnk
FROM employee;
```

### **53. Salary change vs previous hire**

```sql
SELECT id,name,salary,
  salary - LAG(salary) OVER (ORDER BY hire_date) AS salary_diff
FROM employee;
```

---

# 15 — Views / Procedures / Triggers

### **54. View**

```sql
CREATE VIEW v_employee_full AS
SELECT e.id,e.name,e.salary,d.dept_name, m.name manager_name
FROM employee e
LEFT JOIN department d ON e.dept_id = d.dept_id
LEFT JOIN employee m ON e.manager_id = m.id;
```

### **55. Stored Procedure**

```sql
DELIMITER //
CREATE PROCEDURE GetEmployeesByDept(IN p_dept INT)
BEGIN
  SELECT * FROM employee WHERE dept_id = p_dept;
END //
DELIMITER ;
```

### **56. Trigger for salary change**

```sql
DELIMITER //
CREATE TRIGGER tr_salary_change BEFORE UPDATE ON employee
FOR EACH ROW
BEGIN
  IF NEW.salary <> OLD.salary THEN
    INSERT INTO salary_audit (emp_id, old_salary, new_salary)
    VALUES (OLD.id, OLD.salary, NEW.salary);
  END IF;
END;
//
DELIMITER ;
```

---

# 16 — Indexes & Performance

### **57. Create index**

```sql
CREATE INDEX idx_job_role ON employee(job_role);
```

### **58. EXPLAIN**

```sql
EXPLAIN SELECT * FROM employee WHERE job_role='Engineer';
```

### **59. Drop index**

```sql
DROP INDEX idx_job_role ON employee;
```

### **60. Partitioning**

```sql
ALTER TABLE employee PARTITION BY RANGE (dept_id) (
  PARTITION p0 VALUES LESS THAN (2),
  PARTITION p1 VALUES LESS THAN (4),
  PARTITION p2 VALUES LESS THAN MAXVALUE
);
```

---

# 17 — JSON, GROUP_CONCAT, Pivoting

### **61. JSON column**

```sql
ALTER TABLE employee ADD COLUMN meta JSON;

UPDATE employee
SET meta = JSON_OBJECT('skills', JSON_ARRAY('sql','python'))
WHERE id=1;

SELECT JSON_EXTRACT(meta, '$.skills[0]') FROM employee WHERE id=1;
```

### **62. GROUP_CONCAT**

```sql
SELECT dept_id,
  GROUP_CONCAT(name ORDER BY name SEPARATOR ', ') AS employees
FROM employee GROUP BY dept_id;
```

### **63. Manual pivot**

```sql
SELECT
  SUM(CASE WHEN dept_id=1 THEN 1 ELSE 0 END) hr_count,
  SUM(CASE WHEN dept_id=2 THEN 1 ELSE 0 END) sales_count,
  SUM(CASE WHEN dept_id=3 THEN 1 ELSE 0 END) eng_count
FROM employee;
```

---

# 18 — Transactions & Isolation

### **64. Transaction demo**

```sql
START TRANSACTION;
UPDATE employee SET salary = salary + 1000 WHERE id = 1;
ROLLBACK;
```

### **65. Isolation level**

```sql
SET SESSION TRANSACTION ISOLATION LEVEL REPEATABLE READ;
SELECT @@tx_isolation, @@transaction_isolation;
```

---

# 19 — Security, Export/Import

### **66. GRANT privileges**

```sql
CREATE USER 'demo'@'localhost' IDENTIFIED BY 'demo_pass';
GRANT SELECT ON office.employee TO 'demo'@'localhost';
```

### **67. Export CSV**

```sql
SELECT * FROM employee INTO OUTFILE '/tmp/employee.csv'
FIELDS TERMINATED BY ',' ENCLOSED BY '"'
LINES TERMINATED BY '\n';
```

### **68. Import CSV**

```sql
LOAD DATA INFILE '/tmp/employee.csv'
INTO TABLE employee
FIELDS TERMINATED BY ',' ENCLOSED BY '"'
LINES TERMINATED BY '\n';
```

### **69. Show processlist**

```sql
SHOW PROCESSLIST;
```

---

# 20 — Edge Cases & Samples

### **70. Generate sample data**

```sql
INSERT INTO employee (name,salary,dept_id,job_role,hire_date)
SELECT CONCAT('Gen_',t1.n,'_',t2.n),
       30000 + (t1.n * 1000),
       ((t2.n%4)+1),
       'Temp',
       CURDATE() - INTERVAL (t1.n+t2.n) DAY
FROM (SELECT 0 n UNION ALL SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 UNION ALL SELECT 4) t1
CROSS JOIN (SELECT 0 n UNION ALL SELECT 5 UNION ALL SELECT 6 UNION ALL SELECT 7 UNION ALL SELECT 8) t2
LIMIT 20;
```

### **71. Salary > dept average**

```sql
SELECT e.*
FROM employee e
WHERE e.salary > (SELECT AVG(salary) FROM employee WHERE dept_id = e.dept_id);
```

### **72. EXISTS vs IN**

```sql
SELECT * FROM employee e WHERE EXISTS (SELECT 1 FROM employee_copy2 c WHERE c.name = e.name);
SELECT * FROM employee e WHERE name IN (SELECT name FROM employee_copy2);
```

### **73. Purge soft-deleted rows**

```sql
DELETE FROM employee WHERE is_deleted = 1;
```

### **74–75. Composite PK + FK**

```sql
CREATE TABLE project (
  project_id INT AUTO_INCREMENT PRIMARY KEY,
  project_name VARCHAR(100)
);

CREATE TABLE project_assignment (
  emp_id INT,
  project_id INT,
  assigned_on DATE,
  PRIMARY KEY (emp_id, project_id),
  FOREIGN KEY (emp_id) REFERENCES employee(id),
  FOREIGN KEY (project_id) REFERENCES project(project_id)
);
```

---

# 21 — Final Exam Style Queries

### **76. Top N per department**

```sql
SELECT * FROM (
  SELECT e.*, ROW_NUMBER() OVER (PARTITION BY dept_id ORDER BY salary DESC) rn
  FROM employee e
) t WHERE rn <= 2;
```

### **77. Joined in last 6 months**

```sql
SELECT * FROM employee
WHERE hire_date >= CURDATE() - INTERVAL 6 MONTH;
```

### **78. Salary gaps**

```sql
SELECT id,name,salary,
  salary - LAG(salary) OVER (ORDER BY salary) AS diff
FROM employee
HAVING diff > 10000;
```

### **79. Cleanup objects**

```sql
DROP VIEW IF EXISTS v_employee_full;
DROP TRIGGER IF EXISTS tr_salary_change;
DROP PROCEDURE IF EXISTS GetEmployeesByDept;
```

### **80. Drop database**

```sql
DROP DATABASE IF EXISTS office;
```

---
