## SpringMVC 框架

### 什么是SpringMVC？

SpringMVC 是 Spring 框架的一个模块，SpringMVC 和 Spring 无需通过中间整合层进行整合。

SpringMVC 是一个基于 MVC 的 Web 框架。

### MVC 在 B/S 系统下的应用？

MVC是一种设计模式，MVC 在 B/S 系统下的应用：

 ![30](猿blog\文章截图\30.png)

### SpringMVC 框架

第一步：发起请求到前端控制器（DispatcherServlet）

第二步：前端控制器请求 HandlerMapping 查找 Handler，可以根据xml配置、注解进行查找

第三步：处理器映射器 HandlerMapping 向前端控制器返回 Handler

第四步：前端控制器调用处理器适配器去执行 Handler

第五步：处理器适配器 HandlerAdapter 执行 Handler

第六步：处理器适配器向前端控制器返回 ModelAndView （ModelAndView是SpringMVC框架的一个底层对象，包括 Model 和 View）

第七步：处理器适配器向前端控制器返回 ModelAndView

第八步：前端控制器请求视图解析器去进行视图解析（根据逻辑视图名解析成真正的视图（jsp）） 

第九步：视图解析器向前端控制器返回 View

第十步：前端控制器进行视图渲染（视图渲染将模型数据（在 ModelAndView对象中）填充到 request 域）

第十一步：前端控制器向用户响应结果



**组件：**

+ 前端控制器 DispatcherServlet （不需要程序员开发）

  > 作用：接收请求，然后响应结果，相当于转发器，中央处理器
  >
  > 有了 DispatcherServlet 减少了其它组件之间的耦合度。

+ 处理器映射器 HandlerMapping （不需要程序员开发）

  > 作用：根据请求的 url 查找 Handler

+ 处理器 Handler （**需要程序员开发**）

  > 注意：编写 Handler 时按照 HandlerAdapter 的要求去做，这样适配器才可以去正确执行 Handler 。

+ 处理器适配器 HandlerAdapter 

  > 作用：执照特定的规则（HandlerAdapter要求的规则）去执行 Handler

+ 视图解析器 View resolver （不需要程序员开发）

  > 作用：进行视图解析，根据逻辑视图名解析成真正的视图 View

+ 视图 View （**需要程序员来开发jsp**）

  > View 是一个接口，实现类支持不同的 View 类型（jsp、freemarker、pdf...）



