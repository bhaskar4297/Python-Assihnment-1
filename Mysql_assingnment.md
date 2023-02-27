Questions link:
https://drive.google.com/file/d/1eT8ck9JJHFPvq0zsWEkrtbtQxXdSjqSB/view

Solutions:
SQL Questions Set 1
Q1 - Solution

SELECT *
FROM CITY
WHERE (COUNTRYCODE = 'USA' AND POPULATION > 100000);
Q2 - Solution

SELECT name
FROM City
WHERE countrycode = 'USA' AND population > 120000;
Q3 - Solution

SELECT *
FROM City;
Q4 - Solution

SELECT *
FROM City
WHERE ID = 1661;
Q5 - Solution

SELECT *
FROM City
WHERE countrycode = 'JPN';
Q6 - Solution

SELECT name
FROM City
WHERE countrycode = 'JPN';
Q7 - Solution

SELECT city, state
FROM Station;
Q8 - Solution

SELECT DISTINCT city
FROM station
WHERE id%2 = 0;
Q9 - Solution

SELECT COUNT(City) - COUNT(DISTINCT City)
FROM Station;
Q10 - Solution

SELECT City, LENGTH(City)
FROM STATION
ORDER BY LENGTH(City), City
LIMIT 1;

SELECT City, LENGTH(City)
FROM STATION
ORDER BY LENGTH(City) DESC, City
LIMIT 1;
Q11 - Solution

SELECT DISTINCT City
FROM Station
WHERE LEFT(City, 1) IN ('a', 'e', 'i', 'o', 'u');
Q12 - Solution

SELECT DISTINCT City
FROM Station
WHERE RIGHT(City, 1) IN ('a', 'e', 'i', 'o', 'u');
Q13 - Solution

SELECT DISTINCT City
FROM Station
WHERE LEFT(City, 1) NOT IN ('a', 'e', 'i', 'o', 'u');
Q14 - Solution

SELECT DISTINCT City
FROM Station
WHERE RIGHT(City, 1) NOT IN ('a', 'e', 'i', 'o', 'u');
Q15 - Solution

SELECT DISTINCT City
FROM Station
WHERE LEFT(City, 1) NOT IN ('a', 'e', 'i', 'o', 'u') OR RIGHT(City, 1) NOT IN ('a', 'e', 'i', 'o', 'u');
Q16 - Solution

SELECT DISTINCT City
FROM Station
WHERE LEFT(City, 1) NOT IN ('a', 'e', 'i', 'o', 'u') AND RIGHT(City, 1) NOT IN ('a', 'e', 'i', 'o', 'u');
Q17 - Solution

SELECT DISTINCT s1.product_id, product_name
FROM Sales s1 JOIN Product p
ON s1.product_id = p.product_id
WHERE NOT EXISTS (SELECT DISTINCT s2.product_id FROM Sales s2 WHERE ((s1.product_id = s2.product_id) AND s2.sale_date NOT BETWEEN '2019-01-01' AND '2019-03-31'));
Q18 - Solution

SELECT DISTINCT author_id AS id
FROM views
WHERE author_id = viewer_id
ORDER BY id;
Q19 - Solution

SELECT
ROUND (100.0 * (SELECT COUNT(*) FROM Delivery WHERE order_date = customer_pref_delivery_date) / (SELECT COUNT(*) FROM Delivery), 2)
AS immediate_percentage;
Q20 - Solution

WITH T1 AS
(
  SELECT ad_id,
  SUM(CASE WHEN action = 'Clicked' THEN 1 ELSE 0 END) AS click_count,
  SUM(CASE WHEN action = 'Viewed' THEN 1 ELSE 0 END) AS view_count
  FROM Ads
  GROUP BY 1
)
SELECT ad_id,
CASE
  WHEN click_count != 0 AND view_count != 0 THEN ROUND(100.0 * (click_count / (click_count + view_count)), 2)
  ELSE 0
END AS ctr
FROM T1
ORDER BY 2 DESC
Q21 - Solution

WITH T1 AS
(
  SELECT team_id, COUNT(*) AS team_size
  FROM Employee
  GROUP BY 1
)
SELECT employee_id, team_size
FROM Employee e JOIN T1
ON e.team_id = T1.team_id;
Q22 - Solution

SELECT country_name,
CASE
  WHEN AVG(weather_state) < 16 THEN "Cold"
  WHEN AVG(weather_state) > 24 THEN "Hot"
  ELSE "Warm"
