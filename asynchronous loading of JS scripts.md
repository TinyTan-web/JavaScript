#### JS脚本异步加载如何实现 有什么区别？

#### What are the differences in asynchronous loading of JS scripts?



在 Web 应用中，JavaScript 脚本的异步加载可以通过以下方式来实现：



In Web applications, the asynchronous loading of JavaScript scripts can be achieved in the following ways:



1. 动态创建 <script> 标签，并设置其 src 属性为需要加载的脚本 URL。这种方式可以通过设置 onload 或 onreadystatechange 事件来检测脚本是否加载完成。

Dynamically create a **<script>** tag and set its **src** attribute to the URL of the script to be loaded. You can use the **onload** or **onreadystatechange** event to check if the script has finished loading.



```javascript
const script = document.createElement('script');
script.src = 'path/to/script.js';
script.onload = function() {
 // 脚本加载完成后执行的回调函数
};
document.body.appendChild(script);
```



1. 使用 XMLHttpRequest 对象或 Fetch API 发送异步请求，并在请求成功后将响应文本解析为 JavaScript 代码，然后使用 eval() 函数或 Function() 构造函数来执行脚本。

Use the **XMLHttpRequest** object or the **Fetch** API to send an asynchronous request. After a successful request, parse the response text into JavaScript code, and then use the **eval()** function or **Function()** constructor to execute the script.



```javascript
const xhr = new XMLHttpRequest();
xhr.open('GET', 'path/to/script.js');
xhr.onload = function() {
 const script = document.createElement('script');
 script.textContent = xhr.responseText;
 document.head.appendChild(script);
};
xhr.send();
```



使用这两种方式可以实现 JavaScript 脚本的异步加载，相比于同步加载脚本，异步加载具有以下区别：



These two methods can be used to implement the asynchronous loading of JavaScript scripts. Compared to synchronous loading, asynchronous loading has the following differences:



1. 异步加载可以提高页面的加载速度和响应性能，避免因 JavaScript 阻塞而造成页面卡顿的情况。

Asynchronous loading can improve the loading speed and response performance of the page, and avoid the situation that the page is stuck due to JavaScript blocking.



1. 异步加载可以避免因加载脚本而造成的阻塞情况，使页面的其他资源可以更快地加载和呈现。

Asynchronous loading avoids the blocking caused by loading scripts and allows other resources of the page to load and render faster.



1. 异步加载可以更灵活地控制脚本的加载顺序和执行时间，可以根据页面需要动态加载和卸载脚本，提高页面的可维护性和可扩展性。

Asynchronous loading allows you to flexibly control the loading sequence and the execution time of scripts, and dynamically load and unload scripts based on page requirements, thus improving page maintainability and expansibility.