### DOCTYPE(文档类型) 的作用是什么？

DOCTYPE 用来声明**文档类型定义**规范，目的是告诉浏览器应该以什么样 (html 或 xhtml) 的文档类型定义来解析文档。

HTML5 的写法是 `<!DOCTYPE html>`

### 对 HTML 语义化的理解？✨

- **含义**：用正确的标签做正确的事情：根据内容选择合适的标签
- **对机器**：利于 SEO；搜索引擎的爬虫也依赖于 HTML 标记来确定上下文和各个关键字的权重。
- **对人**：容易阅读和维护。

#### 常用的语义化标签

- `<hn>`：h1 ~ h6，分级标题， `<hn>` 与 `<title>` 协调有利于搜索引擎优化
- `<header>`：页眉通常包括网站标志、主导航、全站链接以及搜索框。
- `<nav>`：标记导航，仅对文档中重要的链接群使用。
- `<main>`：页面主要内容，一个页面只能使用一次。如果是 web 应用，则包围其主要功能。
- `<article>`：定义外部的内容，其中的内容独立于文档的其余部分。
- `<section>`：定义文档中的节（section、区段）。比如章节、页眉、页脚或文档中的其他部分。
- `<aside>`：定义其所处内容之外的内容。如侧栏、文章的一组链接、广告、友情链接、相关产品列表等。
- `<footer>`：页脚，只有当父级是 body 时，才是整个页面的页脚。
- `<figure>`：规定独立的流内容（图像、图表、照片、代码等等）（默认有 40px 左右 margin）。
- `<figcaption>`：定义 `figure` 元素的标题，应该被置于 `figure` 元素的第一个或最后一个子元素的位置。
- `<blockquoto>`：定义块引用，块引用拥有它们自己的空间。

### iframe 有哪些缺点？

- **阻塞主页面的 onload 事件**。window 的 onload 事件需要在所有 iframe 加载完毕后（包含里面的元素）才会触发。
- 不利于网页的 SEO。搜索引擎的检索程序无法解读这种页面。
- 影响页面的并行加载。iframe 和主页面共享连接池，而浏览器对相同域的连接有限制。
- 浏览器的后退按钮失效。
- 小型的移动设备无法完全显示框架。

### src 和 href 的区别

src 和 href 都是**用来引用外部的资源**，它们的区别如下：

- **src：** 用在 script 标签上，会暂停其他资源的下载和处理，直到将该资源加载、编译、执⾏完毕，所以⼀般 js 脚本会放在页面底部。
- **href：** 用在 a、link 等标签上。它指向一些网络资源，建立和当前元素或本文档的链接关系。当浏览器识别到它他指向的⽂件时，就会并⾏下载资源，不会停⽌对当前⽂档的处理。

### HTML5 有哪些更新？

- 语义化标签
- 媒体标签：audio、video
- 表单类型：email、number、search、color、time、date ...
- DOM 查询：querySelector、querySelectorAll
- Web 存储：localStorage、sessionStorage
- 图像：canvas，SVG
- 新的 API：拖放，history

### img 的 srcset 属性的作⽤？

srcset 属性用于设置不同设备像素比下，img 会自动加载不同的图片。

```html
<img src="image-128.png" srcset="image-256.png 2x" />
```

### 什么是 web worker？

Web Worker 的作用，就是为 JavaScript 创造多线程环境，允许主线程创建 Worker 线程，将一些任务分配给后者运行。在主线程运行的同时，Worker 线程在后台运行，两者互不干扰。等到 Worker 线程完成计算任务，再把结果返回给主线程。这样的好处是，一些计算密集型或高延迟的任务，被 Worker 线程负担了，主线程（通常负责 UI 交互）就会很流畅，不会被阻塞或拖慢。

Worker 线程一旦新建成功，就会始终运行，不会被主线程上的活动（比如用户点击按钮、提交表单）打断。这样有利于随时响应主线程的通信。但是，这也造成了 Worker 比较耗费资源，不应该过度使用，而且一旦使用完毕，就应该关闭。

**web worker 的作用**

- 处理耗时计算操作
- 轮询

**使用方式**

主线程

```js
// 创建 worker
var worker = new Worker('work.js');

// 发消息
worker.postMessage('Hello World');

// 监听子线程发回来的消息
worker.onmessage = function (event) {
  console.log('Received message ' + event.data);
  // 使用完及时关闭 worker
  closeWorker();
}

function closeWorker() {
  worker.terminate();
}
```

work.js

```js
// 接收和发送消息
self.addEventListener('message', function (e) {
  self.postMessage('You said: ' + e.data);
}, false);
```

