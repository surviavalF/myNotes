
- 这个SpringApplication类整合了其他框架的启动类，只要运行这一个类，所有的整合就完成了。

- 调用run函数，将当前启动类的字节码传入（主要目的是传入@SpringBootApplication这个注解）以及main函数的args函数。

- 通过获取当前启动类的核心信息，创建IOC容器。

