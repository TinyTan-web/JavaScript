#### RequestAnimationFrame/requestIdleCallback，分别有什么用？
#### What are the uses of 'requestAnimationFrame' and 'requestIdleCallback', respectively?

RequestAnimationFrame 和 requestIdleCallback 都是用于在浏览器中执行动画或其他高性能任务的 API。
'RequestAnimationFrame' and 'requestIdleCallback' are both APIs used for performing animations or other high-performance tasks in the browser.

**RequestAnimationFrame** 是浏览器提供的一种动画帧请求机制，它会在浏览器下一次绘制之前执行指定的回调函数。这样做的好处是可以在浏览器下一次绘制时，让浏览器自动完成一些复杂的计算和渲染工作，从而避免了浏览器在短时间内重复执行相同的任务。使用 requestAnimationFrame 可以实现更加流畅的动画效果，同时也可以减少页面的闪烁和卡顿。
**'RequestAnimationFrame'** is a mechanism provided by browsers to request an animation frame. It executes a specified callback function right before the browser's next redraw. The advantage of this approach is that it allows the browser to automatically perform complex calculations and rendering tasks during the next draw, thus preventing the browser from repeating the same tasks within a short period. Using requestAnimationFrame can lead to smoother animations and reduce flickering and stuttering on web pages.

```javascript
function animate() {
 // 在这里编写动画逻辑requestAnimationFrame(animate);
}
requestAnimationFrame(animate);
```

**RequestIdleCallback** 是一个相对较新的 API，它的作用是在浏览器空闲时执行指定的回调函数。这个 API 的目的是让开发者能够在浏览器空闲时，进行一些比较耗时的任务，例如计算和渲染。这样做的好处是可以提高网页的性能和响应速度，同时也可以避免阻塞浏览器的主线程，导致用户体验不佳。
**RequestIdleCallback** is a relatively new API that performs a specified callback function when the browser is idle. The purpose of this API is to enable developers to perform time-consuming tasks such as computation and rendering when the browser is idle. The advantage of this is that it can improve the performance and responsiveness of the web page, while also avoiding blocking the main thread of the browser, resulting in a poor user experience.

```javascript
function doWork(deadline) {
 while (deadline.timeRemaining() > 0) {
 // 在这里编写任务逻辑
 }
 if (还有任务需要执行) {
 requestIdleCallback(doWork);
 }
}
requestIdleCallback(doWork);
```

需要注意的是，requestIdleCallback 的回调函数接受一个 IdleDeadline 参数，它包含了当前空闲时间的相关信息。开发者可以通过这个参数，根据浏览器的空闲时间进行任务调度和优化。
Note that the callback function of requestIdleCallback accepts an IdleDeadline parameter, which contains information about the current idle time. Developers can use this parameter to schedule and optimize tasks according to the idle time of the browser.

综上所述，requestAnimationFrame 适用于需要在下一次绘制之前执行的动画任务，而 requestIdleCallback 则适用于需要在浏览器空闲时执行的耗时任务。
In summary, requestAnimationFrame is suitable for animation tasks that need to be executed before the next drawing, while requestIdleCallback is suitable for time-consuming tasks that need to be executed when the browser is idle.
