HTTP 是 web 的核心动态 web 应用的核心
现代 web 应用如何工作如何构建
动手构建过动态 web 应用

输入 URL--浏览器里显示
点了一个链接、提交了一个表单---显示下一个页面
表单错误提示
浏览器就是一个接口，或者说一扇窗，通过她你就可以与万维网进行互动与交互。
浏览器的背后---有一堆文件 – CSS，HTML，Javascript，视频文件，图片文件等等 – 这些文件构成了你所看到的页面都是通过一个叫做 HTTP 的传输协议从服务器传输到你的浏览器，也就是客户端里
浏览器地址栏输地址的时候前面加的是 http:// 
HTTP是一种协议--应用程序和超文本文档之间的传输联系起来
HTTP 就是机器之间彼此沟通的一个协议，或者说一个消息格式
HTTP 遵循一个简单的模型-----客户端发出请求到服务器并等待响应--“请求–响应协议”
请求和响应都是文本信息，或者说是字符串，信息写法遵循着一个规则，能保证其他机器能够理解上面的内容。
HTTP/1.0 支持传输不同的文件类型--- CSS 文件，视频，脚本和图片


互联网是如何工作的
互联网是由数以百万计的互相连接的网络构成，网络中计算机和其他设备可以互相通信
网络内的所有设备都提供独特的标签。称是互联网协议地址或 IP 地址，是类似于在互联网上的计算机的电话号码。
IP 地址还有端口号--类似于分机号码
IP 地址---192.168.0.1
需要一个端口号的时候---192.168.0.2:1234
 IP 地址是设备或服务器的标识符，可以包含数以千计的端口
 端口都用于不同的交互目标。
互联网上每个设备 互联网服务供应商 (ISP) 提供的公网 IP 地址
访问 Google 没有在浏览器里输入它的 IP 地址，只是输入 Google 的 URL http://www.google.com
电脑是怎么知道它的 IP 地址的呢？？


DNS
URL 和 IP 地址之间对应  域名解析系统 DNS控制
DNS 是一个分布式数据库
域名翻译成 IP 地址，将请求映射到远程服务器
DNS 在互联网上记录 URL 和它对应的 IP 地址
DNS 数据库被安装在叫做 DNS 服务器的设备上
DNS 服务器集群是分层级
如果一个 DNS 服务器里没有一个请求需要的域名---服务器就会把请求转发给这个集群上更上一层节点的 DNS 服务器---域名会在某个 DNS 服务器上的数据库里被发现--- IP 地址所代表的设备就会来接受这个请求



客户端和服务器
Web 浏览器的应用程序
Web 浏览器的职责---发送 HTTP 请求、响应处理成人类友好的形式显示在你的显示器

接收者是被称为服务器的远程计算机-----处理请求的设备
工作就是------发送一个响应回去
服务器发送回去的响应里面都包含了请求中指定的一些数据。


资源 (Resources)
----指的是互联网上你通过 URL 与其交互的东西
包括了图片，视频，网页和其他文件


无状态的 (statelessness)

协议是无状态的--------协议设计成 每一个请求/响应周期与前一个都是互相独立的话
HTTP 协议下服务器不需要在各次请求之间保留状态信息
很难构建有状态的应用
构建有状态应用的时候--模拟 web 应用中的有状态体验
没有退出登录---HTTP 是无状态的--怎么维持登录状态
怎么知道哪个请求是你发出的？
怎么区分你和其他用户的？
web 应用看起来像是有状态的


什么是URL---统一资源定位符
互联网上寻找和访问服务器
web 浏览器向这个地址发送一个 HTTP 请求，然后拿回这个地址的响应结果


URL 组成部分
URL 分解成 3 部分
http：---称为URL 模式（ scheme ）---告诉 web 客户端怎样去访问一个资源诉 web 客户端使用超文本传输协议也就是 HTTP 去发起一个请求
 URL 模式还有ftp、mailto、git
 www.example.com-----资源路径或主机 (host)----告诉客户端，资源的确切位置。
/home/----  URL 路径-----代表了客户端正在请求什么样的本地资源 (对于服务器来说)。

URL 包含一个主机用来监听 HTTP 请求的端口号
http://localhost:3000/profile---- 3000 端口去监听 HTTP 请求
监听 HTTP 请求的默认端口号是 80
URL 中没有指定其他的端口号默认80

查询字符串 / 参数------查询字符串向服务器传递附加信息
是 URL 的一部分
包含一些要发往至服务器的各种类型的数据
http://www.example.com?search=ruby&results=10

查询字符串组件	描述
?				 这是个保留字，标识着查询字符串的开始
search=ruby		 这是一个参数的键/值对儿
&				 这是个保留字，需要给查询字符串添加参数时使用
results=10		 这也是一个参数的键/值对儿

                         参数的键/值对儿
                                |             
http://www.phoneshop.com?product=iphone&size=32gb&color=white
                        |              |         |     |          
                 查询字符串的开始   添加参数         键/值对儿添加参数                          

