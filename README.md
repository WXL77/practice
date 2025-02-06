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

