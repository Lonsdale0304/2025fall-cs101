# Assignment #8: 递归

Updated 1315 GMT+8 Oct 21, 2025

2025 fall, Complied by 2500011806 蒋欣宜



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

### M04147汉诺塔问题(Tower of Hanoi)

dfs, http://cs101.openjudge.cn/pctbook/M04147

思路：

本来写了巨长无比各种if的代码，看到群里大佬讨论可以直接交换醍醐灌顶飞速跑去改完

代码

```python
n,x,y,z=input().split()  
n = int(n)  
def move(n,a,b,c):  
    if n>1:  
        move(n-1,a,c,b)  
    print(f'{n}:{a}->{c}')  
    if n>1:  
        move(n-1,b,a,c)  
move(n,x,y,z)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251104214618.png]]



### M05585: 晶矿的个数

matrices, dfs similar, http://cs101.openjudge.cn/pctbook/M05585

思路：

怎么感觉这题根递归关系不大……？有点类似岛屿那题

代码

```python
 def count(matrix,color,x):  
    c=0  
    for i in range(1,x+1):  
        for j in range(1,x+1):  
            if matrix[i][j]==color:  
                if matrix[i][j-1]!=color and matrix[i-1][j]!=color:  
                    c+=1  
    return c  
n=int(input())  
for i in range(n):  
    y=int(input())  
    lis=[" "*(y+1)]  
    for i in range(y):  
        lis.append(" "+input())  
    print(count(lis,'r',y),count(lis,'b',y),)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### M02786: Pell数列

dfs, dp, http://cs101.openjudge.cn/pctbook/M02786/

思路：

应该是最基础的递归？唯一注意的是先取余数可以防止数据过大
（总有种求特征方程的冲动 虽然这个数据大小应该会超限）

代码

```python
n=int(input())  
for i in range(n):  
    x=int(input())  
    a=1  
    b=0  
    for i in range(x-1):  
        a,b=(2*a+b)%32767,a%32767  
    print(a)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251104232908.png]]




### M46.全排列

backtracking, https://leetcode.cn/problems/permutations/


思路：



代码

```python
class Solution:

def permute(self, nums: List[int]) -> List[List[int]]:

n = len(nums)

a, b = [], []

def back():

if len(sol) == n:

a.append(sol[:])

return

for x in nums:

if x not in sol:

b.append(x)

back()

b.pop()

back()

return a
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251104234705.png]]



### T02754: 八皇后

dfs and similar, http://cs101.openjudge.cn/pctbook/T02754

思路：

自己思考时没想到什么解决斜线的方法，今天听讲解听懂了（）
但是晚上都是课来不及自己重新敲了……可以的话下次补上？
代码

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### T01958 Strange Towers of Hanoi

http://cs101.openjudge.cn/practice/01958/

思路：



代码

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

期中周任务有点多没有另外做什么题……基本上就是看题解和讲解缓慢学习中吧