### addEventListener 第三个参数有哪些值？

`options` 一个指定有关 `listener` 属性的可选参数对象。可用的选项如下：
- capture 监听器会在时间捕获阶段传播到 event.target 时触发。
- passive 监听器不会调用 preventDefault()。
- once 监听器只会执行一次，执行后移除。
- signal 该 `AbortSignal` 的 `abort()` 方法被调用时，监听器会被移除。
`useCapture` 捕获阶段调用监听器

### 什么是事件冒泡和事件捕获？✨

事件冒泡：事件会从一个具体的元素开始触发，然后不断向上传递最终传递给 document

事件捕获：事件会从不具体的元素传递给具体的元素，相当于是事件最开始是从最外部触发，然后不断向内传递，最终传递给具体的元素

#### 什么是事件委托？

如果有很多元素要写事件监听 (也就是事件处理程序)，那么可以给所有元素的共同父元素添加一个事件处理程序, 然后因为事件冒泡流的存在, 在子元素上触发的事件最终会传递给父元素，所以在父元素上也可以监听到在子元素上触发的事件，从而提高页面效率

**优点**

- 可以减少事件注册，节省内存占用
- 当新增子对象时，无需再对其进行事件绑定，对于动态内容部分尤为适合

#### 如何阻止冒泡和捕获？

`e.stopPropagation()` 取消所有后续事件捕获和事件冒泡

#### e.currentTarget 与 e.target 有何区别

`e.currentTarget` 事件绑定的元素
`e.target` 事件触发的元素

#### e.relatedTarget

relatedTarget 事件属性返回与事件的目标节点相关的节点。

- 对于 `mouseover` 事件来说，该属性是鼠标指针移到目标节点上时，离开的那个节点。
- 对于 `mouseout` 事件来说，该属性是离开目标时，鼠标指针进入的节点。

### 如何阻止事件默认行为？

- `e.preventDefault()`: 取消事件
- `e.cancelable`: 事件是否可取消

如果 `addEventListener` 第三个参数 `{ passive: true}`，`preventDefault` 将会会无效

### 如何判断在移动端?

```js
function isPc() {
  var userAgentInfo = navigator.userAgent;
  var Agents = new Array(
    "Android",
    "iPhone",
    "SymbianOS",
    "Windows Phone",
    "iPad",
    "iPod"
  );
  var flag = true;
  flag = !Agents.some((ele) => {
    return userAgentInfo.indexOf(ele) > 0;
  });
  return flag;
}
```

### IntersectionObserver 怎么使用的？怎么知道一个 DOM 节点出现在视口内？

IntersectionObserver 可以监测目标元素和视口或容器元素的交叉状态，可以在目标元素可见或者快要出现的时候执行回调函数。可以用于图片懒加载、无限加载等实现。

IntersectionObserver API 是==异步==的，不随着目标元素的滚动同步触发，只有线程空闲下来，才会执行观察器。这意味着，这个观察器的优先级非常低，只在其他任务执行完，浏览器有了空闲才会执行。

**使用方法**

```js
var io = new IntersectionObserver(callback, option);

// 开始观察，element为目标元素
io.observe(element);
// 需要观察多个元素就多次调用observe
io.observe(element2);

// 停止观察
io.unobserve(element);

// 关闭观察器
io.disconnect();
```

**Callback 参数**

目标元素的可见性变化时，就会调用观察器的回调函数 callback。 ==callback 一般会触发两次：开始可见、开始不可见。==

```js
var io = new IntersectionObserver((entries) => {
  // 遍历所有被观察元素
  for (let entry of entries) {
    // 判断是否在视口中
    if (entry.isIntersecting) {
      const target = entry.target; // 获取目标元素
    }
  }
});
```

**Option 对象**

IntersectionObserver 构造函数的第二个参数是一个配置对象。
- threshold 设定回调函数触发时机
- root 用来交叉检测的根元素，默认是浏览器窗体元素
- rootMargin 检测区域的偏移。支持 1-4 个值，和 margin 属性表示的方位含义一致。正数值是增大视区的检测区域，负值是减小。

```js
const option = {
  threshold: [0, 0.5, 1],  // 目标元素 0%、50%、100% 可见时，触发回调函数
  root: document.querySelector('.container'),
  rootMargin: "500px 0px" 
}
```

### 元素布局、滚动相关属性比较