END AS weather_type
FROM Weather w JOIN Countries c
ON w.country_id = c.country_id
WHERE day BETWEEN "2019-11-01" AND "2019-11-30"
GROUP BY 1;
Q23 - Solution

SELECT p.product_id, ROUND(SUM(price * units) / SUM(units), 2) AS average_price
FROM Prices p JOIN UnitsSold us
ON p.product_id = us.product_id AND (us.purchase_date BETWEEN p.start_date AND p.end_date)
GROUP BY 1;
Q24 - Solution

WITH T1 AS 
(
  SELECT player_id, event_date AS first_login,
  ROW_NUMBER() OVER(PARTITION BY player_id ORDER BY event_date) AS rn
  FROM Activity
  
)
SELECT player_id, first_login
FROM T1
WHERE rn = 1;
Q25 - Solution

WITH T1 AS 
(
  SELECT player_id, device_id,
  ROW_NUMBER() OVER(PARTITION BY player_id ORDER BY event_date) AS rn
  FROM Activity
  
)
SELECT player_id, device_id
FROM T1
WHERE rn = 1;
Q26 - Solution

SELECT product_name, SUM(unit) AS unit
FROM products p JOIN Orders o
ON p.product_id = o.product_id
WHERE order_date BETWEEN "2020-02-01" AND "2020-02-29"
GROUP BY 1
HAVING SUM(unit) > 99;
Q27 - Solution

SELECT *
FROM Users
WHERE mail REGEXP "^[a-zA-Z][a-zA-Z0-9_\\.-]*(@leetcode.com)$";
Q28 - Solution

WITH T1 AS
(
  SELECT o.customer_id, c.name, MONTH(order_date), SUM(price * quantity) AS spent
  FROM Orders o JOIN Product p ON o.product_id = p.product_id JOIN Customers c ON o.customer_id = c.customer_id
  WHERE MONTH(order_date) = 6 OR MONTH(order_date) = 7
  GROUP BY 1, 2, 3
  HAVING SUM(price * quantity) > 99
)
SELECT customer_id, name
FROM T1
GROUP BY 1
HAVING COUNT(*) = 2;
Q29 - Solution

SELECT title
FROM TVProgram t JOIN Content c
ON t.content_id = c.content_id AND Kids_content = "Y" AND content_type = "Movies" AND (program_date BETWEEN "2020-06-01" AND "2020-06-30");
Q30 - Solution

SELECT q.id, q.year,
CASE WHEN npv IS NULL THEN 0 ELSE npv END AS npv
FROM Queries q LEFT JOIN NPV
ON q.ID = NPV.id AND q.year = NPV.year;
Q31 - Solution

SELECT q.id, q.year,
CASE WHEN npv IS NULL THEN 0 ELSE npv END AS npv
FROM Queries q LEFT JOIN NPV
ON q.ID = NPV.id AND q.year = NPV.year;
Q32 - Solution

SELECT unique_id, name
FROM Employees e LEFT JOIN EmployeeUNI uni
ON uni.id = e.id;
Q33 - Solution

SELECT name, 
CASE WHEN SUM(distance) IS NULL THEN 0 ELSE SUM(distance) END AS travelled_distance
FROM Users u LEFT JOIN Rides r
ON u.id = r.user_id
GROUP BY 1
ORDER BY 2 DESC, 1;
Q34 - Solution

SELECT product_name, SUM(unit) AS unit
FROM products p JOIN Orders o
ON p.product_id = o.product_id
WHERE order_date BETWEEN "2020-02-01" AND "2020-02-29"
GROUP BY 1
HAVING SUM(unit) > 99;
Q35 - Solution

(
  SELECT name AS results
  FROM MovieRating mr JOIN Movies m ON mr.movie_id = m.movie_id JOIN Users u ON mr.user_id = u.user_id
  GROUP BY 1
  ORDER BY COUNT(*) DESC, 1
  LIMIT 1
)
UNION
(
  SELECT title AS results
  FROM MovieRating mr JOIN Movies m ON mr.movie_id = m.movie_id JOIN Users u ON mr.user_id = u.user_id
  WHERE created_at BETWEEN "2020-02-01" AND "2020-02-29"
  GROUP BY 1
  ORDER BY AVG(rating) DESC, 1
  LIMIT 1
)
Q36 - Solution

SELECT name, 
CASE WHEN SUM(distance) IS NULL THEN 0 ELSE SUM(distance) END AS travelled_distance
FROM Users u LEFT JOIN Rides r
ON u.id = r.user_id
GROUP BY 1
ORDER BY 2 DESC, 1;
Q37 - Solution

