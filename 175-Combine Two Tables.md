## 175. Combine Two Tables

### 表联结

Table: `Person`

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |
+-------------+---------+
PersonId is the primary key column for this table.

```

Table: `Address`

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |
+-------------+---------+
AddressId is the primary key column for this table.

```

Write a SQL query for a report that provides the following information for each person in the Person table, regardless if there is an address for each of those people:

```
FirstName, LastName, City, State
```

#### 解法一：

直接使用左联结Left join

```
SELECT Person.FirstName, Person.LastName, Address.City, Address.State 
FROM Person 
LEFT JOIN Address ON Person.PersonId = Address.PersonId;
```



#### 解法二：

在使用Left Join时，我们也可以使用关键Using来声明我们相用哪个列名来进行联合：

```
SELECT Person.FirstName, Person.LastName, Address.City, Address.State 
FROM Person 
LEFT JOIN Address USING(PersonId);
```



#### 解法三：

或者我们可以加上Natural关键字，这样我们就不用声明具体的列，MySQL可以自行搜索相同的列：

```
SELECT Person.FirstName, Person.LastName, Address.City, Address.State 
FROM Person 
NATURAL LEFT JOIN Address;
```