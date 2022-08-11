# Filter(过滤器)
目录
- [Filter概念及作用](#Filter概念及作用)
- [一,Filter快速入门](#一,Filter快速入门)
- [二,Filter执行流程](#二,Filter执行流程)
- [三Filter使用细节](#三Filter使用细节)

## Filter概念及作用
* 是javaweb三大组件(Servlet,Filter,Listener)之一
* 过滤器可以把对资源的请求拦截下来
* 过滤器一般完成一些通用操作,比如:权限控制,统一编码处理,敏感字符处理...
## 一,Filter快速入门
 1. 定义类实现filter接口,重写所有方法 
 2. 配置Filter拦截资源路径,在类上定义``@WebFilter``注解
 3. 在doFilter方法输出字符,放行资源
 ```
  //放行前逻辑
  //重写doFilter()方法放行拦截资源
  chain.doFilter(request,respond);
  //放行后逻辑
 ```
## 二,Filter执行流程
 1. 放行前逻辑(一般对request数据进行处理)
     - 执行放行前逻辑
     - 发行
 2. 放行后逻辑(对respond进行数据处理)
     - 放行后访问对应的资源,资源访问完成后会回到Filter(此时respond有数据了)
     - 回到filter,执行放行后的逻辑
 3. 流程:
 ``
 发行前逻辑 ---> 发行 --->访问资源 --->发行后逻辑 ``
## 三Filter使用细节
 1. Filter拦截路径配置
     - 拦截具体资源:`` /hello.jsp``,只有访问hello.jsp时才会被拦截
     - 目录拦截: `` /user/* ``,拦截/user下所有的资源
     - 后缀命拦截 `` *.jsp `` ,
     - 拦截所有 `` /* ``, 
 2. 过滤器链
     - 过滤器链的流程
   ```
   浏览器-->request-->filter1(执行前逻辑-->发行)-->
   Filter2(执行前逻辑-->发行)--->
   web资源--->respond-->Filter2(执行放行后的逻辑)-->
   filter1(执行放行后的逻辑)--->响应浏览器
   ```