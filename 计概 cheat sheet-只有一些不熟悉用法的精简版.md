```python
import sys  
from collections import deque  
import math
def solve()
if __name__ == '__main__':  
        solve()
```
enumerate(iterable, start=0)———映射：需要索引和对应的元素一起时
- `iterable`：一个可迭代对象（如列表、元组、字符串等）。
- `start`：索引起始值，默认为0。
- **返回值：**  返回一个枚举对象，该对象生成由索引和对应的元素组成的元组（无括号）。
- **不可直接修改原始数据**：enumerate() 返回的是元组，不能直接修改

关于不定行输入：
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
sys.stdout.write()
’‘’-作用：直接将字符串写入标准输出缓冲区
    - `print()`：函数调用开销 + 自动换行 + 可能会刷新缓冲区
    - `sys.stdout.write()`：直接写入，没有额外开销‘’‘
```

#### 排序：
lst.sort(key=lambda x:-x[1])
排序依据和正负小

向上取整：可用math.ceil,或者更原始的int负数

大小写转换：uper、lower；替换：replace

**translate：**
mapping=str.maketrans('ABCDEFGHIJKLMNOPRSTUVWXY','222333444555666777888999')  ；x=x.translate(mapping)  

带数据和文字输出：print(f'{n}:{a}->{c}')  
列表无括号输出：print(",".join(map(str,dic[i])))

读取矩阵：
matrix=[list(map(int, input().split())) for _ in range(n)]

### **迭代器**
data = sys.stdin.buffer.read().split()
it = iter(data)  # 创建迭代器
a=next(it)
**主要目的**：不是为了提高速度，而是为了方便**顺序访问**数据。
### set
集合
### tle情况下的优化
#### ==用pypy3交试试！！！==
> - **sys.stdin.read**: 原代码在循环里用 input()，每次都要处理缓冲区。用 read().split() 将所有数据一次性读入内存并切分，配合迭代器 iter() 和 next()，是 Python 刷题处理大量数据的标准做法。
> - **列表 vs 字典**: 列表要快得多。
> - **去除 min() 函数**: 这改成 if val < dp[new][k]: dp[new][k] = val 虽
### deque
`deque`（双端队列）是Python `collections`模块中的一个数据结构，**支持从两端高效添加和删除元素**。它是线程安全的，内存高效，适合队列和栈的操作。

 **1. 基本特性**
- **双向操作**：可在队列**左端（front）**和**右端（rear）**进行添加/删除
 **添加元素**
d = deque([1, 2, 3])
 右端添加
d.append(4)                   # deque([1, 2, 3, 4])
d.extend([5, 6])              # deque([1, 2, 3, 4, 5, 6])
 左端添加
d.appendleft(0)               # deque([0, 1, 2, 3, 4, 5, 6])
d.extendleft([-2, -1])        # 注意：逆序添加！deque([-1, -2, 0, 1, 2, 3, 4, 5, 6])
 **删除元素**
d = deque([1, 2, 3, 4, 5])
右端删除
d.pop()                       # 返回5，deque变为[1, 2, 3, 4]
左端删除
d.popleft()                   # 返回1，deque变为[2, 3, 4]
**旋转**
d.rotate(2)                   # 右移2位：[4, 5, 1, 2, 3]
d.rotate(-1)                  # 左移1位：[5, 1, 2, 3, 4]
**计数**
d = deque([1, 2, 2, 3])
d.count(2)                    # 返回2


| 操作   | list   | deque  | 说明      |
| ---- | ------ | ------ | ------- |
| 左端插入 | `O(n)` | `O(1)` | deque完胜 |
| 右端插入 | `O(1)` | `O(1)` | 相当      |
| 中间插入 | `O(n)` | `O(n)` | 相当      |
| 左端删除 | `O(n)` | `O(1)` | deque完胜 |
| 随机访问 | `O(1)` | `O(n)` | list完胜  |
| 内存效率 | 较低     | 较高     | deque更优 |

#### `enumerate()` 基本语法
```python
enumerate(iterable, start=0)
```
- `iterable`：可迭代对象
- `start`：索引起始值，默认为 0

注意事项：
1. **不可直接修改原始数据**：enumerate() 返回的是元组，不能直接修改
2. **惰性求值**：enumerate() 返回的是生成器，只在需要时计算

### 2. 自定义起始索引
```python
for index, fruit in enumerate(fruits, start=1):
    print(index, fruit)
# 输出：
# 1 apple
# 2 banana
# 3 orange
```
### 2. 同时需要索引和元素值
```python
# 找出列表中所有偶数元素的位置
numbers = [3, 8, 5, 12, 7, 20]
even_positions = []

for i, num in enumerate(numbers):
    if num % 2 == 0:
        even_positions.append(i)

print(even_positions)  # 输出: [1, 3, 5]
```
### 3. 转换为列表或字典
```python
# 转换为列表
fruits = ['apple', 'banana', 'orange']
enum_list = list(enumerate(fruits))
print(enum_list)  # 输出: [(0, 'apple'), (1, 'banana'), (2, 'orange')]

# 转换为字典
enum_dict = dict(enumerate(fruits, start=1))
print(enum_dict)  # 输出: {1: 'apple', 2: 'banana', 3: 'orange'}
```
### 1. 与条件判断结合
```python
# 找出特定元素的所有位置
values = [1, 3, 5, 3, 8, 3]
target = 3
positions = [i for i, val in enumerate(values) if val == target]
print(positions)  # 输出: [1, 3, 5]
```
### 2. 在复杂循环中使用
```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# 遍历二维列表
for row_idx, row in enumerate(matrix):
    for col_idx, value in enumerate(row):
        print(f"matrix[{row_idx}][{col_idx}] = {value}")
```
### 3. 并行迭代多个列表
```python
names = ['Alice', 'Bob', 'Charlie']
scores = [85, 92, 78]

for i, (name, score) in enumerate(zip(names, scores)):
    print(f"{i+1}. {name}: {score}分")
```