SELECT unique_id, name
FROM Employees e LEFT JOIN EmployeeUNI uni
ON uni.id = e.id;
Q38 - Solution

SELECT s.id, s.name
FROM Students s LEFT JOIN Departments d
ON s.department_id = d.id
WHERE d.name IS NULL;
Q39 - Solution

SELECT from_id AS person1, to_id AS person2, COUNT(*) AS call_count, SUM(duration) AS total_duration
FROM
(
  (
    SELECT from_id, to_id, duration
    FROM Calls
    WHERE from_id < to_id
  ) 
  UNION ALL
  (
    SELECT to_id AS from_id, from_id AS to_id, duration
    FROM Calls
    WHERE from_id > to_id
  )
) AS T1
GROUP BY 1, 2;
Q40 - Solution

SELECT p.product_id, ROUND(SUM(price * units) / SUM(units), 2) AS average_price
FROM Prices p JOIN UnitsSold us
ON p.product_id = us.product_id AND (us.purchase_date BETWEEN p.start_date AND p.end_date)
GROUP BY 1;
Q41 - Solution

SELECT name AS warehouse_name, SUM(units * Width * Length * Height) AS volume
FROM Warehouse w JOIN Products p
ON w.product_id = p.product_id
GROUP BY 1;
Q42 - Solution

WITH T1 AS
(
  SELECT sale_date, sold_num
  FROM Sales
  WHERE fruit = "apples"
), 
T2 AS
(
  SELECT sale_date, sold_num
  FROM Sales
  WHERE fruit = "oranges"
)
SELECT T1.sale_date, T1.sold_num - T2.sold_num AS diff
FROM T1 JOIN T2
USING (sale_date)
ORDER BY 1;
Q43 - Solution

SELECT ROUND(
(
  SELECT COUNT(DISTINCT a1.player_id)
  FROM Activity a1 JOIN Activity a2
  ON a1.player_id = a2.player_id AND a1.event_date > a2.event_date
  WHERE DATEDIFF(a1.event_date, a2.event_date) = 1
) / COUNT(DISTINCT player_id), 2) AS fraction
FROM Activity;
Q44 - Solution

SELECT name
FROM Employee
WHERE id IN (SELECT managerId FROM Employee GROUP BY managerId HAVING COUNT(managerId) > 4);
Q45 - Solution

SELECT COUNT(student_id) as student_numbe, dept_name
FROM Department d LEFT JOIN Student s
USING(dept_id)
GROUP BY dept_name
ORDER BY 1 DESC, 2;
Q46 - Solution

SELECT customer_id
FROM customer
GROUP BY customer_id
HAVING COUNT(DISTINCT product_key) = (SELECT COUNT(*) FROM Product);
Q47 - Solution

WITH T1 AS
(
  SELECT p.project_id, MAX(e.experience_years) AS max_exp
  FROM Project p JOIN Employee e
  ON p.employee_id = e.employee_id
  GROUP BY p.project_id
),
T2 AS
(
  SELECT p.project_id, p.employee_id, max_exp
  FROM Project p JOIN T1
  ON p.project_id = T1.project_id
)
SELECT project_id, T2.employee_id
FROM T2 JOIN Employee e
ON T2.employee_id = e.employee_id
WHERE experience_years = max_exp;
Q48 - Solution

SELECT b.book_id, b.name
FROM Books b LEFT JOIN Orders o
ON b.book_id = o.book_id AND dispatch_date >= "2018-06-23"
WHERE available_from < "2019-05-23"
GROUP BY  1, 2
HAVING SUM(quantity) < 10 OR SUM(quantity) IS NULL;
Q49 - Solution

WITH T1 AS
(
  SELECT student_id, MAX(grade) AS max_grade
  FROM Enrollments
  GROUP BY student_id
)
SELECT T1.student_id, MIN(course_id) AS course_id, max_grade AS grade
FROM T1 JOIN Enrollments e
ON T1.max_grade = e.grade AND T1.student_id = e.student_id
GROUP BY 1, 3
ORDER BY 1;
Q50 - Solution

