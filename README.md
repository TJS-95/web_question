自己对常见的前端题的总结，参考了很多大牛的想法，如有漏写链接的请提醒，原文有错请指出，谢谢！！！

# 基础部分

1. 数组去重

```js
// 利用对象属性不能重复的原理
Array.prototype.distinct = function () {
  var arr = this,
  result = [],
  obj = {}
  for (var i in arr) {
    if(!obj[arr[i]]) {
      obj[arr[i]] = 1
      result.push(arr[i])
    }
  }
  return result
}

var arr = [1, 2, 3, 3, 4, 4, 5]
arr.distinct()
```

2. 数组逆序
```js

Array.prototype.myReverse = function () {
  var arr = this
  var len = arr.length,
  i = 0,
  temp
  while(len-(i + 1) >= i) {
    temp = arr[i]
    arr[i] = arr[len-(i+1)]
    arr[len-(i + 1)] = temp
    i++
  }
  return arr
}

var arr = [1, 2, 3, 4, 5]

arr.myReverse()
```

3. 排序

- 冒泡排序

  基本思想：两个数比较大小，较大的数下沉，较小的数冒起来。

  过程：

  比较相邻的两个数据，如果第二个数小，就交换位置。

  从后向前两两比较，一直到比较最前两个数据。最终最小数被交换到起始的位置，这样第一个最小数的位置就排好了。

  继续重复上述过程，依次将第2.3...n-1个最小数排好位置。

```js
var arr = [5, 4, 6, 1, 3, 2, 8, 7, 6]

// 冒泡排序
Array.prototype.bubble = function () {
  var arr = this
  temp = 0
  for (var i = 0; i < arr.length - 1; i++) {
    for (var j = arr.length; j > i; j--) {
      if ( arr[j - 1] > arr[j]) {
        temp = arr[j - 1]
        arr[j -1 ] = arr[j]
        arr[j] = temp
      }
    }
  }
  return arr
}

arr.buble()
```

|        |空间复杂度|时间复杂度 |
|--------|---------|----------|
|冒泡排序 |O(1)     |O(N2)     |

