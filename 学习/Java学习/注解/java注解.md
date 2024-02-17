了解java注解以及记住几个常用注解

- @Override：检查该方法是否是[[重写]]方法

- @Service：标注于业务层，将一个类自动注册到Spring容器

- @Resource：用来实现实例的引用依赖的注入

- @Target：声明作用域

- @ Retention：用来定义该注解在哪一个级别可用，在源代码中(SOURCE)、类文件中(CLASS)或者运行时(RUNTIME)。

- @ApiResource@GetResource@PostResource:框架作者自定义注解，作用是声明访问地址

- @SpringBootConfiguration：装载配置文件

- @EnableAutoConfiguration：启动配置文件的开关

- @Documented：此注解会被javadoc工具提取成文档。

- @ResponseBody：把返回值按照xml或者JSON格式输出[[@RestController#1.@ResponseBody]]

- [[@RestController]]：它结合了@Controller和@ResponseBody两个注解的功能，并提供了更简洁的方式来编写处理HTTP请求并返回响应的控制器。

- [[@SpringBootApplication]]：它是Spring Boot中的核心注解之一，它简化了配置和启动Spring Boot应用程序的过程。通过使用@SpringBootApplication注解，开发人员可以方便地启用自动配置、组件扫描和构建一个可运行的Spring Boot应用程序。