# Python基本概念和语法

## 1. Python概述

### 1.1 Python特点
- **简洁易读**：语法简洁，接近自然语言
- **解释型语言**：无需编译，逐行执行
- **动态类型**：变量类型在运行时确定
- **丰富的库**：标准库和第三方库丰富
- **跨平台**：支持Windows、Linux、macOS
- **面向对象**：支持面向对象编程

### 1.2 Python程序结构
```python
# 注释
"""
多行注释
"""

def main():
    print("Hello, World!")

if __name__ == "__main__":
    main()
```

## 2. 数据类型与变量

### 2.1 基本数据类型
| 类型 | 关键字 | 示例 |
|------|--------|------|
| 整数 | int | 100, -50, 0 |
| 浮点数 | float | 3.14, -2.5, 1e10 |
| 字符串 | str | "hello", 'world' |
| 布尔值 | bool | True, False |
| 空值 | NoneType | None |

### 2.2 变量
```python
# 变量赋值
name = "张三"
age = 25
score = 95.5
is_student = True

# 多变量赋值
a, b, c = 1, 2, 3
x = y = z = 0

# 类型转换
int("123")      # 字符串转整数
float("3.14")   # 字符串转浮点数
str(123)        # 整数转字符串
bool(0)         # 0转为False
```

### 2.3 运算符
```python
# 算术运算符
+   # 加法
-   # 减法
*   # 乘法
/   # 除法（返回浮点数）
//  # 整除（向下取整）
%   # 取余
**  # 幂运算

# 比较运算符
==  # 等于
!=  # 不等于
>   # 大于
<   # 小于
>=  # 大于等于
<=  # 小于等于

# 逻辑运算符
and # 逻辑与
or  # 逻辑或
not # 逻辑非

# 位运算符
&   # 按位与
|   # 按位或
^   # 按位异或
~   # 按位取反
<<  # 左移
>>  # 右移
```

## 3. 控制结构

### 3.1 选择结构
```python
# if-elif-else语句
score = 85

if score >= 90:
    print("优秀")
elif score >= 80:
    print("良好")
elif score >= 60:
    print("及格")
else:
    print("不及格")

# 三元表达式
result = "及格" if score >= 60 else "不及格"

# match-case（Python 3.10+）
command = "quit"
match command:
    case "quit":
        print("退出")
    case "start":
        print("开始")
    case _:
        print("未知命令")
```

### 3.2 循环结构
```python
# for循环
for i in range(10):
    print(i)

for i in range(1, 11):
    print(i)

for i in range(0, 20, 2):  # 步长为2
    print(i)

# while循环
count = 0
while count < 5:
    print(count)
    count += 1

# break和continue
for i in range(10):
    if i == 3:
        continue  # 跳过3
    if i == 7:
        break     # 跳出循环
    print(i)
```

### 3.3 列表推导式
```python
# 基本语法
squares = [x**2 for x in range(10)]

# 带条件
evens = [x for x in range(20) if x % 2 == 0]

# 嵌套
matrix = [[i*j for j in range(3)] for i in range(3)]

# 字典推导式
square_dict = {x: x**2 for x in range(5)}

# 集合推导式
square_set = {x**2 for x in range(5)}
```

## 4. 数据结构

### 4.1 列表（List）
```python
# 创建列表
fruits = ["apple", "banana", "cherry"]
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", 3.14, True]

# 访问元素
fruits[0]        # "apple"
fruits[-1]       # "cherry"
fruits[0:2]      # ["apple", "banana"]

# 修改元素
fruits[0] = "orange"

# 列表方法
fruits.append("date")        # 末尾添加
fruits.insert(1, "banana2")  # 指定位置插入
fruits.remove("banana")      # 删除指定值
fruits.pop()                 # 弹出末尾元素
fruits.sort()                # 排序
fruits.reverse()             # 反转
len(fruits)                  # 长度
```

