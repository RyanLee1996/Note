## B/S

>Browser与Server,中文意思：浏览器端与服务器端架构，这种架构是从用户层面来划分的，Browser浏览器，其实也是一种Client客户端，只是这个客户端不需要大家去安装什么应用程序，只需在浏览器上通过HTTP请求服务器端相关的资源（网页资源），客户端Browser浏览器就能进行增删改查。不依赖用户的电脑操作系统环境，只与浏览器环境有关，当然由于网页复杂性，又延伸出网页前端技术与后端技术，前端技术指的是在浏览器上编程的技术，比如：JS,HTML,CSS，这些前端技术是运行在客户端Browser浏览器上的，而并非在服务器端，如果不信，可以测试一下，当你的页面中包含JS脚本时，若将浏览器属性中的禁用JS启用，你会发现页面中那些依赖JS的技术都没办法使用。后端技术指的是运行在服务器上编程的技术（也就是Server端）

## C/S

>Client与Server ，中文意思：客户端与服务器端架构，这种架构也是从用户层面（也可以是物理层面）来划分的，这里的客户端一般泛指客户端应用程序EXE，程序需要先安装后，才能运行在用户的电脑上，对用户的电脑操作系统环境依赖较大，比如：若想运行基于WINFORM开发的EXE程序，必需要先在电脑上安装.NET FRAMEWORK组件，否则无法正常运行。Server端这里是一个非必要的部份，若客户端是一个单机应用程序，无需数据库或其它分布式技术，那么Server端是可以省略的，若客户端需要数据库或其它分布式技术，那么这里的Server端指的是数据库服务器端或其它分布式技术（WEB API,WEB SERVICE等）所在的服务器端。

## 区别

- 所谓的 Browser-Server 架构其实是 C/S 架构的一种特殊的实现形式，而不是其对立面。

- C/S 是双向的通讯，建立连接后会一直保持，任何一方都可以随时向对方发送信息。比如 QQ 客户端登录后，腾讯的服务器可以随时把新的消息发给客户端，客户端也可以随时向腾讯的服务器发送信息。

- B/S 是「查询」式的通讯，客户端向服务器查询一些信息，在服务器回应之后，(逻辑上)会立刻断开连接。只有客户端向服务器查询时，服务器才能向客户端发送信息，服务器不能主动地向客户端发送信息。
