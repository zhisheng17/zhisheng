![这里写图片描述](http://img.blog.csdn.net/20160901223812707)

题图：from pixabay

相关干货文章阅读：

1. [**《Java研发方向如何准备BAT技术面试(超级干货)》**](http://blog.csdn.net/tzs_1041218129/article/details/52327011)

2. [**《超实用的——BAT面试技巧》**](http://blog.csdn.net/tzs_1041218129/article/details/52280918)

3. [**《如何准备BAT技术面试答案（上）——Java研发方向》**](http://blog.csdn.net/tzs_1041218129/article/details/52355867)

本文是针对文章[**《Java研发方向如何准备BAT技术面试(超级干货)》**](http://blog.csdn.net/tzs_1041218129/article/details/52327011)里面的**JavaEE**和**设计模式**问题的一些答案。如有错误，还请各位网友指正。多谢！！！

文章首发地址为微信公众号：**猿blog** 
文章首发地址为微信公众号：**猿blog **
文章首发地址为微信公众号：**猿blog**

重要的事情说三遍！！！ 
更多干货文章，还请欢迎大家关注和推荐。

![这里写图片描述](http://img.blog.csdn.net/20160901224417928)

**JavaEE:**
<br>
<br>

1.servlet生命周期及各个方法
> 参考文章   http://www.cnblogs.com/xuekyo/archive/2013/02/24/2924072.html



2.servlet中如何自定义filter
> 参考文章  http://www.cnblogs.com/javawebsoa/archive/2013/07/31/3228858.html



3.JSP原理
> 参考文章  http://blog.csdn.net/hanxuemin12345/article/details/23831645




4.JSP和Servlet的区别
> 
> + JSP经编译后就变成了“类servlet”。
> + JSP由HTML代码和JSP标签构成，更擅长页面显示；Servlet更擅长流程控制。
> + JSP中嵌入JAVA代码，而Servlet中嵌入HTML代码。




5.JSP的动态include和静态include
> + 动态include用jsp:include动作实现，如< jsp:include page="abc.jsp" flush="true" />，它总是会检查所含文件中的变化，适合用于包含动态页面，并且可以带参数。会先解析所要包含的页面，解析后和主页面合并一起显示，即先编译后包含。
> + 静态include用include伪码实现，不会检查所含文件的变化，适用于包含静态页面，如<%@ include file="qq.htm" %>，不会提前解析所要包含的页面，先把要显示的页面包含进来，然后统一编译，即先包含后编译。




6.Struts中请求处理过程
> 参考文章  http://www.cnblogs.com/liuling/p/2013-8-10-01.html



7.MVC概念
> 参考文章  http://www.cnblogs.com/scwyh/articles/1436802.html



8.Spring mvc与Struts区别
> 参考文章  http://blog.csdn.net/tch918/article/details/38305395
> 参考文章  http://blog.csdn.net/chenleixing/article/details/44570681



9.Hibernate/Ibatis两者的区别
> 参考文章  http://blog.csdn.net/firejuly/article/details/8190229



10.Hibernate一级和二级缓存
> 参考文章  http://blog.csdn.net/windrui/article/details/23165845




11.简述Hibernate常见优化策略
> 参考文章  http://blog.csdn.net/shimiso/article/details/8819114



12.Spring bean的加载过程(推荐看Spring的源码)
> 参考文章  http://geeekr.com/read-spring-source-1-how-to-load-bean/



13.Spring bean的实例化(推荐看Spring的源码)
> 参考文章  http://geeekr.com/read-spring-source-two-beans-initialization/




14.Spring如何实现AOP和IOC(推荐看Spring的源码)
> 参考文章  http://www.360doc.com/content/15/0116/21/12385684_441408260.shtml





15.Spring bean注入方式
> 参考文章 http://blessht.iteye.com/blog/1162131




16.Spring的事务管理
> 这个主题的参考文章没找到特别好的，http://blog.csdn.net/trigl/article/details/50968079  这个还可以。




17.Spring事务的传播特性
> 参考文章  http://blog.csdn.net/lfsf802/article/details/9417095



18.springmvc原理
> 参考文章  http://blog.sina.com.cn/s/blog_7ef0a3fb0101po57.html




19.springmvc用过哪些注解
> 参考文章  http://aijuans.iteye.com/blog/2160141




20.Restful有几种请求
> 参考文章，http://www.infoq.com/cn/articles/designing-restful-http-apps-roth，该篇写的比较全。




21.Restful好处
> + 客户-服务器：客户-服务器约束背后的原则是分离关注点。通过分离用户接口和数据存储这两个关注点，改善了用户接口跨多个平台的可移植性；同时通过简化服务器组件，改善了系统的可伸缩性。
> + 无状态：通信在本质上是无状态的，改善了可见性、可靠性、可伸缩性.
> + 缓存：改善了网络效率减少一系列交互的平均延迟时间，来提高效率、可伸缩性和用户可觉察的性能。
> + 统一接口：REST架构风格区别于其他基于网络的架构风格的核心特征是，它强调组件之间要有一个统一的接口。




22.Tomcat，Apache，JBoss的区别
> + Apache:HTTP服务器(WEB服务器)，类似IIS，可以用于建立虚拟站点，编译处理静态页面，可以支持SSL技术，支持多个虚拟主机等功能。
> + Tomcat:Servlet容器，用于解析jsp，Servlet的Servlet容器，是高效，轻量级的容器。缺点是不支持EJB，只能用于java应用。
> + Jboss:应用服务器，运行EJB的J2EE应用服务器，遵循J2EE规范，能够提供更多平台的支持和更多集成功能，如数据库连接，JCA等，其对Servlet的支持是通过集成其他Servlet容器来实现的，如tomcat和jetty。




23.memcached和redis的区别
> + 性能对比：由于Redis只使用单核，而Memcached可以使用多核，所以平均每一个核上Redis在存储小数据时比Memcached性能更高。而在100k以上的数据中，Memcached性能要高于Redis，虽然Redis最近也在存储大数据的性能上进行优化，但是比起Memcached，还是稍有逊色。
> + 内存使用效率对比：使用简单的key-value存储的话，Memcached的内存利用率更高，而如果Redis采用hash结构来做key-value存储，由于其组合式的压缩，其内存利用率会高于Memcached。
> + Redis支持服务器端的数据操作：Redis相比Memcached来说，拥有更多的数据结构和并支持更丰富的数据操作，通常在Memcached里，你需要将数据拿到客户端来进行类似的修改再set回去。这大大增加了网络IO的次数和数据体积。在Redis中，这些复杂的操作通常和一般的GET/SET一样高效。所以，如果需要缓存能够支持更复杂的结构和操作，那么Redis会是不错的选择。



24.如何理解分布式锁
> 参考文章   http://blog.csdn.net/zheng0518/article/details/51607063  
>   和  http://blog.csdn.net/nicewuranran/article/details/51730131。



25.你知道的开源协议有哪些
> 常见的开源协议有GPL、LGPL、BSD、Apache Licence vesion 2.0、MIT，详细内容参考文章http://blog.jobbole.com/44175/
> http://www.ruanyifeng.com/blog/2011/05/how_to_choose_free_software_licenses.html



26.json和xml区别
> + XML:
		>> + 应用广泛，可扩展性强，被广泛应用各种场合；
		>> + 读取、解析没有JSON快；
		>> + 可读性强，可描述复杂结构。
> 
<br>
> 
> + JSON:
		>> + 结构简单，都是键值对；
		>> + 读取、解析速度快，很多语言支持；
		>> + 传输数据量小，传输速率大大提高；
		>> + 描述复杂结构能力较弱。

<br>
<br>

**设计模式：**
<br>
<br>

1.设计模式
> 参考文章    http://www.cnblogs.com/beijiguangyong/archive/2010/11/15/2302807.html




2.设计模式的六大原则
> 参考文章  http://www.uml.org.cn/sjms/201211023.asp




3.用一个设计模式写一段代码或画出一个设计模式的UML
> 参考文章  http://www.cnblogs.com/beijiguangyong/archive/2010/11/15/2302807.html




4.高内聚，低耦合方面的理解
> 参考文章 http://my.oschina.net/heweipo/blog/423235 