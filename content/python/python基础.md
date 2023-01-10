
基础知识点：

1.dir(\_\_ builtins \_\_) 查询python的所有内置函数

# 1.列表

为列表添加元素的三种方法：

append()方法只有一个参数，参数内容是一个准备插入列表的元素

extends()方法也只有一个参数，参数内容是一个准备合并入列表的一个列表类似于java的addAll();

insert()方法有两个参数。第一个参数是准备插入的元素的索引值index，第二个参数是准备插入的元素，索引值从第0个开始

**元素交换位置**：number\[0\],number\[1\]=number\[1\],number\[0\]

从列表删除元素的三种方式：

remove()这个方法只有一个参数，参数内容就是list中要移除的元素的名字

del 这个是个语句，不是list的方法 eg：del number\[1\] 这样就把下标为1的元素删除了 del number 直接删除整个list

pop()这个是list的方法，可以带参数也可以不带参数，不带参数取出来的元素就是length-1的元素，带参数就是取对应下标的元素出来

列表分片：number\[start:end\] 含头不含尾 只写start就从start到尾，只写end就从头到end位置，如果两个都不写，那么久拷贝原list number2 = number\[:\] 即可拷贝一个新的集合

# 2.元祖（列表的近亲）

# 3.字符串的bif：

1.capitalize() 把首字母转换为大写

~~~

str = "xiaoxie"

str = str.capitalize()

'Xiaoxie'

~~~

2.casefold() 把字符串中的字母全部转换为小写

~~~

str = "XIAOXIE"

str = str.casefold()

'xiaoxie'

~~~

3.center(length) 把一个字符串两边填充相同长度至length长度

~~~

str = "xiaoxie"

str = str.center(10)

' xiaoxie '

~~~

4.count(sub\[,start\[,end\]\]) 返回sub在字符串中出现的次数，start和end参数表示范围，可选

~~~

str = "xiaoxiaoxiexie"

str.count("xi",0,15)

4

~~~

5.encode(encoding="utf-8",errors="strict") 以指定的编码格式对字符串进行编码

\--encoding -- 要使用的编码，如"UTF-8"。

\--errors -- 设置不同错误的处理方案。默认为 'strict',意为编码错误引起一个UnicodeError。 其他可能得值有 'ignore', 'replace', 'xmlcharrefreplace', 'backslashreplace' 以及通过 codecs.register\_error() 注册的任何值。

~~~

str = "中文字符"

str = str.encode(encoding="GBK",errors="stript")

b'\xd6\xd0\xce\xc4\xd7\xd6\xb7\xfb'

~~~

6.endswith(sub\[,start\[,end\]\])检查字符串是否已sub字符串结束，如果是返回True，否则返回False start和end参数表示范围，可选

~~~

str = "www.baidu.com"

str.endswith("com")

True

~~~

7.expandtabs(\[tabsize=8\]) 把字符串中的tab符号(\\t) 转换Wie空格，如果不指定tabsize，则默认的tabsize=8

~~~

str = "I\tLove\tYOU"

str = str.expandtabs();

'I LOVE YOU'

~~~

8.find(sub\[,start\[,end\]\]) 检测sub是否包含在字符串中，如果有则返回索引值，否则返回-1，start和end参数表示范围，可选

~~~

str = "I LOVE YOU"

str.find("LOVE",2,16);

8

~~~

9.index(sub\[,start\[,end\]\]) 跟find方法一样，不过如果sub不在string中会产生一个异常

~~~

str = str = "I LOVE YOU"

str.index("LOVE",2,16);

以下是异常信息：

Traceback (most recent call last):

File "<pyshell#84>", line 1, in <module>

str.index("LOEV",2,16)

ValueError: substring not found

~~~

10.isalnum() 如果字符串至少有一个字符并且所有字符都是字母或者数字则返回True,否则返回False

~~~

str = "aaaa"

str.isalnum()

True

~~~

11.isalpha() 如果字符串至少有一个字符并且所有字符都是字母则返回True，否则返回False

~~~

str = "aaaa1"

str.isalpha()

False

~~~

12.isdecimal() 如果字符串只包含十进制数字则返回True，否则返回False

~~~

str = "12"

str.isdecimail()

True

~~~

13.isdigit() 如果字符串只包含数字则返回True,否则返回False

~~~

str = "12"

str.isdigit()

True

~~~

14.islower() 如果字符串重至少包含一个区分大小写的字符，并且这些字符都是小写，则返回True,否则返回False

~~~

str = "string"

str.islower()

True

~~~

15.isnumeric() 如果字符串中只包含数字字符，则返回True,否则返回False

~~~

str = "12"

str.isnumeric()

True

~~~

16.isspace() 如果字符串中只包含空格则返回True 否则返回False

~~~

str = " "

str.isspace()

True

~~~

17.istitle() 如果字符串是标题化，（所有的单词都是以大写开始，几区字母均小写）则返回True，否则返回False

~~~

str = "String"

str.istitle()

True

~~~

18.isupper() 如果字符串中至少包含一个区分大小的字符，并且这些字符都是大写，则返回True，否则返回False

~~~

str = "string"

str.isupper()

False

~~~

**以下是常用的字符串的方法，包含了上面的一些已经举例的内容**

~~~

1.capitalize() 把字符串的第一个字符改为大写

2.casefold() 把整个字符串的所有字符改为小写

3.center(width) 将字符串居中，并使用空格填充至长度 width 的新字符串

4.count(sub[, start[, end]]) 返回 sub 在字符串里边出现的次数，start 和 end 参数表示范围，可选。

5.encode(encoding='utf-8', errors='strict') 以 encoding 指定的编码格式对字符串进行编码。

6.endswith(sub[, start[, end]]) 检查字符串是否以 sub 子字符串结束，如果是返回 True，否则返回 False。start 和 end 参数表示范围，可选。

