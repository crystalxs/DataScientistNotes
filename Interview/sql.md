# SQL

## Questions Classify

### Reshape Data

#### Long to Wide

```sql
SELECT <column>
	, MAX(CASE WHEN <condition> THEN ** ELSE ** END) AS <column>
  , MAX(CASE WHEN <condition> THEN ** ELSE ** END) AS <column>
FROM <table>
GROUP BY 1;
```

#### Wide to Long

```sql
SELECT <column>
	, CASE
			WHEN <condition> THEN **
			WHEN <condition> THEN **
			ELSE ** END AS <column>
FROM <table>;
```

## Leetcode

### Window Functions

#### 601. Human Traffic of Stadium

```sql
/* Write your T-SQL query statement below */
select id, visit_date, people
from (
    select *, case when people >= 100
            and lead(people, 1) over (order by visit_date) >= 100
            and lead(people, 2) over (order by visit_date) >= 100
            then 1
        when people >= 100
            and lead(people, 1) over (order by visit_date) >= 100
            and lag(people, 1) over (order by visit_date) >= 100
            then 1
        when people >= 100
            and lag(people, 1) over (order by visit_date) >= 100
            and lag(people, 2) over (order by visit_date) >= 100
            then 1
        else 0 end as flag
    from stadium
) as flagged
where flag = 1;
```

#### 177. Nth Highest Salary

```sql
CREATE FUNCTION getNthHighestSalary(@N INT) RETURNS INT AS
BEGIN
    RETURN (
        /* Write your T-SQL query statement below. */
        select salary 
        from (
            select salary, row_number() over (order by salary desc) as rank
            from (
                select distinct salary
                from employee
            ) dissalary
        ) salaryrank
        where rank = @n
    );
END
```

#### 178. Rank Scores

```sql
/* Write your T-SQL query statement below */
select lhs.score, rhs.rank
from scores lhs
left join (
    select score, row_number() over (
        order by score desc) as rank
    from (
        select distinct score
        from scores) as disscores
) rhs
on lhs.score = rhs.score
order by score desc;
```

#### 185. Department Top Three Salaries

```sql
/* Write your T-SQL query statement below */
with cte as (
    select *, row_number() over (partition by departmentid order by salary desc) rank
    from (
        select salary, departmentid
        from employee
        group by departmentid, salary
    ) dissalary
)

select department.name as department, employee.name as employee, employee.salary
from employee
inner join department
on employee.departmentid = department.id
left join cte
on employee.departmentid = cte.departmentid and employee.salary = cte.salary
where cte.rank < 4;
```

#### 579. Find Cumulative Salary of an Employee

```sql
/* Write your T-SQL query statement below */
SELECT id, month
    , SUM(salary) OVER(PARTITION BY id ORDER BY month 
                       ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) salary
FROM employee outside
WHERE month <> (SELECT MAX(month) FROM employee inside WHERE outside.id = inside.id)
ORDER BY id ASC, month DESC;
```





## 620. Not Boring Movies

```sql
/* Write your T-SQL query statement below */
select id, movie, description, rating
from cinema
where (id%2 = 1) and (description <> 'boring')
order by rating desc;
```

## 595. Big Countries

```sql
/* Write your T-SQL query statement below */
select name, population, area
from world
where (area > 3000000) or (population > 25000000);
```

## 182. Duplicate Emails

```sql
/* Write your T-SQL query statement below */
select distinct email
from person
where email in (
    select email
    from person
    group by email
    having count(email)>1
);
```

## 175. Combine Two Tables

```sql
/* Write your T-SQL query statement below */
select firstname, lastname, city, state
from person
left join address
on person.personid = address.personid;
```

## 181. Employees Earning More Than Their Managers

```sql
/* Write your T-SQL query statement below */
select lhs.name as employee
from employee as lhs
left join employee as rhs
on lhs.managerid = rhs.id
where lhs.salary > rhs.salary;
```

## 183. Customers Who Never Order

```sql
/* Write your T-SQL query statement below */
select name as customers
from customers
left join orders
on customers.id = orders.customerid
where orders.id is null;
```

## 596. Classes More Than 5 Students

```sql
/* Write your T-SQL query statement below */
select class
from courses
group by class
having count(distinct student) > 4;
```

## 184. Department Highest Salary

```sql
/* Write your T-SQL query statement below */
select department.name as department, employee.name as employee, salary
from employee
left join (
    select departmentid, max(salary) as maxsalary
    from employee
    group by departmentid
) as lhs
on employee.departmentid = lhs.departmentid
left join department
on employee.departmentid = department.id
where (employee.salary = lhs.maxsalary) and (department.name is not null);
```

## 626. Exchange Seats

```sql
/* Write your T-SQL query statement below */
select case when id%2 = 1 and id <> rownum then id+1
        when id%2 = 0 then id-1
        else id end as id
    , student
from seat
cross join (
    select count(*) as rownum
    from seat
) as rhs
order by 1;
```

## 197. Rising Temperature

```sql
/* ms-sql */
select id
from (
    select lhs.id, lhs.temperature, rhs.temperature pretemp
    from weather lhs
    left join weather rhs
    on DATEADD(day,-1,lhs.recorddate) = rhs.recorddate
  /*on lhs.recorddate - interval '1' = rhs.recorddate*/
) as previous
where temperature > pretemp;

```

## 180. Consecutive Numbers

```sql
/* Write your T-SQL query statement below */
select distinct lhs.num as consecutivenums
from logs lhs
left join logs
on lhs.id + 1 = logs.id
left join logs rhs
on lhs.id + 2 = rhs.id
where lhs.num = logs.num and lhs.num = rhs.num;
```

## 176. Second Highest Salary

```sql
/* Write your T-SQL query statement below */
select max(salary) as secondhighestsalary
from employee
where salary < (
    select max(salary)
    from employee
);
```

## 262. Trips and Users

```sql
/* Write your T-SQL query statement below */
with cte as 
(select *
from trips lhs
inner join (
    select users_id
    from users
    where banned = 'No'
) rhs
on lhs.client_id = rhs.users_id
where Request_at between '2013-10-01' and '2013-10-03')

select lhs.Request_at as day
    , case when cancelnum is null then 0.00
        else round(cast(cancelnum as float)/count(*),2) end as "cancellation rate"
from cte lhs
left join (
    select Request_at, count(*) as cancelnum
    from cte
    where status <> 'completed'
    group by Request_at
) rhs
on lhs.Request_at = rhs.Request_at
group by lhs.Request_at, rhs.cancelnum
order by lhs.request_at;
```

## 627. Swap Salary

```sql
/* Write your T-SQL query statement below */
update salary set
	sex = case when sex = 'f' then 'm'
		when sex = 'm' then 'f' end;
```

#### 613. Shortest Distance in a Line

```sql
SELECT min(distance) shortest
FROM (
    SELECT x-LAG(x) OVER(ORDER BY x) distance
    FROM point) t;
```

#### 584. Find Customer Referee

```SQL
# Write your MySQL query statement below
SELECT name
FROM customer
WHERE referee_id <> 2 OR referee_id IS NULL;
```

