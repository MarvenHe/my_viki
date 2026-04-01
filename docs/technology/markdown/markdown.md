## Markdown 使用

### 什么是Markdown
Markdown 是一种轻量级的标记语言，由约翰·格鲁伯（John Gruber）于2004年创建。<br>
它的设计理念是让文档的编写更加简洁和易读，使用简单的符号来标记文本格式，而不是复杂的格式化工具栏。<br>

### Markdown的优势
简洁易学：语法简单，几分钟就能掌握基本用法。
可读性强：即使不经过渲染，纯文本格式也很容易阅读。
通用性好：几乎所有的文本编辑器都支持 Markdown，且可以轻松转换为 HTML、PDF 等多种格式。
专注内容：让你将注意力集中在写作本身，而不是排版细节


### 基础语法
#### 1.标题 (Headers)
```markdown
# 一级标题 (H1)
## 二级标题 (H2)
### 三级标题 (H3)
#### 四级标题 (H4)
##### 五级标题 (H5)
###### 六级标题 (H6)
```
<br>

#### 2.强调 (Emphasis)
粗体 (Bold)：使用两个星号 ** 或下划线 __ 包围文字。<br>
```markdown
**这是粗体**
__这也是粗体__
```
实现效果<br>
**这是粗体**<br>
__这也是粗体__<br>

斜体 (Italic)：<br>
使用一个星号 * 或下划线 _ 包围文字。<br>
删除线 (Strikethrough)：<br>
使用两个波浪号 ~~ 包围文字。<br>
<br>

#### 3. 列表 (Lists)
无序列表 (Unordered List)：<br>
使用星号 *、加号 + 或减号 - 作为列表项标记。<br>

有序列表 (Ordered List)：<br>
使用数字加英文句点 1. 来标记。<br>
<br>

#### 4. 链接 (Links)
Markdown 提供两种链接语法：行内式和参考式。<br>
__1) 行内式链接：__ <br>
使用方括号 [] 包含链接文字，紧接着圆括号 () 包含 URL 和可选的链接标题。<br>
```python
[链接文字](https://example.com)
```
__2) 参考式链接：__ <br>
先定义一个引用，然后在链接中使用该引用。<br>
```python
[链接文字][id]
[id]:https://example.com "可选的标题"
```
<br>

#### 5. 图片 (Images)
图片的语法与链接类似，只是在最前面多了一个感叹号 !。<br>
```python
![替代文字](图片URL "可选的标题")
![示例图片](https://via.placeholder.com/150 "这是一个占位图")
```
<br>

#### 6. 代码 (Code)
__行内代码：__<br>
使用1对反引号``包裹代码。<br>
示例： `行内代码 inline code` <br>

__代码块 (Fenced Code Block)：__<br>
使用三个反引号 开始和结束代码块，并可指定语言。<br>
以下为示例:
```python
print("Hello, Markdown!")
```
<br>

### __Mark:__
vscode中打开markdown预览：`Ctrl+Shift+V`
20260401-00
<br>
<br>