7.expandtabs([tabsize=8]) 把字符串中的 tab 符号（\t）转换为空格，如不指定参数，默认的空格数是 tabsize=8。

8.find(sub[, start[, end]]) 检测 sub 是否包含在字符串中，如果有则返回索引值，否则返回 -1，start 和 end 参数表示范围，可选。

9.index(sub[, start[, end]]) 跟 find 方法一样，不过如果 sub 不在 string 中会产生一个异常。

10.isalnum() 如果字符串至少有一个字符并且所有字符都是字母或数字则返回 True，否则返回 False。

11.isalpha() 如果字符串至少有一个字符并且所有字符都是字母则返回 True，否则返回 False。

12.isdecimal() 如果字符串只包含十进制数字则返回 True，否则返回 False。

13.isdigit() 如果字符串只包含数字则返回 True，否则返回 False。

14.islower() 如果字符串中至少包含一个区分大小写的字符，并且这些字符都是小写，则返回 True，否则返回 False。

15.isnumeric() 如果字符串中只包含数字字符，则返回 True，否则返回 False。

16.isspace() 如果字符串中只包含空格，则返回 True，否则返回 False。

17.istitle() 如果字符串是标题化（所有的单词都是以大写开始，其余字母均小写），则返回 True，否则返回 False。

18.isupper() 如果字符串中至少包含一个区分大小写的字符，并且这些字符都是大写，则返回 True，否则返回 False。<--------------------------------以上内容都有举例------------------------------>

19.join(sub) 以字符串作为分隔符，插入到 sub 中所有的字符之间。

20.ljust(width) 返回一个左对齐的字符串，并使用空格填充至长度为 width 的新字符串。

21.lower() 转换字符串中所有大写字符为小写。

22.lstrip() 去掉字符串左边的所有空格

23.partition(sub) 找到子字符串 sub，把字符串分成一个 3 元组 (pre_sub, sub, fol_sub)，如果字符串中不包含 sub 则返回 ('原字符串', '', '')

24.replace(old, new[, count]) 把字符串中的 old 子字符串替换成 new 子字符串，如果 count 指定，则替换不超过 count 次。

25.rfind(sub[, start[, end]]) 类似于 find() 方法，不过是从右边开始查找。

26.rindex(sub[, start[, end]]) 类似于 index() 方法，不过是从右边开始。

27.rjust(width) 返回一个右对齐的字符串，并使用空格填充至长度为 width 的新字符串。

28.rpartition(sub) 类似于 partition() 方法，不过是从右边开始查找。

29.rstrip() 删除字符串末尾的空格。

30.split(sep=None, maxsplit=-1) 不带参数默认是以空格为分隔符切片字符串，如果 maxsplit 参数有设置，则仅分隔 maxsplit 个子字符串，返回切片后的子字符串拼接的列表。

31.splitlines(([keepends])) 在输出结果里是否去掉换行符，默认为 False，不包含换行符；如果为 True，则保留换行符。。

32.startswith(prefix[, start[, end]]) 检查字符串是否以 prefix 开头，是则返回 True，否则返回 False。start 和 end 参数可以指定范围检查，可选。

33.strip([chars]) 删除字符串前边和后边所有的空格，chars 参数可以定制删除的字符，可选。

34.swapcase() 翻转字符串中的大小写。

35.title() 返回标题化（所有的单词都是以大写开始，其余字母均小写）的字符串。

36.translate(table) 根据 table 的规则（可以由 str.maketrans('a', 'b') 定制）转换字符串中的字符。

37.upper() 转换字符串中的所有小写字符为大写。

38.zfill(width) 返回长度为 width 的字符串，原字符串右对齐，前边用 0 填充。

~~~

# 4.字符串格式化符号含义及转义字符含

**字符串格式化符号含义**

| **符号** | **说明** |

| --- | --- |

| %c | 格式化字符及其 ASCII 码 |

| %s | 格式化字符串 |

| %d | 格式化整数 |

| %o | 格式化无符号八进制数 |

| %x | 格式化无符号十六进制数 |

| %X | 格式化无符号十六进制数（大写） |

| %f | 格式化浮点数字，可指定小数点后的精度 |

| %e | 用科学计数法格式化浮点数 |

| %E | 作用同 %e，用科学计数法格式化浮点数 |

| %g | 根据值的大小决定使用 %f 或 %e |

| %G | 作用同 %g，根据值的大小决定使用 %f 或者 %E |



**格式化操作符辅助命令**

| **符号** | **说明** |

| --- | --- |

| m.n | m 是显示的最小总宽度，n 是小数点后的位数 |

| \- | 用于左对齐 |

| + | 在正数前面显示加号（+） |

| # | 在八进制数前面显示 '0o'，在十六进制数前面显示 '0x' 或 '0X' |

| 0 | 显示的数字前面填充 '0' 取代空格 |

**Python 的转义字符及其含义**

| **符号** | **说明** |

| --- | --- |

| ' | 单引号 |

| " | 双引号 |

| \\a | 发出系统响铃声 |

| \\b | 退格符 |

| \\n | 换行符 |

| \\t | 横向制表符（TAB） |

| \\v | 纵向制表符 |

| \\r | 回车符 |

| \\f | 换页符 |

| \\o | 八进制数代表的字符 |

| \\x | 十六进制数代表的字符 |

| \\0 | 表示一个空字符 |

| \\ | 反斜杠 |

# 序列

**list**(列表)

~~~

If no argument is given, the constructor creates a new empty list.

| The argument must be an iterable if specified.

~~~

如果没有给出参数，构造函数将创建一个新的空列表。

如果指定，参数必须是可迭代的。

## 迭代器：

**重复反馈过程的活动就是 迭代 其目的通常是为了接近或者达到所需的目标 每次对这个过程的重复称作迭代，而每一次迭代得到的结果都会被作为下一次迭代的初始值**