### 4.2 元组（Tuple）
```python
# 创建元组
coordinates = (10, 20)
single = (5,)  # 单元素元组需要逗号

# 访问元素
coordinates[0]  # 10

# 元组不可修改
# coordinates[0] = 30  # 错误！

# 元组解包
x, y = coordinates
```

### 4.3 字典（Dictionary）
```python
# 创建字典
person = {
    "name": "张三",
    "age": 25,
    "city": "北京"
}

# 访问值
person["name"]  # "张三"
person.get("age", 0)  # 带默认值

# 修改和添加
person["age"] = 26
person["email"] = "test@example.com"

# 删除
del person["city"]
person.pop("email")

# 字典方法
person.keys()     # 所有键
person.values()   # 所有值
person.items()    # 所有键值对

# 遍历字典
for key, value in person.items():
    print(f"{key}: {value}")
```

### 4.4 集合（Set）
```python
# 创建集合
fruits = {"apple", "banana", "cherry"}

# 添加和删除
fruits.add("date")
fruits.remove("banana")

# 集合运算
set1 = {1, 2, 3}
set2 = {3, 4, 5}

set1 | set2    # 并集 {1, 2, 3, 4, 5}
set1 & set2    # 交集 {3}
set1 - set2    # 差集 {1, 2}
set1 ^ set2    # 对称差集 {1, 2, 4, 5}
```

## 5. 函数

### 5.1 函数定义
```python
# 基本函数
def greet(name):
    return f"Hello, {name}!"

# 带默认参数
def power(x, n=2):
    return x ** n

# 带关键字参数
def introduce(name, age, city):
    print(f"{name} is {age} years old, from {city}")

introduce(name="张三", age=25, city="北京")
```

### 5.2 可变参数
```python
# *args：可变位置参数
def add(*args):
    return sum(args)

add(1, 2, 3)  # 6

# **kwargs：可变关键字参数
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="张三", age=25)
```

### 5.3 Lambda函数
```python
# 匿名函数
square = lambda x: x ** 2
square(5)  # 25

# 作为参数
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x**2, numbers))
evens = list(filter(lambda x: x % 2 == 0, numbers))
```

### 5.4 作用域
```python
x = 10  # 全局变量

def func():
    x = 20  # 局部变量
    print(x)  # 20

func()
print(x)  # 10

def func2():
    global x  # 声明全局变量
    x = 30

func2()
print(x)  # 30
```

## 6. 面向对象编程

### 6.1 类的定义
```python
class Dog:
    # 类属性
    species = "犬科"

    # 初始化方法
    def __init__(self, name, age):
        self.name = name  # 实例属性
        self.age = age

    # 实例方法
    def bark(self):
        return f"{self.name} says: 汪汪!"

    # 类方法
    @classmethod
    def get_species(cls):
        return cls.species

    # 静态方法
    @staticmethod
    def is_adult(age):
        return age >= 3

# 创建对象
my_dog = Dog("旺财", 5)
print(my_dog.bark())
```

### 6.2 继承
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return f"{self.name} says: 汪汪!"

class Cat(Animal):
    def speak(self):
        return f"{self.name} says: 喵喵!"

# 多态
animals = [Dog("旺财"), Cat("小花")]
for animal in animals:
    print(animal.speak())
```

### 6.3 魔术方法
```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return f"({self.x}, {self.y})"

    def __repr__(self):
        return f"Point({self.x}, {self.y})"

    def __eq__(self, other):
        return self.x == other.x and self.y == other.y

    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)
```

## 7. 异常处理

### 7.1 基本语法
```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"除零错误: {e}")
except Exception as e:
    print(f"其他错误: {e}")
else:
    print("没有错误")
finally:
    print("无论如何都会执行")
```

### 7.2 常见异常
```python
# ValueError：值错误
int("abc")

# TypeError：类型错误
"hello" + 123

# IndexError：索引错误
[1, 2, 3][5]

