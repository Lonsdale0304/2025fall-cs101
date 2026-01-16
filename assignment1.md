# Assignment #1: 自主学习

Updated 1306 GMT+8 Sep 14, 2025

2025 fall, Complied by <mark>蒋欣宜 化院 2500011806</mark>

#计算概论B 

## 1. 题目

### E02733: 判断闰年

http://cs101.openjudge.cn/pctbook/E02733/


思路：

简单题，略

代码

```python
n=int(input())  
m="N"  
if n%4==0 and n%100!=0 or n%400==0:  
    m="Y"  
print(m)
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[8cb6b0b80947f14544e5bd3b4ca89b13.png]]



### E02750: 鸡兔同笼

http://cs101.openjudge.cn/pctbook/E02750/



思路：

略

代码

```python
n=int(input())  
if n%2==0:  
    print(str((n+2)//4)+" " +str(n//2))  
else:  
    print("0 0")
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[49b2ab3cbecfeeb986b9f078ba1ba93c.png]]



### 50A. Domino piling

greedy, math, 800, http://codeforces.com/problemset/problem/50/A



思路：

略

代码

```python
a,b=map(int,input().split())
print(str(a*b//2))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[65aa8bb4554a156f09bcae0869eaeab1.png]]



### 1A. Theatre Square

math, 1000, https://codeforces.com/problemset/problem/1/A


思路：

略

代码

```python
n,m,a=map(int,input().split())
print(str((-n//a)*(-m//a)))
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[908ef97dc517e41236ffcd53ef976e40.png]]



### 112A. Petya and Strings

implementation, strings, 1000, http://codeforces.com/problemset/problem/112/A


思路：

略

代码

```python
x=0
a=input().lower()
b=input().lower()
if a<b:
   x=-1
elif a>b:
    x=1
print(x)
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[f1c5c461dd32aa90838fc90f43abe3d6.png]]


### 231A. Team

bruteforce, greedy, 800, http://codeforces.com/problemset/problem/231/A


思路：

略

代码

```python
n=int(input())
m=0
for i in range(n):
    x=sum(map(int,input().split()))
    if x>1:
        m+=1
print(m)

```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[b41fb7dab81970f3dcb6609eb52b764e.png]]




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>


- 更大的收获是**学习md**……之前对md的使用基本就是标题加粗高亮这类，现在学会了**表格、代码块和标签**之类的使用（看到上机课学长演示文稿也是md的，试图探索ing）
- 学会**科学上网**（这个是不是不应该细说）  由于clash更新刷配置，额外给chrome装了个插件记忆代理和直连
- -没买typera，现在在摸索使用**obsidian及其插件**……不得不说双链和多样的插件真的好用，功能强大便于整理，现在记笔记写总结也改用obsidian了（这个md转pdf也是插件一步到位，可调设置可点链接，快乐）
- python学习进度：**复健ing**    没有OI基础，高中选考学过些但很久没碰了，第一周额外做了点E/M的题找找手感（没有跟每日选做因为是补选选上的课……）。下面贴了道印象比较深的题

##### [E02883:checking order](http://cs101.openjudge.cn/pctbook/E02883/)

- 复习**不定行输入**，包括sys.stdin.read()/readline()、while循环+try-except命令
- 第一遍手打排序代码，然后使用sort简化，考思维又练函数使用，一题多用，好耶
- 由于把NO打成N0导致反复WA检查不出来…经典唐氏错误，值得引以为戒

#不定行 #列表输出格式转换

代码：
```python
'''import sys  
data=sys.stdin.read()  
for line in data:'''  #用sys处理不定行的那种
while True:  
    try:  
        a=list(map(int,input().split()))  
        a1=sorted(a)  
        if a==a1:  
            print("Yes")  
        else:  
            x = " ".join(map(str, a1))  
            print("No "+x)  
    except EOFError:  
        break

```