## Why is the result of 'typeof null' an 'object'?



Typeof null 的结果为 "object"，这是 JavaScript 语言的一个历史遗留问题。

The result of 'typeof null' being "object" is a legacy issue of the JavaScript language.



在 JavaScript 最初的版本中，使用 32 位的值表示一个变量，其中前 3 位用于表示值的类型。000 表示对象，010 表示浮点数，100 表示字符串，110 表示布尔值，和其他的值都被认为是指针。

In the original version of JavaScript, a 32-bit value was used to represent a variable, with the first 3 bits representing the type of the value. 000 represents an object, 010 represents a floating point number, 100 represents a string, 110 represents a Boolean value, and other values are all considered pointers.



在这种表示法下，null 被解释为一个全零的指针，也就是说它被认为是一个空对象引用，因此 typeof null 的结果就是 "object"。

In this representation, null was interpreted as an all-zero pointer, that is, it is considered to be an empty object reference, so the result of typeof null is "object".

#### 拓展

#### expand

虽然这个设计是一个历史遗留问题，但是由于历史原因，已经成为 JavaScript 语言的一部分，无法修复。因此在判断变量是否为 null 时，建议使用严格相等运算符（===）进行判断。

Although this design is a legacy issue, it has become part of the JavaScript language for historical reasons and cannot be fixed. Therefore, it is recommended to use the strict equality operator (===) when determining whether a variable is null.

## let全局声明变量，window能取到吗？

### Can variables globally declared with 'let' be accessed via the window object?



使用 let 声明的变量不会挂在全局对象 window 上，因此无法通过 window.variableName 的方式访问。这与使用 var 声明的变量不同，var 声明的变量会被挂载在全局对象上，因此可以通过 window.variableName 的方式访问。

Variables declared with 'let' are not attached to the global 'window' object, and therefore cannot be accessed via 'window.variablename'. This is different from variables declared with 'var', which are mounted on the global object and can be accessed via 'window.variableName'.



举个例子，假设有以下代码：

For example, consider the following code:



```javascript
let foo = 'bar';
var baz = 'qux';
console.log(window.foo); // undefinedconsole.log(window.baz); // 'qux'
```



在这段代码中，使用 let 声明的变量 foo 无法通过 window.foo 访问，而使用 var 声明的变量 baz 可以通过 window.baz 访问。

In this code, the variable 'foo' declared with 'let' is not accessible through 'window.foo', while the variable 'baz' declared with 'var' is accessible through 'window.baz'.