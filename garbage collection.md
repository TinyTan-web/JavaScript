### 1. 浏览器的垃圾回收机制

**Browser garbage collection mechanism** 

#### （1）垃圾回收的概念

**the concept of garbage collection** 

**垃圾回收**：JavaScript代码运行时，需要分配内存空间来储存变量和值。当变量不在参与运行时，就需要系统收回被占用的内存空间，这就是垃圾回收。

**garbage collection** : JavaScript code is running, you need to allocate memory space to store variables and values. When a variable is not running, the system needs to retrieve the occupied memory space, which is garbage collection.



**回收机制**：

**Recycling Mechanism** : 

- Javascript 具有自动垃圾回收机制，会定期对那些不再使用的变量、对象所占用的内存进行释放，原理就是找到不再使用的变量，然后释放掉其占用的内存。
  Javascript has an automatic garbage collection mechanism, which regularly releases the memory occupied by variables and objects that are no longer in use. The principle is to find variables that are no longer in use and then release the memory occupied by them. 
- JavaScript中存在两种变量：局部变量和全局变量。全局变量的生命周期会持续要页面卸载；而局部变量声明在函数中，它的生命周期从函数执行开始，直到函数执行结束，在这个过程中，局部变量会在堆或栈中存储它们的值，当函数执行结束后，这些局部变量不再被使用，它们所占有的空间就会被释放。
  there are two variables in the JavaScript: local variables and global variables. The lifecycle of global variables continues to be unloaded on the page. Local variables are declared in a function. Their lifecycle starts from function execution until function execution ends. In this process, local variables store their values in the heap or stack. When function execution ends, these local variables are no longer used and the space they occupy will be released. 
- 不过，当局部变量被外部函数使用时，其中一种情况就是闭包，在函数执行结束后，函数外部的变量依然指向函数内部的局部变量，此时局部变量依然在被使用，所以不会回收。
  however, when a local variable is used by an external function, one of the cases is closure. After the function is executed, the external variable of the function still points to the local variable inside the function. At this time, the local variable is still in use, so it will not be recycled.



#### （2）垃圾回收的方式

**garbage collection methods**



浏览器通常使用的垃圾回收方法有两种：标记清除，引用计数。

Browsers usually use two garbage collection methods: Tag cleaning and reference counting. 

**1）标记清除**

**Mark Clearance** 

- 标记清除是浏览器常见的垃圾回收方式，当变量进入执行环境时，就标记这个变量“进入环境”，被标记为“进入环境”的变量是不能被回收的，因为他们正在被使用。当变量离开环境时，就会被标记为“离开环境”，被标记为“离开环境”的变量会被内存释放。
  Mark clearing is a common garbage collection method in browsers. When a variable enters the execution environment, it is marked as "enter environment". Variables marked as "enter environment" cannot be collected because they are currently in use. When a variable leaves the environment, it is marked as "leaving the environment", and variables marked as "leaving the environment" are released from memory.
- 垃圾收集器在运行的时候会给存储在内存中的所有变量都加上标记。然后，它会去掉环境中的变量以及被环境中的变量引用的标记。而在此之后再被加上标记的变量将被视为准备删除的变量，原因是环境中的变量已经无法访问到这些变量了。最后。垃圾收集器完成内存清除工作，销毁那些带标记的值，并回收他们所占用的内存空间。
  The garbage collector will mark all variables stored in memory during runtime. Then, it will remove variables in the environment and tags referenced by variables in the environment. And variables marked afterwards will be considered as variables to be deleted, as variables in the environment are no longer accessible. Finally. The garbage collector completes the memory clearing task, destroys marked values, and reclaims the memory space they occupy.



**2）****reference count** 



- 另外一种垃圾回收机制就是引用计数，这个用的相对较少。引用计数就是跟踪记录每个值被引用的次数。当声明了一个变量并将一个引用类型赋值给该变量时，则这个值的引用次数就是1。相反，如果包含对这个值引用的变量又取得了另外一个值，则这个值的引用次数就减1。当这个引用次数变为0时，说明这个变量已经没有价值，因此，在在机回收期下次再运行时，这个变量所占有的内存空间就会被释放出来。
  another garbage collection mechanism is reference counting, which is relatively less used. The reference count is the number of times each value of the trace record is referenced. When a variable is declared and a reference type is assigned to the variable, the number of references to this value is 1. On the contrary, if the variable containing the reference to this value obtains another value, the number of references to this value is reduced by 1. When the number of references changes to 0, this variable is no longer valuable. Therefore, the memory space occupied by this variable will be released when it is run again during the machine payback period.

- 这种方法会引起**循环引用**的问题：例如：`obj1`和`obj2`通过属性进行相互引用，两个对象的引用次数都是2。当使用循环计数时，由于函数执行完后，两个对象都离开作用域，函数执行结束，`obj1`和`obj2`还将会继续存在，因此它们的引用次数永远不会是0，就会引起循环引用。
  this method will cause **loop reference** for example: obj1 and obj2 if you use attributes to reference each other, the number of references to both objects is 2. When loop counting is used, the function execution ends because both objects leave the scope after the function is executed, obj1 and obj2 they will continue to exist, so their reference times will never be 0, which will cause circular reference.

  

```plain
function fun() {
    let obj1 = {};
    let obj2 = {};
    obj1.a = obj2; // obj1 引用 obj2
    obj2.a = obj1; // obj2 引用 obj1
}
```



这种情况下，就要手动释放变量占用的内存：

In this case, the memory occupied by the variable must be manually released: 

```plain
obj1.a =  null
 obj2.a =  null
```



#### （3）减少垃圾回收

**Reduce waste recycling** 

虽然浏览器可以进行垃圾自动回收，但是当代码比较复杂时，垃圾回收所带来的代价比较大，所以应该尽量减少垃圾回收。

although browsers can automatically recycle garbage, garbage collection costs a lot when the code is complex, so garbage collection should be minimized.

- **对数组进行优化：**在清空一个数组时，最简单的方法就是给其赋值为[ ]，但是与此同时会创建一个新的空对象，可以将数组的长度设置为0，以此来达到清空数组的目的。
  **optimize the array:** the easiest way to clear an array is to assign a value of [ ], but at the same time, a new empty object is created. You can set the length of the array to 0 to clear the array. 
- **对**`**object**`**进行优化：**对象尽量复用，对于不再使用的对象，就将其设置为null，尽快被回收。

**optimize the** `***\*object\****` Reuse objects as much as possible, set them to null for objects that are 	no longer in use, and recycle them as soon as possible

- **对函数进行优化：**在循环中的函数表达式，如果可以复用，尽量放在函数的外面。
  **optimize functions:** if you can reuse the function expressions in the loop, try to put them outside the function. 