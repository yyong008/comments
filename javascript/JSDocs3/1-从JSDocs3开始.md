# JSDocs3

## 开始

JSDoc 3是JavaScript的API文档生成器，类似于Javadoc或phpDocumentor。您可以将文档注释直接添加到源代码中，与代码本身一起添加。 JSDoc工具将扫描您的源代码并为您生成HTML文档网站。

## 在代码中添加文档注释

JSDoc的目的是记录JavaScript应用程序或库的API。假设您需要记录模块，命名空间，类，方法，方法参数等内容。

通常应该在记录代码之前放置JSDoc注释。每个注释必须以 `/**` 序列开头，以便JSDoc解析器识别。以`/*`，`/***`或超过3星开头的评论将被忽略。这是一个允许您禁止解析注释块的功能。

**最简单的文档只是一个描述**

```js
/** This is a description of the foo function. */
function foo() {
}
```

添加描述很简单 - 只需在文档注释中键入所需的描述即可。

特殊的“JSDoc标签”可用于提供更多信息。例如，如果函数是类的构造函数，则可以通过添加@constructor标记来指示此函数。

**使用JSDoc标记来描述您的代码**

```js
/**
 * Represents a book.
 * @constructor
 */
function Book(title, author) {
}
```

可以使用更多标签添加更多信息。有关JSDoc 3识别的标记的完整列表，请参阅主页。

**使用标签添加更多信息**

```js
/**
 * Represents a book.
 * @constructor
 * @param {string} title - The title of the book.
 * @param {string} author - The author of the book.
 */
function Book(title, author) {
}
```

## 生成一个网站

一旦您的代码被注释，您就可以使用JSDoc 3工具从源文件生成HTML网站。

默认情况下，JSDoc使用内置的“默认”模板将文档转换为HTML。您可以编辑此模板以满足您自己的需要，或者根据您的喜好创建一个全新的模板。

**在命令行上运行文档生成器**

```bash
jsdoc book.js
jsdocs book.js
```

此命令将在当前工作目录中创建名为out /的目录。在该目录中，您将找到生成的HTML页面。