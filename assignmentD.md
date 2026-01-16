# Assignment #D: Mock Exam下元节

Updated 1729 GMT+8 Dec 4, 2025

2025 fall, Complied by 蒋欣宜 2500011806



>**说明：**
>
>1. Dec⽉考： ==AC4（p.s.月考当天不太舒服，周末抽了两小时限时写的）== 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。
>
>2. 解题与记录：对于每一个题目，请提供其解题思路（可选），并附上使用Python或C++编写的源代码（确保已在OpenJudge， Codeforces，LeetCode等平台上获得Accepted）。请将这些信息连同显示“Accepted”的截图一起填写到下方的作业模板中。（推荐使用Typora https://typoraio.cn 进行编辑，当然你也可以选择Word。）无论题目是否已通过，请标明每个题目大致花费的时间。
>
>3. 提交安排：提交时，请首先上传PDF格式的文件，并将.md或.doc格式的文件作为附件上传至右侧的“作业评论”区。确保你的Canvas账户有一个清晰可见的本人头像，提交的文件为PDF格式，并且“作业评论”区包含上传的.md或.doc附件。
> 
>4. 延迟提交：如果你预计无法在截止日期前提交作业，请提前告知具体原因。这有助于我们了解情况并可能为你提供适当的延期或其他帮助。  
>
>请按照上述指导认真准备和提交作业，以保证顺利完成课程要求。





## 1. 题目

### E29945:神秘数字的宇宙旅行 

implementation, http://cs101.openjudge.cn/practice/29945

思路：



代码

```python
n=int(input())  
while n>1:  
    if n%2==0:  
        print(str(n)+"/2="+str(n//2))  
        n=n//2  
    else:  
        print(str(n)+"*3+1="+str(n*3+1))  
        n=3*n+1  
print("End")
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251209154718.png]]



### E29946:删数问题

monotonic stack, greedy, http://cs101.openjudge.cn/practice/29946

思路：

简单题没检查运行了一下没报错就直接交了结果RE，一看打错了…还是不能掉以轻心（）

代码

```python
n=input()  
k=int(input())  
result=""  
for i in range(len(n)-k):  
    num=n.index(min(n[0:k+1]))  
    result+=n[num]  
    n=n[num+1:]  
    k-=num  
print(int(result))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>


![[Pasted image 20251209154439.png]]


### E30091:缺德的图书馆管理员

greedy, http://cs101.openjudge.cn/practice/30091

思路：

有点像脑筋急转弯
由于同学的编号是无意义的，所以两人同时转向和两人原方向前进毫无区别，直接按固定方向理解就可以

代码

```python
l=int(input())  
n=int(input())  
lst=list(map(int,input().split()))  
min_time,max_time=0,0  
for i in range(n):  
    min_time=max(min_time,min(lst[i],l+1-lst[i]))  
    max_time=max(max_time,max(lst[i],l+1-lst[i]))  
print(min_time,max_time)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>


![[Pasted image 20251209154742.png]]


### M27371:Playfair密码

simulation，string，matrix, http://cs101.openjudge.cn/practice/27371


思路：
感觉这次前三题和后三题难度跨度有点大zzz
思维难度其实不高但是真的麻烦，用了好多不同语法，打了50多行考完简化了一下还有40行…一大半耗时在敲代码上了，虽然思路还算清晰没怎么卡也耗时都快有一小时了zzz导致后两题都没来得及
开始担心机考根本写不完


代码

```python
def pair(text):  
    i=0  
    pairs=[]  
    while i<len(text)-1:  
        if text[i]==text[i+1]:  
            pairs.append((text[i], 'q' if text[i]=='x' else 'x'))  
            i+=1  
        else:  
            pairs.append((text[i], text[i+1]))  
            i+=2  
    if i==len(text)-1:  
        pairs.append((text[i],'q'if text[i] =='x' else 'x'))  
    return pairs #把预处理单独def了一下，这个区别不大，但感觉看起来舒服点 
  
dic=["a","b","c","d","e","f","g","h","i","k","l","m","n",
"o","p","q","r","s","t","u","v","w","x","y","z"] #用列表比直接字符串alphabet的优势是可以直接用pop删，不用再跑一遍循环补全剩余 
key=input().replace("j","i")  
lst=[]  
for i in range(len(key)):  
    if key[i] not in lst:  
        lst.append(key[i])  
        dic.pop(dic.index(key[i]))  
lst=lst+dic  #因为后续直接用除余处理，此处可以不用再生成矩阵
pos={ch: (i//5, i%5) for i, ch in enumerate(lst)}  #创建字典映射，还是很有用的，不用再去一一找索引，看了下题解也是用了这个
  
n=int(input())  
for i in range(n):  #嗯其实用sys很好…差别不大懒得改了
    result=""  
    word=input().replace("j","i")  
    a=pair(word)  
    for i in a:  
        r1,c1= pos[i[0]]  
        r2,c2= pos[i[1]]  
        if r1==r2:  
            c1,c2=(c1+1) %5,(c2+1)%5  
        elif c1 == c2:  
            r1,r2=(r1+1)%5,(r2+1)%5  
        else:  
            c1,c2 =c2,c1  
        result=result+lst[r1*5+c1]+lst[r2*5+c2]  #直接利用最初的key索引返回对应值
    print(result)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251209151845.png]]



### T30201:旅行售货商问题

dp,dfs, http://cs101.openjudge.cn/practice/30201

思路：

还是不太会dp和dfs…听课大致明白了，但今天有晚课和夜训来不及实操zzz

代码

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### T30204:小P的LLM推理加速

greedy, http://cs101.openjudge.cn/practice/30204

思路：

确实不难的贪心（）纯粹时间不够加被文字描述吓到了，感觉这题比T4简单应该只有M的
其实可以直接得出最优方案，但思维转化成代码还是有点繁琐，需要考虑各种if else，
还是尹同学的这个方法更加直接清晰（赞美）

代码

```python
n,m = map(int,input().split())  
simble,pairs = [], []  
for i in range(n):  
    x,y = map(int,input().split())  
    simble.append(x)  
    pairs.append(x+y)  
simble.sort()  
pair = min(pairs)  
ans = 0  
pre = [0]  
for i in simble:  
    pre.append(pre[-1]+i)  
for i,p in enumerate(pre):  
    ans = max(ans,((m-p)//pair)*2+i)  
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251209233124.png]]



## 2. 学习总结和收获

如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。





