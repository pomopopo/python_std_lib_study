# 内置数据类型

## 谁是 True?

只要知道谁是 False 就可以:

- 已定义好的常量: None, False
- 数值为 0 的数: 0, 0.0, 0j, Decimal(0), Fraction(0, 1)
- 空序列/空集合: '', (), {}, [], set(), range(0)

trick: `not not a_var`  快速转换成 bool 类型

## 逻辑操作 and, or, not

注意事项:

- `a = x or y` 当 x 不存在/为0/false时候, a = y. 比较常见
- `a = x and y` 当 x 是false, a = x. 少见?
- `not a == b` 相当于 `not (a == b)`. 因为 not 优先级比较低.

## 比较

- `x < y < z` 相当于 `x < y and y < z`, 但 y 只需要计算一次; 如果前半句 False 的话, 后半句在两种情况下都不计算.
- 定义了 `__eq__()`, `__lt__()`, `__le__()`, `__qt__()`, `__ge__()` (通常定义 `__lt__()`, `__eq__()` 即可)的类,就可以用来比较了.
- `is`, `is not` 不能重载
- `in`, `not in` 只要实现 `可迭代` 或 `__contains__()` 就可以支持.

## 数值类型 int, float, complex

- boolean 是整数的子类型
- 整数有无限精度
- 浮点数通常由该平台 C 的双精度数实现. Ref `sys.float_info`

```python
>>> sys.float_info
sys.float_info(max=1.7976931348623157e+308, max_exp=1024, max_10_exp=308, min=2.2250738585072014e-308, min_exp=-1021, min_10_exp=-307, dig=15, mant_dig=53, epsilon=2.220446049250313e-16, radix=2, rounds=1)
```

### 可用的运算符 `+ - * / // **`

### 常见函数

- abs(), int(), float(), complex(re,im), c.conjugate(), divmode(), pow(x,y)
- math.trunc(x), round(x[,n]), math.floor(x), math.ceil(x)

## 整数的操作 `| ^ & << >> ~`

- 位操作, 不能左移 or 右移 负数, 报 ValueError
- int.bit_length() 需要用多少 bit 表示一个 int
- int.bit_count() 一个数的二进制里 1 的个数!
- int.to_bytes(length, byteorder, *, signed=False) 整数的 bytes 格式. byteorder = 'big' | 'little'
- int.from_bytes(bytes, byteorder, *, signed=False) byte array 转 int
- int.as_integer_ratio() 转成分式tuple (x, 1). 如果是整数的话, 分母恒为 1. (3.8 才开始有) (ref float.as_integer_ratio())

## 浮点数的一些操作

- float.as_integer_ratio() 浮点数转为整数比 (分子, 分母). 返回结果是个 tuple
- float.is_integer() 判断是不是整数. e.g. `(-2.0).is_integer() == True`
- float.hex() 返回浮点数的 16 进制表示, 格式: [sign] 0x 整数部分 ['.' 分数部分] [p 指数部分]. int 是没有 .hex() 的.
- float.fromhex(s) 把 16 进制字符串转为浮点数.

## 可迭代类型

容器类的话, 要实现 `__iter__()` 才是可迭代的.

满足 `__iter__()` 和 `__next__()` 的, 就是可迭代类型.

- iterator.`__iter__()` 返回迭代器自己, 如果没定义的话, 解释器会退阶找 `__getitem__`.
- iterator.`__next__()` 返回下一个元素, 内置函数 `next()` 也是调这个.

p.s. 一个 `__next__()` 如果报 `StopIteration` 异常了, 后续就要一直报异常, 不能后面改掉.

## 生成器类型

(详见 yield)

## 序列 list, tuple, range

- 常见操作: in, not in, +, *, 切片, len(), max(), min(), .index(x[, i[, j]]), .count(x)
- 注意 `*` 的坑: `[[]]*3` 得到的是 3 个指向同一地址的 []

## 不可变序列

tuple, 字典的键值, set, frozenset

## 可变序列

自己定义可变序列的话, 建议从 `collections.abc.MutableSequence` 拓展

可用的操作:

