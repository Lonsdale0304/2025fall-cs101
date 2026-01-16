# Assignment #B: dp

Updated 1448 GMT+8 Nov 18, 2025

2025 fall, Complied by 蒋欣宜 2500011806



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### LuoguP1255 数楼梯

dp, bfs, https://www.luogu.com.cn/problem/P1255

思路：

最基础的模型……洛谷账号忘了用了哪个邮箱了登不上所以没有提交记录zzz

代码：

```python
n=int(input())  
lst=[1]*(n+1)  
for i in range(2,n+1):  
    lst[i]=lst[i-1]+lst[i-2]  
print(lst[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### 27528: 跳台阶

dp, http://cs101.openjudge.cn/practice/27528/

思路：

和上一题也没什么大区别

代码：

```python
n=int(input())  
lst=[1]*(n+1)  
for i in range(2,n+1):  
    lst[i]=sum(lst[:i])  
print(lst[-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20260103221715.png]]



### M23421:《算法图解》小偷背包问题

dp, http://cs101.openjudge.cn/pctbook/M23421/

思路：

对从小到大每一个重量值计算最高价值，即更改或者不更改中更高的那个

代码：

```python
def solve():  
    n,b= map(int, input().split())  
    prices=list(map(int, input().split()))  
    weights=list(map(int, input().split()))  
    dp = [0] * (b + 1)  
    for i in range(n):  
        for w in range(b, weights[i]-1,-1):  
            dp[w]= max(dp[w], dp[w-weights[i]]+prices[i])  
    print(dp[b])  
if __name__ == "__main__":  
    solve()
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20260107223230.png]]




### M5.最长回文子串

dp, two pointers, string, https://leetcode.cn/problems/longest-palindromic-substring/

思路：



代码：

```python
class Solution:

def longestPalindrome(self, s: str) -> str:

if not s:

return""

n=len(s)

start=end=0

for i in range(n):

l=r=i

while l>=0 and r<n and s[l]==s[r]:

l-=1;r+=1

if r-l-2>end-start:

start,end=l+1,r-1

l,r=i,i+1

while l>=0 and r<n and s[l]==s[r]:

l-=1;r+=1

if r-l-2>end-start:

start,end=l+1,r-1

return s[start:end+1]
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20260107224653.png]]





### 474D. Flowers

dp, 1700 https://codeforces.com/problemset/problem/474/D

思路：

第一次知道还可以用sys.stdout.write()  的方式输出（）

代码：

```python
import sys  
mod=100000000  
mx=100000  
def main():  
    d=sys.stdin.read().split()  
    if not d:  
        return  
    it=iter(d)  
    t=int(next(it));k=int(next(it))  
    q=[]  
    m=0  
    for _ in range(t):  
        a=int(next(it));b=int(next(it))  
        q.append((a,b))  
        if b>m:m=b  
    dp=[0]*(m+1)  
    dp[0]=1  
    for i in range(1,m+1):  
        dp[i]=dp[i-1]  
        if i>=k:  
            dp[i]=(dp[i]+dp[i-k])%mod  
    pre=[0]*(m+1)  
    pre[0]=1  
    for i in range(1,m+1):  
        pre[i]=(pre[i-1]+dp[i])%mod  
    out=[]  
    for a,b in q:  
        if a==0:  
            ans=pre[b]  
        else:  
            ans=(pre[b]-pre[a-1])%mod  
        out.append(str(ans))  
    sys.stdout.write("\n".join(out))  
if __name__=="__main__":  
    main()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### M198.打家劫舍

dp, https://leetcode.cn/problems/house-robber/

思路：



代码：

```python
class Solution:

def rob(self, nums: List[int]) -> int:

n = len(nums)

if n == 0:

return 0

if n == 1:

return nums[0]

first = nums[0]

second = max(nums[0], nums[1])

for i in range(2, n):

now = max(second, first + nums[i])

first = second

second = now

return second
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20260107225936.png]]



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>





