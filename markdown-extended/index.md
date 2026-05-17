# Markdown 扩展语法


本文展示了 **FixIt Flavored Markdown** 扩展语法。

## 警示

警示（Alert）也被称为 **Callout** 或 **Admonition**，是用于强调关键信息的引用块。

### 基本语法

使用基本的 Markdown 语法，每个警示的第一行是一个警示指示符，由一个感叹号和警示类型组成，用中括号括起来。

Alert 基本语法与 GitHub、Obsidian 和 Typora 兼容。

以下是所有五种类型的示例：

```markdown
> [!NOTE]
> 突出显示用户应考虑的信息，即使只是浏览也应考虑。

> [!TIP]
> 可选信息，可帮助用户取得更大的成功。

> [!IMPORTANT]
> 用户成功所需的关键信息。

> [!WARNING]
> 由于存在潜在风险，需要用户立即关注的关键内容。

> [!CAUTION]
> 操作的潜在负面后果。
```

呈现的输出效果：

> [!NOTE]
> 突出显示用户应考虑的信息，即使只是浏览也应考虑。

> [!TIP]
> 可选信息，可帮助用户取得更大的成功。

> [!IMPORTANT]
> 用户成功所需的关键信息。

> [!WARNING]
> 由于存在潜在风险，需要用户立即关注的关键内容。

> [!CAUTION]
> 操作的潜在负面后果。

### 扩展语法

使用扩展 Markdown 语法，你可以选择包含警示符号或警示标题。警示符号是 `+` 或 `-` 之一，通常用于指示警示是否可以图形折叠。

Alert 扩展语法与 Obsidian 和 Fixit admonition shortcode 兼容。

> **警告**：扩展语法与 GitHub 或 Typora 不兼容。如果包含警示符号或警示标题，这些应用程序会将 Markdown 渲染为引用块。

#### 更改标题

默认警示标题是其类型标识符的标题大小写。你可以通过在类型标识符后添加文本来更改它：

```markdown
> [!NOTE] FixIt
> 一个简洁、优雅且高效的 Hugo 主题。
```

你甚至可以省略正文来创建仅标题的警示：

```markdown
> [!TIP] 仅标题的警示
```

#### 可折叠警示

你可以通过在类型标识符后直接添加加号（+）或减号（-）来使警示可折叠。

```markdown
> [!WARNING]+ 辐射危害
> 请勿在没有防护装备的情况下接近或操作。

> [!QUESTION]- 警示可以折叠吗？
> 是的！在可折叠警示中，内容在折叠时被隐藏。
```

#### 嵌套警示

你可以在多个级别中嵌套警示。

```markdown
> [!question] 警示可以嵌套吗？
> > [!todo] 可以！它们可以。
> > > [!example] 你甚至可以使用多层嵌套。
```

#### 仅内容警示

你可以通过在类型标识符后直接添加波浪号（`~`）来创建仅内容警示。

这是 FixIt 独有的扩展语法，与 Obsidian 或其他 Markdown 应用不兼容。

```markdown
> [!TIP]~
> 这是一个没有标题的仅内容警示。
```

#### 支持的类型

Alert 扩展语法支持 **13** 种类型的警示横幅，除非你自定义 Admonition，否则任何不支持的类型都会默认为 `note` 类型。类型标识不区分大小写。

| 类型 | 别名 |
|------|------|
| `note` | — |
| `abstract` | `summary`, `tldr` |
| `info` | — |
| `todo` | — |
| `tip` | `hint`, `important` |
| `success` | `check`, `done` |
| `question` | `help`, `faq` |
| `warning` | `caution`, `attention` |
| `failure` | `fail`, `missing` |
| `danger` | `error` |
| `bug` | — |
| `example` | — |
| `quote` | `cite` |

## 颜色预览

在文章内容中，可以使用反引号在句子中标注颜色。反引号内支持的颜色模型将显示颜色的可视化效果。

