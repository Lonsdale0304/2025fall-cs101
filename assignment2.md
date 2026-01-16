# Assignment #2: 语法练习

Updated 1335 GMT+8 Sep 16, 2025

 2025 fall, Complied by  *化院 蒋欣宜（2500011806）*


## 1. 题目

### 263A. Beautiful Matrix

implementation, 800, https://codeforces.com/problemset/problem/263/A


思路：

略 用时6min+优化3min

代码

```python
m=0  
for i in range(5):  
    n=list(map(int,input().split()))  
    for j in range(5):  
        if n[j]==1:  
            m=abs(i-2)+abs(j-2)  
            break  
print(m)

```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[e4de371752984199e8edc932af3434dd.png]]


### 1328A. Divisibility Problem

math, 800, https://codeforces.com/problemset/problem/1328/A


思路：

略 用时11min+优化4min

代码

```python
n=int(input())  
for i in range(n):  
    a,b=map(int,input().split())  
    x=((a-1)//b+1)*b-a  
    print(x)
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[7e183ca76f98ba4a0c31c29ad7f7615b.png]]


### 427A. Police Recruits

implementation, 800, https://codeforces.com/problemset/problem/427/A


思路：

略 用时8min

代码

```python
n=int(input())  
a,b=0,0  
x=list(map(int,input().split()))  
for i in range(n):  
    a=a+x[i]  
    if a<0:  
        b-=a  
        a=0  
print(b)
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[79b7c6557d3bc32a8a0e6b082c345632.png]]


### E02808: 校门外的树

implementation, http://cs101.openjudge.cn/pctbook/E02808/


思路：
- 无需复杂数学运算，直接创建列表遍历即可
- 一注意到从0开始
- 做题过程中几点改进：
	将习惯性写的`for i in range(length+1):  m.append(1)`
	改为更直接的`m=[1]*(length+1)`；
	本来最终用for循环导出还在的树的值：
	```for i in range(length+1):  if m[i]==1:  n+=1```
    后来发现可以直接用sum或者count，避免循环
    
   用时21min+优化

代码

```python
length,number=map(int,input().split())  
m=[1]*(length+1)  
for i in range(number):  
    start,end=map(int, input().split())  
    for j in range(start,end+1):  
        m[j]=0  
print(sum(m))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[fc29f9896161d4981c90a53826e8e17f.png]]


### sy60: 水仙花数II

implementation, https://sunnywhy.com/sfbj/3/1/60



思路：

略 用时9min

代码

```python
a,b=map(int,input().split())  
total=""  
for i in range(a,b+1):  
    x=0  
    n=str(i)  
    for j in n:  
        x+=int(j)**3  
    if i==x:  
        total+=n+" "  
if total=="":  
    print("NO")  
else:  
    print(total[:-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>


![[72beb6b74ae55d12cd45c515edfe8d69.png]]


### M01922: Ride to School

implementation, http://cs101.openjudge.cn/pctbook/M01922/



思路：

忽略复杂题目描述，本题实际求的是”在0s之后出发的人最早何时到达“
取最小：sort【0】
向上取整：可用math.ceil,或者更原始的int负数
由于浮点数位数问题，先乘和先除得不同

用时：不可考，估计≥40min（解决浮点数问题用了好久）

代码

```python
import math  
while True:  
    n=int(input())  
    if n==0:  
        break  
    x=[]  
    for i in range(n):  
        a,b=map(int,input().split())  
        if b<0:  
            continue  
        else:  
            x.append(math.ceil(4500/a*3.6+b))  
    print(min(x))
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[4ab148278fc74eb06a1c0b31a54040f6.png]]

## 2. 学习总结和收获


#### 1.M01002:方便记忆的电话号码

|[http://cs101.openjudge.cn/pctbook/M01002/](http://cs101.openjudge.cn/pctbook/M01002/)|

思路与收获：

原本用字典进行翻译，搜索后发现可用改用translate改进代码
输出感觉还有简化空间但还没想到较好的方法

代码：
```python
mapping=str.maketrans('ABCDEFGHIJKLMNOPRSTUVWXY','222333444555666777888999')  
tel={}  
num=int(input())  
for i in range(num):  
    x=input().replace('-','')  
    if len(x)!=7:  
        continue  
    else:  
        x=x.translate(mapping)  
        x=x[0:3]+"-"+x[3:]  
        if x in tel:  
            tel[x]=tel[x]+1  
        else:  
            tel[x]=1  
m=0  
for key in sorted(tel):  
    if tel[key]!=1:  
        print(key,tel[key])  
        m+=1  
if m==0:  
    print("No duplicates.")
```

代码运行截图：![[607de86a1f4b79e04b0f395b2801cfb5.png]]


#### 2.M04030：统计单词数（9.18每日选做）

http://cs101.openjudge.cn/pctbook/M04030/

思路与收获：

考虑到空格也占文章位置，不能用list提取单词，只能保持字符串用前后空格判定
在开头和结尾还要特殊考虑，刚开始没有考虑到开头空格的情况而反复WA，后改正
用find还可以再度简化代码
学习到大小写可以用lower/upper

代码：
```python
word=input().strip().lower()  
n=len(word)  
sentence=input().lower()  
count=[]  
for i in range(len(sentence)-n+1):  
    if sentence[i:i+n]==word and (i==0 or i==len(sentence)-n or sentence[i-1]==sentence[i+n]==' '):  
        count.append(i)  
if not count:  
    print(-1)  
else:  
    print(len(count),count[0])
```

代码运行截图：
![[9bae82306a18fd98cb061ffd40d4d4e8.png]]

