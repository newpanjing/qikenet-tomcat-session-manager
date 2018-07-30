- qikenet-tomcat-session-manager
- tomcat redis session共享
1.支持tomcat版本：7.0.x,8.0.x
2.本项目使用https://github.com/jcoleman/tomcat-redis-session-manager 为基础。由于这个项目的作者已经2年多没有维护了，所以自己拷贝了代码打算以后维护。
-Jar包下载地址：
>https://github.com/newpanjing/qikenet-tomcat-session-manager/tree/master/release

- jar包依赖
1.除了下载qikenet-tomcat-session-manager jar包之外，还需要这两个：
2.jedis-2.5.2.jar(redis Java版客户端)
3.commons-pool2-2.2.jar(连接池)

- 新增特性
1.添加了tomcat8.0.x支持
2.移除多余引用和无效的代码
3.添加了maven支持
- 使用方法：
1.将commons-pool2-2.0.jar、jedis-2.3.0.jar复制到tomcat的lib目录下。
2.如果是用tomcat7就用qikenet-tomcat7.0.X-session-manager-1.0.0.jar复制到lib目录下，
3.如果是tomcat8就用qikenet-tomcat8.0.X-session-manager-1.0.0.jar复制到lib目录下
4.改tomcat的conf目录下的context.xml
5.在Context标签中加入：
`<Valve className="com.qikenet.tomcat.session.redis.RedisSessionHandlerValve" />        
	<Manager className="com.qikenet.tomcat.session.redis.RedisSessionManager" 
	    host="localhost" 
	    port="6379" 
	    database="0" 
	    maxInactiveInterval="60"/>`
      
- 配置说明：
+ host=redis的ip或者域名
+ port redis的端口
+ database 数据库编号从0开始，redis的默认数据库是0，如果有其他应用这个database最好改成其他的，防止key重复。
+ maxInactiveInterval session的有效时间
-redis集群配置：
+ sentinelMaster master name例如：sentinelMaster="mymaster"
+ sentinels redis服务器地址，例如：sentinels="127.0.0.1:26379,127.0.0.1:26380,127.0.0.1:26381,127.0.0.1:26382"

- 使用redis共享tomcat内存的好处 
+ session持久化及时tomcat重启session不会失效。
+ 利用nginx进行代理转发实现tomcat集群。
+ 不用担心session撑爆tomcat。