tuple(元祖)

~~~

| If no argument is given, the constructor returns an empty tuple.

| If iterable is specified the tuple is initialized from iterable's items.

~~~

如果没有给出参数，构造函数返回一个空元组。

如果指定了iterable，则从iterable的项初始化元组。

~~~

str() 把数据装换为字符串 和int() 一样的功能

len() 得到一个列表（list） 或者 元祖（tuple）的元素个数 长度

max() 得到列表或者元祖中的最大值

min() 同上得到最小值

sum(iterable[,start=0]) 求和一个可迭代的列表或者元祖 start是可选参数 会最终加在求和的值上

sorted() 排序一个可迭代的列表或者元祖

number = [14,15,52,63,51,85,96,14,98,-48]

reversed() 返回列表或者元素的迭代器对象 组合用法 list(reversed(number)) 可以得到list的倒叙结构[-48, 98, 14, 96, 85, 51, 63, 52, 15, 14]

enumerate() 生成列表或者元祖的index值和item值组成的元祖 [(index,value),(index,value)]

zip() 返回由各个参数序列组成的元祖 zip(a,b) 结果是 [(a[0],b[0]),...(a[len(len(a)>len(b)?b:a)-1],b[len(len(a)>len(b)?b:a)-1])] 这个len取决于a或者b的长度短的那个元祖或列表 如果len(a) < len(b) 那么就是len(a) 反之则是len(b)

~~~

# 5.函数

~~~

1.定义一个函数的语法格式

def 函数名():

函数体

....

eg:

def myfunc():

print("I Love Python")

2.调用函数的语法格式

函数名()

eg:

myfunc()

3.函数带参数

def 函数名(参数变量):

eg:

myfunc(name):

print("你好！"+name)

myfunc("python")

'你好！python'

4.函数的返回值

def myfunc(num1,num2):

return (num1+num2)

eg:

print(myfunc(5,6))

11

5.函数的doc文档

函数名.__doc__ 即可查看#注释下的函数逻辑实现的解释

6.手机参数==可变参数

def myfunc(*params)

eg:

def myfunc(*params)

print("参数的长度是："+len(params))

print("第二个参数是："+param[1])

myfunc(1,"老乌龟",3.14,56,15,25)

参数的长度是：6

第二个参数是：老乌龟

~~~

# 6.局部变量和全局变量

~~~

def myfunc(price,rate):

final_price = price * rate

print('这里试图打印全局变量old_price的值：',old_price)

old_price = 50

price("修改后的old_price的值是1：",old_price)

return final_price

old_price = float(input("请输入原价:"))

rate = float(input("请输入折扣率:"))

new_price = myfunc(old_price,rate)

price("修改后的old的值是2：",old_price)

price("打折后的价格是：",new_price)

这里的运行结果会出错 UnboundLocalError: local variable 'old_price' referenced before assignment 局部变量重复定义

~~~

**不要直接在函数中去修改一个全局变量的值，如果修改的话，python会创建一个和全局变量同名的局部变量代替全局变量在函数中使用(shadowing 在函数中屏蔽掉全局变量并声明同名的局部变量) 如果非要在函数中去修改一个全局变量的值 在修改前加上global 告诉python编译器我是修改的全局变量**

# 7.闭包(closure)

闭包：如果在一个内部函数里对外部作用于（但不是在全局作用的变量进行引用）那么内部函数就会被认为是闭包（closure）

闭包中的外部函数局部变量在闭包函数中的使用

~~~

方式一：使用容器 list列表来实现闭包函数使用外部函数局部变量

def fun1():

x = [5]

def fun2():

x[0] *= x[0]

return x[0]

reutrn fun2()

方式二：使用3.x的关键字 nonlocal variable

def fun1():

x = 5

def fun2():

nonlocal x

x *= x

return x

return fun2()

~~~

# 8.lambda表达式

~~~

使用lambda定义匿名的函数

语法：lambda argument:return value

关键字 参数：返回值

冒号前面你的你需要传的形参名称 冒号后面为你的函数执行返回值

~~~

补充两个结合lambda实现的便捷BIF

## 1.filter(过滤器)

~~~

| Return an iterator yielding those items of iterable for which function(item)

| is true. If function is None, return the items that are true.

返回一个迭代器，该迭代器生成用于哪个函数(项)的可迭代项

|是正确的。如果函数为None，则返回为true的项。

~~~

filter(function or None, iterable) --> filter object

这个BIF有两个参数 如果第一个参数是一个function函数的话，就会把后面迭代器里面的值以参数的形式传递给前面的function 然后filter就会过滤掉function返回false的结果，得到返回true的结果，并返回一个list，如果第一个参数不是一个function的话，就会直接把第二个列表参数里面的返回true的结果返回。过滤掉false 并返回结果list

eg：

~~~

需求：过滤掉100以内的所有的偶数，得到所有的基数

方式1：

def iseven(i):

return i%2

list = range(0,100)

list(filter(iseven,list))

[1,3,5,...99]

​

方式二：

list(filter(lambda i:i%2,range(0,100)))

[1,3,5,...99]

~~~

## 2.map

~~~

| Make an iterator that computes the function using arguments from

| each of the iterables. Stops when the shortest iterable is exhausted.

创建一个迭代器，它使用来自的参数计算函数

每个迭代器。当最短的迭代器耗尽时停止。

~~~

map(func, \*iterables) --> map object

map有两个参数第一个参数是一个函数，第二个参数是一个可迭代的序列 这个bif的功能是将序列的每个元素作为function的参数传递到function中 然后在function内容将每一个元素进行运算加工，直到序列可迭代元素都加工完毕，返回所有加工后的元素构成的新序列（新list）

eg:

~~~

需求：将一些价格批量打0.8折，并返回打折之后的价格

直接使用lambda实现

list(map(lambda price:price * 0.8,[300,250,100,200,360]))

