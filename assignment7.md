# Assignment #7: 矩阵、队列、贪心

Updated 1315 GMT+8 Oct 21, 2025

2025 fall, Complied by  2500011806 蒋欣宜




## 1. 题目

### M12560: 生存游戏

matrices, http://cs101.openjudge.cn/pctbook/M12560/

思路：



代码

```python
m,n=map(int,input().split())  
result=[[0 for i in range(n)] for j in range(m)]  
a=[[0 for i in range(n+2)] for j in range(m+2)]  
for i in range(m):  
    a[i+1][1:n+1]=list(map(int,input().split()))  
for i in range(1,m+1):  
    for j in range(1,n+1):  
        neighbor=a[i-1][j]+a[i-1][j-1]+a[i-1][j+1]+a[i][j+1]+a[i][j-1]+a[i+1][j]+a[i+1][j+1]+a[i+1][j-1]  
        if a[i][j]==0:  
            if neighbor==3:  
                result[i-1][j-1]=1  
        else:  
            if neighbor==2 or neighbor==3:  
                result[i-1][j-1]=1  
for i in range(m):  
    print(" ".join(map(str,result[i])))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251024192945.png]]



### M04133:垃圾炸弹

matrices, http://cs101.openjudge.cn/pctbook/M04133/

思路：

OJ居然不让用numpy，哭了，不得不循环嵌套找最值（还有没有什么别的方法吗……）
以及第一遍忘了垃圾辐射范围（bushi）可能超边界导致re，发现后限定了一下

代码

```python
d=int(input())  
point=int(input())  
matrix=[[0 for i in range(1025)] for j in range(1025)]  
for i in range(point):  
    x,y,number=map(int,input().split())  
    for i in range(max(x-d,0),min(1025,x+d+1)):  
        for j in range(max(y-d,0),min(y+d+1,1025)):  
            matrix[i][j]+=number  
m=matrix[0][0]  
count=1  
for row in matrix:  
    for val in row:  
        if val==m:  
            count+=1  
        elif val>m:  
            m=val  
            count=1  
print(count,m)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251026114152.png]]




### M02746: 约瑟夫问题

implementation, queue, http://cs101.openjudge.cn/pctbook/M02746/

思路：

感谢高中数学基础让我直接用数学递推方法（

代码

```python
while True:  
    n,m=map(int,input().split())  
    if n==0 and m==0:  
        break  
    result=0  
    for i in range(1,n+1):  
        result=(result+m)%i  
    print(result+1)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251026121405.png]]



### M26976:摆动序列

greedy, http://cs101.openjudge.cn/pctbook/M26976/


思路：



代码

```python
n=int(input())  
m=list(map(int,input().split()))  
a=[]  
for i in range(n-1):  
    if m[i+1]<m[i]:  
        a.append(1)  
    elif m[i+1]>m[i]:  
        a.append(-1)  
    else:  
        a.append(0)  
result=1  
b=0  
for i in range(n-1):  
    if a[i]!=b and a[i]!=0:  
            b=a[i]  
            result+=1  
print(result)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251026150208.png]]



### T26971:分发糖果

greedy, http://cs101.openjudge.cn/pctbook/T26971/

思路：

法1:拆分成逐级增和逐级减两种，分别统计对应糖果数，其中较大值即为两边都考虑时的糖果树；
法2：从小到大遍历得出对应糖果数
	实际操作中发现直接按从小到大排序遍历会tle，加限制条件可以过但有点麻烦，还是上一种较为简便

代码

```python
n=int(input())
ratings=list(map(int,input().split()))
up,down=[1],[1]
a,b,gifts=1,1,0
for i in range(n-1):
    if ratings[i]<ratings[i+1]:
        a+=1
    else:
        a=1
    up.append(a)
for i in range(n-1,0,-1):
    if ratings[i-1]>ratings[i]:
        b+=1
    else:
        b=1
    down.append(b)
down.reverse()
for i in range(n):
    gifts+=max(up[i],down[i])
print(gifts)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251103111532.png]]



### 1868A. Fill in the Matrix

constructive algorithms, implementation, 1300, https://codeforces.com/problemset/problem/1868/A

思路：

敲不出来……（绝望） 上课听完又看题解才明白思路
还是太菜

代码

```python
N= int(input())  
for _ in range(N):  
    n, m = map(int, input().split())  
    if m == 1:  
        print(0)  
    elif n > m - 1:  
        print(m)  
    else:  
        print(n + 1)  
  
    for i in range(min(m - 1, n)):  
        for j in range(m):  
            print((j + i) % m, end=' ')  
        print()  
  
    if n > m - 1:  
        for i in range(m - 1, n):  
            for j in range(m):  
                print(j, end=' ')  
            print()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251103112626.png]]



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

期中周其他课程压力有点大，计概稍微没有额外做太多orz…只能过两周赶赶进度了😭



