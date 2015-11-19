#Pre某Project

###Simple Client/Server

 Client/Server最常见的是HTTP吧，然后是一个典型的synchronous。
 
 1. Client obtain the network address of the server.
 2. Client creates a connection/socket to the server across the network.
 3. Client sends a request message to the server and waits for a response.
 4. The server processes the request, producing some information.
 5. The server sends a response message containing the needed information back to the waiting client.
 6. The client continues processing with the response information.
 
能找到的最简单的[例子][id]

[id]:https://github.com/KrisYu/OSConceptsExamples/tree/master/superSimpleServerExample


Server端：建立一个ServerSocket,然后让其一直处于listen状态，然后有消息来就accept，各种处理。给返回消息。


Client端：同样需要建立socket，然后往里写东西给server接收。同时可以接收和处理server的返回信息。

例子好看，好用，测试的时候先运行server，然后才能运行client。


### binary data

msg.getBytes()适用于string转bytes.

binary data到底是个什么鬼，ascii data是文本，一般文本使用，而binary data比如图片啥的也可以方便的binary化，然后传输比如图片，比如莫名文件就用binary data么?

然后比如inputStream，outputStream都是binary data么...


可能之后会用：

<http://stackoverflow.com/questions/4211705/binary-to-text-in-java>

<http://codereview.stackexchange.com/questions/46080/read-and-convert-binary-files-to-ascii-text>

###JUnit文档一篇  / Apahce log4j

Junit用起来还蛮方便的.如文档：

<https://courses.cs.washington.edu/courses/cse143/11wi/eclipse-tutorial/junit.shtml>

同时一个project的property有一个好用的Java Build Path用来加各种external jar和libarary.


Apache的log4j用起来貌似也不难/不烦.

### Abstract

然后终于，interface是用来implement的，abstract是用来subclass的，然后通过这个project，终于算用了eclipse里面的一些平常都没用过的功能。

###File Directory

File Directory是要提前建好的，否则可是会报错的。

### to do

detail:

write完成

framework搭好

<br/>

general:

stream传来传去，如何接收相应信息.

测试的时候可以使用图片测试，除了Juint测试，可以自己把图片binary stream化，然后传入测试（赞！）

try/catch throw 机制，走一点心/肾/肝/肺.