[240.0, 200.0, 80.0, 160.0, 288.0]

~~~

# 9 递归

## 1.补充知识 设置递归上限层级

~~~

import sys

sys.setrecursionlimit(你需要设置的层数)

~~~

~~~

需求：递归求阶乘

def factorial(n):

if n == 1:

return 1

else:

return n * factorial(n-1)

number = int(input("请输入一个正整数:"))

result = factorial(number)

print("%d 的阶乘是：%d" % (number,result))

~~~

~~~

需求 求兔子的数量(斐波拉切数)

实现方法1 递归

def rabbit(n):

if n == 1 or n == 2:

print("兔子的数量是：1")

return 1

elif n > 2:

number = rabbit(n - 1) + rabbit(n - 2)

print("兔子的数量是：%d" % number)

return number

month = int(input("请输入月数："))

number = rabbit(month)

print("%d 个月之后兔子的数量是：%d" % (month,number))

实现方式2 迭代

def rabbit(n):

n1=n2=n3 = 1

while((n - 2) > 0):

n3= n1 + n2

n1,n2 = n2,n3

n -=1

return n3;

month = int(input("请输入月数："))

number = rabbit(month)

print("%d 个月之后兔子的数量是：%d" % (month,number))

~~~

# 10.字典 dict java中的map类型

## 1.字典的符号是大括号{} 形式是key:value 相邻元素以逗号隔开

eg:dict = {"one":1,"two":2,"three":3}，

## 2.字典可以通过添加键值对的形式添加元素，还可以通过key来添加value的形式改变或者添加到字典中

eg dict\['four'\] = 4 这个例子中，如果存在four这个key值的话就会修改掉原来key值对应的value值，如果key值不存在的话就会直接将这对key和value添加到字典中

## 3.dict()不是一个bif，是一个工厂函数（调用该方法会返回对应工厂所产生的是实例）

## 4.字典所对应的bif函数：

### 4.1.使用fromkeys创建并返回一个新的字典

dict.fromkeys(key\[,value\]) 这个方法有两个参数，第一个参数是key值，第二个是key对应的的value value是可选的

### 4.2.keys()是返回字典键的引用。

就是返回字典中所有的key值 例如在集合中for循环中遍历是 for i in dict.keys()

### 4.3.values 是返回字典值的引用

返回字典中所有的value值，使用for循环遍历也是同样的效果 for val in dict.values()

### 4.4 items()是返回字典中的每一对key和value的键值对。

相当于java map中的entry对象，返回每一组key:value

### 4.4 使用get()方法可以避免在索引值不存在的情况下抛出异常的情况。

如果直接使用dict\[len(dict)+1\] 则会直接出现错误 KeyError: index ，如果是用get()方法则不会抛出异常，则会返回一个None eg:print(dict.get(len(dict)+1)) 这样的方法获取None

这个方法支持第一个参数是字典中的索引值index，第二个值为如果找不到的情况下返回的值，如果找到则不会返回第二个参数值 eg：print(dict.get(len(dict)+1)，“不存在”) 返回的值是：不存在

### 4.5还可以通过成员资格操作符 in和not in判断这个key是否存在于字典中 key in dict 或者key not in dict

存在返回True 不存在返回False 检查成员操作资格比序列更加高效，当字典中的数据相当大事，使用成员资格操作符的效率会更加高效

### 4.6 clear()方法用于清空一个字典

eg:dict.clear() 则会把dict这个字典清空

### 4.7浅拷贝 copy() 拷贝复制给一个新的字典 新的!!，它们所对应的内存地址不相同 可以通过id()来查看

补充知识:id()函数用于获取对象的内存地址

### 4.8 pop(key) 给定字典中的一个key值，弹出这个key对应的value值 这个方法有参数 就是key

### 4.9 popitem() 给定字典中的一个key值，弹出包含这个key和对应的value的项，弹出key:value 这个方法没有参数，带参数报错

### 4.10 setdefault() 给字典中添加一项 有两个参数，第一个参数必填 key 第二个参数选填value 没有设置第二个参数则value是None 如果设置第二个值则value是第二个参数

### 4.11 update() 这个方法是利用一个字典或者映射关系去更新另一个字典 eg：dict.update({3,"三"}) 就可以将原先 3的映射“three”改为“三” 这个方法的关键是，他支持同时对多个keys的value值进行更改

# 11 集合 set 字典的近亲 没有体现影射关系的就是集合 关键字 唯一

无序，key唯一， 使用num1 = list(set(num1)) 可以去去除num1中的重复的内容

集合同样适用成员资格操作符来判断成员是否在这个集合中

## 1.集合的bif：

### 1.1 add()追加元素 有一个参数

### 1.2 remove() 从集合中移除 有一个参数

### 1.3 frozenset() 不可变集合 不能使用add和remove 不能改变其内部的值

# 12.文件操作

## 1.文件的打开方式是open() 函数 返回一个文件对象

open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None) 除了第一个是必填以外，其他的都是有默认值的

参数列表:

file 打开的文件 如果带路径就是打开对应路径下的文件，如果不带路径就是打来当前路径下的同名文件

mode 打开文件的模式

| "r" | 以只读方式打开文件(默认) |

| --- | --- |

| "w" | 以写入的方式打开文件，会覆盖已存在的文件 |

| "x" | 如果文件已经存在，使用此模式打开将引发异常 |

| "a" | 以写入模式打开，如果文件存在，则在末尾追加写入 |

| "b" | 以二进制模式打开文件 |

| "t" | 以文本模式打开文件(默认) |

| "+" | 可读写模式(可添加到其他模式中使用) |

| "U" | 通用换行符支持 |

**文件对象方法**

| **文件对象方法** | **执行操作** |

| --- | --- |

| f.close() | 关闭文件 |

