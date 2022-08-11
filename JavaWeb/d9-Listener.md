# Listener(监听器)
 目录
   - [一,Listener认识](#一,Listener认识)
   - [二,Listener分类 ](#二,Listener分类)
   - [三,SevletContextListener使用](#三,SevletContextListener使用)
## 一,Listener认识
   - 概念: javaweb三大组件之一(监听器)
   - 监听器可以监听
        当application,session,request对象创建,销毁或者添加修改删除属性时,自动执行代码功能的组件.
## 二,Listener分类
<html> 
<table>
<tr>
<td>监听器分类</td>
<td>监听器名称</td>
<td>作用</td>
</tr>
<tr>
<td rowspan="2">ServletContext监听</td>
<td>ServletContextListener</td>
<td>对ServletContext对象进行监听(创建,销毁)</td>
</tr>
<tr>
<td>ServletContextAtrributeListener</td>
<td>对ServletContext对象中属性进行监听(增删改)</td>
</tr>
<tr>
<td rowspan="4">Session监听</td>
<td>HttpSessionListener</td>
<td>对HttpSession对象进行监听(创建,销毁)</</td>
</tr>
<tr>
<td>HttpSessionAtrributeListener</td>
<td>对HttpSession对象中属性进行监听(增删改)</td>
</tr>
<tr>
<td>HttpSessionBindingListener</td>
<td>监听对象于Session的绑定与解除</td>
</tr>
<tr>
<td>HttpSessionActivationListener</td>
<td>对Session对象的钝化与活化监听</td>
</tr>
<tr>
<td rowspan="2">Request监听</td>
<td>ServletRequestListener</td>
<td>对ServletRequest对象进行监听(创建,销毁)</</td>
</tr>
<tr>
<td>ServletRequestAtrributeListener</td>
<td>对ServletRequest对象中属性进行监听(增删改)</td>
</tr>
</table>
<hr>
</html>

## 三,SevletContextListener使用
1. 定义类,实现``ServletContextListener``接口
     - 重写方法
     1. ``contextInitialized(SevletContextEven sce)``
     用于加载资源
     2. ``contextDestroyed(SevletContextEven sce)``
     用于释放资源
2. 添加``@webListener``注解