- 切片 [i], [i:j], [i:j:k]
- del s[i:j] 相当于 s[i:j] = []
- append(x), clear(), copy() (浅拷贝), extend(t), insert(i, x), pop(), pop(i), remove(x), reverse()

## list

可用的方法有:

- sort(*, key=None, reverse=False)

## tuple

怎么造一个

- 用括号 ()
- 单个的, 后面加个逗号: `a,` 或者 `(a,)`
- 多个, 逗号分隔: `a,b,c` 或者 `(a,b,c)`
- 用 tuple() 强制

参考: collections.namedtuple() 可用用名来访问

## range(stop), range(start, stop[, step])

## str

构成:

- 单引号 `'blabla'`
- 双引号 `"blabla"`
- 三引号 `'''hi'''`, `"""there"""`

一行中,中间有空白的引号可用自动拼装: `('a' 'b') == 'ab'`

可用方法:

- str.capitalize() 首字母大写
- str.casefold() 很激进的大写转小写, 特殊字符会被替代
- str.center(width[, fillchar]) 文字居中, 并用 fillchar 填充, 不指定就是空格填充
- str.count(sub[, start[, end]]) 在 [start, end] 区间里找 sub 的个数, 区域不重叠!
- str.encode(encoding='utf-8', errors='strict')  errors = ['strict', 'ignore', 'replace', 'xmlcharrefreplace', 'backslashreplace'] 编码方式很多, 见标准编码
- str.endswith(suffix[, start[, end]]) 以 suffix 结束. suffix 可用是 tuple, 一次性比较多个. 如果有 [start, end] 则只比较该区域内
- str.expandtabs(tabsize=8) `\t` 换成空格
- str.find(sub[, start[, end]]) 看看能不能在 `s[start:end]` 切片内找到 sub
- str.format(*args, **kwargs)
- str.format_map(mapping) 和 str.format(**mapping) 一样的
- str.index(sub[,start[, end]])
- str.isalnum() 是 isalpha, isdecimal, isdigit, isnumeric 之一
- str.isalpha()
- str.isascii()
- str.isdecimal() 是十进制的数字
- str.isdigit() 一些各种不同语言的数字也算, 哪怕不是十进制
- str.isidentifier() 判断标识符. 判断 keyword 的话, 用 keyword.iskeyword() 来测.
- str.islower()
- str.isnumeric() 中文的 万, 壹 也算
- str.isprintalbe()
- str.isspace()
- str.istitle()
- str.isupper()
- str.join(iterable)
- ljust lower lstrip maketrans partition removeprefix removesuffix replace rfind rindex rjust rpartition rsplit rstrip split splitlines startswith strip swapcase title translate upper zfill

f-string

## 二进制序列 bytes, bytearray, memoryview

memoryview 用 buffer 协议原地操作 bytes, bytearray, 不需要新生成 copy

### bytes([source[, encoding[, errors]]])

- bytes.fromhex(string) 把 '2Ef0 F1f2' 这样的字符串转成 b'.\xf0\xf1\xf2'
- bytes.hex([sep[, bytes_per_sep]]) 把 b'\xf0\xf1\xf2'.hex() 转成 'f0f1f2'

### bytearray([source[, encoding[, errors]]])

也有 fromhex(), hex()

### bytes, bytearray 通用操作

- .count()
- .removeprefix
- .removesuffix
- .decode
- .endswith
- .find
- .index
- .join
- .maketrans
- .partition
- .replace
- .rfind
- .rindex
- .rpartition
- .startswith
- .translate
- .center
- .ljust
- .lstrip
- .rjust
- .rsplit
- .rstrip
- .split
- .captialize
- .expandtabs
- string 的东西都有

### memoryview

可用的方法

- `__eq__` 比较形状, 内容是否一致
- tobytes
- hex
- tolist
- toreadonly 返回一个只读copy 原来的就可以随便改了
- release !!
- cast(format[, shape]) 修改格式/形状!
- obj
- nbytes
- readonly
- format
- itemsize
- ndim
- shape
- strides
- suboffsets
- c_contiguous
- f_contiguous
- contiguous

## set, frozenset