| f.read(\[size=-1\]) | 从文件读取size个字符，当未给定size或给定负值的时候，读取剩余的所有字符，然后作为字符串返回 |

| f.readline(\[size=-1\]) | 从文件中读取并返回一行（包括行结束符），如果有size有定义则返回size个字符 |

| f.write(str) | 将字符串str写入文件 |

| f.writelines(seq) | 向文件写入字符串序列seq，seq应该是一个返回字符串的可迭代对象 |

| f.seek(offset, from) | 在文件中移动文件指针，从from（0代表文件起始位置，1代表当前位置，2代表文件末尾）偏移offset个字节 |

| f.tell() | 返回当前在文件中的位置 |

| f.truncate(\[size=file.tell()\]) | 截取文件到size个字节，默认是截取到文件指针当前位置 |

# 13.OS模块

**os模块中关于文件/目录常用的函数使用方法**

| **函数名** | **使用方法** |

| --- | --- |

| getcwd() | 返回当前工作目录 |

| chdir(path) | 改变工作目录 |

| listdir(path='.') | 列举指定目录中的文件名（'.'表示当前目录，'..'表示上一级目录） |

| mkdir(path) | 创建单层目录，如该目录已存在抛出异常 |

| makedirs(path) | 递归创建多层目录，如该目录已存在抛出异常，注意：'E:\\a\\b'和'E:\\a\\c'并不会冲突 |

| remove(path) | 删除文件 |

| rmdir(path) | 删除单层目录，如该目录非空则抛出异常 |

| removedirs(path) | 递归删除目录，从子目录到父目录逐层尝试删除，遇到目录非空则抛出异常 |

| rename(old, new) | 将文件old重命名为new |

| system(command) | 运行系统的shell命令 |

| walk(top) | 遍历top路径以下所有的子目录，返回一个三元组：(路径, \[包含目录\], \[包含文件\])【具体实现方案请看：第30讲课后作业^\_^】 |

| *以下是支持路径操作中常用到的一些定义，支持所有平台* | |

| os.curdir | 指代当前目录（'.'） |

| os.pardir | 指代上一级目录（'..'） |

| os.sep | 输出操作系统特定的路径分隔符（Win下为'\\'，Linux下为'/'） |

| os.linesep | 当前平台使用的行终止符（Win下为'\\r\\n'，Linux下为'\\n'） |

| os.name | 指代当前使用的操作系统（包括：'posix', 'nt', 'mac', 'os2', 'ce', 'java'） |

# 14 os.path模块中关于路径常用的函数使用方法

| **函数名** | **使用方法** |

| --- | --- |

| basename(path) | 去掉目录路径，单独返回文件名 |

| dirname(path) | 去掉文件名，单独返回目录路径 |

| join(path1\[, path2\[, ...\]\]) | 将path1, path2各部分组合成一个路径名 |

| split(path) | 分割文件名与路径，返回(f\_path, f\_name)元组。如果完全使用目录，它也会将最后一个目录作为文件名分离，且不会判断文件或者目录是否存在 |

| splitext(path) | 分离文件名与扩展名，返回(f\_name, f\_extension)元组 |

| getsize(file) | 返回指定文件的尺寸，单位是字节 |

| getatime(file) | 返回指定文件最近的访问时间（浮点型秒数，可用time模块的gmtime()或localtime()函数换算） |

| getctime(file) | 返回指定文件的创建时间（浮点型秒数，可用time模块的gmtime()或localtime()函数换算） |

| getmtime(file) | 返回指定文件最新的修改时间（浮点型秒数，可用time模块的gmtime()或localtime()函数换算） |

| *以下为函数返回 True 或 False* | |

| exists(path) | 判断指定路径（目录或文件）是否存在 |

| isabs(path) | 判断指定路径是否为绝对路径 |

| isdir(path) | 判断指定路径是否存在且是一个目录 |

| isfile(path) | 判断指定路径是否存在且是一个文件 |

| islink(path) | 判断指定路径是否存在且是一个符号链接 |

| ismount(path) | 判断指定路径是否存在且是一个挂载点 |

| samefile(path1, paht2) | 判断path1和path2两个路径是否指向同一个文件 |

# 15.pickle(泡菜) 模块 用于吧列表 元祖 集合 字典等对象形式的数据装换二进制的数据

eg:

~~~

import pickle

my_list = [123,3.14,"小甲鱼",["another list"]]

pickle_file = open("my_list.pkl","wb") #这里的保存文件后缀名自定义就好，然后文件的操作模式必须是“wb” 不然会报错 w:以写入的方式打开文件，会覆盖已存在的文件 b:以二进制模式打开文件

pickle.dump(my_list,pickle_file)

pickle_file.close()

#上面的是写入操作，下面的是读取操作

pickle_file = open("my_list.pkl","rb") #这里的文件操作模式是rb r:以只读方式打开文件(默认) b:以二进制模式打开文件

my_list2 = pickle.load(pickle_file)

print(my_list2)

[123,3.14,"小甲鱼",["another list"]]

~~~

# 16 python中的异常

| AssertionError | 断言语句（assert）失败 |

| --- | --- |

| AttributeError | 尝试访问未知的对象属性 |

| EOFError | 用户输入文件末尾标志EOF（Ctrl+d） |

| FloatingPointError | 浮点计算错误 |

| GeneratorExit | generator.close()方法被调用的时候 |

| ImportError | 导入模块失败的时候 |

| IndexError | 索引超出序列的范围 |

| KeyError | 字典中查找一个不存在的关键字 |

| KeyboardInterrupt | 用户输入中断键（Ctrl+c） |

| MemoryError | 内存溢出（可通过删除对象释放内存） |

| NameError | 尝试访问一个不存在的变量 |

| NotImplementedError | 尚未实现的方法 |

| OSError | 操作系统产生的异常（例如打开一个不存在的文件） |

| OverflowError | 数值运算超出最大限制 |

