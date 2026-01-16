# Assignment #3: 语法练习

Updated 1440 GMT+8 Sep 23, 2025

2025 fall, Complied by 2500011806 蒋欣宜 化院


==（不知道10.8交包不包括10.8当天……这份先交了，其他有些笔记心得写在没带回家的板子里，等10.8回到学校拿上会再交一遍）==


## 1. 题目

### E28674:《黑神话：悟空》之加密

http://cs101.openjudge.cn/pctbook/E28674/



思路：

略

代码

```python
k=int(input())%26  
s=input()  
s1=""  
for i in range(len(s)):  
    if 65<=ord(s[i])<65+k or 97<=ord(s[i])<97+k:  
        s1+=chr(ord(s[i])-k+26)  
    else:  
        s1+=chr(ord(s[i])-k)  
print(s1)

```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20250924150807.png]]


### E28691: 字符串中的整数求和

http://cs101.openjudge.cn/pctbook/E28691/


思路：

略（好短）

代码

```python
n=input().replace(' ','')  
print(int(n[:2])+int(n[3:5]))
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[ab220a8b-93f3-4e4c-8f17-7e8fcdb2d40d.png]]


### M28664: 验证身份证号 

http://cs101.openjudge.cn/pctbook/M28664/



思路：

本来在思考可否直接replace和translate，但由于出现两位数和非int类型的X，感觉本题还是得用到字典或者字符串转化……不知道还有什么简化方法

代码

```python
dic={0:1,1:0,2:"X",3:9,4:8,5:7,6:6,7:5,8:4,9:3,10:2}
key=[7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2]
n=int(input())
result=[]
for i in range(n):
    x=input()
    y=0
    for j in range(17):
        y+=int(x[j])*key[j]
    if str(dic[y%11])==x[17]:
        print("YES")
    else:
        print("NO")
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>


![[4a9658b339fc3ddd13c1476b6e81dba2.png]]


### M28678: 角谷猜想

http://cs101.openjudge.cn/pctbook/M28678/


思路：

很想知道这道题难度为什么是M不是E……

代码

```python
n=int(input())  
while n>1:  
    if n%2==1:  
        print(str(n)+"*3+1="+str(n*3+1))  
        n=n*3+1  
    else:  
        print(str(n)+"/2="+str(n//2))  
        n=n//2  
print("End")
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### M28700: 罗马数字与整数的转换

http://cs101.openjudge.cn/pctbook/M28700/


思路：

- 阿拉伯数字转罗马数字：第一遍AC时采用类似进制转换的累减/除余方法，非常暴力地写了一堆if elif else…虽然逻辑是清晰的但是过于繁琐
后来才想到其实可以一位一位翻译，不需要数学，直接用字典zzz（其实列表会更短更好打就是字典对应看起来更清楚一点）
改完整个代码看着都舒服了
（这次是思维定势害人实例）
- 罗马数字转阿拉伯数字：罗马数字表义有一位和两位两种，于是想到直接把两位的find统计后去除，剩下的count
*感觉这道题思路应该会有很多，翻了下这个六百多B代码应该算比较短的了，但也看到有四五百的，很好奇是怎么写的

代码

```python 
n=input()  
m=""  
if n[0] in "1234567890":  
    dic={"9":["IX","XC","CM"],"8":["VIII","LXXX","DCCC"],"7":["VII","LXX","DCC"],"6":["VI","LX","DC"],"5":["V","L","D"],  
         "4":["IV","XL","CD"],"3":["III","XXX","CCC","MMM"],"2":["II","XX","CC","MM"],"1":["I","X","C","M"],"0":["","",""]}  
    for i in range(len(n)):  
        m=m+dic[n[i]][len(n)-1-i]  
else:  
    m=0  
    dic={"CM":900,'CD':400,'XC':90,'XL':40,'IX':9,"IV":4}  
    for i in dic:  
        a=n.find(i)  
        if a!=-1:  
            m+=dic[i]  
            n=n[:a]+n[a+2:]  
    m=(m+n.count('I')+n.count('X')*10+n.count('C')*100+n.count('M')*1000  
       +n.count("V")*5+n.count("L")*50+n.count("D")*500)  
print(m)
```


代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[52d5550daea9a034462a80142c48d0a7.png]]


### 158B. Taxi

*special problem, greedy, implementation, 1100,  https://codeforces.com/problemset/problem/158/B



思路：

类比下文装箱的简易版

代码

```python
group=int(input())  
m=list(map(int,input().split()))  
n1=m.count(4)  
n2=m.count(3)  
n3=m.count(2)  
n4=(group-n1-n2-n3)-n2-n3%2*2  
if n4<=0:  
    print(n1+n2+(n3+1)//2)  
else:  
    print(n1+n2+(n3+1)//2+(n4+3)//4)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![[Pasted image 20251001163432.png]]



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2025fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

*（p.s.写完了才发现装箱是下一次的作业orz…想想不删了）*
#### M1017：装箱问题

http://cs101.openjudge.cn/pctbook/M01017/

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

