
大段文字看起来眼睛好累，所以我随便按每10个进行一次分割。  
如果你有更好的展现形式，欢迎投稿，非常感谢！

# 记录一些坑眼

* `let` 和 `const` 不会像 `var` 一样会在 window 下声明，比如 `let a` 是取不到 `window.a` 的
* `wx.onMenuShareAppMessage` 的 `type` 不能是空字符串，要么不传，要么 `type: "link"`
* `wx.config` 需要传入的链接，苹果机下如果使用过 history api 将签名失败。
* Safari 和 IE9- 浏览器中，`option` 设 `display:none` 无效，可包一层隐藏的 `span` 或重新拼 dom
* CSS 的 `centent` 的文本和图片，是不可选择的
* 苹果机键盘弹起后元素上移，键盘收回后元素不归位，用 `$(document).scrollTop(0, 0);` 解决（部分机型依旧不行）
* 3.0 版本前的 `$.param` 会把空格转为 `+` 号，可能后来发现链接中的 + 与空格的 + 冲突所以砍掉了
* IOS 下的 webgl 不清晰，可显示 2d 的 canvas 绘制隐藏的 webgl 的 getImageDate 能清晰
* 小程序不会正确处理图片链接中 `\`，造成图片请求但不显示，只能是 `/` 式的路径，比如 [图片](http://images.duocaixing.net\undefined/2019-06-04/201906041118494757_wKgED1ws7UCAKPhVAAVr2lUbIUI02.jpeg)

-----

* 部分安卓机 `background-image` 与 `border-radius` 合用会不显示图片，需加上 `background-color` 才行
* `input[type="number"]` 不支持使用 selection 相关的光标操作
* 用 `data:image/svg+xml,` 拼出来的 SVG 背景图，`background-size` 不支持拉伸了。
* ES6 用变量作对象属性名时有点小问题，如 `var a = 'x'; var obj = { [a]: 1 }; obj[a]; // 1` 但 `obj.a` 不会
* 苹果机 Safari 下设 `user-scalable=no` 的 `<meta>` 无效
* `btoa` 转 base64 不支持传入中文等 Unicode 字符，可搭配 `encodeURIComponent` 使用
* 极少情况下 `textarea` 书写时双标签间有回车会不显示 `placeholder`，可能与编辑器有关
* IOS 的 `iframe` 不支持传高度，最好有个父级包着并设 `-webkit-overflow-scrolling` 滚动
* `[0, , 2, 3].indexOf()` 得 `-1`，`[0, undefined, 2, 3].indexOf()` 得 `1`
* `RegExp` 第二个参数，若传入 `'s'` 部分苹果机报错，看 [文档](http://www.w3school.com.cn/jsref/jsref_obj_regexp.asp) 确实说只能传 `'igm'`

-----

* 给 `option` 设 `label` 而不写在 `innerText`，部分苹果机会不显示文本但能滑动选择
* 在 vue 的根节点进行 `innerHTML += 'x'` 会造成 vue-router 失效，`appendChild` 是 OK 的
* `input[type="checkbox"]` 加字符串 `checked="false"` 或 `setAttribute('checked', '')` 也会勾选
* html 中 `data-userId` 会显示为全小写 `data-userid`，但 `attr('data-USERID')` 不区分大小写都能获取到
* UTF-16 字符在处理字符串时需注意，比如 `'𠮷'.slice(-1)` 会得到未知字符，恐怕只能用 `for-of` 来做了
* 空数组进行 `every` 判断始终为 `true`，需根据场景做好排除
* 在 SCSS 中 `@extend .x` 不仅会继承 `.x`，与其相关无论写在何处的 `h1.x` 也会被继承
* `:last-child` 是按 dom 位置来的，并不受 `order` 排序的影响
* 给伪元素的 `content` 直接加 `text-indent:-999em` 无效，需改为其他 `display` 才行，即 `inline` 不可以
* `JSON.stringify(Infinity) === "null"`（NaN 也是），`JSON.stringify({a: undefined}) === "{}"`（但 null 不会）

-----

* 父级 `overflow:auto; position:relative;`，子级绝对定位并超出，结果会显示滚动条，并非完全脱离文档流
* 父级无高度时，子级 `position: relative` 的百分比定位 `top: 50%` 会无效
* ueditor 插件初始化时会触发 `hashchange` 事件，希望你在这里面没有写什么操作
* `display: flex` 和子级 `margin: auto;` 合用时，效果很奇妙，比如居中/两个子级的自动空隙等
* `<script src="xx.js" />` 不能使用单标签格式，不然会把后面的都当做文本
* 属性选择器 `[id=value]` 中当 value 中有小数点时会报错，保险起见还是带双引号更好 `[id="value"]`
* 小程序覆盖在 input 上的元素，键盘弹起后，点击就无法触发了
* ElementUI 的 `el-date-picker[type="daterange"]` 在 **火狐** 下不支持 `yyyy.MM.dd` 格式数据的传入，`-/` 可以
* 有 `mask` 的元素 `box-shadow` 非 `inset` 形态无效，`filter:drop-shadow()` 也是如此（可放到父级去）
* `min-width` 的默认是 `auto`，而 `max-width` 的默认是 `none`

-----

* https 下无法点击打开下载 http 的资源
* `input[type="file"]` 的触发会触发 `window.onblur` 事件，可用 `document.activeElement` 来进行排除
* 点击在 `label[for]` 的父级上，会触发两次 `click`，很迷
* IOS will only allow focus to be triggered on other elements
* `new RegExp` 需对特殊字符进行转义，比如 `new RegExp('\\d').test(1)` 才有效，还是 `/\d/.test(1)` 好呀。
* 设置 `border-image` 后，`border-radius` 失效。
* 给**定位**的 `body` 设 `background-size`，如 `100% 100%` 或 `contain` 会没有相对高度，但 `cover` 有效。
* 正则的括号会在 `match` 时再单独提取出来一份，比如 `"ab".match(/(b)/)` 会得到 `["b","b"]`
* 苹果机上当 `div` 的 `click` 委托在 `document` 或 `body` 上会无法点击，可换为 `a` 或添加 `cursor: pointer` 等。[见文](https://www.cnblogs.com/Steping/p/5737547.html)
* 苹果机移动端 `contenteditable` 无效，需加上 `-webkit-user-select: text`

-----

* 苹果机在纵向 `flex: 1` 时非常尴尬，有时 `flex-basis: 100%` 可行，有时必须定高。
* 小程序的 `cover-view` 不能使用 `:before` 和 `gradient` 样式
* `disabled` 会禁掉 `mouse` 事件，却没有禁 `touch` 事件
* `$.fn.serializeArray` 方法会把回车 `\n` 改为 `\r\n`，增加了字符串长度
* `Math.round` 四舍五入方法可能有误，见 [推文](https://mp.weixin.qq.com/s/MlnVE0_bWHVGb7MAPBBG1Q)
* 看 [源码](https://blog.csdn.net/lixuepeng_001/article/details/53742589) 发现，`Array.sort` 是要返回正负，而非布尔值
* 浏览器开始禁止音频视频的自动播放，暂时无解
* `<a><a>x</a></a>` 会被解析为 `<a></a><a>x</a>`，但 `append` 的话可以嵌套， p>div | p>p 也是如此。
* jquery 在 table 中 html 个 table 会无效，append 个 table 有时报错，[源码](https://blog.csdn.net/chaiyining007/article/details/8213699)。
* `location.origin` 在 IE11 以下不兼容

-----

* 苹果机在 QQ 浏览器中修改 `document.title` 无效，需新建删除一个 `iframe` 来骚操作
* 粘贴功能 `execCommand('paste')` 被各家浏览器禁用掉了
* 小程序的 `cover-view` 手机上不触发 touch 事件
* 小程序的 `cover-image` 不能单独定位，如果父级 `cover-view` 定位了那倒可以了
* 写 HTML 时两个节点间有换行或空格，需要两次 nextSibling 才能找到上一个节点，因为中间多了一个空白的 text 节点
* 小程序的 toast 和 loading 等其实解决不了点击太快的问题，还得靠变量来阻止才行
* `inline` 行级元素设置 `transform` 无效
* 苹果机没有原生双击事件 `dblclick`
* `:not(.x):last-of-type` 并不代表去掉 `.x` 后的最后一个，它们是并列关系而非先后关系
* `table-layout: fixed` 表示不再自动分配宽度，傻逼的我还以为是固定 `thead` 达到类似 `position:fixed` 的效果

-----

* `writing-mode:vertical-rl` 在 Safari 上异常（无解，等于苹果浏览器不能玩耍了）
* `translate3d` 下的 `fixed` 失效，与 `absolute` 等效，反正能不用 fixed 绝不用
* `touchend` 或 `tap` 会出现事件穿透，其实浏览器已经做了优化，`click` 是可以满足我们的要求的
* 元素未显示时的 swiper 的初始化是有误的，`mySwiper.update()` 有效
* 苹果机 `new Date(d)` 时 `d` 不能采用 "xxxx-xx-xx" 格式
* `display:flex` 被 `display: none` 覆盖后再使用 jquery 的 `fadeIn()` 将显示 `display: block`
* 苹果机有滚动反弹，与 `position: fixed` 一起玩耍时很可怕，特别是微信浏览器
* `clip:rect(1,2,3,4)` 必须要和 `absolute` 合用，且 2&3 必须有(作为宽高)，更推荐使用 `clip-path`
* `scaleX` 等的默认值是 0 不是 1，所以小心 css 动画时会有一闪的状态，虽然通常我们会用 `scale(x, y)` 更多

-----

* `text-transform` 有时会在跳页时回归最初（什么特定情况还未总结出）
* 极少部分苹果机图片加载会阻塞后续程序
* 最好不要 `for` 里面套 ajax，不然你的服务器会超级崩溃的，当然浏览器也会报出请求过量的错误
* overflow:hidden 在子级 transform 时无效，需要再套一层父级，有时子级的父级也无效，需要祖父级添加 overflow:hidden
* setTimeout("x()",500) 的 x 必须为全局函数，否则报错，所以还是用 setTimeout(x,500) 吧，同理 `<div onclick="aaa()">` 的 aaa 也必须是全局函数
* 有些手机 `<audio>` 不支持 m4a 格式的音频
* 禁用了 `window` 的 `touchstart` 后 `input` 也不能点了
* 苹果机的 `blur` 自主触发（即 `$dom.blur()`）有问题，有待实验
* `iframe` 套的网页会缓存，修改后刷新可能无效，且会保存 history，最好用一次就新建删除一次
* `<datalist>` 并不好用，有时会不出现内容，且样式不可控，不推荐使用

-----

* 苹果手机自动播放音频得放在 `wx.ready` 里面
* 摇一摇事件有时清除不掉，可能是触发太多烧机器，推荐再加个变量控制开关
* `onstorage` 事件监听必须两个页面都打开着才能互传信息
* `submit` 和 `
