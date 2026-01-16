# Assignment #9: Mock Exam立冬前一天

Updated 1658 GMT+8 Nov 6, 2025

2025 fall, Complied by 2500011806 蒋欣宜



>**说明：**
>
>1. Nov⽉考： AC6<mark>（请改为同学的通过数）</mark> 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。
>
>2. 解题与记录：对于每一个题目，请提供其解题思路（可选），并附上使用Python或C++编写的源代码（确保已在OpenJudge， Codeforces，LeetCode等平台上获得Accepted）。请将这些信息连同显示“Accepted”的截图一起填写到下方的作业模板中。（推荐使用Typora https://typoraio.cn 进行编辑，当然你也可以选择Word。）无论题目是否已通过，请标明每个题目大致花费的时间。
>
>3. 提交安排：提交时，请首先上传PDF格式的文件，并将.md或.doc格式的文件作为附件上传至右侧的“作业评论”区。确保你的Canvas账户有一个清晰可见的本人头像，提交的文件为PDF格式，并且“作业评论”区包含上传的.md或.doc附件。
> 
>4. 延迟提交：如果你预计无法在截止日期前提交作业，请提前告知具体原因。这有助于我们了解情况并可能为你提供适当的延期或其他帮助。  
>
>请按照上述指导认真准备和提交作业，以保证顺利完成课程要求。





## 1. 题目

### E29982:一种等价类划分问题

hashing, http://cs101.openjudge.cn/practice/29982

思路：

感觉本题比下一题难不少

代码

```python
def count(a):
    b=0
    for i in str(a):
        b+=int(i)
    return b
m,n,k=map(int,input().split(","))
dic={}
for i in range(m+1,n):
    if count(i) in dic:
        dic[count(i)].append(i)
    elif count(i) %k==0:
        dic[count(i)]=[i]
a=sorted(dic)
for i in a:
    print(",".join(map(str,dic[i])))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251110102557.png]]



### E30086:dance

greedy, http://cs101.openjudge.cn/practice/30086

思路：



代码

```python
n,d=map(int,input().split())
height=list(map(int,input().split()))
height.sort()
ans="Yes"
for i in range(n):
    if abs(height[2*i]-height[2*i+1])>d:
        ans="No"
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251110102621.png]]



### M25570: 洋葱

matrices, http://cs101.openjudge.cn/practice/25570

思路：



代码

```python
def yangcong(matrix,n):
    count=[0 for i in range((n+1)//2)]
    for i in range(n):
        for j in range(n):
            if matrix[i][j] != 0:
                count[min(i,j,n-i-1,n-j-1)]+=matrix[i][j]
    return max(count)
n=int(input())
matrix=[]
for i in range(n):
    row=list(map(int,input().split()))
    matrix.append(row)
print(yangcong(matrix,n))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251110102659.png]]
![[Pasted image 20251110103905.png]]


### M28906:数的划分

dfs, dp, http://cs101.openjudge.cn/practice/28906


思路：

考试现场写了一个超绝多重循环dfs并成功tle（bushi）考完简单调了下剪枝过了但代码感觉还是有些丑陋
后来在指导下理解了dp的方法并重写（这样感觉舒服多了…）不过感觉要想到这种写法思维难度对我来说还是不低的，考场上不一定想的到

代码

```python
n,m = map(int, input().split())  
dp = [[0] * (n + 1) for _ in range(m + 1)]  
for k in range(m + 1):  
    dp[k][0] = 1  
for k in range(1, m + 1):  
    for i in range(1, n + 1):  
        dp[k][i] = dp[k-1][i]  
        if i >= k:  
            dp[k][i] += dp[k][i - k]  
print(dp[m][n]-dp[m-1][n])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251111225055.png]]



### M29896:购物

greedy, http://cs101.openjudge.cn/practice/29896

思路：

就正常贪心吧，感觉自己目前对贪心的掌握还可以……
此处是从小到大计算的，每次算要能组成第m种对应的面值n-1需要的第m-1种硬币数，累加就可以了
听群里讨论从大到小也行，尝试了一下没过，但群里大佬好像又没有发代码，非常好奇（）

代码

```python
x,n=map(int,input().split())
money=sorted(list(map(int,input().split())))
count=0
if 1 not in money:
    print(-1)
else:
    total=0
    for i in range(n-1):
        a=-((-min(x,money[i+1])+total+1)//money[i])
        total+=a*money[i]
        count+=a
        if total>=x:
            break
    if total<x:
        count+=-((total-x)//money[n-1])
    print(count)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251110102737.png]]



### T25353:排队

greedy, http://cs101.openjudge.cn/practice/25353

思路：



代码

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





## 2. 学习总结和收获

如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。

发现自己的贪心掌握的不错，但深搜递归动态规划都没有系统掌握，甚至基本用的都是自己摸索出的东西……还是要多看题解和讲解