```markdown
对于 `Light` 模式，背景色为`#ffffff`，对于 `Dark` 模式，背景颜色为`#000000`。
```

当前支持的颜色模型：

| Color | 语法 | 示例 | 输出 |
|-------|------|------|------|
| HEX | `` `#RRGGBB` `` | `` `#0969DA` `` | `#0969DA` |
| RGB | `` `rgb(R,G,B)` `` | `` `rgb(9, 105, 218)` `` | `rgb(9, 105, 218)` |
| HSL | `` `hsl(H,S,L)` `` | `` `hsl(212, 92%, 45%)` `` | `hsl(212, 92%, 45%)` |

> **注意**：支持的颜色模型在反引号内不能有任何前导或尾随空格。

## 任务列表

要创建任务列表，请在每个列表项前添加一个短横线和空格，然后跟上 `[ ]`。

```markdown
- [x] 这是一个已完成的任务。
- [ ] 这是一个未完成的任务。
```

你可以在括号内使用任何字符来标记任务为已完成或其他状态：

```markdown
- [ ] 未完成
- [x] 已完成
- [/] 进行中
- [-] 已取消
- [<] 已计划
- [>] 已重新计划
- [!] 重要
- [?] 问题
```

> **提示**：如果你想要更多类型的任务列表，请查看进阶篇 - 自定义任务列表章节。

## 下划线

> **如何开启 Hugo 扩展语法**：下划线、标记文本、下标和上标语法默认关闭，需更新 Hugo 版本到 `0.128.0` 以上且开启以下配置：

```toml
[markup]
[markup.goldmark]
[markup.goldmark.extensions]
strikethrough = false

[markup.goldmark.extensions.extras]
[markup.goldmark.extensions.extras.delete]
enable = true
[markup.goldmark.extensions.extras.insert]
enable = true
[markup.goldmark.extensions.extras.mark]
enable = true
[markup.goldmark.extensions.extras.subscript]
enable = true
[markup.goldmark.extensions.extras.superscript]
enable = true
```

**Hugo** 支持一种 **下划线** Markdown 扩展语法：

```markdown
FixIt 主题的作者是 ++Lruihao++。
```

呈现的输出效果：FixIt 主题的作者是 ++Lruihao++。

## 标记文本

**Hugo** 支持一种 **标记文本** Markdown 扩展语法：

```markdown
==FixIt== 是一个很棒的 Hugo 主题！
```

呈现的输出效果：==FixIt== 是一个很棒的 Hugo 主题！

扩展的标记文本语法支持 **6** 种类型的标记文本。

```markdown
==Primary==[primary]
==Secondary==[secondary]
==Success==[success]
==Info==[info]
==Warning==[warning]
==Danger==[danger]
```

除非你自定义标记文本，否则任何不支持的类型都会默认为 `default` 类型。

自定义标记文本示例：

```markdown
==这是一个带有粉色的自定义类型。==[pink]
```

在项目目录 `assets/css/_custom.scss` 中添加 CSS 来自定义：

```scss
.mark-pink {
  --fi-mark-background-color: pink;
}
```

输出的 HTML 类似于：`<mark class="mark-pink">这是一个带有粉色的自定义类型。</mark>`

## 下标

**Hugo** 支持一种 **下标** Markdown 扩展语法：

```markdown
水的化学式是 H~2~O。
```

呈现的输出效果：水的化学式是 H~2~O。

## 上标

**Hugo** 支持一种 **上标** Markdown 扩展语法：

```markdown
2^10^ 等于 1024。
```

呈现的输出效果：2^10^ 等于 1024。

## Emoji 支持

这部分内容在 Emoji 支持页面中介绍。

## 数学公式

**FixIt** 基于 KaTeX 或 MathJax 提供数学公式的支持，默认引擎为 KaTeX。

你可以在主题配置中修改数学公式自动渲染的相关配置：

```toml
[markup]
[markup.goldmark]
[markup.goldmark.extensions]
[markup.goldmark.extensions.passthrough]
enable = true

[markup.goldmark.extensions.passthrough.delimiters]
block = [
  ['\\[', '\\]'],
  ['$$', '$$']
]
inline = [
  ['\\(', '\\)'],
  ['$', '$']
]

[params]
[params.page]
[params.page.math]
enable = true
type = "katex"

[params.page.math.katex]
copyTex = true
throwOnError = false
errorColor = "#ff4949"
```

