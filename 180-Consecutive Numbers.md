### 180.Consecutive Numbers

#### 连续数字

Write a SQL query to find all numbers that appear at least three times consecutively.

```
+----+-----+
| Id | Num |
+----+-----+
| 1  |  1  |
| 2  |  1  |
| 3  |  1  |
| 4  |  2  |
| 5  |  1  |
| 6  |  2  |
| 7  |  2  |
+----+-----+

```

For example, given the above `Logs` table, `1` is the only number that appears consecutively for at least three times.

```
+-----------------+
| ConsecutiveNums |
+-----------------+
| 1               |
+-----------------+
```

#### 解法一

这道题给了我们一个Logs表，让我们找Num列中连续出现相同数字三次的数字，那么由于需要找三次相同数字，所以我们需要建立三个表的实例，我们可以用l1分别和l2, l3内交，l1和l2的Id下一个位置比，l1和l3的下两个位置比，然后将Num都相同的数字返回即可

```
SELECT DISTINCT l1.Num FROM Logs l1
JOIN Logs l2 ON l1.Id = l2.Id - 1
JOIN Logs l3 ON l1.Id = l3.Id - 2
WHERE l1.Num = l2.Num AND l2.Num = l3.Num;
```

#### 解法二:

下面这种方法没用用到Join，而是直接在三个表的实例中查找，然后把四个条件限定上，就可以返回正确结果了：

```
SELECT DISTINCT l1.Num FROM Logs l1, Logs l2, Logs l3
WHERE l1.Id = l2.Id - 1 AND l2.Id = l3.Id - 1
AND l1.Num = l2.Num AND l2.Num = l3.Num;
```

