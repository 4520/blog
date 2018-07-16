---
layout: post
title: spring boot部署中一个斜杠引发的血案
date: 2018-02-06 23:34:18
tags:  ['spring-boot', 'thymeleaf']
---

### org.thymeleaf.exceptions.TemplateInputException

![美丽的火烈鸟](https://blog.xlinyu.com/assets/images/2018-02-06/2015011809154211067.jpg)



本地开发环境没有任何问题，但是打成jar部署到服务器时，就出现异常信息了，以为没有把模板文件打入到jar中，可以通过``jar xvf spring-boot-thymeleaf-0.0.1-SNAPSHOT.jar ``查询jar中的内容，可以看到我们的模板文件。

<!-- more -->

![jar中的文件内容](https://blog.xlinyu.com/assets/images/2018-02-06/20180207000230.png)

**后台异常信息**

```tex
2018-02-06 23:06:39.547 ERROR 13904 --- [p-nio-80-exec-1] o.a.c.c.C.[.[.[/].[dispatcherServlet]    : Servlet.service() for servlet [dispatcherServlet] in context with path [] threw exception [Request processing failed; nested exception is org.thymeleaf.exceptions.TemplateInputException: Error resolving template "/index", template might not exist or might not be accessible by any of the configured Template Resolvers] with root cause

org.thymeleaf.exceptions.TemplateInputException: Error resolving template "/index", template might not exist or might not be accessible by any of the configured Template Resolvers
        at org.thymeleaf.TemplateRepository.getTemplate(TemplateRepository.java:246) ~[thymeleaf-2.1.6.RELEASE.jar!/:2.1.6.RELEASE]
        at org.thymeleaf.TemplateEngine.process(TemplateEngine.java:1104) ~[thymeleaf-2.1.6.RELEASE.jar!/:2.1.6.RELEASE]
        at org.thymeleaf.TemplateEngine.process(TemplateEngine.java:1060) ~[thymeleaf-2.1.6.RELEASE.jar!/:2.1.6.RELEASE]
        at org.thymeleaf.TemplateEngine.process(TemplateEngine.java:1011) ~[thymeleaf-2.1.6.RELEASE.jar!/:2.1.6.RELEASE]
        at org.thymeleaf.spring4.view.ThymeleafView.renderFragment(ThymeleafView.java:335) ~[thymeleaf-spring4-2.1.6.RELEASE.jar!/:2.1.6.RELEASE]
        at org.thymeleaf.spring4.view.ThymeleafView.render(ThymeleafView.java:190) ~[thymeleaf-spring4-2.1.6.RELEASE.jar!/:2.1.6.RELEASE]

```

**项目结构如下图**
![工程结构](https://blog.xlinyu.com/assets/images/2018-02-06/20180206233431.png)

**问题代码**

```java
@Controller
@RequestMapping(value = "/demo")
public class DemoController {

    @GetMapping(value = "/01")
    public String index_01(){
        return "/demo/01";
    }

}
```

仔细排查后发现是``return "/demo/01";``这行代码多了个``/``，去掉``/``搞定。

### 示例代码

[https://github.com/ncc0706/spring-boot-demos/tree/master/spring-boot-thymeleaf](https://github.com/ncc0706/spring-boot-demos/tree/master/spring-boot-thymeleaf)