### KaTeX

KaTeX 通过 Hugo 的 `transform.ToMath` 函数在 **服务器端渲染**，所以客户端加载速度更快。

#### 行内公式

默认的行内公式分割符有：

- `$ ... $`
- `\( ... \)`

例如：

```markdown
$c = \pm\sqrt{a^2 + b^2}$ 和 \(f(x)=\int_{-\infty}^{\infty} \hat{f}(\xi) e^{2 \pi i \xi x} d \xi\)
```

#### 公式块

默认的公式块分割符有：

- `$$ ... $$`
- `\[ ... \]`

例如：

```markdown
$$ c = \pm\sqrt{a^2 + b^2} $$

\[f(x)=\int_{-\infty}^{\infty} \hat{f}(\xi) e^{2 \pi i \xi x} d \xi\]

$$
\begin{equation*}
  \rho \frac{\mathrm{D} \mathbf{v}}{\mathrm{D} t}=\nabla \cdot \mathbb{P}+\rho \mathbf{f}
\end{equation*}
$$

$$
\begin{equation}
  \mathbf{E}=\sum_{i} \mathbf{E}_{i}=\mathbf{E}_{1}+\mathbf{E}_{2}+\mathbf{E}_{3}+\cdots
\end{equation}
$$

$$
\begin{align}
  a&=b+c \\
  d+e&=f
\end{align}
$$

$$
\begin{alignat}{2}
   10&x+&3&y = 2 \\
   3&x+&13&y = 4
\end{alignat}
$$

$$
\begin{gather}
   a=b \\
   e=b+c
\end{gather}
$$

$$
\begin{CD}
   A @>a>> B \\
   @VbVV @AAcA \\
   C @= D
\end{CD}
$$
```

#### 复制公式

**Copy-tex** 是一个 KaTeX 的插件。通过这个扩展，在选择并复制 KaTeX 渲染的公式时，会将其 LaTeX 源代码复制到剪贴板。

在主题配置中的 `[params.page.math.katex]` 下面设置属性 `copyTex = true` 来启用 Copy-tex。

#### 化学方程式

**mhchem** 是一个 KaTeX 的插件，提供了 `\ce` 和 `\pu` 函数。通过这个扩展，你可以在文章中轻松编写化学方程式。

```markdown
$$ \ce{CO2 + C -> 2 CO} $$

$$ \ce{Hg^2+ ->[I-] HgI2 ->[I-] [Hg^{II}I4]^2-} $$

$$C_p[\ce{H2O(l)}] = \pu{75.3 J // mol K}$$
```

#### 自定义宏

你可以在主题配置中的 `[params.page.math.katex.macros]` 下面添加自定义宏。

例如：

```toml
[params.page.math.katex.macros]
"\\f" = "#1f(#2)" # usage: $\f{a}{b}$
```

然后在文章中使用：

```markdown
$$
\f\relax{x} = \int_{-\infty}^\infty
    \f\hat\xi\,e^{2 \pi i \xi x}
    \,d\xi
$$
```

#### 错误信息

如果在渲染公式时遇到错误，KaTeX 会在页面上显示错误信息。鼠标悬停在错误信息上可以查看详细的错误信息。

> **小心**：如果你设置 `params.page.math.katex.throwOnError` 为 `true`，则会抛出错误并停止渲染。

### MathJax

MathJax 在页面加载后通过 JavaScript 进行 **客户端渲染**，速度较慢但功能更加强大。这部分内容在 MathJax 支持页面中介绍。

## 字符注音或者注释

**FixIt** 主题支持一种 **字符注音或者注释** Markdown 扩展语法：

```markdown
[FixIt]^(一个简洁、优雅且高效的 Hugo 主题)
```

## 分数

**FixIt** 主题支持一种 **分数** Markdown 扩展语法：

```markdown
[浅色]/[深色]

[99]/[100]
```

## Font Awesome

