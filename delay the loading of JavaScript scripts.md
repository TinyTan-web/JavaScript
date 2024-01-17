## What are the methods for delaying the loading of Javascript scripts?

Dalayed loading is to wait until the page is loaded before loading Javascript file. Js delayed loading helps to speed up page loading.

Generally, there are the following methods:

-  defer attribute: Add the defer attribute to the js script. **The attribute synchronizes the script loading and Document parsing,and then executes the script file after the document parsing is completed**. In this way, the page rendering is not blocked. Multiple scripts with preceding attribute are executed sequentially according to  specifications, but this may not be the case in some browsers. 
-  async attribute: Add the async attribute to js script**. This attribute will asynchronously load the script and will not block the parsing.process of the page. However, when the script is loaded, **the is script will executed immediately. If the document is not parsed not parsed, it will also be blocked. The execution sequence of scripts with multiple async attributes is unpredictable and is generally not executed in sequence according to the code sequence. 
-  dynamic DOM creation method: to dynamically create DOM tags, **you can listen to document loading events. After the document is loaded, you can dynamically create script tags to introduce js scripts. **
-  use setTimeout delay method: set a timer to delay loading js script files. 
-  let js finally load: Put the js script at the bottom of document so that the js script can be loaded and executed at the end as much as possible 

![](https://cdn.nlark.com/yuque/0/2024/png/26734946/1705395605342-f1602d78-e056-4dea-9f43-e740d4f949f8.png#averageHue=%23f9f8f5&clientId=u59feb369-456d-4&from=paste&id=u13e68da8&originHeight=262&originWidth=696&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=ubb6869b1-d5e6-49fb-b6c4-b2a0d51d424&title=)
Defer:  异步下载文件，之后立即加载但延迟执行，延迟到在所有的dom元素解析完成后，Loaded时间之前触发

Async: 异步下载文件，之后立即加载和异步执行文件，该过程是与后续dom元素的渲染过程是同步执行的
