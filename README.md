## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/DealBelinda/DealBelinda.github.io/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/DealBelinda/DealBelinda.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.

###my logback file

<?xml version="1.0" encoding="UTF-8"?>
<!-- 配置信息，每60s扫描一次，这里的debug若设置为true，则会实时打印出logback的信息，所以这里我们设置为false-->
<configuration scan="true" scanPeriod="60 second" debug="false">
    <!-- 定义参数常量 -->
    <!-- TRACE<DUBUG<INFO<WARNING<ERROR 从小到大 -->
    <!-- log的level默认值是debug -->
    <property name="log.level" value="debug"></property>
    <!-- 文件保留时间。30天 -->
    <property name="log.maxhistory" value="30"></property>
    <!-- log的totalSizeCap默认值是2GB -->
    <property name="log.totalSizeCap" value="2GB"></property>
    <!-- 日志文件的存储跟路径，catalina.base是tomcat下实例的路径 -->
    <property name="log.filePath" value="${catalina.base}/logs/mt_correction"></property>
    <!-- 日志内容的形式（格式） +执行的线程+日志级别+日志相关的信息-->
    <property name="log.pattern"
        value="%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level [%logger{50}:%line] - %msg%n%ex"></property>
    <!-- 定义5个appender，后三个将日志分为4个级别。 -->
    <!-- 控制台输出日志 -->
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>${log.pattern}</pattern>
            <charset>UTF-8</charset>
        </encoder>
    </appender>
    <!-- DEBUG -->
    <appender name="debugAppender"
        class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 过滤器,过滤掉非dubug level的信息。 -->
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>DEBUG</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
        <!-- 文件路径 -->
        <file>${log.filePath}/debug/debug.log</file>
        <!-- rolling策略 -->
        <rollingPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">
          <!-- rollover daily -->
          <fileNamePattern>${log.filePath}/debug/debug-%d{yyyy-MM-dd}.%i.gz</fileNamePattern>
           <!-- each file should be at most 100MB, keep 30 days worth of history, but at most 10GB -->
           <maxFileSize>50MB</maxFileSize>    
           <maxHistory>${log.maxhistory}</maxHistory>
           <totalSizeCap>${log.totalSizeCap}</totalSizeCap>
        </rollingPolicy>
        <encoder>
            <pattern>${log.pattern}</pattern>
        </encoder>
    </appender>
    <!-- INFO 与debug配置形式相似-->
    <appender name="infoAppender"
        class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 过滤器,过滤掉非dubug level的信息。 -->
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>INFO</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
        <!-- 文件路径 -->
        <file>${log.filePath}/info/info.log</file>
        <!-- rolling策略 -->
        <rollingPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">
          <!-- rollover daily -->
          <fileNamePattern>${log.filePath}/info/info-%d{yyyy-MM-dd}.%i.gz</fileNamePattern>
           <!-- each file should be at most 100MB, keep 30 days worth of history, but at most 10GB -->
           <maxFileSize>50MB</maxFileSize>    
           <maxHistory>${log.maxhistory}</maxHistory>
           <totalSizeCap>${log.totalSizeCap}</totalSizeCap>
        </rollingPolicy>
        <encoder>
            <pattern>${log.pattern}</pattern>
        </encoder>
    </appender>
    <!-- ERROR 与debug配置形式相似 -->
    <appender name="errorAppender"
        class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 过滤器,过滤掉非dubug level的信息。 -->
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>ERROR</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
        <!-- 文件路径 -->
        <file>${log.filePath}/error/error.log</file>
        <!-- rolling策略 -->
        <rollingPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">
          <!-- rollover daily -->
          <fileNamePattern>${log.filePath}/error/error-%d{yyyy-MM-dd}.%i.gz</fileNamePattern>
           <!-- each file should be at most 100MB, keep 30 days worth of history, but at most 10GB -->
           <maxFileSize>50MB</maxFileSize>    
           <maxHistory>${log.maxhistory}</maxHistory>
           <totalSizeCap>${log.totalSizeCap}</totalSizeCap>
        </rollingPolicy>
        <encoder>
            <pattern>${log.pattern}</pattern>
        </encoder>
    </appender>
    <!-- WARN 与debug配置形式相似 -->
    <appender name="warnAppender"
        class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 过滤器,过滤掉非dubug level的信息。 -->
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>WARN</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
        <!-- 文件路径 -->
        <file>${log.filePath}/warn/warn.log</file>
        <!-- rolling策略 -->
        <rollingPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">
          <!-- rollover daily -->
          <fileNamePattern>${log.filePath}/warn/warn-%d{yyyy-MM-dd}.%i.gz</fileNamePattern>
           <!-- each file should be at most 100MB, keep 30 days worth of history, but at most 10GB -->
           <maxFileSize>50MB</maxFileSize>    
           <maxHistory>${log.maxhistory}</maxHistory>
           <totalSizeCap>${log.totalSizeCap}</totalSizeCap>
        </rollingPolicy>
        <encoder>
            <pattern>${log.pattern}</pattern>
        </encoder>
    </appender>
    <!-- logger配置，定义日志对象 ，日志需要记录的package。需要与appender绑定 -->
    <!-- additivity =true,logger会将root下面的appender放入logger中，此项目中，会在控制台中输入相关的信息。 -->
    <logger name="com.mt" level="${log.level}" additivity="true">
        <appender-ref ref="debugAppender"></appender-ref>
        <appender-ref ref="infoAppender"></appender-ref>
        <appender-ref ref="errorAppender"></appender-ref>
        <appender-ref ref="warnAppender"></appender-ref>
    </logger>
    <!--  特殊的logger，相当于logger的父属性-->
    <root level="${log.level}">
        <appender-ref ref="STDOUT"></appender-ref>
    </root>
</configuration>

<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>jcl-over-slf4j</artifactId>
    <version>${slf4j.version}</version>
</dependency>
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>jul-to-slf4j</artifactId>
    <version>${slf4j.version}</version>
</dependency>
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-access</artifactId>
    <version>${logback.version}</version>
</dependency>

