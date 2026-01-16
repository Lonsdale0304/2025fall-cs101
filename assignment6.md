# Assignment #6: 矩阵、贪心

Updated 1432 GMT+8 Oct 14, 2025

2025 fall, Complied by <mark>同学的姓名、院系</mark>



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

### M18211: 军备竞赛

greedy, two pointers, http://cs101.openjudge.cn/pctbook/M18211



思路：

很难得地第一反应就是对的且没调试直接一遍过了的题
感觉贪心有点上手了

代码

```python
money=int(input())  
n=0  
weapons=sorted(map(int,input().split()))  
while len(weapons)>0:  
    if money>=weapons[0]:  
        money-=weapons.pop(0)  
        n+=1  
    else:  
        if n==0 or len(weapons)==1:  
            break  
        money+=weapons.pop()  
        n-=1  
print(n)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251016153044.png]]



### M21554: 排队做实验

greedy, http://cs101.openjudge.cn/pctbook/M21554/



思路：

比较常规，相同时间的问题用

代码

```python
n=int(input())
time=list(map(int,input().split()))
time1=sorted(time)
order=[]
total=0
for i in range(n):
    order.append(time.index(time1[i])+1)
    total+=time1[i]*(n-i-1)
    time[time.index(time1[i])]=0
print(" ".join(map(str,order)))
print("%.2f"%(total/n))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251020113513.png]]



### E23555: 节省存储的矩阵乘法

implementation, matrices, http://cs101.openjudge.cn/pctbook/E23555



思路：

非零项中A[j]=B[i]时相乘有意义，得A[i]xB[j].
处理时用了两种方式：
一是用字典和列表排序直接计算并输出非零项
二是生成相乘得到的矩阵再输出其中非零项
意外的是两者内存占用和耗时居然差不多甚至后者更少……不知道是不是字典占用比较高？

字典的key不能是列表，为了规避用了元组再转成列表，稍微有点麻烦
以及用了好多层for循环……虽然题解实例里面用了更多的循环bushi

代码

```python
n,m1,m2=map(int,input().split())  
a,b=[],[]  
for i in range(m1):  
    a.append(list(map(int,input().split())))  
for i in range(m2):  
    b.append(list(map(int,input().split()))) 
#上面一样，之后写了两种：
c={}
for i in a:  
    for j in b:  
        if i[1]==j[0]:  
            if (i[0],j[1]) in c:  
                c[(i[0],j[1])]+=i[2]*j[2]  
            else:  
                c[(i[0],j[1])]=i[2]*j[2]  
for i in sorted(c):  
    print(i[0],i[1],c[i]) #用字典直接输出非零项

c=[[0 for i in range(n)] for j in range(n)]  
for i in a:  
    for j in b:  
        if i[1]==j[0]:  
                c[i[0]][j[1]]+=i[2]*j[2]  
for i in range(n):  
    for j in range(n):  
        if c[i][j]!=0:  
             print(i,j,c[i][j])#生成相乘得到的矩阵再输出其中非零项
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251021145352.png]]



### M12558: 岛屿周⻓

matrices, http://cs101.openjudge.cn/pctbook/M12558


思路：



代码

```python
a,b=map(int,input().split())
area=[]
n=0
for i in range(a):
    m=list(map(int,input().split()))
    n+=sum(m)*4
    area.append(m)
    for j in range(b):
        if area[i][j]==1:
            if j!=0 and area[i][j-1]==1:
                n-=2
            if i!=0 and area[i-1][j]==1:
                n-=2
print(n)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251020113922.png]]



### M01328: Radar Installation

greedy, http://cs101.openjudge.cn/practice/01328/



思路：

==dbq突然有新想法了正在赶零点前不一定赶得完先交了==

代码

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### 545C. Woodcutters

dp, greedy, 1500, https://codeforces.com/problemset/problem/545/C



思路：



代码

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>