查询字符串是通过 URL 传递的，他们仅使用 HTTP 的 GET 请求
限制：
有最大长度
不推荐用敏感信息 用户名或密码
查询字符串中无法使用空格和特殊字符比如&。它们必须用 URL 编码代替，我们接下来会讨论这个。


URL 编码 (URL Encoding)

默认只接受 ASCII 码
不是 ASCII 码的字符---转义或者编码
URL 编码的原理----不符合格式的字符--%开头跟着两个十六进制数字代表的 ASCII 码的一串字符
                                   space----020
http://www.thedesignshop.com/shops/tommy%020hilfiger.html
&---查询字符串的分隔符
保留字符特殊用途可以不用编码

准备工作
HTTP 如何工作的工具



浏览器的 HTTP 请求
承载 Reddit 网站的服务器处理你的请求并返回给你的浏览器一个响应
处理过的服务器响应
响应的本来面目

怎么样才能看到原始的 HTTP 响应数据呢

审查器 (Inspector)-----浏览器都有查看 HTTP 请求和响应的方法
工具，然后选择开发者工具---打开审查器

 Network 标签
有很多项----每一项都是一个单独的请求
访问了这一个 URL浏览器就发起了多个请求
一个请求对应着一个资源 （图片，文件等等）。

点击一下对主页的第一个请求---看到特定的请求头部，cookies，还有原始的响应数据
Response 子标签去看看原始响应数据。
 Network 标签下，除了第一个请求，还有一堆其他请求的返回：

为什么会出现这些额外的响应，谁发起的这些请求？
对于www.reddit.com的请求----返回了一些 HTML---HTML 里又引用了其他的资源---浏览器为了展示出一个能够给人看的网页----把这些引用到的资源也一并拿来---浏览器对得到的初次响应里的每一个资源再一一发起请求

其他的请求保证了这个网页和其他一些东西能正常良好的显示在你的屏幕上


请求方法

Network 标签里的响应数据--两列 Method 和 Status

 Method ---HTTP 请求方法--GET 和POST
Status---- 请求的响应状态码
每一个请求都会得到一个响应


GET 请求---超链接或者浏览器的地址栏
超链接的默认行为就是向一个 URL 发送GET请求

用 HTTP 工具发送带查询字符串的请求

浏览器会自动对这些资源发起请求，纯粹的 HTTP 工具则不会


POST 请求---给服务器提交一些数据

怎样不通过 URL，仅仅是提交表单就把数据发送到服务器的呢？
HTTP 的正文 （ Body ）
正文包含了正在传输的 HTTP 消息
可以发送一个没有正文的 HTTP 消息，要使用正文的时候，可以包含 HTML，图片，音频

正文看成包裹在信封里发出的信件（:URL 就好比是信封上写的地址是可见的，而信的内容在信封里是不可见的）
表单然后提交，被重定向到下一个页面
重定向到下一个页面的关键信息---HTTP 响应头部里的一部分
浏览器看到这个响应头部---自动向Location 头部里的 URL 发起一个全新请求

浏览器对你隐藏了大量的 HTTP 请求/响应的细节
浏览器POST 请求---Location 得到头部的响应---发起另一个请求--得到的响应内容展示

 使用HTTP 工具，能看到第一个 POST 请求的 Location 响应头部不会自动发起第二个请求


HTTP 头部
在请求/响应的 HTTP 周期里发送额外的信息
纯文本格式--冒号分隔的键值对儿
审查器来看看
Request Headers---请求和响应包含着不同的头部

请求头部
字段名	             描述	                    举例
Host	      服务器域名	        Host:www.reddit.com
Accept-Language	可接受的语言	     Accept-Language: 
User-Agent	一个标识客户端的字符串	User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_5) AppleWebKit/537.36 (KHTML，like Gecko) Chrome/38.0.2125.101 Safari/537.36
Connection	客户端连接的类型	Connection: keep-alive


处理响应
服务器发回的原始 HTTP 数据
服务器返回的原始数据就是所谓的响应
HTTP 响应里的各种组成部分。

状态码
HTTP 状态码
服务器接收到请求后发送的标识请求状态---三位数
状态文本---审查器的Status
200----意思是请求被正确处理
302	Found	所请求的资源已暂时更改.通常会重定向到另一个 URL
404	Not Found	所请求的资源无法找到
500	Internal Server Error	服务器出现一般性错误

302 Redirect（重定向）
资源的位置移动---
解决方案---旧 URL 的请求重新引导到新 URL -----重定向（ redirect ）
302 响应状态码的时候，他就知道这个资源已经移动到别处了，然后就会自动跳转到 Location 响应头部里指定的 URL
演示重定向


响应头部
Content-Encoding	数据的编码类型	Content-Encoding: gzip
Server	服务器的名称	Server:thin 1.5.0 codename Knife
Location	通知客户端新的资源位置	Location: http://www.github.com/login
Content-Type	响应数据的类型	Content-Type:text/html; charset=UTF-8


HTTP 只不过是一个协议，用于指示客户端与服务器之间如何使用某种格式的文本进行通信。


有状态的WEB应用
HTTP 协议是无状态
请求之间，服务器是不会保留你的 “状态” 信息。
不同的请求之间并不知道对方的存在
web 开发者在开发有状态的 web 应用时十分的困难

