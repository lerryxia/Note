## 1 日志技术和输出语句的区别

#### 1.1 输出语句的弊端

● ① 想要取消记录的信息，需要修改代码才能完成。
● ② 信息只能展示在控制台，不能将其记录到其他的位置（文件、数据库等）。

#### 1.2 日志

● 生活中的日志：生活中的日志就好比日记，可以记录生活中的点点滴滴。
● 程序中的日志：程序中的日志可以记录程序在运行的时候的点点滴滴，并可以进行永久存储。

#### 1.3 区别

输出语句	日志技术
取消日志	需要修改代码，灵活性较差	不需要修改代码，灵活性较好
输出位置	只能是控制台	                      可以将日志信息写入到文件或数据库中
多线程	和业务代码处于一个线程中	多线程方式记录日志，不影响业务代码的性能

## 2 日志技术的体系结构

![](/img/JavaBasic/1633675090442-1844373a-df53-4b33-97bb-f25ce796fa22.png)
## 3 LogBack

### Logback介绍

Logback 分为三个模块：Core、Classic 和 Access。Core模块是其他两个模块的基础。 Classic模块扩展了core模块。 Classic模块相当于log4j的显著改进版。Logback-classic 直接实现了 SLF4J API。

要引入logback，由于Logback-classic依赖slf4j-api.jar和logback-core.jar，所以要把slf4j-api.jar、logback-core.jar、logback-classic.jar，添加到要引入Logbac日志管理的项目的class path中.

### 创建日志对象

public static  final Logger _TESTLOG _= LoggerFactory._getLogger_(Test.class);

### LogBack日志输出位置，格式设置

- 通过logback.xml中的<append>标签可以设置输出位置和日志信息详细格式
- 一般可以设置两个输出位置文件系统或控制台
- Logback将执行日志事件输出的组件称为Appender
- 实现的Appender必须继承 ch.qos.logback.core.Appender接口,这个接口有一个doAppender方法
- Appender最终都会负责输出日志，但是他们也可能将日志格式化的工作交给Layout，或者Encoder对象。

1. 输出到文件系统配置
`<appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender"> `
2. 输出到控制台配置
`<appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">`
3. 输出格式
`<encoder>
<!--格式化输出：%d表示日期，%thread表示线程名，%-5level：级别从左显示5个字符宽度 %msg：日志消息，%n是换行符 %c代表class文件-->
<pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%-5level]  %c [%thread] : %msg%n</pattern>
</encoder>`
4. 日志编码
`<charset>utf-8</charset>`
5. 日志输出路径
`<file>D:\Project\Java\java\15_logs\data\test.log</file>`
6. 日志拆分和压缩规则
`<rollingPolicy
class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">
<!--通过指定压缩文件名称，来确定分割文件方式-->
<fileNamePattern>D:\Project\Java\java\15_logs\data\test-%d{yyyy-MMdd}.log%i.gz</fileNamePattern>
<!--文件拆分大小-->
<maxFileSize>1MB</maxFileSize>
</rollingPolicy>`
7. level:用来设置打印级别，大小写无关
```
<!--level:用来设置打印级别，大小写无关：TRACE, DEBUG, INFO, WARN, ERROR, ALL 和 OFF， 默认debug
 <root>可以包含零个或多个<appender-ref>元素，标识这个输出位置将会被本日志级别控制。
 -->
<root level="ALL">
<appender-ref ref="CONSOLE"/> //不配置只打错误日志
<appender-ref ref="FILE" /> //不记录日志
</root>
```