WITH T1 AS
(
  SELECT player_id, MAX(score) AS score
  FROM
  (
    (SELECT first_player AS player_id, MAX(first_score) AS score FROM Matches GROUP BY 1)
    UNION
    (SELECT second_player AS player_id, MAX(second_score) AS score FROM Matches GROUP BY 1)
  ) AS tmp
  GROUP BY 1
),
T2 AS
(
  SELECT group_id, MAX(score) AS max_score
  FROM T1 JOIN Players p
  ON T1.player_id = p.player_id
  GROUP BY group_id
)
SELECT p.group_id, MIN(p.player_id) AS player_id
FROM T1 JOIN Players p
ON T1.player_id = p.player_id
JOIN T2 ON p.group_id = T2.group_id AND T1.score = max_score
GROUP BY 1
ORDER BY 1;
SQL Questions Set 2
Q51 - Solution

SELECT name, population, area
FROM World
WHERE area >= 3000000 OR population >= 25000000;
Q52 - Solution

SELECT name
FROM Customer
WHERE referee_id!=2 OR referee_id IS NULL;
Q53 - Solution

SELECT name AS Customers
FROM Customers
WHERE id NOT IN (SELECT customerId FROM Orders);
Q54 - Solution

WITH T1 AS
(
  SELECT team_id, COUNT(*) AS team_size
  FROM Employee
  GROUP BY 1
)
SELECT employee_id, team_size
FROM Employee e JOIN T1
ON e.team_id = T1.team_id;
Q55 - Solution

WITH T1 AS
(
	SELECT id, c.name
	FROM Person p JOIN Country c
	ON LEFT(phone_number, 3) = country_code
),
T2 AS
(
	SELECT name, AVG(duration) AS avg_duration
    FROM
    (
		(SELECT caller_id AS id, duration FROM Calls)
		UNION ALL
		(SELECT callee_id AS id, duration FROM Calls)
	) AS TMP JOIN T1
    ON TMP.id = T1.id
    GROUP BY 1
)
SELECT name
FROM T2
WHERE T2.avg_duration > (SELECT AVG(duration) FROM Calls);
Q56 - Solution

WITH T1 AS
(
	SELECT player_id, MIN(event_date) AS min_date
	FROM Activity
	GROUP BY 1
)
SELECT T1.player_id, device_id
FROM Activity a JOIN T1
ON a.player_id = T1.player_id AND event_date = min_date;
Q57 - Solution

SELECT customer_number
FROM orders
GROUP BY customer_number
ORDER BY COUNT(customer_number) DESC
LIMIT 1;
Q58 - Solution

SELECT DISTINCT c1.seat_id
FROM Cinema c1 JOIN Cinema c2
ON ABS(c2.seat_id - c1.seat_id) = 1 AND c1.free = 1 AND c2.free= 1
ORDER BY 1;
Q59 - Solution

SELECT s.name
FROM salesperson AS s
WHERE s.sales_id NOT IN (SELECT o.sales_id
                         FROM orders AS o
                         WHERE o.com_id = (SELECT c.com_id FROM company AS c WHERE c.name = 'RED')
                        );
Q60 - Solution

SELECT *,
CASE
	WHEN x + y > z AND x + z > y AND y + z > x THEN 'Yes'
	ELSE 'No'
END AS 'triangle'
FROM triangle;
Q61 - Solution

SELECT ABS
(
	(SELECT MIN(x) FROM Point)
	-
	(SELECT MIN(x) FROM Point WHERE x NOT IN (SELECT MIN(x) FROM Point))
) AS shortest;
Follow up: How could you optimise your query if the Point table is ordered in ascending order?
SELECT ABS
(
	(SELECT x FROM Point LIMIT 1)
	-
	(SELECT x FROM Point LIMIT 1 OFFSET 1)
) AS shortest;
Q62 - Solution

SELECT actor_id, director_id
FROM ActorDirector
GROUP BY 1, 2
HAVING COUNT(*) > 2;
Q63 - Solution

SELECT product_name, year, price
FROM Sales s JOIN Product p
ON s.product_id = p.product_id;
Q64 - Solution

SELECT project_id, ROUND(AVG(experience_years), 2) AS average_years
FROM Project p JOIN Employee e
ON p.employee_id = e.employee_id
GROUP BY 1;
Q65 - Solution

WITH T1 AS
(
	SELECT seller_id , SUM(price) AS max_sales
	FROM Sales
	GROUP BY 1
)
SELECT seller_id
FROM T1
WHERE max_sales = (SELECT MAX(max_sales) FROM T1);
Q66 - Solution

WITH T1 AS 
(
  SELECT DISTINCT buyer_id, product_name
  FROM Sales s JOIN Product p
  ON s.product_id = p.product_id
)
SELECT buyer_id
FROM T1
WHERE product_name IN ('S8', 'iPhone')
GROUP BY 1
HAVING COUNT(*) = 1
Q67 - Solution

