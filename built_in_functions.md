# 内置函数

针对 3.10 增加了 aiter() 和 anext(). 其他还好.

## 按功能 by usage

### 数学计算

abs()   divmod()    len()   max()   min()
pow()   round()     sum()

### 判断

all()   any()   bool()
callable()
isinstance()
issubclass()
type()

### 类型转换

ascii()     bin()   chr()   float()     hex()
int()       oct()   ord()   str()       bytes()

### 异步

aiter()     anext()

### 编译,调试,执行

breakpoint()
compile()
dir()
eval()
exec()
id()
locals()    globals()
vars()

### 输入输出

input()
print()     format()

### 类型定义

bytearray()     complex()       dict()
frozenset()     list()          set()
tuple()

### 类 class

classmethod()
delattr()   getattr()   setattr()
object()
property()
super()

### 杂项

hash()
help()
open()
`__import__()`

### 迭代

enumerate()     filter()    iter()      map()
next()          range()     repr()      reversed()
slice()         sorted()    staticmethod()
zip()

### 内存操作

memoryview()

## 按字母顺序 by alphabet

### A

`abs(x)`    整数/浮点/复数都可以. 实现 `__abs__()` 的也可以.
`aiter(async_iterable)`     3.10才开始有. 返回异步迭代器, 等效于 `x.__aiter__()`
`all(iteralbe)`     全 True 返回 True. 空也是 True

```python
>>> all([])
True
```

`anext()`

`any(iterable)`     任一 True 就返回 True. 空返回 False.

```python
>>> any([])
False
```

anext

ascii

### B

bin()

bool()

breakpoint()

bytearray()

bytes()

### C

callable()
chr()
classmethod()
compile()
complex()

### D

delattr()
dict()
dir()
divmod()

### E

enumerate()
eval()
exec()

### F

filter()
float()
format()
forzenset()

### G

getattr()
globals()

### H

hasattr()
hash()
help()
hex()

### I

id()
input()
int()
isinstance()
issubclass()
iter()

### L

len()
list()
locals()

### M

map()
max()
memoryview()
min()

### N

next()

### O

object()
oct()
open()
ord()

### P

pow()
print()
property()

### R

range()
repr()
reversed()
round()

### S

set()
setattr()
slice()
sorted()
staticmethod()
str()
sum()
super()

### T

tuple()
type()

### V

vars()

### Z

zip()