# 正则表达式Re（写在引号里）

http://tool/oschina/net/regex测试正则表达式网址

re.png



![1528891539471](C:\Users\dell\AppData\Local\Temp\1528891539471.png)

## re.match(pattern,string,flags=())

## 从第一个开始匹配（此语法不常用）

## 第一个参数：正则表达式

## 第二个参数：匹配的字符串

## 第三个参数：匹配的模式

import re

content = 'Hello 123 4567 World_This is a Regex Demo'
res = re.match('^Hello\s\d\d\d\s\d{4}\s\w{10}\s.*',content)
print(res)

```
<_sre.SRE_Match object; span=(0, 41), match='Hello 123 4567 World_This is a Regex Demo'>
```

## group是把内容打印出来

content = 'Hello 123 4567 World_This is a Regex Demo'
res = re.match('^Hello\s\d\d\d\s\d{4}\s\w{10}\s.*',content)
print(res.group())

```
Hello 123 4567 World_This is a Regex Demo
```

## .*泛匹配，除换行符外，其余皆可匹配

content = 'zhangrui is a good man'
res = re.match('^z\w{7}\s\w\w\s\w\s\w{4}\s\w{3}',content)
print(res.group())

```
zhangrui is a good man
```

用.*表示：

content = 'zhangrui is a good man'
res = re.match('^z.*',content)
print(res.group())

```
zhangrui is a good man
```



## 匹配目标（）提取括号里的内容

import re
content = 'Hello 123 4567 World_This is a Regex Demo'
res = re.match('^Hello\s\d{3}\s(\d{4}).*',content)
print(res.group(1))

```
4567
```



## group里什么都不写，则返回所有

import re
content = 'Joker is 213 a bad 123 man and hahaha'
res = re.match('^J.*\s(\d{3}).*\s(\d{3}).*\s(\w{6})',content)
print(res.group(1))
print(res.group(2))
print(res.group(3))
print(res.group())

```
213
123
hahaha
Joker is 213 a bad 123 man and hahaha
```

## 贪婪匹配  尽可能匹配多个元素

import re
content = 'Hello 1234567 World_This is a Regex Demo'
res = re.match('^Hello\s(\d+)',content)
print(res.group(1))

```
1234567
```

贪婪模式：

import re
content = 'Hello 1234567 World_This is a Regex Demo'
res = re.match('^Hello.*(\d+)',content)
print(res.group(1))

```
7
```

非贪婪模式：

import re
content = 'Hello 1234567 World_This is a Regex Demo'
res = re.match('^Hello.*?(\d+)',content)
print(res.group(1))

```
1234567
```

# 作业：

# 找出4，2，456

import re
content = 'Hello 1234567 hahaha 123 lalala 456'
res = re.match('^H\w{4}\s\d{3}(\d)\d{3}\s\w{6}\s\d(\d)\d\s\w{6}\s(\d{3})',content)
print(res.group(1))
print(res.group(2))
print(res.group(3))

```
4
2
456
```

