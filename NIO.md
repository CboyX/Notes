#### 1.NIO(new IO)

NIO与IO 的区别：

![1551365179328](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1551365179328.png)

NIO的核心在于：通道（channel）和缓冲区（Buffer），通道表示打开到IO设备（例如：文件、套接字（socket））的连接。若要使用NIO，需要获取用于连接IO设备的通道以及用于容纳数据的缓冲区，然后操作缓冲区，对数据进行处理。**简而言之，Channel负责传输，Buffer负责存储数据**