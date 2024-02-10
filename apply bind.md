### 

## Implementing the apply Function Manually



apply 函数的实现步骤：

Steps to implement the **apply** function:



1. 判断调用对象是否为函数，即使我们是定义在函数的原型上的，但是可能出现使用 call 等方式调用的情况。

Determine if the calling object is a function. Even though it's defined on the function's prototype, there may be instances where it is invoked using methods like **call**.



1. 判断传入上下文对象是否存在，如果不存在，则设置为 window 。

Check if the incoming context object exists; if not, set it to **window**.



1. 将函数作为上下文对象的一个属性。

Assign the function as a property of the context object.



1. 判断参数值是否传入

Determine if the parameter values have been passed in.



1. 使用上下文对象来调用这个方法，并保存返回结果。

Invoke the method using the context object and save the returned result.



1. 删除刚才新增的属性

Remove the property that was just added.



1. 返回结果

Return the result



```plain
// apply 函数实现
Function.prototype.myApply = function(context) {
  // 判断调用对象是否为函数
  if (typeof this !== "function") {
    throw new TypeError("Error");
  }
  let result = null;
  // 判断 context 是否存在，如果未传入则为 window
  context = context || window;
  // 将函数设为对象的方法
  context.fn = this;
  // 调用方法
  if (arguments[1]) {
    result = context.fn(...arguments[1]);
  } else {
    result = context.fn();
  }
  // 将属性删除
  delete context.fn;
  return result;
};
```



### 13. 手写 bind 函数

**1Implementing the bind Function Manually**



bind 函数的实现步骤：

Steps to implement the bind function:



1. 判断调用对象是否为函数，即使我们是定义在函数的原型上的，但是可能出现使用 call 等方式调用的情况。

Determine if the calling object is a function. Even though it's defined on the function's prototype, there may be instances where it is invoked using methods like **call**.



1. 保存当前函数的引用，获取其余传入参数值。

Save a reference to the current function and retrieve the rest of the passed-in parameter values.



1. 创建一个函数返回

Return a new function.



1. 函数内部使用 apply 来绑定函数调用，需要判断函数作为构造函数的情况，这个时候需要传入当前函数的 this 给 apply 调用，其余情况都传入指定的上下文对象。

 Internally, the function uses **apply** to bind the function call. It's important to account for the function being used as a constructor. In such cases, the current function's '**this'** needs to be passed to **apply**, while in all other cases, the specified context object is passed.



```plain
// bind 函数实现
Function.prototype.myBind = function(context) {
  // 判断调用对象是否为函数
  if (typeof this !== "function") {
    throw new TypeError("Error");
  }
  // 获取参数
  var args = [...arguments].slice(1),
      fn = this;
  return function Fn() {
    // 根据调用方式，传入不同绑定值
    return fn.apply(
      this instanceof Fn ? this : context,
      args.concat(...arguments
    );
  };
}
```