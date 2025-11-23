📘 Sequential MySQL Problems Sheet (Markdown Version)

1 — Setup & Basic Table Creation

1. Create a database named office.


2. Create a table department with dept_id (PK) and dept_name.


3. Create a table employee with fields: id, name, salary, manager_id, dept_id, job_role, hire_date, is_deleted.


4. Insert sample employee rows including duplicates and NULLs.




---

2 — Table Copying

5. Create a table employee_copy with the same structure as employee.


6. Create a table employee_copy2 with the same structure and data as employee.


7. Create a table salary_audit for logging salary changes.




---

3 — Basic SELECT / Filtering

8. Find employees whose name begins with ‘A’.


9. Find employees whose name contains a substring (like “an”).


10. Fetch employees with NULL hire_dates.


11. Show hire_dates but replace NULL values with a default value.




---

4 — Sorting & Pagination

12. Fetch the first 10 employees.


13. Fetch the last 5 employees using ORDER BY + subquery.


14. Fetch the 8th employee.


15. Implement pagination: fetch page 2 with page size 5.


16. Fetch alternate rows (every 2nd row).




---

5 — Aggregation & Grouping

17. Find avg, min, max, sum salary per department.


18. Department-wise employee count.


19. Departments where employee count is less than a value.


20. Percentage of salary contribution of each employee to their department.




---

6 — Window Functions

21. Find top 3 salaries per department using window functions.


22. Compute a running total of salary by hire_date.


23. Show each employee’s previous and next salary.




---

7 — Highest Salaries

24. Find the second highest salary using subquery.


25. Find the third highest salary using subquery.


26. Find second & third highest salary using LIMIT and OFFSET.


27. Find second & third highest salary using RANK/DENSE_RANK.




---

8 — Joins (All Types)

28. INNER JOIN employee with department.


29. LEFT JOIN to find employees without a department.


30. RIGHT JOIN demonstration.


31. FULL OUTER JOIN equivalent.


32. CROSS JOIN demonstration.


33. SELF JOIN to show employee → manager.


34. Multi-table join: employee + department + manager.




---

9 — Set Operations

35. Fetch common records between employee and employee_copy2.


36. Fetch records in employee_copy2 that are not present in employee.


37. Demonstrate UNION vs UNION ALL.




---

10 — Duplicate Handling

38. Find duplicate rows in employee.


39. Remove duplicate rows while keeping one copy.


40. Detect near-duplicate names (case-insensitive).




---

11 — Data Cleanup

41. Normalize employee names to upper/lower/title case.


42. Detect missing employee IDs (gaps in sequence).


43. Implement soft delete using an is_deleted column.




---

12 — DML (Insert/Update/Delete)

44. Perform an UPSERT (insert or update on conflict).


45. Increase salary of a department by a percentage.


46. Delete rows with employee_id greater than 6.


47. Delete all rows without deleting table structure.


48. Delete the employee table entirely.




---

13 — Manager & Team Analytics

49. Find managers with the number of their direct reports.


50. Find managers ranked by total team salary.


51. Find employees who do not have a manager.




---

14 — Advanced Window Function Problems

52. Rank employees by salary (global rank).


53. Show salary difference between each employee and the previous one.




---

15 — Views, Procedures, Triggers

54. Create a view showing employee + department + manager name.


55. Create a stored procedure to get employees by department.


56. Create a trigger that logs salary changes into salary_audit.




---

16 — Indexing & EXPLAIN

57. Create an index on job_role.


58. Analyze a query using EXPLAIN.


59. Drop an existing index.


60. Partition a table by department range.




---

17 — JSON, Text Aggregation & Pivot

61. Add a JSON column and insert JSON data.


62. Show employees per department using GROUP_CONCAT.


63. Convert department-wise row counts into columns (manual pivot).




---

18 — Transactions

64. Demonstrate a transaction with COMMIT and ROLLBACK.


65. Change and verify transaction isolation levels.




---

19 — Security & Administration

66. Create a user with only SELECT permission on employee.


67. Export table data into a CSV file.


68. Import data from CSV file back into employee.


69. Show and analyze active database connections.




---

20 — Additional Advanced Problems

70. Generate sample data using cross joins.


71. Fetch employees whose salary is greater than their department’s average.


72. Compare EXISTS vs IN queries.


73. Permanently delete all soft-deleted employees.


74. Create a table with a composite primary key.


75. Create a table with a foreign key referencing another primary table.




---

21 — Final Round Problems

76. Find top 2 highest paid employees per department.


77. Find employees who joined in the last 6 months.


78. Detect employees whose salary jumped by more than a threshold.


79. Drop the view, trigger, and procedure created earlier.


80. Drop the office database entirely.
