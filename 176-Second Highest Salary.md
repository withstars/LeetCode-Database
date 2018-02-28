### 176. Second Highest Salary

#### 第二高薪水问题

Write a SQL query to get the second highest salary from the `Employee` table.

```
+----+--------+
| Id | Salary |
+----+--------+
| 1  | 100    |
| 2  | 200    |
| 3  | 300    |
+----+--------+

```

For example, given the above Employee table, the query should return `200` as the second highest salary. If there is no second highest salary, then the query should return `null`.

```
+---------------------+
| SecondHighestSalary |
+---------------------+
| 200                 |
+---------------------+
```

### 方法一

所谓的“第二高”是指去重后的仅次于最高值的分数因此只需借助于MAX关键词即可.

```
select MAX(Salary) AS SecondHighestSalary 
from Employee
where Salary < (select MAX(Salary) from Employee);
```

或

```
SELECT MAX(Salary) AS SecondHighestSalary 
FROM Employee
where Salary NOT IN
(SELECT MAX(Salary) FROM Employee)
```

### 方法二:

MySQL中Limit后面的数字限制了我们返回数据的个数，Offset是偏移量，那么如果我们想找第二高薪水，我们首先可以先对薪水进行降序排列，然后我们将Offset设为1，那么就是从第二个开始，也就是第二高薪水，然后我们将Limit设为1，就是只取出第二高薪水，如果将Limit设为2，那么就将第二高和第三高薪水都取出来.

```
SELECT Salary FROM Employee GROUP BY Salary
UNION ALL (SELECT NULL AS Salary)
ORDER BY Salary DESC LIMIT 1 OFFSET 1;
```