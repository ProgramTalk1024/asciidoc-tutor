![](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301251143816.png)

# AsciiDoc的文档使用基本教程
![](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281504444.png)

AsciiDoc是一种比Markdown功能更加丰富的文档，用其编写技术文档尤为合适，[Spring官网](https://spring.io)的很多文档都是使用其编写的。

# 块
## 分隔块
分隔块就是一块内容区域，分隔块是 AsciiDoc 中所有块类型的子集，他是通过结构化容器实现的。内置的块有很多。



### 注释块

使用////来作为首位标记，实现评论块，注释块不会在页面等上面展示出来
```asciidoc
////
使用////来作为首位标记，实现评论块，注释块不会在页面等上面展示出来
////
```



### 样例块

使用`====`作为前后标记实现样例块

```asciidoc
====
使用====作为前后标记实现样例块
====
```
效果图：
![](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281526069.png)

如果需要换行，则需要空一整行。
```asciidoc
====
使用====作为前后标记实现样例块

换行需要空一整行来实现
====
```

效果图：

![image-20230128155707945](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281557049.png)



### 清单块

使用----作为前后标记实现清单块

```asciidoc
----
使用----作为前后标记实现清单块
----
```

效果图：

![image-20230128155803376](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281558454.png)

### 排版块
使用....作为前后标记实现排版（literal）块

```asci
....
// 使用....作为前后标记实现排版（literal）块
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
....
```

效果图：

![image-20230128160249945](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281602025.png)



```asciidoc
....
AsciiDoc是一种比Markdown功能更加丰富的文档，用其编写技术文档尤为合适，[Spring官网](https://spring.io)的很多文档都是使用其编写的。
....
```
效果图：
![](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281511172.png)

```asciidoc
====
使用四个=作为标记实现代码块
====
```

效果图：
![](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281514098.png)

还有其他的，暂不一一尝试，后面慢慢会说到！

我们也可以使用另外一种标记方法来实现块的功能：
![](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281550822.png)
上面我使用的是右侧的红色区域标记的语法，也可以使用左侧红色区域标记的语法。
比如：
```asciidoc
[example]
使用====作为前后标记实现样例块
```
效果跟使用`====`是一样的！

## 块标题

是可以添加标题的，在块上方使用“.”后面再放文字即可。
```asciidoc
.example标题
====
example
====
```

![](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281614567.png)

## 分配ID

可以给块分配一个ID，之后可以通过语法链接到该块

使用`[#块的ID]`来定义ID

```asciidoc
[#blockId1]
====
Content of delimited example block
====

点击<<blockId1>>，查看内容
```
这里使用了`<<anchors>>`来实现了锚点跳转，后面会具体说这个。
效果图：

![image-20230128162932361](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281629426.png)

# 文档属性

## 属性说明

每个文档可以设置属性（kv键值对），文档属性有内置的，也可以用户自定义（不和内置的重叠即可）。

内置属性会影响文档的展示样式等信息，用户自定义的属性则对于文档编写很有用处，比如定义一个属性，后期可以通过变量引入的方式引用，定义处修改，则处处修改。

属性的使用方式如下：

```text
:属性名:属性值
```
属性最常在文档的header中声明，也会在块的标题下方声明。这里有作用范围的概念，在header中声明的则作用于全局。

这些细节性的要求，短期谁也记不住的，多使用就会记住，而且一般编辑器也会提示错误。

## 内置属性

设置样例：

```asciidoc
//空属性值，会使用默认值
:toc:
// 也可以不用默认值（doctype的默认值是article），设置为book
:doctype: book
:description: AsciiDoc教程
```

特别要注意空格和冒号。

![image-20230128164800572](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281648641.png)

打开浏览器控制台，可见文档属性设置已经被添加到header中了。

## 取消属性

取消属性使用!和属性名搭配的方式，有多种策略

```text
// 取消以name开头的属性
:!name: 
// 取消以name结尾的属性
:name!:
```

# 文档头（Header）

## 文档标题

文档标题是0级章节标题，使用一个= 定义。通常放到文件的最顶端，默认模式下（article）只能有一个文档标题，如果是book类型则可以有多个文档标题（0级章节标题）。

```asciidoc
= 这是文档标题
```

## 标题变量

标题可以通过变量引用

```asciidoc
{doctitle} 标题被成功引入
```

效果图：
![](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281707711.png)

可见大括号内容被成功替换。

## 副标题

通过在主标题后使用:来定义副标题，副标题在网页上是无效的，在PDF、Word上才有效。

```asciidoc
= 这是文档主标题: 副标题
```
## 作者信息
作者信息使用多个内置属性来设置。
通过属性`author`和`email`来设置，必须放到文档标题下方。

```asciidoc
= 这是文档主标题: 副标题
:author: ProgramTalk
:email: ProgramTalk@163.com
```
效果图
![](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281721846.png)

多个作者也使用这两个属性，但是要在后面加上_数字（从一开始），比如：

```
:author_1: ProgramTalk
:email_1: ProgramTalk@163.com
:author_2: ProgramTalk2
:email_2: ProgramTalk2@163.com
```

效果图：

![image-20230128172447766](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281724828.png)



也可以不用属性，而是使用文档标题下放一行文字来实现。多个作者使用分号隔开。

```asciidoc
= 这是文档主标题: 副标题
// :author: ProgramTalk
// :email: ProgramTalk@163.com
// 多个作者
// :author_1: ProgramTalk
// :email_1: ProgramTalk@163.com
// :author_2: ProgramTalk2
// :email_2: ProgramTalk2@163.com
//使用一行来设置
ProgramTalk <ProgramTalk@163.com>; ProgramTalk2 <ProgramTalk2@163.com>
```

特别注意不能够有空行！！！

![image-20230128174122222](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281741293.png)



## 修订信息

可以使用属性设置

```asciidoc
= 这是文档主标题: 副标题
// :author: ProgramTalk
// :email: ProgramTalk@163.com
// 多个作者
// :author_1: ProgramTalk
// :email_1: ProgramTalk@163.com
// :author_2: ProgramTalk2
// :email_2: ProgramTalk2@163.com
//使用一行来设置
ProgramTalk <ProgramTalk@163.com>; ProgramTalk2 <ProgramTalk2@163.com>
//设置修订信息
:revdate: April 4, 2022
:revnumber: LPR55
:revremark: The spring incarnation of {doctitle}
:version-label!:
```

![image-20230128174011137](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281740204.png)

也可使用行的方式设置

```asciidoc
= 这是文档主标题: 副标题
// :author: ProgramTalk
// :email: ProgramTalk@163.com
// 多个作者
// :author_1: ProgramTalk
// :email_1: ProgramTalk@163.com
// :author_2: ProgramTalk2
// :email_2: ProgramTalk2@163.com
//使用一行来设置
ProgramTalk <ProgramTalk@163.com>; ProgramTalk2 <ProgramTalk2@163.com>
// 设置修订信息
// :revdate: April 4, 2022
// :revnumber: LPR55
// :revremark: The spring incarnation of {doctitle}
// :version-label!:
LPR55 April 4, 2022: The spring incarnation of {doctitle}
```



## 文档元数据（meta）

使用内置属性设置。

比如下方的description属性，就是设置html中meta中的description属性。

```asciidoc
:description: A story chronicling the inexplicable \
hazards and unique challenges a team must vanquish \
on their journey to finding an open source \
project's true power.
```

效果图：

![image-20230128174611826](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281746895.png)



**再次提醒！！！，切记在设置文档属性的时候不要出现空行！！！**

# 文档类型

文章 （`article`)

