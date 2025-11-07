***A PRIMARY KEY is a column (or a set of columns) in a database table that uniquely identifies each row in that table.
Key Characteristics:

Uniqueness: No two rows can have the same primary key value.
Non-null: A primary key cannot contain NULL values.
Single or Composite: It can be a single column (like student_id) or a combination of columns (like first_name + last_name + birth_date).***

-- Find employees with salary between 40000 and 60000
SELECT * FROM employees
WHERE salary BETWEEN 40000 AND 60000;
