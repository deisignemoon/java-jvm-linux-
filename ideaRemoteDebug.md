1. 由于java是运行在虚拟机上，以统一字节码的形式在JVM中运行，所以本地与远程服务器的类文件是相同的。只要两边的代码相同，就可以以远程连接的方式进行调试。
2. 进行远程调试，远程服务器上的虚拟机启动参数必须有
''' -Xdebug  -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=8089 '''。
其中address规定可以远程调试的IP和port。
3. idea远程调试需要打开Edit Configuration配置。添加Name，Host，Port。JVM argument默认就可以，Host为远程主机IP，Port为远程服务JVM启动参数的debug的address的端口号。
4. 选择ok完成配置
5. 以此配置启动debug，会连接到对应的远程服务器上。
6. 在本地代码需要的地方打上断点，如果正确，断点上会出现对勾。
7. 开始远程debug吧