默认文档类型。 在 DocBook 中，包括附录、摘要、参考书目、词汇表和索引部分。 除非你正在制作一本书或一个手册页，否则你不需要担心文档类型。 默认值就足够了。

书 （`book`)

以文章文档类型为基础，具有使用顶级标题作为部分标题的附加功能，包括附录、奉献、前言、参考书目、词汇表、索引和序言。 还有多部分书籍的概念，但与普通书籍的区别取决于内容。 一本书只有章节和特殊部分，而多部分书籍则按部分划分，每个部分包含一个或多个章节或特殊部分。

手册页 （`manpage`)

用于为 Unix 和类 Unix 操作系统生成 roff 或 HTML 格式的手册页（手册页）。 此 doctype 指示解析器识别特殊的文档标题和节命名约定，以便将 AsciiDoc 内容组织为手册页。 有关如何使用 AsciiDoc 构建手册页并使用 Asciidoctor生成手册页的详细信息，请参阅[从 AsciiDoc 生成手册页](https://docs.asciidoctor.org/asciidoctor/latest/manpage-backend/)。

内联 （`inline`)

在某些情况下，您可能只想将内联 AsciiDoc 格式应用于输入文本，而不将其包装在块元素中。 例如，在 Asciidoclet 项目（Javadoc 中的 AsciiDoc）中，Javadoc 标记中的文本只需要内联格式。



# 文章标题和级别

标题一共有六级，使用1-6个=号来开头。

```asciidoc
// 文章标题和级别
= 一级标题
== 二级标题
=== 三级标题
==== 四级标题
===== 五级标题
====== 六级标题
```

![image-20230128175308347](https://itlab1024-1256529903.cos.ap-beijing.myqcloud.com/202301281753416.png)


