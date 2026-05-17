# Markdown 基本语法


这篇文章提供了可以在 Hugo 的文章中使用的基本 Markdown 语法示例。

> 注意：这篇文章借鉴了一篇很棒的来自 Grav 的文章。

如果你想了解 **FixIt** 主题的扩展 Markdown 语法，请阅读扩展 Markdown 语法页面。

编写 Web 内容很麻烦。WYSIWYG（所见即所得）编辑器帮助减轻了这一任务，但通常会导致代码太糟，或更糟糕的是，网页也会很丑。**Markdown** 是一种更好的生成 HTML 内容的方式。

一些主要好处：

1. Markdown 简单易学，几乎没有多余的字符，因此编写内容也更快。
2. 用 Markdown 书写时出错的机会更少。
3. 可以产生有效的 XHTML 输出。
4. 将内容和视觉显示保持分开，这样就不会打乱网站的外观。
5. 可以在你喜欢的任何文本编辑器或 Markdown 应用程序中编写内容。
6. Markdown 使用起来很有趣！

John Gruber, Markdown 的作者如是说：

> "Markdown 格式的首要设计目标是更具可读性。最初的想法是 Markdown 格式的文档应当以纯文本形式发布，而不会看起来像被标签或格式说明所标记。"

## 标题

从 `h2` 到 `h6` 的标题在每个级别上都加上一个 `＃`:

```markdown
## h2 标题
### h3 标题
#### h4 标题
##### h5 标题
###### h6 标题
```

**标题 ID** — 要添加自定义标题 ID，请在与标题相同的行中将自定义 ID 放在花括号中：

```markdown
### 一个很棒的标题 {#custom-id}
```

输出：`<h3 id="custom-id">一个很棒的标题</h3>`

## 注释

注释是和 HTML 兼容的：

```markdown
<!-- 这是一段注释 -->
```

## 水平线

HTML 中的 `<hr>` 标签用来在段落元素之间创建一个"专题间隔"。使用 Markdown，你可以用以下方式创建：

- `___`：三个连续的下划线
- `---`：三个连续的破折号
- `***`：三个连续的星号

## 段落

按照纯文本的方式书写段落，纯文本在呈现的 HTML 中将用 `<p>`/`</p>` 标签包裹。可以使用一个空白行进行**换行**。

## 内联 HTML 元素

如果你需要某个 HTML 标签（带有一个类），则可以简单地像这样使用：

```markdown
Markdown 格式的段落。

<div class="class">
    这是 <b>HTML</b>
</div>

Markdown 格式的段落。
```

## 强调

### 加粗

```markdown
**渲染为粗体**
__渲染为粗体__
```

输出：`<strong>渲染为粗体</strong>`

### 斜体

```markdown
*渲染为斜体*
_渲染为斜体_
```

输出：`<em>渲染为斜体</em>`

### 删除线

按照 GFM（GitHub Flavored Markdown）你可以使用删除线：

```markdown
~~这段文本带有删除线。~~
```

输出：`<del>这段文本带有删除线。</del>`

### 组合

加粗、斜体和删除线可以组合使用：

```markdown
_**加粗和斜体**_
~~**删除线和加粗**~~
~~_删除线和斜体_~~
~~_**加粗，斜体和删除线**_~~
```

## 引用

在要引用的任何文本之前添加 `>`:

```markdown
> **Fusion Drive** combines a hard drive with a flash storage (solid-state drive) and presents it as a single logical volume with the space of both drives combined.
```

引用也可以嵌套：

```markdown
> Donec massa lacus, ultricies a ullamcorper in, fermentum sed augue.
Nunc augue augue, aliquam non hendrerit ac, commodo vel nisi.
>> Sed adipiscing elit vitae augue consectetur a gravida nunc vehicula.
```

## 列表

### 无序列表

你可以使用 `*`、`-` 或 `+` 来表示无序列表中的项：

```markdown
* Lorem ipsum dolor sit amet
* Consectetur adipiscing elit
* Integer molestie lorem at massa
* Facilisis in pretium nisl aliquet
* Nulla volutpat aliquam velit
  * Phasellus iaculis neque
  * Purus sodales ultricies
  * Vestibulum laoreet porttitor sem
  * Ac tristique libero volutpat at
* Faucibus porta lacus fringilla vel
* Aenean sit amet erat nunc
* Eget porttitor lorem
```

### 有序列表

