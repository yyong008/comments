# 在JSDoc 3中使用namepath

## JSDoc 3中的Namepaths

在引用文档中其他位置的JavaScript变量时，必须提供映射到该变量的唯一标识符。名称路径提供了一种方法，并在实例成员，静态成员和内部变量之间消除歧义。

**JSDoc 3中Namepath的基本语法示例**

```js
myFunction
MyConstructor
MyConstructor#instanceMember
MyConstructor.staticMember
MyConstructor~innerMember // note that JSDoc 2 uses a dash
```

下面的示例显示：名为“say”的实例方法，也称为“say”的内部函数，以及名为“say”的静态方法。这三种不同的方法都是彼此独立存在的。

**使用文档标记来描述您的代码。**

```js
/** @constructor */
Person = function() {
    this.say = function() {
        return "I'm an instance.";
    }

    function say() {
        return "I'm inner.";
    }
}
Person.say = function() {
    return "I'm static.";
}

var p = new Person();
p.say();      // I'm an instance.
Person.say(); // I'm static.
// there is no way to directly access the inner function from here
```

您将使用三种不同的名称路径语法来引用三种不同的方法：

**使用文档标记来描述您的代码**

```js
Person#say  // the instance method named "say."
Person.say  // the static method named "say."
Person~say  // the inner method named "say."
```

您可能想知道为什么有一种语法可以引用内部方法，因为该方法无法从定义的函数外部直接访问。虽然这是真的，因此很少使用“〜”语法，但它是可能的从该容器内的另一个方法返回对内部方法的引用，因此代码中的某个对象可能会借用内部方法。

请注意，如果构造函数的实例成员也是构造函数，则可以将名称路径链接在一起以形成更长的名称路径：

**使用文档标记来描述您的代码。**

```js
/** @constructor */
Person = function() {
    /** @constructor */
    this.Idea = function() {
        this.consider = function(){
            return "hmmm";
        }
    }
}

var p = new Person();
var i = new p.Idea();
i.consider();
```

在这种情况下，要引用名为“考虑”的方法，您将使用以下名称路径：Person＃Idea＃consideration
此链接可以与连接符号的任意组合一起使用：＃.〜

**特殊情况：模块，外部和事件**

```js
/** A module. Its name is module:foo/bar.
 * @module foo/bar
 */
/** The built in string object. Its name is external:String.
 * @external String
 */
/** An event. Its name is module:foo/bar.event:MyEvent.
 * @event module:foo/bar.event:MyEvent
 */
```

有一些特殊情况的名称路径：@module名称前缀为“module：”，@外部名称前缀为“external：”，@ event名称前缀为“event：”。

**名称中包含特殊字符的对象的名称路径。**

```js
/** @namespace */
var chat = {
    /**
     * Refer to this by {@link chat."#channel"}.
     * @namespace
     */
    "#channel": {
        /**
         * Refer to this by {@link chat."#channel".open}.
         * @type {boolean}
         * @defaultvalue
         */
        open: true,
        /**
         * Internal quotes have to be escaped by backslash. This is
         * {@link chat."#channel"."say-\"hello\""}.
         */
        'say-"hello"': function (msg) {}
    }
};

/**
 * Now we define an event in our {@link chat."#channel"} namespace.
 * @event chat."#channel"."op:announce-motd"
 */
```

上面是一个名称空间的示例，其成员名称中包含“异常”字符（哈希字符，短划线，偶数引号）。 要参考这些，你只需要引用名称：chat。“＃channel”，chat。“＃channel”。“op：announce-motd”，依此类推。 名称中的内部引号应使用反斜杠转义：chat。“＃channel”。“say  -  \”hello \“”。