# Assignment #C: bfs & dp

Updated 1436 GMT+8 Nov 25, 2025

2025 fall, Complied by 2500011806 蒋欣宜



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### sy321迷宫最短路径

bfs, https://sunnywhy.com/sfbj/8/2/321

思路：



代码：

```python
from collections import deque  

def solve():  
    n,m=map(int, input().split())  
    maze=[list(map(int, input().split())) for _ in range(n)]  
    directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]  
    visited = [[False] * m for _ in range(n)]  
    pre = [[None] * m for _ in range(n)]  
  
    queue = deque()  
    queue.append((0,0))  
    visited[0][0] = True  
  
    while queue:  
        x,y=queue.popleft()  
        if x == n - 1 and y == m - 1:  
            break  
        for i in directions:  
            nx, ny = x + i[0], y + i[1]  
            if 0 <= nx < n and 0 <= ny < m and maze[nx][ny] == 0 and not visited[nx][ny]:  
                visited[nx][ny] = True  
                pre[nx][ny] = (x, y)  
                queue.append((nx, ny))  
  
    path=[]  
    x,y=n-1,m-1  
    while x!=0 or y!=0:  
        path.append((x+1,y+1))  
        x,y=pre[x][y]  
    path.append((1,1))  
    path.reverse()  
    for x,y in path:  
        print(x,y)  
if __name__=='__main__':  
    solve()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251224161848.png]]



### sy324多终点迷宫问题

bfs, https://sunnywhy.com/sfbj/8/2/324

思路：

因为直接在前一题基础上修改了所以没有删去visited这一部分，实际上不需要，即count=-1即可

代码：

```python
from collections import deque  
  
def solve():  
    n,m=map(int, input().split())  
    maze=[list(map(int, input().split())) for _ in range(n)]  
    directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]  
    visited = [[False] * m for _ in range(n)]  
    count= [[-1] * m for _ in range(n)]  
    count[0][0] = 0  
    queue = deque()  
    queue.append((0,0))  
    visited[0][0] = True  
  
    while queue:  
        x,y=queue.popleft()  
        for i in directions:  
            nx, ny = x + i[0], y + i[1]  
            if 0 <= nx < n and 0 <= ny < m and  not visited[nx][ny]:  
                visited[nx][ny] = True  
                if maze[nx][ny] == 0:  
                    count[nx][ny] =count[x][y]+1  
                    queue.append((nx, ny))  
  
    for i in count:  
        print(" ".join(map(str, i)), )  
if __name__=='__main__':  
    solve()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251224164836.png]]



### M02945: 拦截导弹

dp, greedy http://cs101.openjudge.cn/pctbook/M02945

思路：

相当于递减子序列问题（

代码：

```python
k = int(input())  
heights = list(map(int, input().split()))  
dp = [1] * k  
for i in range(k):  
    for j in range(i):  
        if heights[j] >= heights[i]:  
            dp[i] = max(dp[i], dp[j] + 1)  
print(max(dp))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251209164020.png]]



### 189A. Cut Ribbon

brute force/dp, 1300, https://codeforces.com/problemset/problem/189/A

思路：



代码：

```python
def solve():
    n, a, b, c = map(int, input().split())

    dp = [-1] * (n + 1) 
    dp[0] = 0
    for i in range(1, n + 1):
        if i >= a and dp[i - a] >= 0:
            dp[i] = max(dp[i], dp[i - a] + 1)
        if i >= b and dp[i - b] >= 0:
            dp[i] = max(dp[i], dp[i - b] + 1)
        if i >= c and dp[i - c] >= 0:
            dp[i] = max(dp[i], dp[i - c] + 1)
    print(dp[n])

if __name__ == "__main__":
    solve()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20260107182935.png]]





### M01384: Piggy-Bank

dp, http://cs101.openjudge.cn/practice/01384/

思路：

从d老师那学了迭代器用法（）虽然此处似乎并非很需要…
（以及理论上迭代器和sys输入应该都会快，但做了好多题似乎都没发现有什么区别？）

代码：

```python
import sys

def solve():
    data = sys.stdin.read().strip().split()
    if not data:
        return
    it = iter(data)
    T = int(next(it))
    results = []
    INF = 10**9 
    
    for _ in range(T):
        E = int(next(it))
        F = int(next(it))
        M = F - E 
        N = int(next(it))
        coins = []
        for _ in range(N):
            P = int(next(it))
            W = int(next(it))
            coins.append((P, W))
        
        dp = [INF] * (M + 1)
        dp[0] = 0
        
        for P, W in coins:
            for j in range(W, M + 1):
                if dp[j - W] != INF:
                    dp[j] = min(dp[j], dp[j - W] + P)
        
        if dp[M] == INF:
            results.append("This is impossible.")
        else:
            results.append(f"The minimum amount of money in the piggy-bank is {dp[M]}.")
    
    sys.stdout.write("\n".join(results))

if __name__ == "__main__":
    solve()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![[Pasted image 20260107222321.png]]
（最初的和多次实验试图换方法和优化的，虽然好像也没真的优化zzz）



### M02766: 最大子矩阵

dp, kadane, http://cs101.openjudge.cn/pctbook/M02766

思路：


代码：

```python
import sys  
def maxi(a):  
    max1 = a[0]  
    max2 = a[0]  
    for x in a[1:]:  
        max1 = max(x, max1 + x)  
        max2 = max(max1,max2)  
    return max2  
  
def main():  
    data = sys.stdin.read().strip().split()  
    if not data:  
        return  
    it = iter(data)  
    n= int(next(it))  
    matrix = []  
    for _ in range(n):  
        row = []  
        for _ in range(n):  
            row.append(int(next(it)))  
        matrix.append(row)  
  
    max_sum = -10 ** 9   
for top in range(n):  
        col_sum = [0] * n    
        for bottom in range(top, n):  
            for c in range(n):  
                col_sum[c] += matrix[bottom][c]  
            current_max = maxi(col_sum)  
            max_sum = max(max_sum, current_max)  
    print(max_sum)  
  
if __name__ == "__main__":  
    main()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20260103153047.png]]



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

写完作业题感觉自己dp、bfs和dfs还是学的比较差，虽然基本模型大致能写但加一些变化就会不知道要往哪个方向走，可能要都试试耗时很久才能写出来（）于是另外把晴问上dfs、bfs的都过了一遍，大致明白方向了zzz 后续可能