# KeyError：键错误
{"name": "张三"}["age"]

# FileNotFoundError：文件未找到
open("nonexistent.txt")

# AttributeError：属性错误
"hello".push("!")
```

### 7.3 自定义异常
```python
class CustomError(Exception):
    def __init__(self, message):
        self.message = message
        super().__init__(message)

def check_age(age):
    if age < 0:
        raise CustomError("年龄不能为负数")
    return True

try:
    check_age(-5)
except CustomError as e:
    print(e)
```

## 8. 文件操作

### 8.1 文件读写
```python
# 写入文件
with open("file.txt", "w") as f:
    f.write("Hello, World!\n")
    f.write("第二行\n")

# 读取文件
with open("file.txt", "r") as f:
    content = f.read()
    print(content)

# 逐行读取
with open("file.txt", "r") as f:
    for line in f:
        print(line.strip())
```

### 8.2 文件模式
| 模式 | 说明 |
|------|------|
| 'r' | 只读（默认） |
| 'w' | 写入（覆盖） |
| 'a' | 追加 |
| 'x' | 创建（已存在则报错） |
| 'b' | 二进制模式 |
| 't' | 文本模式（默认） |
| '+' | 读写模式 |

### 8.3 JSON操作
```python
import json

# 写入JSON
data = {"name": "张三", "age": 25}
with open("data.json", "w", encoding="utf-8") as f:
    json.dump(data, f, ensure_ascii=False, indent=2)

# 读取JSON
with open("data.json", "r", encoding="utf-8") as f:
    data = json.load(f)
    print(data)
```

## 9. 模块与包

### 9.1 导入模块
```python
import math
print(math.pi)

from math import sqrt, pow
print(sqrt(16))

from datetime import datetime as dt
print(dt.now())

import os.path as path
```

### 9.2 常用标准库
```python
import os          # 操作系统接口
import sys         # 系统参数
import math        # 数学函数
import random      # 随机数
import datetime    # 日期时间
import re          # 正则表达式
import json        # JSON处理
import collections # 高级数据结构
import itertools   # 迭代器工具
import functools   # 函数工具
```

### 9.3 包结构
```
mypackage/
├── __init__.py
├── module1.py
├── module2.py
└── subpackage/
    ├── __init__.py
    └── module3.py
```

```python
# 导入包中的模块
import mypackage.module1
from mypackage import module2
from mypackage.subpackage import module3
```

## 10. 常见考点

### 10.1 可变与不可变类型
```python
# 不可变类型
x = 10
y = x
x = 20
print(y)  # 10，y不变

# 可变类型
list1 = [1, 2, 3]
list2 = list1
list1.append(4)
print(list2)  # [1, 2, 3, 4]，list2也变了
```

### 10.2 浅拷贝与深拷贝
```python
import copy

list1 = [[1, 2], [3, 4]]
list2 = copy.copy(list1)     # 浅拷贝
list3 = copy.deepcopy(list1) # 深拷贝

list1[0][0] = 100
print(list2)  # [[100, 2], [3, 4]]，浅拷贝受影响
print(list3)  # [[1, 2], [3, 4]]，深拷贝不受影响
```

### 10.3 装饰器
```python
import functools

def timer(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        import time
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} 执行时间: {end - start:.2f}秒")
        return result
    return wrapper

@timer
def slow_function():
    import time
    time.sleep(1)
    return "完成"
```

### 10.4 生成器与迭代器
```python
# 生成器函数
def fibonacci():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

# 使用生成器
fib = fibonacci()
for _ in range(10):
    print(next(fib))

# 生成器表达式
squares = (x**2 for x in range(10))
```

### 10.5 上下文管理器
```python
# 自定义上下文管理器
class FileManager:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
        self.file = None

    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file

    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.file:
            self.file.close()

# 使用
with FileManager("test.txt", "w") as f:
    f.write("Hello")
```