​	[冒泡排序](https://www.cnblogs.com/jingmoxukong/p/4302718.html)


- 选择排序

  基本思想：

  在长度为N的无序数组中，第一次遍历n-1个数，找到最小的数值与第一个元素交换；

  第二次遍历n-2个数，找到最小的数值与第二个元素交换；

  。。。

  第n-1次遍历，找到最小的数值与第n-1个元素交换，排序完成。

```js
Array.prototype.select_sort = function () {
  var arr = this
  len = arr.length
  index = 0
  temp = 0
  for (var i = 0; i < len - 1; i++) {
    index = i
    //  找出最小值得元素下标
    for (var j = i + 1; j < len - 1; j++) {
      if (arr[j] < arr[index]) {
        index = j
      }
    }
    if (index !== i) {
      temp = arr[i]
      arr[i] = arr[index]
      arr[index] = temp
    }
  }
  return arr
}
```

|    | 空间复杂度 | 时间复杂度 |
|----|-----------|-----------|
| 选择排序|       | O(n2)    |

- 插入排序

基本思想：

在要排序的一组数中，假定前n-1个数已经排好序，现在将第n个数插到前面的有序数列中，使得这n个数也是排好顺序的。如此反复循环，直到全部排好顺序。

```js
Array.prototype.insert_sort = function () {
  var arr = this
  temp = 0
  for (var i = 0; i < arr.length; i++) {
    for (var j = i + 1; j > 0; j--) {
      if (arr[j] < arr[j - 1]) {
        temp = arr[j - 1]
        arr[j - 1] = arr[j]
        arr[j] = temp
      }else{ //不需要交换
        break;
      }
    }
  }
  return arr
}
```

|    | 空间复杂度 | 时间复杂度 |
|----|-----------|-----------|
| 插入排序|       | O(n2)    |

4. http和https有什么区别， 端口号多少 

   **基本概念**

   **HTTP**（HyperText Transfer Protocol：超文本传输协议）是一种用于分布式、协作式和超媒体信息系统的应用层协议。 简单来说就是一种发布和接收 HTML 页面的方法，被用于在 Web 浏览器和网站服务器之间传递信息。

   HTTP 默认工作在 TCP 协议 80 端口，用户访问网站 http:// 打头的都是标准 HTTP 服务。

   HTTP 协议以明文方式发送内容，不提供任何方式的数据加密，如果攻击者截取了Web浏览器和网站服务器之间的传输报文，就可以直接读懂其中的信息，因此，HTTP协议不适合传输一些敏感信息，比如：信用卡号、密码等支付信息。

   **HTTPS**（Hypertext Transfer Protocol Secure：超文本传输安全协议）是一种透过计算机网络进行安全通信的传输协议。HTTPS 经由 HTTP 进行通信，但利用 SSL/TLS 来加密数据包。HTTPS 开发的主要目的，是提供对网站服务器的身份认证，保护交换数据的隐私与完整性。

   HTTPS 默认工作在 TCP 协议443端口，它的工作流程一般如以下方式：

   - 1、TCP 三次同步握手

   - 2、客户端验证服务器数字证书

   - 3、DH 算法协商对称加密算法的密钥、hash 算法的密钥

   - 4、SSL 安全加密隧道协商完成

   - 5、网页以加密的方式传输，用协商的对称加密算法和密钥加密，保证数据机密性；用协商的hash算法进行数据完整性保护，保证数据不被篡改。

     ​

   **HTTP 与 HTTPS 区别**

   - HTTP 明文传输，数据都是未加密的，安全性较差，HTTPS（SSL+HTTP） 数据传输过程是加密的，安全性较好。
   - 使用 HTTPS 协议需要到 CA（Certificate Authority，数字证书认证机构） 申请证书，一般免费证书较少，因而需要一定费用。证书颁发机构如：Symantec、Comodo、GoDaddy 和 GlobalSign 等。
   - HTTP 页面响应速度比 HTTPS 快，主要是因为 HTTP 使用 TCP 三次握手建立连接，客户端和服务器需要交换 3 个包，而 HTTPS除了 TCP 的三个包，还要加上 ssl 握手需要的 9 个包，所以一共是 12 个包。
   - http 和 https 使用的是完全不同的连接方式，用的端口也不一样，前者是 80，后者是 443。
   - HTTPS 其实就是建构在 SSL/TLS 之上的 HTTP 协议，所以，要比较 HTTPS 比 HTTP 要更耗费服务器资源。

   ​

5. http状态码

   | 状态码 | 状态码英文名称                  | 中文描述                                                     |
   | ------ | ------------------------------- | ------------------------------------------------------------ |
   | 100    | Continue                        | 继续。客户端应继续其请求                                     |
   | 101    | Switching Protocols             | 切换协议。服务器根据客户端的请求切换协议。只能切换到更高级的协议，例如，切换到HTTP的新版本协议 |
   |        |                                 |                                                              |
   | 200    | OK                              | 请求成功。一般用于GET与POST请求                              |
   | 201    | Created                         | 已创建。成功请求并创建了新的资源                             |
   | 202    | Accepted                        | 已接受。已经接受请求，但未处理完成                           |
   | 203    | Non-Authoritative Information   | 非授权信息。请求成功。但返回的meta信息不在原始的服务器，而是一个副本 |
   | 204    | No Content                      | 无内容。服务器成功处理，但未返回内容。在未更新网页的情况下，可确保浏览器继续显示当前文档 |
   | 205    | Reset Content                   | 重置内容。服务器处理成功，用户终端（例如：浏览器）应重置文档视图。可通过此返回码清除浏览器的表单域 |
   | 206    | Partial Content                 | 部分内容。服务器成功处理了部分GET请求                        |
   |        |                                 |                                                              |
   | 300    | Multiple Choices                | 多种选择。请求的资源可包括多个位置，相应可返回一个资源特征与地址的列表用于用户终端（例如：浏览器）选择 |
   | 301    | Moved Permanently               | 永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替 |
   | 302    | Found                           | 临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI |
   | 303    | See Other                       | 查看其它地址。与301类似。使用GET和POST请求查看               |
   | 304    | Not Modified                    | 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源 |
   | 305    | Use Proxy                       | 使用代理。所请求的资源必须通过代理访问                       |
   | 306    | Unused                          | 已经被废弃的HTTP状态码                                       |
   | 307    | Temporary Redirect              | 临时重定向。与302类似。使用GET请求重定向                     |
   |        |                                 |                                                              |
   | 400    | Bad Request                     | 客户端请求的语法错误，服务器无法理解                         |
   | 401    | Unauthorized                    | 请求要求用户的身份认证                                       |
   | 402    | Payment Required                | 保留，将来使用                                               |
   | 403    | Forbidden                       | 服务器理解请求客户端的请求，但是拒绝执行此请求               |
   | 404    | Not Found                       | 服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置"您所请求的资源无法找到"的个性页面 |
   | 405    | Method Not Allowed              | 客户端请求中的方法被禁止                                     |
   | 406    | Not Acceptable                  | 服务器无法根据客户端请求的内容特性完成请求                   |
   | 407    | Proxy Authentication Required   | 请求要求代理的身份认证，与401类似，但请求者应当使用代理进行授权 |
   | 408    | Request Time-out                | 服务器等待客户端发送的请求时间过长，超时                     |
   | 409    | Conflict                        | 服务器完成客户端的 PUT 请求时可能返回此代码，服务器处理请求时发生了冲突 |
   | 410    | Gone                            | 客户端请求的资源已经不存在。410不同于404，如果资源以前有现在被永久删除了可使用410代码，网站设计人员可通过301代码指定资源的新位置 |
   | 411    | Length Required                 | 服务器无法处理客户端发送的不带Content-Length的请求信息       |
   | 412    | Precondition Failed             | 客户端请求信息的先决条件错误                                 |
   | 413    | Request Entity Too Large        | 由于请求的实体过大，服务器无法处理，因此拒绝请求。为防止客户端的连续请求，服务器可能会关闭连接。如果只是服务器暂时无法处理，则会包含一个Retry-After的响应信息 |
   | 414    | Request-URI Too Large           | 请求的URI过长（URI通常为网址），服务器无法处理               |
   | 415    | Unsupported Media Type          | 服务器无法处理请求附带的媒体格式                             |
   | 416    | Requested range not satisfiable | 客户端请求的范围无效                                         |
   | 417    | Expectation Failed              | 服务器无法满足Expect的请求头信息                             |
   |        |                                 |                                                              |
   | 500    | Internal Server Error           | 服务器内部错误，无法完成请求                                 |
   | 501    | Not Implemented                 | 服务器不支持请求的功能，无法完成请求                         |
   | 502    | Bad Gateway                     | 作为网关或者代理工作的服务器尝试执行请求时，从远程服务器接收到了一个无效的响应 |
   | 503    | Service Unavailable             | 由于超载或系统维护，服务器暂时的无法处理客户端的请求。延时的长度可包含在服务器的Retry-After头信息中 |
   | 504    | Gateway Time-out                | 充当网关或代理的服务器，未及时从远端服务器获取请求           |
   | 505    | HTTP Version not supported      | 服务器不支持请求的HTTP协议的版本，无法完成处理               |

6. TCP和UDP的区别

* TCP面向连接（如打电话要先拨号建立连接）;UDP是无连接的，即发送数据之前不需要建立连接
* TCP提供可靠的服务。也就是说，通过TCP连接传送的数据，无差错，不丢失，不重复，且按序到达;UDP尽最大努力交付，即不保证可靠交付。
* Tcp通过校验和，重传控制，序号标识，滑动窗口、确认应答实现可靠传输。如丢包时的重发控制，还可以对次序乱掉的分包进行顺序控制。
* UDP具有较好的实时性，工作效率比TCP高，适用于对高速传输和实时性有较高的通信或广播通信。
* 每一条TCP连接只能是点到点的;UDP支持一对一，一对多，多对一和多对多的交互通信
* TCP对系统资源要求较多，UDP对系统资源要求较少。

为什么UDP有时比TCP更有优势?

UDP以其简单、传输快的优势，在越来越多场景下取代了TCP,如实时游戏。
（1）网速的提升给UDP的稳定性提供可靠网络保障，丢包率很低，如果使用应用层重传，能够确保传输的可靠性。
（2）TCP为了实现网络通信的可靠性，使用了复杂的拥塞控制算法，建立了繁琐的握手过程，由于TCP内置的系统协议栈中，极难对其进行改进。
采用TCP，一旦发生丢包，TCP会将后续的包缓存起来，等前面的包重传并接收到后再继续发送，延时会越来越大，基于UDP对实时性要求较为严格的情况下，采用自定义重传机制，能够把丢包产生的延迟降到最低，尽量减少网络问题对游戏性造成影响。



7. 三次握手过程

   在TCP/IP协议中，TCP协议通过三次握手建立一个可靠的连接

   ![img](https://www.runoob.com/wp-content/uploads/2018/09/05234233-eed6ddcba93c42be8847e98d6da62802.jpg)

- 第一次握手：客户端尝试连接服务器，向服务器发送 syn 包（同步序列编号Synchronize Sequence Numbers），syn=j，客户端进入 SYN_SEND 状态等待服务器确认

- 第二次握手：服务器接收客户端syn包并确认（ack=j+1），同时向客户端发送一个 SYN包（syn=k），即 SYN+ACK 包，此时服务器进入 SYN_RECV 状态

- 第三次握手：第三次握手：客户端收到服务器的SYN+ACK包，向服务器发送确认包ACK(ack=k+1），此包发送完毕，客户端和服务器进入ESTABLISHED状态，完成三次握手

  [三次握手](https://www.runoob.com/w3cnote/http-vs-https.html)



8. 四次挥手过程

9. 域名解析过程

10. 进程和线程的区别

    1. 一个程序至少有一个进程,一个进程至少有一个线程

    2. 线程的划分尺度小于进程，使得多线程程序的并发性高

    3. 另外，进程在执行过程中拥有独立的内存单元，而多个线程共享内存，从而极大地提高了程序的运行效率

    4. 线程在执行过程中与进程还是有区别的。每个独立的线程有一个程序运行的入口、顺序执行序列和程序的出口。但是线程不能够独立执行，必须依存在应用程序中，由应用程序提供多个线程执行控制 

    5. 从逻辑角度来看，多线程的意义在于一个应用程序中，有多个执行部分可以同时执行。但操作系统并没有将多个线程看做多个独立的应用，来实现进程的调度和管理以及资源分配。这就是进程和线程的重要区别

11. 三列布局中间固定左右自适应的三种写法

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
        <style>
            .box, .left, .middle, .right {
                height: 100px;
                margin-bottom: 5px;
            }
            .left {
                background: tomato;
            }
            .middle {
                background: lightgreen;
            }
            .right {
                background: gold;
            }
            /* 左右分别设置绝对定位 中间设置外边距 */
            .box1 {
                position: relative;
            }
            .box1 .left {
                position: absolute;
                width: 100px;
            }
            .box1 .middle {
                margin: 0 200px 0 100px;
            }
            .box1 .right {
                position: absolute;
                width: 200px;
                top: 0;
                right: 0;
            }
            /* flex 布局 */
            .box2 {
                display: flex;
            }
            .box2 .left {
                flex: 0 0 100px;
            }
            .box2 .middle {
                flex: auto;
            }
            .box2 .right {
                flex: 0 0 200px;
            }
            /* 浮动布局 但是 html 中 middle要放到最后 */
            .box3 .left {
                float: left;
                width: 100px;
            }
            .box3 .right {
                float: right;
                width: 200px;
            }
            .box3 .middle {
                margin: 0 200px 0 100px;
            }
        </style>
    </head>
    <!-- 三栏布局 左右固定 中间自适应 -->
    <body>
        <div class="box box1">
            <div class="left">1-left</div>
            <div class="middle">1-middle</div>
            <div class="right">1-right</div>
        </div>
        <div class="box box2">
            <div class="left">2-left</div>
            <div class="middle">2-middle</div>
            <div class="right">2-right</div>
        </div>
        <div class="box box3">
            <div class="left">3-left</div>
            <div class="right">3-right</div>
            <div class="middle">3-middle</div>
        </div>
    </body>
    </html>
    ```

    - 双飞翼布局
    - 圣杯布局

12. 变量提升问题

    - 变量提升只会提升变量名的声明，而不会提升变量的赋值初始化。
    - 函数提升的优先级大于变量提升的优先级，即函数提升在变量提升之上。

    ​

13. 那些数组方法会生成一个新数组，那些不会生成新数组

|不会改变原来数组的方法|                  |
|------------------|------------------|
| concat()         | 连接两个或更多的数组，并返回结果。 |
| every()          | 检测数组元素的每个元素是否都符合条件。|
| some()           | 检测数组元素中是否有元素符合指定条件。|
| filter()         | 检测数组元素，并返回符合条件所有元素的数组。|
| indexOf()        | 搜索数组中的元素，并返回它所在的位置。|
| join()           | 把数组的所有元素放入一个字符串。|
| toString()       | 把数组转换为字符串，并返回结果。|
| lastIndexOf()    | 返回一个指定的字符串值最后出现的位置，在一个字符串中的指定位置从后向前搜索。|
| map()            | 通过指定函数处理数组的每个元素，并返回处理后的数组。|
| slice()          | 选取数组的的一部分，并返回一个新数组。|
| valueOf()        | 返回数组对象的原始值。|


|会改变原来数组的方法|   |
|------------------|---------------|
|pop()    |删除数组并返回末尾的一个元素|
|push()   |向数组的末尾添加一个或更多元素，并返回新的长度。|
|shift()  |删除并返回数组的第一个元素。|
|unshift()|向数组的开头添加一个或更多元素，并返回新的长度。|
|reverse()|反转数组的元素顺序。|
|sort()   |对数组的元素进行排序。|
|splice() |用于插入、删除或替换数组的元素。|

14. 怎样理解语义化

- 为了在没有CSS的情况下，页面也能呈现出很好地内容结构、代码结构:为了裸奔时好看；

- 用户体验：例如title、alt用于解释名词或解释图片信息、label标签的活用；

- 有利于SEO：和搜索引擎建立良好沟通，有助于爬虫抓取更多的有效信息：爬虫依赖于标签来确定上下文和各个关键字的权重；

- 方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页；

- 便于团队开发和维护，语义化更具可读性，是下一步吧网页的重要动向，遵循W3C标准的团队都遵循这个标准，可以减少差异化。

[语义化](http://www.html5jscss.com/html5-semantics-section.html)

15. 怎样理解表现与样式分离

WEB标准提倡结构、表现和行为相分离---HTML结构、CSS表现、JavaScript行为

16. 什么是混杂模式严格模式，怎样触发

17. 常见的mate标签 

    - **页面关键词**，每个网页应具有描述该网页内容的一组唯一的关键字。
      使用人们可能会搜索，并准确描述网页上所提供信息的描述性和代表性关键字及短语。标记内容太短，则搜索引擎可能不会认为这些内容相关。另外标记不应超过 874 个字符。

    ```
    <meta name="keywords" content="your tags" />
    ```

    - **页面描述**，每个网页都应有一个不超过 150 个字符且能准确反映网页内容的描述标签。

    ```
    <meta name="description" content="150 words" />
    ```

    - **搜索引擎索引方式**，robotterms是一组使用逗号(,)分割的值，通常有如下几种取值：none，noindex，nofollow，all，index和follow。确保正确使用nofollow和noindex属性值。

    ```
    <meta name="robots" content="index,follow" />
    <!--
        all：文件将被检索，且页面上的链接可以被查询；
        none：文件将不被检索，且页面上的链接不可以被查询；
        index：文件将被检索；
        follow：页面上的链接可以被查询；
        noindex：文件将不被检索；
        nofollow：页面上的链接不可以被查询。
     -->
    ```

    - **页面重定向和刷新**：content内的数字代表时间（秒），既多少时间后刷新。如果加url,则会重定向到指定网页（搜索引擎能够自动检测，也很容易被引擎视作误导而受到惩罚）。

    ```
    <meta http-equiv="refresh" content="0;url=" />
    ```

    - **其他**

    ```
    <meta name="author" content="author name" /> <!-- 定义网页作者 -->
    <meta name="google" content="index,follow" />
    <meta name="googlebot" content="index,follow" />
    <meta name="verify" content="index,follow" />
    ```

    ## 移动设备

    - **viewport**：能优化移动浏览器的显示。如果不是响应式网站，不要使用initial-scale或者禁用缩放。
      大部分4.7-5寸设备的viewport宽设为360px；5.5寸设备设为400px；iphone6设为375px；ipone6 plus设为414px。

    ```
    <meta name="viewport" content="width=device-width, initial-scale=1.0,maximum-scale=1.0, user-scalable=no"/>
    <!-- `width=device-width` 会导致 iPhone 5 添加到主屏后以 WebApp 全屏模式打开页面时出现黑边  -->
    ```

    1. width：宽度（数值 / device-width）（范围从200 到10,000，默认为980 像素）
    2. height：高度（数值 / device-height）（范围从223 到10,000）
    3. initial-scale：初始的缩放比例 （范围从>0 到10）
    4. minimum-scale：允许用户缩放到的最小比例
    5. maximum-scale：允许用户缩放到的最大比例
    6. user-scalable：用户是否可以手动缩 (no,yes)
    7. minimal-ui：可以在页面加载时最小化上下状态栏。（已弃用）

    注意，很多人使用initial-scale=1到非响应式网站上，这会让网站以100%宽度渲染，用户需要手动移动页面或者缩放。如果和initial-scale=1同时使用user-scalable=no或maximum-scale=1，则用户将不能放大/缩小网页来看到全部的内容。

    - **WebApp全屏模式**：伪装app，离线应用。

    ```
    <meta name="apple-mobile-web-app-capable" content="yes" /> <!-- 启用 WebApp 全屏模式 -->
    ```

    - **隐藏状态栏/设置状态栏颜色**：只有在开启WebApp全屏模式时才生效。content的值为default | black | black-translucent 。

    ```
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
    ```

    - **添加到主屏后的标题**

    ```
    <meta name="apple-mobile-web-app-title" content="标题">
    ```

    ![meta123](https://www.runoob.com/wp-content/uploads/2015/06/meta123.jpg)

    - **忽略数字自动识别为电话号码**

    ```
    <meta content="telephone=no" name="format-detection" />
    ```

    - **忽略识别邮箱**

    ```
    <meta content="email=no" name="format-detection" />
    ```

    - **添加智能 App 广告条 Smart App Banner**：告诉浏览器这个网站对应的app，并在页面上显示下载banner(如下图)。[参考文档](https://developer.apple.com/library/ios/documentation/AppleApplications/Reference/SafariWebContent/PromotingAppswithAppBanners/PromotingAppswithAppBanners.html)

    ```
    <meta name="apple-itunes-app" content="app-id=myAppStoreID, affiliate-data=myAffiliateData, app-argument=myURL">
    ```

    [常见的meta标签](https://www.runoob.com/w3cnote/meta.html)

18. 什么是文本流 文档流 dom树

- **文档流**：

将窗体自上而下分成一行一行,并在每行中按从左至右的挨次排放元素，即为普通流/文档流。

- **文本流**：

文档的读取和输出顺序，也就是我们通常看到的由左到右、由上而下的读取和输出形式。

**脱离文档流的情况：**

1. float    浮动

浮动会脱离文档流而不会脱离文本流，其他盒模型中的文字还是会为其让出位置，> 环绕在其周围

2. position：absolute/fixed   绝对定位

绝对定位会使元素脱离文档流同时脱离文本流，其他盒模型元素和其中的文字的排> 列都会忽略它

**文档流和文本流可以理解为定位/位置**

- **DOM**

JavaScript操作网页的接口，全称为“文档对象模型”(Document Object Model)。

有这几个概念：文档、元素、节点

整个文档是一个文档节点

每个标签是一个元素节点

包含在元素中的文本是文本节点

每一个属性是一个属性节点

注释属于注释节点

- **DOM树：**
DOM树是结构

所谓层级结构是指元素和元素之间的关系

父子，兄弟

解析器输出的树是由DOM元素和属性节点组成的

当我们说树中包含DOM节点时，意思就是这个树是由实现了DOM接口的元素组成。这些实现包含了其它一些浏览器内部所需的属性。

脱离文档流后层级结构关系还是没有变的

[原文链接](https://www.jianshu.com/p/3056fdca6fce)


19. 什么是行元素 什么是块元素 通过那些属性可以让行元素转换成块元素

20. 可以设置宽高的行元素叫什么

21. css常见几种选择器

22. 选择器的权重值分别多少

23. js中有几种变量类型 哪些放在堆 哪些放在栈

24. 变量类型隐形转换问题

25. 如何声明函数


# 进阶部分

1. 各种场景下的this指针问题

2. 闭包是什么，怎么形成这种结构 有什么用处何危害 有没有实际的案例

3. settimeout在不同的情况下的执行顺序

4. settimeout中的this指针指向 

5. 手写继承实现

-  原型式继承

```js
function Animal(name) {
    this.name = name
    this.list = [1, 2, 3, 4]
}
Animal.prototype.say = function () {
    console.log(this.name)
}

// 构造继承，无法继承方法
function Dog1(name) {
    Animal.call(this, name)
    this.dogName = name
}

var d1 = new Dog1('dog1')
console.log(d1)
console.log(d1.name)
// d1.say() 无法继承

// 原型继承, 子类数据共享，如数组：改一个所有都跟着改变
function Dog2(name) {
    this.dogName = name
} 

Dog2.prototype = new Animal()
var d2 = new Dog2('dog2')
var d22 = new Dog2('dog22')
console.log(d2)
console.log(d2.name) // undefined

d2.list.push(5)
console.log(d2.list)  // [1, 2, 3, 4, 5]
console.log(d22.list) // [1, 2, 3, 4, 5]

d2.name = 'test'
console.log('d2.name', d2.name) //test

// 构造 + 原型继承 = 组合继承
function Dog3(name) {
    Animal.call(this, name)
    this.dogName = name
}
Dog3.prototype = new Animal()

var d3 = new Dog3('dog3')
var d33 = new Dog3('dog3')

d3.list.push(5)
console.log(d3.list) // [1, 2, 3, 4, 5]
console.log(d33.list) // [1, 2, 3, 4]

// 原型+构造+优化1
function Dog4(name) {
    Animal.call(this, name)
    this.dogName = name
}
Dog4.prototype = Object.create(Animal.prototype)
var d4 = new Dog4('dog4')
var d44 = new Dog4('dog4')

d4.list.push(5)
console.log(d4.list)  // [1, 2, 3, 4, 5]
console.log(d44.list) // [1, 2, 3, 4]

// 原型+构造+优化2
function Dog5(name) {
    Animal.call(this, name)
    this.dogName = name
}
Dog5.prototype = Object.create(Animal.prototype)
Dog5.prototype.constructor = Dog5
var d5 = new Dog5('dog5')
var d55 = new Dog5('dog5')

d5.list.push(5)
console.log(d5.list) // [1, 2, 3, 4, 5]
console.log(d55.list) // [1, 2, 3, 4]
```



6. 手写深浅数组克隆

```js
// 浅克隆
function clone(obj) {
    var newObj = {}
    for(var k in obj) {
        newObj[k] = obj[k]
    }
    return newObj
}

// 深克隆
function deepClone(obj1, obj2) {
    for (var k in obj1) {
        if(typeof(obj1[k]) === 'object') {
            obj2[k] = obj1.constructor === 'Array' ? [] : {}
            deepClone(obj1[k], obj2[k])
        } else {
            obj2[k] = obj1[k]
        }
    }
}
```

7. 手写一个方法取出url后面的参数

```js
function getUrlParam(url) {
  var url = url || location.search
  var param = url.split('?')[1]
  var params = param.split('&')
  var obj = {}
  params.forEach(item => {
    obj[item.split('=')[0]] = item.split('=')[1]
  })
  return obj
} 
```
8. 几种跨域的方法

    1. jsonp（jsonp 的原理是动态插入 script 标签）

    2. document.domain + iframe

    3. window.name、window.postMessage

    4. 服务器上设置代理页面

9. 手写ajax函数兼容ie和标准浏览器
```js
function ajax(obj) {
    return new Promise((resolve, reject) => {
        var xhr = null
        // 兼容ie
        if(window.XMLHttpRequest) {
            xhr = new XMLHttpRequest()
        } else {
            xhr = new ActiveXObject('Microsoft.XMLHTTP')
        }
        xhr.open(obj.method, obj.url, true)
        xhr.send()
        xhr.onreadystatechange = function () {
            if(xhr.readyState === 4 && xhr.status === 200) {
               var res = JSON.parse(xhr.responseText)
               resolve(res)
            } else {
                reject(new Error(xhr.statusText))
            }
        }
    })
}
```
9. 浏览器状态码有哪些


# 扩展部分

1. 什么是宏任务什么是微任务

[原文参照](https://www.jianshu.com/p/75107522813f)

2. promise的运行机制，几种状态 

3. 介绍缓存机制

[原文链接](https://www.cnblogs.com/sunshq/p/9273320.html)

4. 垃圾回收机制

1) 问什么是垃圾

一般来说没有被引用的对象就是垃圾，就是要被清除， 有个例外如果几个对象引用形成一个环，互相引用，但根访问不到它们，这几个对象也是垃圾，也要被清除。

2) 如何检垃圾

一种算法是标记 标记-清除 算法，还想说出不同的算法可以参考[这里](https://www.jianshu.com/p/a8a04fd00c3c)。

[原文链接](https://segmentfault.com/a/1190000018605776?utm_source=tag-newest)

5. cookie session localstorage区别

6. mvc mvvm区别 

MVC:

MVC与MVVM都是前端web开发的框架模式

MVC（Model View Controller 模型-视图-控制器）是一种Web架构的模式。

特点：把业务逻辑、模型数据、用户界面分离开来，让开发者将数据与表现解耦。

用户操作view, 用户操作View去改变Controller，Controller改变Model, Model再直接根据业务代码显示在View上。

优点是 当时极大程度降低了页面与逻辑的耦合性

缺点是 mvc的界面和逻辑关联紧密，数据直接从数据库读取 | 

MVVM：

MVVM 的三部分：

Model 层代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑；

View 代表UI 组件，它负责将数据模型转化成UI 展现出来，

ViewModel 是一个同步View 和 Model的对象。

View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互。

ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发

相当于MVC的升级版，因为双向绑定，真正做到了View与数据逻辑分离，用JS去实现界面的值与Model的关联。

缺点是 ViewModel会增多。

[原文](https://blog.csdn.net/qq_42329594/article/details/81380665) 

7. angular vue react区别 

8. angular双向数据绑定原理

9. vue双向数据绑定原理 

10. 什么是虚拟dom 怎么实现 

11. diff算法的原理是什么

12. vue组件传值的五种方法

13. vuex是什么

14. 输入一个url到页面显示都会发什么

[参考链接](https://www.jianshu.com/p/03b4f87e3d37)

15. 性能优化的点

16. 如何实现节省流量 

17. 前端安全攻击有几种 如何避免 

17. dom树的节点遍历

但是js基础一直是重中之重，一些很复杂的问题都是从js基础进行分析解决的，不要觉得学了几个框架，抄了几个demo就可以自信满满的去找工作了，面试官更看重的是学习能力和基础。

    