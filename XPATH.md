# XPATH（只认识网页里的代码）

# XPATH简单模式（但不稳定）：谷歌浏览器—页面元素审查—右键copy xpath

## 一层一层往下挖模式

> '/'	从根节点选取
> '//'	从匹配选择的当前节点选择文档中的节点，而不考虑它们的位置 **
>  '.'	选取当前节点 **
>  '..'	选取当前节点的父节点
>
> '@'   提取属性和控制属性 ** 
>
> '[]'  属性容器
> '*'	匹配任何元素节点
text() 以文本的方式返回提取的内容 **

#<book>开始，</book>结束

from lxml import etree

html = '''
<?xml version="1.0" encoding="ISO-8859-1"?>

<bookstore>
<div class="hahaha">男朋友</div>
<book>#标签，标签名是book，第一个是开始
  <p>王润泽生日快乐<p>
  <title lang="eng">早日找到男朋友</title>
  <div class="hahaha">男朋友</div>
  <price>29.99</price>
  <a href="www.baidu.com"></a>
</book>#这是结束

<book>#开始

  <title lang="engg">张瑞早日结婚</title>

  <price>39.95</price>
</book>#结束

</bookstore>

'''

tree = etree.HTML(html)
tree

```
<Element html at 0x273bf3e2f48>
```

# 查找标签内容（代码修改后要重新运行）

## /	从根节点选取；  //  从匹配选择的当前节点选择文档中的节点，而不考虑它们的位置

tree.xpath('//book/p')

```
[<Element p at 0x273bf4bb588>, <Element p at 0x273bf4bb508>]
```

##text() 以文本的方式返回提取的内容，即打印

tree.xpath('//book/p/text()')

```
['王润泽生日快乐', '\n  ']
```

tree.xpath('//book/title/text()')  因为属性相同的有两个，所以回去出两个

```
['早日找到男朋友', '张瑞早日结婚']
```

tree.xpath('//book/title[@lang="engg"]/text()')

```
['张瑞早日结婚']
```

属性相同的有两个，用索引，即可提取其中一个

tree.xpath('//book[1]/title/text()')

```
['早日找到男朋友']
```

## .选取当前节点 

book = tree.xpath('//book')
print(book)
for i in book:
    print(i.xpath('./title/text()'))

```
[<Element book at 0x1f512e67b08>, <Element book at 0x1f512e83f48>]
['早日找到男朋友']
['张瑞早日结婚']
```

## ..选取当前节点的父节点

book = tree.xpath('//book')
print(book)
for i in book:
    print(i.xpath('../div/text()'))

```
[<Element book at 0x1f512e9df08>, <Element book at 0x1f512e9d788>]
['男朋友']
['男朋友']
```

## @    提取属性和控制属性

tree.xpath('//book/a[@href]/@href')

```
['www.baidu.com']
```

## *   匹配任何元素节点

tree.xpath('//*[@href]/@href')

```
['www.baidu.com']
```

