## @RestController注解

当使用Spring MVC构建RESTful风格的应用程序时，@RestController注解是一个非常实用的注解。它结合了@Controller和@ResponseBody两个注解的功能，并提供了更简洁的方式来编写处理HTTP请求并返回响应的控制器。

>具体来说，@RestController注解用于标记一个类，表明该类是一个控制器，并且其下的方法都将返回数据作为响应。使用@RestController注解时，不再需要在方法上添加@ResponseBody注解，因为@RestController默认将所有方法的返回值自动序列化为响应体。

@RestController注解主要有以下特点和优势：

- **自动序列化：**@RestController将控制器类中的方法的返回值自动序列化为适当的格式（如JSON、XML）作为响应体返回给客户端。

- **省略@ResponseBody注解：** 使用@RestController不需要在控制器方法上使用@ResponseBody注解，这减少了冗余的代码，使代码更加简洁。

- **结合@Controller和@ResponseBody：** @RestController结合了@Controller和@ResponseBody注解的功能，既可以处理HTTP请求，又可以将方法的返回值直接序列化为响应数据。

- **常用于构建RESTful API：** 由于@RestController的灵活性和方便性，通常用于构建RESTful API，提供数据接口供客户端调用。

总之，@RestController注解简化了编写RESTful风格控制器的过程，使代码更加简洁和可读。它将控制器和方法的返回值自动序列化为响应体，方便开发者构建Web服务接口。

既然我们在这里提到了@ResponseBody和@Controller两个注解，我们就再来介绍一下这两个注解：

## 1.@ResponseBody

ResponseBody注解是一个在Spring框架中常用的注解，用于标识方法返回的内容应该作为HTTP响应的正文部分返回给客户端。

当我们在Spring MVC中定义控制器方法时，我们可以使用ResponseBody注解来告诉Spring将方法返回的内容直接作为响应体返回，而不是视图渲染。

具体来说，使用ResponseBody注解可以实现以下功能：

- 序列化对象：ResponseBody注解会自动将方法返回的对象进行序列化，并将序列化后的结果作为响应的主体内容返回给客户端。常见的序列化方式包括将对象转换为JSON、XML或其他格式的字符串。

- 控制响应的内容类型：通过配合在Controller方法上使用produces属性，ResponseBody注解可以指定响应的内容类型（即Content-Type头），以告诉客户端应该如何解析响应的内容。

- 自定义响应状态码：通过配合在Controller方法上使用ResponseStatus注解，ResponseBody注解可以将自定义的HTTP状态码应用到响应上。

总结来说，ResponseBody注解是用于将方法的返回值直接作为HTTP响应体返回给客户端的注解。它使得开发者可以灵活地控制返回的内容和响应的格式。

## 2.@Controller

@Controller注解的作用是将一个类标识为处理HTTP请求的控制器。这意味着，被@Controller注解标记的类可以接收并处理来自客户端的请求，并生成对应的响应。

具体来说，使用@Controller注解的类可以有以下特点：

- 处理请求：被@Controller注解标记的类中可以定义多个方法，每个方法用于处理不同的HTTP请求。这些方法被称为控制器方法(controller method)或处理器方法(handler method)。它们通常被使用@RequestMapping等注解来标识请求的URL路径和请求方法，以指定由哪个控制器方法来处理特定的请求。

- 生成响应：控制器方法通常返回一个视图(View)或一个包含数据模型的模型(Model)作为响应。视图决定了生成响应时要使用的模板以及模型数据的填充方式。而模型包含了要呈现给视图的数据。

- 处理业务逻辑：控制器类可以包含业务逻辑的处理，例如调用服务(Service)层的方法来处理请求，并对数据进行处理、封装和验证。

- 处理请求参数：控制器方法可以通过方法参数来接收请求的参数。可以使用@RequestParam注解来绑定参数名称，或通过@PathVariable注解来绑定URL路径中的变量。

总结来说，@Controller注解是用于标识类为Spring MVC框架中的控制器。被@Controller注解标记的类可以处理HTTP请求，生成对应的响应，并包含业务逻辑的处理。

## 3.杂项知识点：

在Spring MVC中，即使我们不使用@ResponseBody或者@RestController来对返回结果进行序列化，Spring MVC也会自动将其转换为JSON格式，并作为响应体返回给客户端。

这是因为在Spring MVC中，默认情况下，使用了Jackson或其他合适的库来进行对象的序列化和反序列化。当返回一个普通的对象时，Spring MVC会根据设置的消息转换器（MessageConverter）自动选择合适的转换器，将对象转换为JSON格式。