应用大都是有状态
表示---目前状态是通过了身份验证
对服务器发起新的请求---并不会突然就退出登录
服务器返回的响应页面里依然有我们的用户名显示着---维持它们的状态

web 开发者常用的实现 “有状态” 体验的技术手段
用于高效展示动态页面信息的技术
会话（ session ）
Cookies
异步 javascript 调用（ AJAX ）

服务器是怎么知道你的用户名，并动态显示在页面上的
刷新页面发起新的请求也不影响你的登录状态

会话 （ session ）
无状态的 HTTP 协议通过某种方式保持状态
服务器发送响应数据----带一个唯一的令牌（英文叫 token，就是一串数）--客户端向服务器发起请求的时候都把这个令牌附加在后面---服务器能够辨识这个客户端

来回传递的令牌叫做会话标识符session identifier 

客户端与服务器之间传递会话 id的机制----让服务器创建一种各次请求之间的持续连接状态
人造的状态--构建复杂的应用程序
必须检查每个请求必须检查每个请求
有会话标识符会话 ，id服务器必须检查id 是没有过期的----服务器需要维护一些关于如何处理会话过期，如何存储会话数据的规则

服务器要基于这个会话 id 取出这个会话的数据
服务器要根据取出的会话数据重新创建应用程序的状态，将其作为响应返回给客户端
 Ajax 代替了全页面刷新

存储会话信息的方法: 浏览器 cookie 。

Cookies
服务器发送给客户并存端储在客户端的一段数据
存储在浏览器里包含着会话信息的小文件
第一次访问一个网站---服务器会给你发送会话信息并将其存储在你本地电脑浏览器的 cookie ----真正的会话数据是存在服务器上-----

客户端发起每一个请求------服务器就会比对客户端的 cookie 和服务器上的会话数据标识当前的会话
再次访问同一个网站的时候，服务器就会通过 cookie 和里面的信息来认出你的会话。

真实的案例
cookie 是存在浏览器里的。现在，就算你关掉浏览器，关掉电脑， cookie 里的信息也不会消失的

web 应用是如何在我们发起的一个又一个请求中记住我们的登录状态

应用程序是如何 “记住” 我们的登录状态？


application 标签然后访问http://www.reddit.com
 value 那一列看到第一次发起请求后服务器返回给我们的 cookie 了:

http://www.reddit.com---set-cookie头部-----http://www.reddit.com---cookie头部出现了---登录----出现了一个唯一的会话 id---- id 会存在你浏览器的 cookie 里---- Reddit.com 的请求都会附上这个会话 id 。

每一个请求都会包含这个会话 id----服务器收到一个带有会话 id 的请---根据这个 id 去找对应的数据---数据里就有服务器"记住"的客户端的状态


会话数据存在哪里？
服务器上的某个地方---内存、数据库或者键 / 值存储

会话 id 存储在客户端是访问存储在服务器上的会话数据的 “钥匙”
 id 是唯一很短的过期时间

会话过期后你需要重新登录退出登录， 会话 id 就会消失。
手动删掉会话 id 也是同样的效果（在审查器里，右键 cookies 然后删除它）

会话数据是由服务器生成并存储在服务器上
会话 id 以 cookie 的形式发送到客户端上

AJAX---异步 javascript 和 XML “ 的简称
主要特点就是允许浏览器发送请求和处理响应的时候不用刷新整个页面
的服务器会把各种信息组合起来，显示在你的时间线上，十分复杂的 HTML 页面
每一个请求都重新生成一次页面的成本是非常高的

AJAX的时候，所有客户端发送的请求都是异步的，就是说页面不会刷新
每敲一个字都会发起一个新的请求---按下键都会触发一个 AJAX 请求
请求的响应会通过一些回调来处理
理解回调
把一些逻辑存放在某个函数里---某个条件被触发后才回来执行你前面存放的逻辑
响应返回的时候，回调就会被触发---回调函数会用新的搜索结果去更新网页上的 HTML 

AJAX 请求就像是普通请求
唯一不同就是----不是通过浏览器刷新来处理响应，客户端的一些 javascript 代码来处理。
web 开发者用来在无状态的 HTTP 协议上构建有状态应用的技术

安全的 HTTP（HTTPS）
请求和响应里的信息都是通过明文字符串发送的
黑客连接到同一网络--用数据包嗅探技术来读取来回发送的消息
别人复制了这个会话 id ，他们可以手动创建到服务器的请求，伪装成你的客户端，甚至都不需要你的用户名和密码就可以自动登陆

通过 HTTPS 发送的请求和响应在发送前都会被加密----得到的信息都是加密的和无用

HTTPS 通过一个叫做 TLS 的加密协议来加密消息
早期 HTTPS 使用 SSL

加密
加密协议在加密数据之前---用证书与远程服务器进行通信----交换安全密钥

网站进行交互之前---览器都会替你对网站的证书做一些检查---


同源策略（ Same-origin policy ）
允许来自同一站点的资源进行互相访问而不受限制阻止其他不同站点对文档/资源的访问

同源的文档必须有相同的协议，主机名和端口号