| ReferenceError | 弱引用（weak reference）试图访问一个已经被垃圾回收机制回收了的对象 |

| RuntimeError | 一般的运行时错误 |

| StopIteration | 迭代器没有更多的值 |

| SyntaxError | Python的语法错误 |

| IndentationError | 缩进错误 |

| TabError | Tab和空格混合使用 |

| SystemError | Python编译器系统错误 |

| SystemExit | Python编译器进程被关闭 |

| TypeError | 不同类型间的无效操作 |

| UnboundLocalError | 访问一个未初始化的本地变量（NameError的子类） |

| UnicodeError | Unicode相关的错误（ValueError的子类） |

| UnicodeEncodeError | Unicode编码时的错误（UnicodeError的子类） |

| UnicodeDecodeError | Unicode解码时的错误（UnicodeError的子类） |

| UnicodeTranslateError | Unicode转换时的错误（UnicodeError的子类） |

| ValueError | 传入无效的参数 |

| ZeroDivisionError | 除数为零 |

以下是 Python 内置异常类的层次结构：

BaseException

+-- SystemExit

+-- KeyboardInterrupt

+-- GeneratorExit

+-- Exception

+-- StopIteration

+-- ArithmeticError

| +-- FloatingPointError

| +-- OverflowError

| +-- ZeroDivisionError

+-- AssertionError

+-- AttributeError

+-- BufferError

+-- EOFError

+-- ImportError

+-- LookupError

| +-- IndexError

| +-- KeyError

+-- MemoryError

+-- NameError

| +-- UnboundLocalError

+-- OSError

| +-- BlockingIOError

| +-- ChildProcessError

| +-- ConnectionError

| | +-- BrokenPipeError

| | +-- ConnectionAbortedError

| | +-- ConnectionRefusedError

| | +-- ConnectionResetError

| +-- FileExistsError

| +-- FileNotFoundError

| +-- InterruptedError

| +-- IsADirectoryError

| +-- NotADirectoryError

| +-- PermissionError

| +-- ProcessLookupError

| +-- TimeoutError

+-- ReferenceError

+-- RuntimeError

| +-- NotImplementedError

+-- SyntaxError

| +-- IndentationError

| +-- TabError

+-- SystemError

+-- TypeError

+-- ValueError

| +-- UnicodeError

| +-- UnicodeDecodeError

| +-- UnicodeEncodeError

| +-- UnicodeTranslateError

+-- Warning

+-- DeprecationWarning

+-- PendingDeprecationWarning

+-- RuntimeWarning

+-- SyntaxWarning

+-- UserWarning

+-- FutureWarning

+-- ImportWarning

+-- UnicodeWarning

+-- BytesWarning

+-- ResourceWarning

异常的捕获：

## 16.1.try except

eg:

~~~

try:

f = open("不存在的文件.txt")

print(f.read())

f.close

except OSError as reason:

print("文件出错啦T_T,错误的原因是："+str(reason))

文件出错啦T_T,错误的原因是：[Errno 2] No such file or directory: '不存在的文件.txt'

~~~

和java一样 except是可以多层嵌套的，不同类型的异常使用不用的处理方式

except 后面不跟异常的类型表示在前面的except 所对应的异常类型没有符合的，就进入都最后的except（后面不带异常类型）中

## 16.2 try except finally

这个的用法和java很相似 不做过多注释

## 16.3raise 抛出一个异常 类似于java throw 的作用 raise 后面写一个异常的类型（异常的参数） 和java类似

17 丰富的else语句和简洁的with语句

1.else和if语句搭配可以实现 **“要么怎样，要么不怎样”** 的逻辑处理

2.else和循环语句for或者while搭配实现 **“干完了能怎样，干不完就别想怎样”** 的逻辑处理

3.else和try except异常处理搭配实现**“没有问题的话怎样”** 的逻辑处理

第一种举例：

~~~

if i%2 ==0:

......要么怎样的处理逻辑

else:

......要么不怎样的处理逻辑

~~~

第二种举例

~~~

def showMaxFactor(num)

count = num // 2

while count > 1:

if num % count ==0

print("%d最大的约数是%d" % (num,count))

break

count -=1

else:

print("%d是一个素数" % num)

num = int(input("请输入一个数:"))

showMaxFactor(num)

~~~

第三种举例：

~~~

try:

int(123)

except ValueError as reason:

print('除错误啦：'+ str(reason))

else:

print("没有出现任何的异常！")

~~~

with是相当于java 1.7更新的内存流自动关闭的特性

比如你再读取文件的时候，你读取一个不存在的文件肯定会发生异常，但你发生异常之后使用finally去关闭的时候，你会先没有开启这个文件的open，所以就会出问题，当你使用with之后，如果文件打开之后，他会自动关闭

~~~

try:

with open('data.txt','w') as f:

for wach_line in f:

print(each_line)

except OSError as reason：

print("出错啦，" + str(reason))

~~~

# 17.图形用户界面 easygui

