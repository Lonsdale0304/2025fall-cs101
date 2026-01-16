# Assignment #5: 20251009 cs101 Mock Exam寒露第二天

Updated 1651 GMT+8 Oct 9, 2025

2025 fall, Complied by 蒋欣宜 2500011806 化院



## 1. 题目

### E29895: 分解因数

implementation, http://cs101.openjudge.cn/practice/29895/



思路：

总用时5min

代码

```python
n=int(input())
for i in range(2,n):
    if n%i==0:
        print(n//i)
        break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251010160907.png]]



### E29940: 机器猫斗恶龙

greedy, http://cs101.openjudge.cn/practice/29940/



思路：

总用时5min

代码

```python
n=int(input())
m=list(map(int,input().split()))
a,least=1,1
for i in m:
    a-=i
    if a>least:
        least=a
print(least)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251010160934.png]]



### M29917: 牛顿迭代法

implementation, http://cs101.openjudge.cn/practice/29917/



思路：

因为没看懂题目中切线是什么意思没敢写（x）
实际上只要记得不定行和保留小数点就很简单了
用时大概20min

代码

```python
import sys  
a=sys.stdin.read().splitlines()  
for j in range(len(a)):  
    n=float(a[j])  
    m,m1,i=1,0,0  
    while abs(m-m1)>=1E-6:  
        m,m1=0.5*(m+n/m),m  
        i+=1  
    print(i,"%.2f"%m)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251012180324.png]]



### M29949: 贪婪的哥布林

greedy, http://cs101.openjudge.cn/practice/29949/



思路：

将矿石按价格排序,用index返回对应重量，注意一下装不满和一种都装不下的情况
##### **对这道题有一个很大的疑惑：**
注意到如果列表中有多个相同值，sort后返回index只会返回第一个，而如果每次取完最值后remove掉则是对的，例子如下：
```python
a=[1,3,2,1,5,1,2,0]  
b=[1,2,3,4,5,6,7,8]  
m,n=[],[]  
a1=sorted(a,reverse=True)  
for i in range(len(a)):  
    m.append(b[a.index(a1[i])])
print(m)       
for i in range(len(a)):  
    x=a.index(max(a))  
    n.append(b[x])  
    a.remove(a[x]),b.remove(b[x])  
print(n)
```
![[Pasted image 20251013111510.png]]
那为何这道题用sort后返回index可以AC，remove最大值反而会WA？是不涉及这种价值相同的情况，还是后者有一些其他问题？

代码

```python
n,m=map(int,input().split())  
price,weight=[],[]  
total=0  
for i in range(n):  
    v,w=map(int,input().split())  
    weight.append(w),price.append(v/w)  
price1=sorted(price,reverse=True)  
for i in range(n):  
    a=price.index(price1[i])  
    if weight[a]>=m:  
        total+=price[a]*m  
        break  
    else:  
        m-=weight[a]  
        total+=weight[a]*price1[i]  
print("%.2f"%total)
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251010200404.png]]



### M29918: 求亲和数

implementation, http://cs101.openjudge.cn/practice/29918/



思路：

利用因数成对的性质，在分解因数时通过开根号缩短所需时间以防tle即可
跟同学讨论的时候说到也许可以直接用质因数的欧拉公式（？）
用时18min

代码

```python
def familiar(m):
    a=1
    for j in range(2,int(m**0.5+1)):
        if m%j==0:
            a+=j+m//j
    return a
n=int(input())
for i in range(n+1):
    b=familiar(i)
    if i<b<=n:
        if familiar(b)==i:
            print(i,b)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251010190623.png]]




### T29947:校门外的树又来了（选做）

http://cs101.openjudge.cn/practice/29947/



思路：

（内存限制不让用遍历所有树后就变成数学题)
一种想法：将所有地铁按起点顺序排列；如果后一段和前面有重叠，就叠加合并为更长的一段；如果没有重叠，就新建一段；最后统计会占用的位置数
（已经做了一些简化但感觉还是有点麻烦，好奇有没有简便做法）

代码

```python
length,number=map(int,input().split())
start,end=[],[]
for i in range(number):
    a,b=map(int, input().split())
    start.append(a),end.append(b)
start1=sorted(start)
x,y=[start1[0]],[end[start.index(start1[0])]]
n=0
for i in range(number):
    a=start1[i]
    b=end[start.index(a)]
    if a<=y[n]:
        y[n]=max(y[n],b)
    else:
        x.append(a),y.append(b)
        n+=1
print(length-(sum(y)-sum(x)+len(x))+1)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251010190546.png]]




## 2. 学习总结和收获

##### 关于不定行输入：
```python
import sys
sys.stdin.read()#读取多行，为一整个字符串，但会换行
sys.stdin.readline()#仅读取一行为字符串
sys.stdin.readlines()#读取多行，总体为列表，每行为字符串形式，但会带"/n"
sys.stdin.read().splitlines()#不会带"/n",其他同上
#或：
while true:
	try:
	except EOFError:  
        break
```

（其他的题过两天再放？）

