# Assignment #4: T-primes + 贪心

Updated 1814 GMT+8 Sep 30, 2025

2025 fall, Complied by 2500011805 蒋欣宜 化院



>**说明：**
>
>1. **解题与记录：**
>
>  对于每一个题目，请提供其解题思路（可选），并附上使用Python或C++编写的源代码（确保已在OpenJudge， Codeforces，LeetCode等平台上获得Accepted）。请将这些信息连同显示“Accepted”的截图一起填写到下方的作业模板中。（推荐使用Typora https://typoraio.cn 进行编辑，当然你也可以选择Word。）无论题目是否已通过，请标明每个题目大致花费的时间。
>
>2. 提交安排：**提交时，请首先上传PDF格式的文件，并将.md或.doc格式的文件作为附件上传至右侧的“作业评论”区。确保你的Canvas账户有一个清晰可见的本人头像，提交的文件为PDF格式，并且“作业评论”区包含上传的.md或.doc附件。
> 
>4. **延迟提交：**如果你预计无法在截止日期前提交作业，请提前告知具体原因。这有助于我们了解情况并可能为你提供适当的延期或其他帮助。  
>
>请按照上述指导认真准备和提交作业，以保证顺利完成课程要求。





## 1. 题目

### 34B. Sale

greedy, sorting, 900, https://codeforces.com/problemset/problem/34/B



思路：

略 约10min

代码

```python
a,b=map(int,input().split())  
m=sorted(list(map(int,input().split())))  
n=0  
for i in range(b):  
    if m[i]<0:  
        n-=m[i]  
print(n)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251007145150.png]]



### 160A. Twins

greedy, sortings, 900, 



思路：

略

代码

```python
n=int(input())  
m=sorted(list(map(int,input().split())))  
half=sum(m)//2  
pick,count=0,0  
for i in range(n-1,-1,-1):  
    pick+=m[i]  
    count+=1  
    if pick>half:  
        break  
print(count)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251007153940.png]]



### 1879B. Chips on the Board

constructive algorithms, greedy, 900, https://codeforces.com/problemset/problem/1879/B



思路：

看起来很复杂实际好简单……
代码就短短几行

代码

```python
for i in range(int(input())):  
    n=int(input())  
    a=sorted(map(int,input().split()))  
    b=sorted(map(int,input().split()))  
    print(min((sum(a)+n*b[0],sum(b)+n*a[0])))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251007164143.png]]



### M01017: 装箱问题

greedy, http://cs101.openjudge.cn/pctbook/M01017/


思路：

感觉是道纯数学题，看着很复杂实际上思路清晰即可
从大到小塞，654都要单装，3最多装4个
主要需要讨论的就是2x2，在原来3x3的基础上可能可以再放0/1/3/5个；本来使用if语句，然后想到可以直接用列表值；计算出可以插空塞下的数目，剩下>0单装
1x1最好处理直接减一下就行了
向上取整其实这么打不太好……算个人习惯吧
最后写出来只有短短的300b的代码看着真的很有成就感（）

代码：
```python
while True:  
    m=list(map(int, input().split()))  
    if m==[0]*6:  
        break  
    num=m[5]+m[4]+m[3]+(m[2]+3)//4  
    empty=[0,5,3,1]  
    n2=m[1]-m[3]*5-empty[m[2]%4]  
    if n2>0:  
        num+=(n2+8)//9  
    n1=m[0]-(num*36-m[5]*36-m[4]*25-m[3]*16-m[2]*9-m[1]*4)  
    if n1>0:  
        num+=(n1+35)//36  
    print(num)
```

代码运行截图

![[Pasted image 20251003171958.png]]


代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### M01008: Maya Calendar

implementation, http://cs101.openjudge.cn/practice/01008/



思路：



代码

```python
month_name = ["pop", "no", "zip", "zotz", "tzec", "xul", "yoxkin",  
              "mol", "chen","yax", "zac", "ceh", "mac",  
              "kankin", "muan", "pax", "koyab", "cumhu", "uayet"]  
day_name = ["imix", "ik", "akbal", "kan", "chicchan",  
                "cimi", "manik", "lamat", "muluk", "ok",  
                "chuen", "eb", "ben", "ix", "mem",  
                "cib", "caban", "eznab", "canac", "ahau"]  
a=int(input())  
b=[]  
for i in range(a):  
    day,month,year=input().replace('.','').split()  
    n=int(year)*365+month_name.index(month)*20+int(day)+1  
    year=n//260  
    month=day_name[n%20-1]  
    date=n%13  
    if date==0:  
        date=13  
    b.append(str(date)+" "+month+" "+str(year))  
print(a)  
for i in b:  
    print(i)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### 230B. T-primes（选做）

binary search, implementation, math, number theory, 1300, http://codeforces.com/problemset/problem/230/B



思路：



代码

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>





