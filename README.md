## [「新」动计划 · 编程入门](https://leetcode.cn/studyplan/primers-list/)

### [258.各位相加](https://leetcode.cn/problems/add-digits/description/?envType=study-plan-v2&envId=primers-list)
**题目：** 给定一个非负整数 num，反复将各个位上的数字相加，直到结果为一位数。返回这个结果。  
**本质：** 计算nums的树根，数根是自然数的一种性质，每个自然数都有一个数根。对于给定的自然数，反复将各个位上的数字相加，直到结果为一位数，则该一位数即为原自然数的数根。  
**解题：**  
&ensp;&ensp;方法一：模拟  
&ensp;&ensp;&ensp;&ensp;每次计算当前整数除以 10 的余数得到最低位数，将最低位数加到总和中，然后将当前整数除以 10。重复上述操作直到当前整数变成 0。
```python
# 输入num，例如输入num=38
# num不是个位数，则进入循环
while num >= 10:
    sum = 0
    while num:            #只要num不为0，就继续循环
        sum += num % 10   #%取余运算，取出num的最后一位数，加到sum上
        num //= 10        #//取被除数运算，去掉num的最后一位数
    num = sum
return num
```
&ensp;&ensp;方法二：数学
&ensp;&ensp;&ensp;&ensp;


### [231.2的幂](https://leetcode.cn/problems/power-of-two/description/?envType=study-plan-v2&envId=primers-list)
**题目：** 给你一个整数 n，请你判断该整数是否是 2 的幂次方。如果是，返回 true ；否则，返回 false。
**解题：**  
&ensp;&ensp;方法一：二进制表示


### SQL
**用户**
```SQL
-- 每个用户的首次登陆时间和最后登录时间
select uid,min(date) first_date,max(date) last_date
from login
group by 1
```
```SQL
-- 每天用户数
with t1 as(
    select distinct
        uid,
        date(logdate) date
    from login
)
select
    date,
    count(uid)
from t1
group by 1
```
```SQL
-- 每天的新用户数
with t1 as (
    select distinct
        uid,
        date
    from login
),
t2 as(
select
    uid,
    date,
    date = min(date) over (partition by uid) as tag
from t1
)
select date,sum(tag)
from t2
group by date
```
```SQL
-- 留存率基础表
with t1 as (
    select distinct
        uid,
        date
    from login
),
t2 as (
    select *,
        datediff(lead(date,1,date) over (partition by uid order by date),date) as diff
    date =min(date) over (partition by uid) as tag
    from t1
)
```
```SQL
-- 连续天数基础表
with t1 as (
    select distinct
        uid,
        date
    from login
),
t2 as (
select
    *,
    subdate(date,row_number() over (partition by uid order by date)) as val
from t1    
),
t3 as (
select
    *,
    count(val) over (partition by uid,val order by date ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING) AS cnt),
    date =min(date) over (partition by uid) as tag
)
```


