- **clientWidth/clientHeight** 元素的内部宽度 content + padding，不包含滚动条
- **offsetWidth/offsetHeight** 元素的布局宽度 content + padding + border ，包含了滚动条。
- **scrollWidth/scrollHeight** content + padding + 溢出内容的尺寸
- **scrollX/scrollY** 获取一个元素的内容垂直/水平方向滚动的像素数（*已滚动的距离，未滚动时为 0*）
- **scrollTop/scrollLeft** 值与 scrollX/scrollY 一致，但是可读可写
- **offsetTop** 只读属性，它返回当前元素相对于其 `offsetParent` （*指向最近的包含该元素的 `定位元素` 或者 `table,td,th,body` 元素*）元素的顶部内边距的距离（*包括自身 margin， `offsetParent` 的边框和滚动条*），==不会随着滚动条的滚动而发生改变==。

![[Pasted image 20240301190309.png]]

#### getBoundingClientRect

返回元素的大小及其相对于视口的位置

- top: 元素上边距离页面上边的距离
- left: 元素右边距离页面左边的距离
- right: 元素右边距离页面左边的距离
- bottom: 元素下边距离页面上边的距离
- width: 元素宽度
- height: 元素高度

**出现滚动的情况**

当页面的元素在浏览器的左上角时，得到的 top 和 left 值为负值，right 和 bottom 值为正值。

![[Pasted image 20240223110500.png]]

### DOM 常见的操作有哪些？

- 创建节点
	- `createElement` 创建新元素，接受一个参数，即要创建元素的标签名
	- `createTextNode` 创建一个文本节点
	- `createDocumentFragment` 创建一个文档碎片，用来存储临时节点，然后把文档碎片的内容一次性添加到 `DOM` 中
- 查询节点
	- `querySelector` 传入任何有效的 `css` 选择器，即可选中单个 `DOM` 元素（首个）
	- `querySelectorAll` 返回一个包含节点子树内所有与之相匹配的 `Element` 节点列表
- 更新节点
	- `innerHTML` 不但可以修改一个 `DOM` 节点的文本内容，还可以直接通过 `HTML` 片段修改 `DOM` 节点内部的子树
- 添加节点
	- `appendChild` 把一个子节点添加到父节点的最后一个子节点
	- `insertBefore` 把子节点插入到指定的位置
	- `setAttribute` 在指定元素中添加一个属性节点，如果元素中已有该属性改变属性值
- 删除节点
	- `removeChild` 传入要删除的节点
- 其他
	- `parentNode`、`childNodes`、`firstChild`、`lastChild`、`nextSibling`、`previousSibling`

### 如何判断一个元素是否在可视区域中？

```js
function isInViewPortOfOne(el) {
  // viewPortHeight 兼容所有浏览器写法
  const viewPortHeight =
    window.innerHeight ||
    document.documentElement.clientHeight ||
    document.body.clientHeight;
  const offsetTop = el.offsetTop;
  const scrollTop = document.documentElement.scrollTop;
  const top = offsetTop - scrollTop;
  return top <= viewPortHeight;
}

```

```js
function isInViewPort(element) {
  const viewWidth = window.innerWidth || document.documentElement.clientWidth;
  const viewHeight =
    window.innerHeight || document.documentElement.clientHeight;
  const { top, right, bottom, left } = element.getBoundingClientRect();

  return top >= 0 && left >= 0 && right <= viewWidth && bottom <= viewHeight;
}
```

```js
const options = {
  // 表示重叠面积占被观察者的比例，从 0 - 1 取值，
  // 1 表示完全被包含
  threshold: 1.0,
  root: document.querySelector("#scrollArea"), // 必须是目标元素的父级元素
};
const callback = (entries, observer) => {};
const observer = new IntersectionObserver(callback, options);
const target = document.querySelector('.target');
observer.observe(target);
```

### 如何实现上拉加载，下拉刷新？

**上拉加载**

```js
let clientHeight = document.documentElement.clientHeight; //浏览器高度
let scrollHeight = document.body.scrollHeight;
let scrollTop = document.documentElement.scrollTop;

let distance = 50; //距离视窗还有50的时候，开始触发；

if (scrollTop + clientHeight >= scrollHeight - distance) {
  console.log("开始加载数据");
}
```

**下拉刷新**

- 监听原生 `touchstart` 事件，记录其初始位置的值，`e.touches[0].pageY`；
- 监听原生 `touchmove` 事件，记录并计算当前滑动的位置值与初始位置值的差值，大于 `0` 表示向下拉动，并借助 CSS3 的 `translateY` 属性使元素跟随手势向下滑动对应的差值，同时也应设置一个允许滑动的最大值；
- 监听原生 `touchend` 事件，若此时元素滑动达到最大值，则触发 `callback`，同时将 `translateY` 重设为 `0`，元素回到初始位置