```markdown
1. Lorem ipsum dolor sit amet
2. Consectetur adipiscing elit
3. Integer molestie lorem at massa
4. Facilisis in pretium nisl aliquet
5. Nulla volutpat aliquam velit
6. Faucibus porta lacus fringilla vel
7. Aenean sit amet erat nunc
8. Eget porttitor lorem
```

> 技巧：如果你对每一项使用 `1.`，Markdown 将自动为每一项编号。

## 代码

### 行内代码

用 `` ` `` 包装行内代码段：

```markdown
在这个例子中，`<section></section>` 会被包裹成 **代码**。
```

### 缩进代码

> 不推荐使用。

将几行代码缩进至少四个空格：

```
    // Some comments
    line 1 of code
    line 2 of code
    line 3 of code
```

### 围栏代码块

> 推荐使用。

使用"围栏" ` ``` ` 来生成一段带有语言属性的代码块：

````markdown
```markdown
Sample text here...
```
````

### 语法高亮

GFM（GitHub Flavored Markdown）也支持语法高亮。只需在第一个代码"围栏"之后直接添加你要使用的语言的文件扩展名，例如 ` ```js `，语法高亮显示将自动应用于渲染的 HTML 中。

````javascript
grunt.initConfig({
  assemble: {
    options: {
      assets: 'docs/assets',
      data: 'src/data/*.{json,yml}',
      helpers: 'src/custom-helpers.js',
      partials: ['src/partials/**/*.{hbs,md}']
    },
    pages: {
      options: {
        layout: 'default.hbs'
      },
      files: {
        './': ['src/templates/pages/index.hbs']
      }
    }
  }
});
````

## 表格

通过在每个单元格之间添加竖线作为分隔线，并在标题下添加一行破折号（也由竖线分隔）来创建表格：

```markdown
| Option | Description |
| ------ | --------------------------------------------------------------------------- |
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default.    |
| ext    | extension to be used for dest files.                                      |
```

**Markdown 表格对齐规则：** 在分隔线左侧加 `:` 左对齐，右侧加 `:` 右对齐，两侧都加或不加则居中。

```markdown
| 姓名 | 年龄 | 城市 |
| :--- | ---: | :--: |
| 张三 | 28   | 北京 |
| 李四 | 34   | 上海 |
```

## 链接

### 基本链接

```markdown
<https://assemble.io>
<contact@revolunet.com>
[Assemble](https://assemble.io)
```

### 添加一个标题

```markdown
[Upstage](https://github.com/upstage/ "Visit Upstage!")
```

### 引用式链接

引用式链接分为两部分：与文本保持内联的部分以及存储在文件中其他位置的部分，以使文本易于阅读。

```markdown
[text][id]
⋮
[id]: http://example.org/ "title"
```

例如：

```markdown
[FixIt][fixit-repo]

[fixit-repo]: https://github.com/hugo-fixit/FixIt "A clean, elegant but advanced blog theme for Hugo"
```

### 定位标记

定位标记使你可以跳至同一页面上的指定锚点：

```markdown
## Table of Contents
  * [Chapter 1](#chapter-1)
  * [Chapter 2](#chapter-2)
  * [Chapter 3](#chapter-3)
```

将跳转到这些部分：

```markdown
## Chapter 1 <a id="chapter-1"></a>
Content for chapter one.

## Chapter 2 <a id="chapter-2"></a>
Content for chapter two.

## Chapter 3 <a id="chapter-3"></a>
Content for chapter three.
```

## 脚注

脚注使你可以添加注释和参考，而不会使文档正文混乱。要创建脚注引用，请在方括号中添加插入符号和标识符 (`[^1]`)。标识符可以是数字或单词，但不能包含空格或制表符。

```markdown
这是一个数字脚注 [^1]
这是一个带标签的脚注 [^label]

[^1]: 这是一个数字脚注
[^label]: 这是一个带标签的脚注
```

## 图片

图片的语法与链接相似，但包含一个在前面的感叹号：

```markdown
![Droidtocat](https://octodex.github.com/images/droidtocat.png)
```

或者带标题：

```markdown
![Alt text](https://octodex.github.com/images/spidertocat.png "The Spidertocat")
```

像链接一样，图片也具有引用式的语法：

```markdown
![Alt text][id]
```

稍后在文档中提供参考内容：

```markdown
[id]: https://octodex.github.com/images/ironcat.jpg  "The IronCat"
```


---

> 作者: 西塘  
> URL: https://sheetung.github.io/markdown-basics/  
> 转载 URL: https://fixit.lruihao.cn/zh-cn/documentation/content-management/markdown-syntax/basics/
