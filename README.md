在实现提供 WebSocket 服务的项目中，一般有如下几种解决方案：

- 方案一 Spring WebSocket
- 方案二 Tomcat WebSocket
- 方案三 Netty WebSocket

# SpringWebSocket
​	Spring 4.0为WebSocket通信提供了支持，包括： 

- ​	发送和接收消息的低层级API；
- ​	发送和接收消息的高级API；
- ​	用来发送消息的模板；
- ​	支持SockJS，用来解决浏览器端、服务器以及代理不支持WebSocket的问题。 



### spring websocket可选择以下几种方式

​	**使用Spring的低层级WebSocket API：**

​		直接使用WebSocket（或SockJS）就很类似于使用TCP套接字来编写Web应用。因为没有高层级的线路协议（wire protocol），因此就需要我 们定义应用之间所发送消息的语义，还需要确保连接的两端都能遵循这些语义。 不过，好消息是我们并非必须要使用原生的WebSocket连接。就像HTTP在TCP套接字之上添加了请求-响应模型层一样，STOMP在 WebSocket之上提供了一个基于帧的线路格式（frame-based wire format）层，用来定义消息的语义。 



​	**使用STOMP简单代理：**

​	在Spring MVC中为控制器方法添加@MessageMapping注解，使其处理STOMP消息，它与带 有@RequestMapping注解的方法处理HTTP请求的方式非常类似。 



​	**使用STOMP代理中继:(RabbitMQ、 ActiveMQ )**

 	对于初学来讲，简单的代理是很不错的，但是它也有一些限制。尽管它模拟了STOMP消息代理，但是它只支持STOMP命令的子集。因为它是 基于内存的，所以它并不适合集群，因为如果集群的话，每个节点也只能管理自己的代理和自己的那部分消息。 

​	对于生产环境下的应用来说，你可能会希望使用真正支持STOMP的代理来支撑WebSocket消息，如RabbitMQ或ActiveMQ。这样的代理提供了 可扩展性和健壮性更好的消息功能，当然它们也会完整支持STOMP命令。  