1.下载并解压 [https://github.com/robertlugg/easygui](https://github.com/robertlugg/easygui) 去github下载easygui模块包 然后解压

2.使用命令行切换到下载的easygui路径下，然后输入**python setup.py install**

3实例eg

~~~

import easygui as g #这里相当于取一个别名 来调用easygui

g.msgbox("图形化窗口")

~~~

4.扩展阅读:[https://fishc.com.cn/forum.php?mod=viewthread&tid=46069&extra=page%3D1%26filter%3Dtypeid%26typeid%3D403](https://fishc.com.cn/forum.php?mod=viewthread&tid=46069&extra=page%3D1%26filter%3Dtypeid%26typeid%3D403) 小甲鱼翻译的easygui中文教程

# 18.面向对象

**1.三大特征 封装、继承、多态 和java一样**

**2.创建类**

~~~

语法：

class 类名:

类的属性。。。。

类的行为方法。。。

eg:

class Animal:

name = ""

age = ""

def cry:

print("动物在叫")

~~~

**3.创建对象**

~~~

语法:

对象名 = 类名()

eg：

dog = animal()

~~~

**4.继承**

~~~

语法:

class 类名(父类名):

类的属性。。。。

类的行为方法。。。

eg:

class Mylist(list):

list1 = Mylist()

list1.append(1)

~~~

**5.封装私有**

私有属性、方法——Python并没有真正的私有化支持，但可用下划线得到伪私有 尽量避免定义以下划线开头的变量 （1）\_xxx "单下划线 " 开始的成员变量叫做保护变量，意思是只有类对象（即类实例）和子类对象自己能访问到这些变量，需通过类提供的接口进行访问；不能用'from module import \*'导入 （2）**xxx 类中的私有变量/方法名 （Python的函数也是对象，所以成员方法称为成员变量也行得通。）," 双下划线 " 开始的是私有成员，意思是只有类对象自己能访问，连子类对象也不能访问到这个数据。 （3）**xxx\_\_ 系统定义名字，前后均有一个“双下划线” 代表python里特殊方法专用的标识，如 **init**() 代表类的构造函数

~~~

eg:

class animal():

__name = ""

def getName(self):

print(self.__name)

~~~

**6.self对象的作用和方法，self相当于是java中的this，但不全是，self是一个中间变量，用来做绑定可能比较合适意思，因为，当你的实力对象调用父类的方法的时候，需要通过self来绑定你调用的这个实力对象，但是，这个对象不用显式的传递，只需要在父类的定义方法时，将self写在形式参数的第一个位置，然后在方法里面去使用self来传递参数**

**7.对象和类的一些BIF**

7.1.insubclass(class,classinfo) 如果第一个参数对象是第二个参数对象的子类的话，就会返回True（非严格性的检查，一个类被认为是他自己的子类，第二个参数可以为一个元素，多个中找一个）

7.2 isinstance(Object,classInfo) 这是用来检查一个实例对象是否是一个class的实例 ，就是参数1是否是参数2的实例对象

7.3 hasattr(object,name) 判断一个实例对象中是否有指定的属性

7.4 getattr(object,name\[,defaultValue\]) 获取对象的指定name属性值，如果设置了defaultValue的值，在没有获取成功的情况下，则会返回defaultValue的值，如果没有设置defaultValue的值，则会抛出一个attrError

7.5 setattr(object,name,value) 设置一个对象的属性值，如果不存在会创建一个并设置这个属性值

7.6 delattr(object,name)删除对象的一个属性，如果不存在则会抛出一个异常，存在则删除

7.7 property(fget=None,fset=None,fdel=None,fdoc=None) 是通过属性来操作属性的方法

eg:

~~~

class book:

def __init__(self,pages):

self.pages = pages

def getPages(self):

return self.pages()

def setPages(self,pages):

self.pages = pages

def delPages(self):

del self.pages

x = property(getPages,setPages,delPages)

然后在每个book类的实例中如果想要改变pages只需要调用x来就可以，就相当于操作一个对象

~~~

7.8 “\_\_ init \_\_(self\[,attrvalue\])” 是构造方法 和ava的构造方法一样，这个方法是不用做返回值，也不能返回值

7.9 “\_\_ new \_\_(class\[,attrvalue\])” 是创建对象的方法

7.10 ‘\_\_ del \_\_(self) ’这个是对象在没有任何标签指向该对象时，被垃圾回收机制回收的时候调动的方法 相当于java.的finaline()方法

**8.魔法方法**

| **魔法方法** | **含义** |

| --- | --- |

| | **基本的魔法方法** |

| **new**(cls\[, ...\]) | 1\. **new** 是在一个对象实例化的时候所调用的第一个方法 2. 它的第一个参数是这个类，其他的参数是用来直接传递给 **init** 方法 3. **new** 决定是否要使用该 **init** 方法，因为 **new** 可以调用其他类的构造方法或者直接返回别的实例对象来作为本类的实例，如果 **new** 没有返回实例对象，则 **init** 不会被调用 4. **new** 主要是用于继承一个不可变的类型比如一个 tuple 或者 string |

| **init**(self\[, ...\]) | 构造器，当一个实例被创建的时候调用的初始化方法 |

| **del**(self) | 析构器，当一个实例被销毁的时候调用的方法 |

| **call**(self\[, args...\]) | 允许一个类的实例像函数一样被调用：x(a, b) 调用 x.**call**(a, b) |

| **len**(self) | 定义当被 len() 调用时的行为 |

| **repr**(self) | 定义当被 repr() 调用时的行为 |

| **str**(self) | 定义当被 str() 调用时的行为 |

| **bytes**(self) | 定义当被 bytes() 调用时的行为 |

| **hash**(self) | 定义当被 hash() 调用时的行为 |

| **bool**(self) | 定义当被 bool() 调用时的行为，应该返回 True 或 False |

| **format**(self, format\_spec) | 定义当被 format() 调用时的行为 |

| | **有关属性** |

| **getattr**(self, name) | 定义当用户试图获取一个不存在的属性时的行为 |

| **getattribute**(self, name) | 定义当该类的属性被访问时的行为 |

| **setattr**(self, name, value) | 定义当一个属性被设置时的行为 |

| **delattr**(self, name) | 定义当一个属性被删除时的行为 |

| **dir**(self) | 定义当 dir() 被调用时的行为 |

| **get**(self, instance, owner) | 定义当描述符的值被取得时的行为 |

| **set**(self, instance, value) | 定义当描述符的值被改变时的行为 |

| **delete**(self, instance) | 定义当描述符的值被删除时的行为 |

| | **比较操作符** |

| **lt**(self, other) | 定义小于号的行为：x < y 调用 x.**lt**(y) |

| **le**(self, other) | 定义小于等于号的行为：x <= y 调用 x.**le**(y) |

| **eq**(self, other) | 定义等于号的行为：x == y 调用 x.**eq**(y) |

| **ne**(self, other) | 定义不等号的行为：x != y 调用 x.**ne**(y) |

| **gt**(self, other) | 定义大于号的行为：x > y 调用 x.**gt**(y) |

| **ge**(self, other) | 定义大于等于号的行为：x >= y 调用 x.**ge**(y) |

| | **算数运算符** |

| **add**(self, other) | 定义加法的行为：+ |

| **sub**(self, other) | 定义减法的行为：- |

| **mul**(self, other) | 定义乘法的行为：\* |

| **truediv**(self, other) | 定义真除法的行为：/ |

| **floordiv**(self, other) | 定义整数除法的行为：// |

| **mod**(self, other) | 定义取模算法的行为：% |

| **divmod**(self, other) | 定义当被 divmod() 调用时的行为 |

| **pow**(self, other\[, modulo\]) | 定义当被 power() 调用或 \*\* 运算时的行为 |

| **lshift**(self, other) | 定义按位左移位的行为：<< |

| **rshift**(self, other) | 定义按位右移位的行为：>> |

| **and**(self, other) | 定义按位与操作的行为：& |

| **xor**(self, other) | 定义按位异或操作的行为：^ |

| **or**(self, other) | 定义按位或操作的行为：| |

| | **反运算** |

| **radd**(self, other) | （与上方相同，当左操作数不支持相应的操作时被调用） |

| **rsub**(self, other) | （与上方相同，当左操作数不支持相应的操作时被调用） |

| **rmul**(self, other) | （与上方相同，当左操作数不支持相应的操作时被调用） |

| **rtruediv**(self, other) | （与上方相同，当左操作数不支持相应的操作时被调用） |

| **rfloordiv**(self, other) | （与上方相同，当左操作数不支持相应的操作时被调用） |

| **rmod**(self, other) | （与上方相同，当左操作数不支持相应的操作时被调用） |

| **rdivmod**(self, other) | （与上方相同，当左操作数不支持相应的操作时被调用） |

| **rpow**(self, other) | （与上方相同，当左操作数不支持相应的操作时被调用） |

| **rlshift**(self, other) | （与上方相同，当左操作数不支持相应的操作时被调用） |

| **rrshift**(self, other) | （与上方相同，当左操作数不支持相应的操作时被调用） |

| **rand**(self, other) | （与上方相同，当左操作数不支持相应的操作时被调用） |

| **rxor**(self, other) | （与上方相同，当左操作数不支持相应的操作时被调用） |

| **ror**(self, other) | （与上方相同，当左操作数不支持相应的操作时被调用） |

| **增量赋值运算** | **增量赋值运算** |

| **iadd**(self, other) | 定义赋值加法的行为：+= |

| **isub**(self, other) | 定义赋值减法的行为：-= |

| **imul**(self, other) | 定义赋值乘法的行为：\*= |

| **itruediv**(self, other) | 定义赋值真除法的行为：/= |

| **ifloordiv**(self, other) | 定义赋值整数除法的行为：//= |

| **imod**(self, other) | 定义赋值取模算法的行为：%= |

| **ipow**(self, other\[, modulo\]) | 定义赋值幂运算的行为：\*\*= |

| **ilshift**(self, other) | 定义赋值按位左移位的行为：<<= |

| **irshift**(self, other) | 定义赋值按位右移位的行为：>>= |

| **iand**(self, other) | 定义赋值按位与操作的行为：&= |

| **ixor**(self, other) | 定义赋值按位异或操作的行为：^= |

| **ior**(self, other) | 定义赋值按位或操作的行为：|\= |

| **一元操作符** | **一元操作符** |

| **pos**(self) | 定义正号的行为：+x |

| **neg**(self) | 定义负号的行为：-x |

| **abs**(self) | 定义当被 abs() 调用时的行为 |

| **invert**(self) | 定义按位求反的行为：~x |

| **类型转换** | **类型转换** |

| **complex**(self) | 定义当被 complex() 调用时的行为（需要返回恰当的值） |

| **int**(self) | 定义当被 int() 调用时的行为（需要返回恰当的值） |

| **float**(self) | 定义当被 float() 调用时的行为（需要返回恰当的值） |

| **round**(self\[, n\]) | 定义当被 round() 调用时的行为（需要返回恰当的值） |

| **index**(self) | 1\. 当对象是被应用在切片表达式中时，实现整形强制转换 2. 如果你定义了一个可能在切片时用到的定制的数值型,你应该定义 **index** 3. 如果 **index** 被定义，则 **int** 也需要被定义，且返回相同的值 |

| | **上下文管理（with 语句）** |

| **enter**(self) | 1\. 定义当使用 with 语句时的初始化行为 2. **enter** 的返回值被 with 语句的目标或者 as 后的名字绑定 |

| **exit**(self, exc\_type, exc\_value, traceback) | 1\. 定义当一个代码块被执行或者终止后上下文管理器应该做什么 2. 一般被用来处理异常，清除工作或者做一些代码块执行完毕之后的日常工作 |

| **容器类型** | **容器类型** |

| **len**(self) | 定义当被 len() 调用时的行为（返回容器中元素的个数） |

| **getitem**(self, key) | 定义获取容器中指定元素的行为，相当于 self\[key\] |

| **setitem**(self, key, value) | 定义设置容器中指定元素的行为，相当于 self\[key\] = value |

| **delitem**(self, key) | 定义删除容器中指定元素的行为，相当于 del self\[key\] |

| **iter**(self) | 定义当迭代容器中的元素的行为 |

| **reversed**(self) | 定义当被 reversed() 调用时的行为 |

| **contains**(self, item) | 定义当使用成员测试运算符（in 或 not in）时的行为 |
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTYwNjA5ODMwMV19
-->