WITH T1 AS
(
  SELECT visited_on, SUM(amount) AS amount
  FROM Customer
  GROUP BY 1
  ORDER BY 1 DESC
)
SELECT *,
ROUND(AVG(amount) OVER(ORDER BY visited_on ROWS BETWEEN 7 PRECEDING AND CURRENT ROW), 2) AS average_amount
FROM T1
LIMIT 18446744073709551615
OFFSET 6;
Q68 - Solution

SELECT gender, day, 
SUM(score_points) OVER(PARTITION BY gender ORDER BY gender, day) AS total
FROM Scores;
Q69 - Solution

WITH T1 AS
(
  SELECT log_id, ROW_NUMBER() OVER (ORDER BY log_id) AS rn
  FROM Logs
)
SELECT MIN(log_id) AS start_id, MAX(log_id) AS end_id 
FROM T1 
GROUP BY log_id - rn 
ORDER BY 1;
Q70 - Solution

WITH T1 AS
(
  SELECT student_id, subject_name, COUNT(*) AS attended_exams
  FROM Examinations
  GROUP BY 1, 2
),
T2 AS
(
  SELECT s.student_id, student_name, sub.subject_name
  FROM Students s JOIN Subjects sub
  ON 1 = 1
)
SELECT T2.student_id, student_name, T2.subject_name,
CASE WHEN attended_exams IS NULL THEN 0 ELSE attended_exams END AS attended_exams
FROM T2 LEFT JOIN T1
ON T2.student_id = T1.student_id AND T2.subject_name = T1.subject_name
ORDER BY 1, 3;
Q71 - Solution

WITH T1 AS
(
  SELECT employee_id
  FROM Employees
  WHERE manager_id = 1 AND employee_id != 1
),
T2 AS
(
  SELECT employee_id
  FROM Employees
  WHERE manager_id IN (SELECT employee_id FROM T1)
),
T3 AS
(
  SELECT employee_id
  FROM Employees
  WHERE manager_id IN (SELECT employee_id FROM T2)
)
SELECT * FROM T1 
UNION 
SELECT * FROM T2 
UNION 
SELECT * FROM T3
Q72 - Solution

SELECT CONCAT(YEAR(trans_date), "-", MONTH(trans_date)) AS month,
country,
COUNT(*) AS trans_count,
SUM(CASE WHEN state = "approved" THEN 1 ELSE 0 END) AS approved_count,
SUM(amount) AS trans_total_amount,
SUM(CASE WHEN state = "approved" THEN amount ELSE 0 END) AS approved_total_amount 
FROM Transactions 
GROUP BY 1, 2;
Q73 - Solution

WITH T1 AS
(
  SELECT DISTINCT action_date,
  (100.0 * COUNT(r.post_id) OVER(PARTITION BY action_date) / COUNT(a.post_id) OVER(PARTITION BY action_date)) AS percent
  FROM Actions a LEFT JOIN Removals r
  ON a.post_id = r.post_id
  WHERE extra = "spam"
)
SELECT ROUND(AVG(percent), 2) AS average_daily_percent
FROM T1;
Q74 - Solution

WITH T1 AS
(
  SELECT player_id, MIN(event_date) AS first_login 
  FROM Activity
  GROUP BY 1
)
SELECT ROUND((COUNT(DISTINCT T1.player_id) / (SELECT COUNT(DISTINCT player_id) FROM Activity)), 2) AS fraction
FROM T1 JOIN Activity a
ON T1.player_id = a.player_id AND DATEDIFF(T1.first_login, a.event_date) = -1;
Q75 - Solution

WITH T1 AS
(
  SELECT player_id, MIN(event_date) AS first_login 
  FROM Activity
  GROUP BY 1
)
SELECT ROUND((COUNT(DISTINCT T1.player_id) / (SELECT COUNT(DISTINCT player_id) FROM Activity)), 2) AS fraction
FROM T1 JOIN Activity a
ON T1.player_id = a.player_id AND DATEDIFF(T1.first_login, a.event_date) = -1;
Q76 - Solution

WITH T1 AS
(
  SELECT company_id,
  CASE WHEN MAX(salary) < 1000 THEN 0 WHEN MAX(salary) > 10000 THEN 0.49 ELSE 0.24 END AS percent
  FROM Salaries
  GROUP BY 1
)
SELECT s.company_id, employee_id, employee_name, ROUND((salary - percent * salary)) AS salary
FROM T1 JOIN Salaries s
ON T1.company_id = s.company_id;