**FixIt** 主题使用 Font Awesome V6 作为图标库。你同样可以在文章中轻松使用这些图标。

从 Font Awesome 网站上获取所需的图标 `class`。

```markdown
去露营啦！:(fa-solid fa-campground fa-fw): 很快就回来。

真开心！:(fa-regular fa-grin-tears):
```

## 转义字符

在某些特殊情况下，你的文章内容会与 Markdown 的基本或者扩展语法冲突，并且无法避免。转义字符语法可以帮助你渲染出想要的内容：

```markdown
{?X} -> X
```

例如，两个 `:` 会启用 emoji 语法。但有时候这不是你想要的结果。可以像这样使用转义字符语法：

```markdown
{?:}joy:
```

呈现的输出效果：:joy: 而不是 😂

另一个例子：

```markdown
[link{?]}(#escape-character)
```

呈现的输出效果：[link](#escape-character) 而不是一个链接。

## Markdown 属性

Hugo 支持图像和块元素上的 Markdown 属性，包括块引用、围栏代码块、标题、水平线、列表、段落和表格。

### 语法

```markdown
some Markdown content
{#id .class1 .class2 key1="value1" key2="value2"}
```

在大多数情况下，将属性列表放置在标记元素下方。对于标题和围栏代码块，将属性列表放在右侧。

| 标记元素 | 属性放置的位置 |
|---------|-------------|
| blockquote | 底部 |
| fenced code block | 右侧 |
| heading | 右侧 |
| horizontal rule | 底部 |
| image | 底部 |
| list | 底部 |
| paragraph | 底部 |
| table | 底部 |

### 例子

#### 分割线

带有 CSS 类的分割线：

```markdown
---
{.awesome-hr}
```

#### 引用

带有 CSS 类的块引用：

```markdown
> The quick brown fox jumps over the lazy dog.
{.blockquote-center}
```

#### 表格 & 列表

```markdown
* 水果
  * 苹果
  * 橙子
  * 香蕉
  {.text-success}
* 乳制品
  * 牛奶
  * 奶酪
  {.text-warning}
{.text-primary}
```

## 代码块扩展语法

**FixIt** 主题扩展了标准 Markdown 代码围栏，支持高级功能，包括图表、图形和交互式可视化。

### 语法

扩展的代码围栏使用与标准 Markdown 相同的三重反引号语法，但使用特定语言标识符来触发特殊的渲染引擎：

```markdown
```LANG [OPTIONS]
// 在这里输入特定语言的内容
```
```

### 语言

这些功能在 FixIt 主题中自动启用，无需额外配置：

| 语言标识符 | 描述 |
|-----------|------|
| `goat` | ASCII 艺术图表，渲染为可缩放的矢量图形 |
| `mermaid` | 专业图表，包括流程图、时序图等 |
| `echarts` | 交互式数据可视化图表和图形 |
| `timeline` | 具有丰富格式的时间线事件显示 |
| `json` | 格式化和可折叠的 JSON 数据视图 |
| `file-tree` | 渲染文件和目录结构为交互式树 |
| `toggle` | 以 TOML、YAML 和 JSON 格式渲染语法高亮的配置数据 |

### 选项

你可以通过 Hugo 语法高亮选项、主题代码块配置、Markdown 属性或者以下选项来自定义代码块：

| 选项 | 描述 | 类型 |
|-----|------|------|
| `title` | 代码块标题 | `string` |
| `name` | 代码块名称或标签项名称 | `string` |
| `group` | 代码块标签组名称 | `string` |
| `before_tabs` | 在标签项之前显示的内容 | `string` |
| `filename` | 代码块文件名 | `string` |

`group` 和 `name` 选项可以一起使用来创建标签页式的代码块：

````markdown
```python {group="languages", name="Hi Python"}
print('Hello, world!')
```

```js {group="languages", name="Hi JS", .active}
console.log('Hello, world!');
```
````


---

> 作者: 西塘  
> URL: https://sheetung.github.io/markdown-extended/  
> 转载 URL: https://fixit.lruihao.cn/zh-cn/documentation/content-management/markdown-syntax/extended/
