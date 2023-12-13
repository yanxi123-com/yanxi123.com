---
title: "使用示例"
# meta title
meta_title: ""
# meta description
description: "This is meta description"
# save as draft
draft: false
---

{{< toc >}}


下面是一个标题的例子。可以通过以下 markdown 规则来写标题。例如：标题1使用 `#` ，标题6使用 `######`` 。

# 一级标题

## 二级标题

### 三级标题

#### 四级标题

##### 五级标题

###### 六级标题

<hr>

### 强调

通过斜体强调，使用 _下划线_。

通过加粗强调，使用 **星号**。

组合使用星号和下划线 **星号和 _下划线_**。

删除线使用两个波浪号，~~划掉这个~~。

<hr>

### 按钮

{{< button label="按钮" link="/" style="solid" >}}

<hr>

### 链接

[我是内联样式链接](https://www.google.com)

[我是带标题的内联样式链接](https://www.google.com "谷歌主页")

[我是引用风格链接][Arbitrary case-insensitive reference text]

[我是对仓库文件的相对引用](../blob/master/LICENSE)

[你可以使用数字定义引用风格链接][1]

或者留空，使用 [链接文本本身]。

URL和尖括号中的URL会自动转换为链接。
<http://www.example.com> 或 <http://www.example.com> 有时
example.com (但在Github上不行，比如)。

一些文本显示引用链接可以稍后跟随。

[arbitrary case-insensitive reference text]: https://www.themefisher.com
[1]: https://gethugothemes.com
[link text itself]: https://www.getjekyllthemes.com

<hr>

### 段落

知识是痛苦的，智慧是宝贵的，智慧是无限的。真的，真的。但是，如果你不相信上帝的话，你就不会感到悲伤。


<hr>

### 有序列表

1. 列表项
2. 列表项
3. 列表项
4. 列表项
5. 列表项

<hr>

### 无序列表

- 列表项
- 列表项
- 列表项
- 列表项
- 列表项

<hr>

### 注意

{{< notice "note" >}}
这是一个简单的提示。
{{< /notice >}}

{{< notice "tip" >}}
这是一个简单的技巧。
{{< /notice >}}

{{< notice "info" >}}
这是一个简单的信息。
{{< /notice >}}

{{< notice "warning" >}}
这是一个简单的警告。
{{< /notice >}}

<hr>

### 标签页

{{< tabs >}}
{{< tab "标签 1" >}}

#### 你来这里有什么特别的事吗？

你是为了某件特别的事情还是只是来批评瑞克？当你加速到最大曲速时，你似乎瞬间出现在两个地方。我们船上有一个破坏者。我们知道你在处理赃物。但我想谈谈对沃尔夫中尉的暗杀企图。

{{< /tab >}}

{{< tab "标签 2" >}}

#### 我想谈谈暗杀企图

知识是痛苦的，智慧是宝贵的，智慧是无限的。真的，真的。但是，如果你不相信上帝的话，你就不会感到悲伤。

知识是痛苦的，智慧是宝贵的，智慧是无限的。真的，真的。但是，如果你不相信上帝的话，你就不会感到悲伤。

{{< /tab >}}

{{< tab "标签 3" >}}

#### 我们知道你在处理偷来的矿石

知识是痛苦的，智慧是宝贵的，智慧是无限的。真的，真的。但是，如果你不相信上帝的话，你就不会感到悲伤。

知识是痛苦的，智慧是宝贵的，智慧是无限的。真的，真的。但是，如果你不相信上帝的话，你就不会感到悲伤。

{{< /tab >}}
{{< /tabs >}}

<hr>

### 手风琴

{{< accordion "为什么你需要这样做？" >}}

- 痛苦之人，应被视为有智慧之人。
- 痛苦之人，应被视为有智慧之人。
- 痛苦之人，应被视为有智慧之人。

{{< /accordion >}}

{{< accordion "我怎样调整水平居中？" >}}

- 痛苦之人，应被视为有智慧之人。
- 痛苦之人，应被视为有智慧之人。
- 痛苦之人，应被视为有智慧之人。

{{< /accordion >}}

{{< accordion "你应该使用负边距吗？" >}}

- 痛苦之人，应被视为有智慧之人。
- 痛苦之人，应被视为有智慧之人。
- 痛苦之人，应被视为有智慧之人。

{{< /accordion >}}


<hr>

### 代码和语法高亮

这是一个 `Inline code` 样例。


```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```

```python
s = "Python syntax highlighting"
print s
```

<hr>

### 引用块

> 你是为了某件特别的事情来的还是只是来批评瑞克？当你加速到最大曲速时，你似乎瞬间出现在两个地方。

<hr>

### 表格

| 物品        |      颜色      |  价格 |
| ------------- | :-----------: | ----: |
| 冰淇淋    | 黄色 | 30元|
| 巧克力      |   棕色    |   20元 |
| 棉花糖 |   白色    |    10元 |

<hr>

### 图片

{{< image src="images/image-placeholder.png" caption="" alt="替代文本" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="图片标题"  webp="false" >}}

<hr>

### 画廊

{{< gallery dir="images/gallery" class="" height="400" width="400" webp="true" command="Fit" option="" zoomable="true" >}}

<hr>

### 滑块

{{< slider dir="images/gallery" class="max-w-[600px] ml-0" height="400" width="400" webp="true" command="Fit" option="" zoomable="true" >}}

<hr>

### Youtube视频

{{< youtube ResipmZmpDU >}}

<hr>

### 自定义视频

{{< video src="https://www.w3schools.com/html/mov_bbb.mp4" width="100%" height="auto" autoplay="false" loop="false" muted="false" controls="true" class="rounded-lg" >}}
