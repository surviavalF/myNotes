
[原文链接](https://www.zhihu.com/question/509707651/answer/2512335914)

首先不说Spring那一坨，咋们先来说说JavaWeb。看样子能刷到这个问题的都不是什么JavaWeb的熟手，但是至少Java基础是熟手吧？那么就仔细说说。

**JavaWeb，顾名思义就是用Java来做Web程序。那啥又是Web程序呢？那顾名思义就是运行在Web上面的程序。**

**那Web程序是啥我就不用再解释了吧？复制百度的解释：**

>“Web应用程序是一种可以通过Web访问的应用程序，程序的最大好处是用户很容易访问应用程序，用户只需要有浏览器即可，不需要再安装其他软件。”

那不就是相当于用浏览器可以访问的程序就是Web程序吗，那Javaweb就是，用Java写出来的一个可以通过浏览器来访问的程序，这就是Java web。

一边是在浏览器上，这就是客户端，Browser；一边是Java写的程序，也就是服务端，Server。

这种模式也就被叫做BS模式【Browser/Server】，当然，除了BS模式以外，还有CS模式，也就是Client/Server，这种是啥呢，就类似于QQ那种，需要安装在你电脑【或者物理机】上的软件，然后对应一个服务器，这就是CS模式。不过呢，JavaWeb搞出来的玩意儿，一般都是BS模式的应用，相当于有一个可以联网的环境，加一个浏览器就可以使用了。

---

## 其实一切的技术路线，都离不开历史的发展

### 一、JDBC是啥？

我们就来了解一下Java web这段历史是怎么发展过来的吧。那么我们现在学习JavaWeb，接触的一定就是**Servlet+JSP + JDBC**技术了。

JDBC还好说，Java Database Connectivity，就是一个用Java语言去访问数据库的技术。不会有兄弟连数据库是啥都不知道吧，不知道那该去补一补数据库的课了。

我们平时用的SQLYog，Navicat，Dbeaver那些可不是数据库，那些只是连接到数据库用的第三方软件。数据库其实核心也是一个Server，也叫数据库引擎。

**我们平时操作数据库引擎都是用上面说的那些第三方软件，在可视化的界面上手动操作。而JDBC就是，我们需要用Java语言，用编程的方式来连接数据库的引擎。**

注意哈，JDBC不是用Java去链接SQLyog，Navicat这些三方可视化客户端，而是用Java去连接类似MySQL服务器，Oracle服务器，SQL Server服务器，Click House服务器，DB2服务器......等等这种。这里稍微解释一下，免得有兄弟搞混了。

毕竟网站运行，后台的服务端是Java程序写的，Java程序运行在JVM上，JVM是基于内存运行的，只要内存一释放，数据就没了。所以某些重要或者关键的数据【就比如用户的账号密码之类，对吧？】需要转移到硬盘上存储，那么数据库就是干这个的。所以访问数据库进行数据保存，在专业和高逼格的角度上又叫数据持久化。JDBC就是通过Java去连接数据库引擎，来实现Java操作数据库的一种技术。

当然，数据库引擎不只是做数据的持久化保存，还可以对于数据库的数据进行增删改查。这点学过数据库的兄弟们都知道的吧？不会还有兄弟不知道增删改查吧？在以后我们一般简称CRUD，也就是增删改查，这里简单提一下。至于为啥要叫CRUD？答主英语不好，不知道，但是别人前辈都是这样叫的，那就这样叫吧。

### 二、Servlet和JSP是啥呢？

Servlet其实就是Service Applet的简写，翻译过来就是服务端小程序。JSP就是Java Server Pages，Java服务端页面。

那这三个玩意儿怎么完成一个JavaWeb程序的呢？其实我们想想就大概知道了：

**用户至少不可能在服务器上写代码吧，用户肯定是在浏览器上的网页里面各种点。那么用户在浏览器上的点击部分就会被转化为对于后端服务器的请求。Servlet就是来接受浏览器发过来的请求，这也是他身为服务端小程序的职责所在。然后他通过一系列业务逻辑的处理【业务逻辑这个就不确定了，不同系统有不同业务，对吧？】，比如有时候还需要去本地数据库查询数据，那么这就会用到JDBC技术。然后Servlet最后把解析完成的视图界面【HTML页面】返回给前端浏览器，然后浏览器显示给用户看，这就是JSP。**

那这时候有些靓仔就要问了，那你既然是HTML页面，那为啥不直接给浏览器运行呢？为啥还非要Java服务器，把解析好的HTML返回给浏览器显示呢？因为有些页面的数据是需要服务器这边动态渲染的。就比如，一个展示所有用户列表的页面，那些用户数据是写死的吗？那肯定不是啊，那肯定是要根据后端从数据库中查询出来的结果来动态渲染的啊，所以这就是为什么HTML页面也一定要经过后端渲染以后，然后返回给浏览器显示。

所以当时JSP，就是HTML + Java代码混着写的方式，让页面在后端被解析，里面的Java代码被数据动态渲染完成以后，成为浏览器能看懂的纯HTML以后，再通过服务器发送给浏览器显示。这样的方式，使得前后端人员联手开发，效率非常非常的低。后端如果对于JSP里面HTML的样式有意见了，自己改不来，还得让前端小伙伴来看。前端要改JSP呢，里面还耦合着一堆Java代码，前端小伙伴也看不懂，稍有不慎就会让页面中的Java代码报错，错误信息前端小伙伴还看不懂，双方都是一肚子苦水。

>所以最早最开始的时候，JavaWeb的开发，所有压力都在服务器这边，不管是JDBC的数据库查询，Servlet的请求接受，还是JSP页面在服务器的动态渲染，对于服务器压力很大。对开发人员的精神攻击也很大。

当时搞开发的后端程序员，不会点前端知识是没法做的，比如session cookie，html+css+javascript+bootstrap【一些前端组件库】，ajax异步请求等等，在那个时候，前后端协同开发效率很低，前端不懂点Java也没法写，后端不懂点前端也没法搞。

服务器又要承担接受请求，又要承担查询数据库的业务逻辑的处理，还要承担把页面渲染好返回的压力，几乎老一代的项目压力全部在后台服务器，如果代码还不进行规范的话就会看着非常混乱，难以维护，也难以扩展，这种代码被叫做屎山。所以网上经常有梗，新手你别动！这个系统就是依靠那个bug跑起来的，你一旦自作主张的优化bug，系统就崩了。

于是在这种情况下，老一辈的程序员们急需一种规范，来规范服务器端的代码。

### 三、MVC的来历

于是，顺着老一辈猴子们的期望和要求，MVC思想就出来了。MVC设计思想希望程序员对于服务器层面的逻辑进行分层管理，分为Model【这一层主要负责处理业务，包括数据库的交互】，Controller【这一层主要负责接收请求，然后根据不同情况把请求转发给不同的Model层业务组件处理】，View【这一层就专门负责处理视图在后端服务器的渲染】。

>所以MVC这种思想【注意，MVC不是一个具体的技术哈，它只是一种指导思想】，也就在那时候流行起来了。所以基于MVC的Servlet + JSP + JDBC + 一些前端知识就构成当时Java web的主要学习路线了。

**这时候的MVC就相当于是：**

- **Servlet充当MVC里面的C【Controller】，接受请求**
- **JDBC和一些业务类作为MVC里面的M【Model】，用来处理业务逻辑**
- **JSP作为MVC里面的V【View】，视图层界面，由后端把数据动态渲染上去以后返回给浏览器前端显示**

当然，JavaWeb肯定不止这三个技术，我说的是个大概，比如Web开发三大组件：Servlet Filter Lisenter等等，这个对于目前的刚入门的程序员来说，本人觉得了解就好了，不用太过精通。【就是说没必要用这些技术去做一个完整的项目，只要知道这些技术，会单独用即可】。毕竟现在也不是以前那个时代了。

---

### 四、Spring开始统一JavaWeb开发时代的开端：

前面说那么一堆，但这又和Spring有啥关系呢？

这咋们就得说说Java这语言的特性了。

JavaWeb是Java语言开发的对吧。

Java是啥语言？学过都知道，OOP的呗，面向对象为核心原理的语言。

其实不管再怎么复杂，啥封装继承多态，集合泛型反射，然后又是啥JVM JUC并发啥的，还有后面Java一大堆花里胡哨的框架和生态圈。

但是本质呢？其实离不开对象。**Java这门语言的开发，就是我们程序员在不断的封装对象，使用对象，管理对象，维护对象之间的关系，来达到我们最终目的的一个过程。**

所以回到我们的JavaWeb开发，老一辈做着做着就感觉还是很乱。明明是一个整体的项目，给搞成MVC三层，搞成三层还就算了，比如我想在Controller里面用一次Model的对象，我就得new一次【Controller调用Model前面有讲过】，我比如Controller层调用View层，我又要new一个对象。

这样new，少一点没关系，但是如果项目大起来，new对象就满天飞，这边new一个，那边new一个，Java的GC垃圾回收机制得累死，还不说随便乱new，不管空间回收的话还很容易发生内存溢出。

那咋整呢？这一个项目，里面各种对象new的满天飞，但是我们很多时候new出来就只是为了用一下这个类的对象，来调用里面的一个方法而已呀。

人多了，得找个管事儿的。

对象多了，也得找个管事儿的。

于是Spring就出来了。

**Spring是啥，他就是一个容器，干啥的？放对象的，或者说，管理对象的**

那就有人要说了，你这讲的也不靠谱啊，Spring哪里才只是一个管理对象的呢？Spring可以给Web开发提供那么多功能，比如事务管理，对象增强，自动化配置，异步调度等等。我知道，但是如果懂Spring底层的看官，你们仔细想想，这些所谓的功能是不是也离不开Spring的Bean Post后置处理机制呢？是不是离不开IOC初始化refresh里面提供的诸多扩展性方法呢？是不是离不开Spring对象增强时候所用的方法拦截器Method Interceptor，转化成拦截器链然后对切面进行增强的逻辑呢？

所以用一句话来概括Spring，就是管理对象的，对于新手来说，这样理解准没错。

但是Spring的管理对象可不是那么简单，不过新手目前那么理解就行。

相当于我们就用一个容器，来管理这个项目里面所有可能会被用到的对象。Spring把这些对象称为Bean，也就是大豆，就像是春天豆荚里面的很多大豆。

这个比喻也挺恰当，一个容器里面管理存放很多对象 = 春天的一个豆荚里面放着长着很多大豆。

那么这些对象，在项目中任何地方需要被使用到的时候，你直接从Spring的容器中拿就行了，这样就可以避免满天飞的new对象了。

**这个放对象的容器，在Spring中有一个很牛逼的叫法，叫IOC容器。** Inversion Of Control。[控制反转](https://www.zhihu.com/search?q=%E6%8E%A7%E5%88%B6%E5%8F%8D%E8%BD%AC&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2512335914%7D)，啥意思呢，就是说，以后用对象不用new，直接从我这拿就得了，这就是控制反转了呗。

再加上Spring对于这些对象【也就是Bean】的管理，Spring的IOC还可以对这些Bean的初始化，实例化，属性赋值，投入使用，销毁的时候提供很多扩展功能。这样，光是之前的一个简单的new出来的对象，在Spring的管理下都能被玩出花儿来。

所以，Spring就是一个管理对象的东西，具体就是用的IOC容器。只不过，这种能够为我们开发提供特定好处的东西，我们都把他叫框架，所以Spring框架，也就是Spring FrameWork，也就成为了后来Spring生态圈的一个基石框架。

其实有关IOC，AOP这些概念，Spring之前还有更老的EJB，那个新手了解一下这段历史就好了，不用深究，就是知道有这么个事儿就成。Spring的作者：美 Rod Johnson 还出过一本书，来直接当面吐槽EJB，当时也挺出名的：《[Expert One-on-One J2EE Development without EJB](https://www.zhihu.com/search?q=Expert%20One-on-One%20J2EE%20Development%20without%20EJB&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2512335914%7D)》

这个框架出来以后，那是叫好声一片，因为总算对于对象管理混乱的项目，有一个解决方法了。【至于Spring的AOP，具体的内容，后面说，这也是管理对象用的】

---

### 五、百花齐放——框架开发时代的来临：

继Spring推出来以后，那么比如之前的Servlet，JSP，JDBC那些也表示咋们也不甘示弱。

Spring都那么牛逼的出框架了，我们也得出一个框架。

要不然每一次写项目都要从0开始写，太麻烦。比如不用框架，每一次要始从0搭建Servlet + JSP的Web环境的头大，上一个项目的基本架构这一个新项目又要重新搞——太头痛了，这种痛只能那一带老程序员，也就是主流用Eclipse，JBulider，NetBeans得那一带才体会得到。

那咋办呢？那我们MVC这些层的技术，那也得支棱起来。

- 于是Struts就来了，为了取代以前这种原生的Servlet开发的痛苦。
- 于是Mybatis/Hibernate就来了，为了取代以前原生JDBC开发的痛苦。

那Struts到底解决了什么痛点呢？

>Struts就是取代了之前的Servlet开发模式，具体取代了啥呢？
>
>**以前，一个[Servlet类](https://www.zhihu.com/search?q=Servlet%E7%B1%BB&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2512335914%7D)对应一个请求的处理。要写一个Servlet，就必须继承HttpServlet类，然后重写里面的doGet个doPost方法，来对应get和post的请求逻辑。Servlet对应的请求的映射，还要再web.xml里面配置。在Servlet3.0以后，支持用@WebServlet注解来配置请求映射，但是还是麻烦。**
>一百个Servlet类对应一百个请求，但是一百个类看着眼睛不疼啊？
>
>在之前的[原生Servlet](https://www.zhihu.com/search?q=%E5%8E%9F%E7%94%9FServlet&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2512335914%7D)开发模式下，东一个请求西一个请求，杂乱无章。
>
>**按理说，在原生Servlet模式下的后端开发，把所有Servlet类放在一个目录下，比如都放在com.xxx.servlet下面，然后给每个Servlet都取一个合适的名字：XXXServlet，尽量见名知意多好：比如UserLoginServlet，一看就是处理登录逻辑的；UserQueryServlet，一看就是处理User数据的查询逻辑的，等等等等**
>
>可是当时总有些逆天的项目，一个大项目，Servlet到处都是。项目里面每一个路径，每一个目录下面都分散着各种不同的Servlet，而且名字还乱取。
>
>本人非常不幸的接触过一个，比如有些Servlet还好，他放在com.xxx.servlet包下面，但是名字乱取，比如明明是权限验证的，他给你取个名字，叫CheckingBusiness，这就算了。还有些更逆天的，甚至把Servlet放在[com.xx.util](https://www.zhihu.com/search?q=com.xx.util&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2512335914%7D)下面，名字还是XXXTask【某某调度任务的意思】



所以有问题吗，当然必须有，啥问题，Servlet管理太混乱，写请求路径映射太麻烦。要改，怎么改？

>所以，参照Spring的方式呗，Servlet多了，咋办，搞一个管理的。
>
>Struts就来了，他用一个配置文件，xml文件，来管理所有的Servlet。
>
>【当然，Struts里面不叫Servlet，叫Action。每一个Action，也就是Servlet，都要继承Struts里面的ActionSupport。Action可以理解为Servlet，一个意思】
>
>那么，这样一来，不管你再怎么乱写，我有一个配置文件，里面写好所有Action的路径和该Action的请求映射。那么，不管你Action放哪里去，怎么取名字，我一看这个配置文件，就完事儿，极大的方便了管理。
>
>但是在目前的时代，这种Struts框架也过时了，不推荐学习，了解即可。

那Hibernate，MyBatis之类的又解决了什么痛点呢？

>原生的JDBC开发，现在的兄弟们入门JavaWeb都必须要学习的，最开始我们查询数据库就是从JDBC来的，JDBC步骤麻烦不？每个SQL手写麻烦不？字符串拼接麻烦不？各种连接资源的释放麻烦不？
>
>没经历过都不知道，数据库连接的资源是不会被JVM的GC给自动回收的，如果不手动释放，频繁去创建，多线程访问，系统刚上线一会儿就翻车。

举个实际点的例子吧：比如，我要通过用户传入的用户名和密码去精确查询，咋写?
```java
//Controller层  
String userName = request.getParameter(xxxx)
String passWord = request.getParameter(xxxx)
XXService.queryUser(userName,passWord);//Model层，也就是Service业务层  
public XXX queryUser(){//通过一大串的代码获取到JDBC连接  
Statement s = connection.createStatement();
Stringsql="select xxx from user where userName = '"+userName+"' and passWord = '"+passWord+"'";//执行查询etc，略  
}
```


>你们就光是欣赏这句SQL，头大了没有？
>
>因为SQL里面的字符串是要自带单引号的，然后还要和Java里面的String双引号拼接。那有人说，你可以用PrepareStatement来填充啊，确实可以，但是还不是要自己手写SQL？
>
>但是比如SQL查询以后返回值到Java对象的映射，增删改对于[数据库事务](https://www.zhihu.com/search?q=%E6%95%B0%E6%8D%AE%E5%BA%93%E4%BA%8B%E5%8A%A1&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2512335914%7D)的控制，以及数据源Connection连接的手动控制，以及那一层层看着头皮发麻的try-catch等等等等，以及一定要自己亲手手写SQL的情况，这难道不是JDBC原生的缺陷？
>
>能否优化？
>
>能，Hibernate，MyBatis等全自动和半自动的ORM框架便推出了。至于他们具体是怎么实现对于JDBC的简化的，具体细节这就不属于本文的讲解范围啦，自行去了解，这两个对于JDBC进行封装的持久层框架，也是现在的学习路线。
>
>但是重点在于，他们确实简化，并且也优化了以前非常复杂并且易错的JDBC原生写法。
>
>不过现在外面企业，MyBatis这种半自动化的ORM框架用的更多一点，所以请更重点的了解一下MyBatis以及他的增强版MyBatisPlus。当然，没有MyBatisPlusProMax了....

但是一个项目要用那么多框架，每个框架都有自己的边边角角，大家一凑起来那肯定是硬碰硬谁也不服谁，那咋办呢？

这之前不是说了吗，这项目毕竟还是个JavaWeb，Java语言是大哥，再怎么支棱那也得是对象，要不然想干啥，还想上天？

所以Spring就站出来了，行，你们各有菱角，但是你们好歹最后总得是用对象来实现功能吧？那就都加入Spring的IOC容器，SpringIOC里面为你们的对象提供一个全方位的管理，想完成啥功能，直接给Spring吱一声就好了，Spring利用对于对象生命周期的[回调函数](https://www.zhihu.com/search?q=%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2512335914%7D)一全盘帮你搞定【其实底层就是PostProcess机制，目前就暂不说了】。

比如完成对象自定义增强的AOP功能，比如实现异步非阻塞功能，比如实现数据库事务控制，都可以利用IOC里面的对象的PostProcess机制来搞定。

于是这就是最早期的，框架整合式开发，SSH：Structs + Spring + Hibernate，这样搞，但是前端还是JSP在服务器渲染，始终不得劲。所以还得改，那怎么改呢？

那就要讲到下一个时代了，而这一次，是大改。但是在大改来临之前，还有一些风吹草动。

---

### 六、Spring生态圈的扩展：

同时，Spring的野心也开始大起来了，有了Spring这个老大哥作为底牌，Spring的生态圈开始不断扩展，逐渐不满足于只是做一个Web程序的对象管理了。之前我是当胶水，来耦合各个框架，现在我也想来取代这些框架了。

比如，Spring就发现了Struts的一个明显缺陷：**他只是用了一个xml来管理所有的Action，但是访问规则还是基于Servlet的，也就是一个类，对应一个请求。** 但是一个大型系统，怎么可能才数十个请求？至少也是百来计数。如果用Servlet的一个类映射一个请求这样来开发，未必也太慢，太复杂了。

所以咋办呢？

之前Servlet开发的请求处理，是在【类】的维度。现在我能不能换个想法呢？我把对于请求的处理，改变到【方法】的维度呢？

>其实之前学过Struts2的也应该知道，每一个Action里面，也是execute方法在起作用。那么SpringMVC就想，能不能让请求映射的维度下降到【类中的方法】呢？
>
>之前是：
>
>一个请求对应Struts中的一个Action，然后每个Action执行execute来处理请求
>
>现在能否：
>
>一个请求对应类中的一个方法签名，然后让这个类里面的多个方法来映射多个请求呢？
>
>答案是可以的，只需要修改一下Servlet请求映射的维度就行，之前是【一个请求映射一个类的全类名】现在是【一个请求映射一个类的全类名 + 里面一个方法的方法签名】
>
>至于还需要像Servlet时代，在一个单独的web.xml里面配置，或者Struts时代，单独在Struts.xml中配置吗？
>
>SpringMVC觉得太复杂了，他提供了一个注解：@RequestMapping

比如一段SpringMVC的代码：
```java
@RequestMapping("/xxxxxx")
public XXX abcdefg(){
	//业务逻辑...  
}
```


这就表示，该类中的abcdefg方法，映射来自前端的xxxxxx请求。

在这种设定下，SpringMVC就这样推出了。

历史证明，他成功的取代了Struts。SpringMVC是Spring Framework在Controller层一共的一套完整的解决方案。在历史的发展中，Controller层经历Struts、WebWord、Struts2等诸多产品更迭之后，迄今为止，SpringMVC仍然是JavaWeb开发的Controller层开发的首选技术方案

当然，未来或许还会有更好的框架来取代SpringMVC，但是从现在来看，或许难以下定数，毕竟在目前的时代，Spring生态圈几乎已经统一了整个JavaWeb开发的技术栈了，任何在JavaWeb开发中遇到的技术性问题，Spring生态圈中总是能找到一套相应的解决方案。比如数据库的Spring Data JPA，权限控制的Spring Security，批处理框架Spring Batch，还有目前最主流的快速开发框架Spring Boot，分布式微服务一站式处-理框架Spring Cloud等等等等........发展成现在，Spring生态圈在JavaWeb开发这方面的地位几乎没法动摇了。

---

更新一下，收看官老爷提醒，有个SpringWebFlux的东西，是Spring5推出来的，感觉有点抢SpringMVC的饭碗。属于是Spring自家神仙打架了

---

当然，SpringMVC能够迅速成为JavaWeb的MVC思想中，Controller层的首选，也不是没有原因的：

- 第一点，也是最重要的一点，他的父辈，Spring FrameWork给他打下了最坚固的江山，再加之他本来就是Spring生态圈的产品，于Spring的整合程度不是一般的高，也很简便，几乎不用开发者做什么太复杂的操作，也不会出现其与框架整合Spring的时候出现的奇奇怪怪的bug。
- 他本身的，对于请求处理的实现维度，从Servlet时代的【类】，降低到了【方法】，这样使得大型系统，请求再多也会没有那么复杂，可以通过不同类划分多种类请求【比如SysUserController里面所有方法就处理所有对于SysUser的请求】。
- 性能本身就很强，适合目前大型和超大型系统的开发
- 但是也不离开历史发展的根本，其底层还是Servlet的支持，学过SpringMVC的兄弟们都应该知道，SpringMVC底层基于DispatcherServlet，这个DispatcherServlet对于所有请求和响应都做了极大的支持和简化，再配合处理器映射（handlerMapping), 处理器适配器（HandlerAdapter), 和视图解析器（ViewResolver），能够为我们的开发提供很大的便利。
- 视图解析器也不是只支持JSP，还支持多种其他视图技术，对于视图层的兼容性也有很好的支持。

光说没用，那你说，举个例子看看呗，行，那我们就举个例子看看：

```java
//之前Servlet时代获取请求参数【简写】  
protecteddoGet(request,response){
	String xxx = request.getParameter(xxx);
	String yyyy = newString(request.getParameter(yyy).getBytes("ISO-8859-1"),"UTF-8")
	
	Object obj = request.getParameter(xxx);
	if(obj!=null){
		if(obj.getXXX() != nul){
		//.......  
		}//获取Session  
		request.getSession()
		//.....  
	}
}

```


用过Servlet开发的小伙伴才知道，之前的乱码处理，JSON格式化，参数校验，那个玩意儿简直了，虽然可以用Filter和Listener，但是方法参数一多简直就是酸爽，，，

那么SpringMVC呢？

```java
//还是获取参数  
@RequestMapping("/xxxx")//不返回视图只返回数据就用@ResponseBody，返回String直接跳转View视图  
public XXX xxxx(HTPServletRequest request,String xxxx,String yyyy，ModelMap mmap,HTTPSession session,@Validated Object obj){//....  
}
```


之前那些疑难杂症解决了，通过参数名匹配，SpringMVC可以自动把请求那边的数据接收过来，中文还会转码【因为网络传输中编码是ISO-8859-1】，还可以随便的获取到request，session等对象，还支持注解直接入参校验。

这还不是他强大的原因吗。

于是，慢慢的，SSM架构开始流行了，SpringMVC + Spring + MyBatis。

**那可能有靓仔就要问了，那SSM和MVC有啥关系呢？SpringMVC和MVC又有啥关系呢？Spring和SpringMVC又有啥关系呢？**

>能问出第二个和第三个问题的都是人才。作者在此提出表扬。
>
>Q1：先来回答第一个问题，SSM和MVC有啥关系？
>
>A1：SSM指的是三个框架的整合开发，SpringMVC + Spring + MyBatis。MVC只是一种思想，是一种前人帮我们总结出来的，能够大幅提升后台代码质量的规范。当然，你不遵守，又有什么关系呢？
>
>在MVC【Model-View-Controller】的思想指导下，SpringMVC框架充当Controller层，用来接收请求和处理请求；MyBatis这个持久层框架和一些被Spring管理的业务类，作为Model层，负责请求分发过来以后，业务的处理和数据的持久化操作；JSP或者是其他的视图技术，作为View层，这就不多说了。
>
>所以一般我们后面都会把后台分为Controller【或者Provider】 - Service - DAO三个包，下面放各种Java文件。但是这三个包不是对应的MVC，我也说了，具体来说应该是：
>
>1、Controller包，使用的框架是SpringMVC，对应MVC的Controller。
>
>2、Service和DAO层，Service就是一些Java文件，使用SpringIOC来管理，DAO使用的框架是Mybatis，对应MVC的Model
>
>3、视图层，JSP，对应MVC的View。

>有靓仔又要问了，说你这Service和DAO是啥。Service一般就是我们手动创建的业务类，这些类的对象会被Spring管理，每当请求来了以后，比如一个请求要用到UserService和SysLogService，Controller层就会从Spring的IOC里面找到这两个Service对象，然后把请求分发给业务处理即可。
>
>业务一般会涉及到数据的数据库持久化，那么就会访问数据库，访问数据库的操作我们一般也封装为一层，叫做DAO层，这一层就是MyBatis框架实现的。DAO就是Data Access Object，数据访问对象，通过这一层和数据库交互。当然，有些业务不需要涉及到和数据库的交互。那么我们的Service，也就不一定会用到DAO。
>
>注：DAO后面开发中我们更倾向于称为Mapper，比如之前的UserDAO，我们一般在后面开发中喜欢叫做UserMapper，Mybatis中也是这种叫法。
>
>所以，Service和DAO，也就是我们自己写的业务组件 + MyBatis，共同组成了MVC思想中的，Model层。
>
>Spring还是老大哥，永远的粘合剂，他在三层都有大用处，但是他不属于任何一层。
>
>Q2和Q3的人才们，让评论区老哥为你们解惑吧。作者溜了。

**从这时候开始，一般我们的开发模式就从之前的原生技术开发转化为框架整合开发了：SSH或者SSM：Spring + Struts + Hibernate/Spring + SpringMVC + MyBatis。视图层都是JSP或者其他服务端渲染技术。**

**注意，目前还是服务端渲染技术，相当于页面还是基于服务器端渲染的。**

风吹草动也快结束了，于是下一个时代的改革，开始了。

---

### 七、前后端新思维的来临：

那么随着时代进步，虽然MVC体现出了诸多的架构优势，但是还是敌不过压力全部集中在服务器这边，一旦网站大起来以后，所有请求，所有业务处理，所有前端动态渲染全部在服务器这边完成，当然，这就成为了明显的一个系统性能的瓶颈了。那么接下来咋办呢？

这不是浏览器啥活都没怎么干呐，就只是显示一个后端渲染好的HTML页面即可。

>OK，之前服务器端代码逻辑混乱，项目中各个对象难以管理，原生开发问题颇多，这些全都解决了：逻辑混乱，那就MVC思想的架构来安排；各个对象难以管理，那就用Spring的IOC来整治；原生技术开发局限性大，那就框架整合来搞。

但是后端压力还是大呐？JSP这个玩意儿还是像以前一样，HTML + Java混合写，然后后端渲染完成，把JSP变成一个彻底的HTML以后交给前端浏览器显示。之前的Servlet + JDBC + JSP，各种沧海桑田的变化，什么MVC，SSH，SSM啥的，但是JSP就是找不到一个改变的方法。

那就有天才要想了，不就是数据渲染吗？我浏览器那么牛逼，什么Js的V8引擎，放着白来的性能不用，让服务器那边受苦受累，他在这里被用户用着风光无限？

那肯定不行，要给你点活干

干啥活呢？以后后端渲染页面这一步交给你了。我们后端就只负责处理数据了，数据后端丢给浏览器，后端不管了，撤手了，至于你浏览器爱怎么用这些数据，和我后端服务器啥关系？没关系

好了，这下前后端就彻底分离开了。

>前端就主要负责写页面了，至于那些需要被后台数据给动态渲染的地方呢？那就到时候用到了以后，给后端发请求呗，找后端要数据去。要来了数据就动态渲染就行了。
>
>反观后端呢？后端这下甩掉了一个活儿，轻松了，这样后端就只负责接受请求，然后处理请求，查询数据库，处理数据，然后把前端想要的数据返回就行了，至于数据怎么渲染？那也我和后端没关系了。
>
>相当于之前页面都是在后端通过数据进行动态渲染以后发给前端浏览器显示的模式，逐渐演化为，希望后端只是负责处理数据，然后把数据返回给前端，由前端浏览器动态渲染的模式了

那么数据的格式呢？我请求里面的某些参数要通过前端发给后端，然后后端解析以后进行相关CRUD的业务操作；后端的响应数据要发给前端，然后前端解析数据以后，开始动态渲染页面。

也就是说，现在前端需要数据就给后端发Request，后端处理完成以后就给前端反馈Response，但是Request和Response都无可厚非的不可避免地要携带很多业务数据，那这个数据的交换格式总要有个规范吧？也就是说，我总要有一种大家都认可的数据交换格式吧？比如数组该怎么表示，时间该怎么表示，对象该怎么表示。

>于是这时候，JSON这种轻量级的数据交换格式，（JavaScript Object Notation, JS 对象简谱) ,就发挥了他的特点了,也成为了目前前端后开发，甚至是网络中，数据交互的一种非常常用的格式了。
>
>JSON与传统的XML格式相比，有啥优点，还有JSON有啥特点，这个就不具体展开讲了，但是JSON是Web后端开发学习路线中必学的，一种轻量级的数据交换格式。
>
>技术介绍讲究点到为止，至于具体细节，期待各位了解学习以后再做深究。

这种思想和MVC差不多，前后端分离，那么技术实现呢？？

总要有个技术落地吧？前后端分离的思想和MVC一样，只是个思想，MVC思想下的实现很多，什么Servlet + JSP + JDBC，SSH + JSP，SSM + JSP。

咋办呢？

于是有天才就提出了，那JSP的缺陷是啥？最大的缺陷其实都还不是服务器端渲染，毕竟只要给服务器做集群【就是很多个服务器，就叫集群】，然后给每个服务器多插几根内存，还是可以解决的。

那最大的问题，也是最大的痛点是啥？

开发人员的精神攻击，之前有说过。这个问题在原生的Servlet + JDBC + JSP时代就一直延续下来了，也对于前后端联调造成了很大的困扰。

那咋办？改呗。咋改？

我之前JSP写出来的页面是xx.jsp。这些页面根本没法直接像xx.html一样在浏览器打开，要去访问这些JSP文件，还必须启动服务器，通过Servlet来动态渲染。或者后端开发来手动替换前端小伙伴写好的HTML。

这也就是为啥最开始的时候，JavaWeb路线要推荐后端开发的人必须要会一点前端知识的原因。

>那么能不能这样呢？我给出一种技术，写出来的还是xxx.html，能够直接在浏览器打开，让前端小伙伴直接利用浏览器调试。那么涉及到数据渲染的地方呢？
>
>我不像JSP用JSTL标签，比如c:forEach这种标签来做了。这些标签不属于HTML规范，无法被浏览器解析。
>
>那么我利用HTML标签的属性呢？就算不存在该属性，浏览器确实会无视，但是不影响运行呀。

相当于这种
```html
<table th:forEach ="...">
</table>
```


属性识别不了，但是可以直接不经过服务器，就给浏览器解析显示出来，前端就直接能够调试页面样式了。

于是ThymeLeaf就出来了。他写出来的页面，就是xxx.html，不经过后端，就可以直接被浏览器解析。只不过有些地方的数据，没有后端的返回，无法渲染，但是不干涉整体页面的显示效果。要想真正显示出页面，那还是要经过后端Controller层返回的数据，在服务器动态渲染。但是这样已经使得前后端分离了一部分了，但是还是没那么彻底。毕竟事情还是需要经历一个过程嘛。

ThymeLeaf这种就被称为[模板引擎](https://www.zhihu.com/search?q=%E6%A8%A1%E6%9D%BF%E5%BC%95%E6%93%8E&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2512335914%7D)。这出来的模板不经过后端渲染也可以运行，这样至少方便了前端小伙伴调试页面的问题。至少对于前后端开发的精神攻击少很多了。

也别担心学习成本，熟练使用JSP，特别的EL表达式的话，Thyme leaf分分钟上手。

---

### 八、Spring生态圈统一JavaWeb开发的时代：

前后端闹矛盾的时代，在模板引擎出世以后，已经减少很多了。

虽然说此时页面还是在服务端渲染，但是给服务器多插几根内存条，还是能解决的。前后端联调时候已经比JSP时代要轻松不少了。

但是SSM的后端架构还是有抱怨声。啥情况，还不满意？

确实，写过SSM开发的小伙伴知道，那个配置，简直被称为配置地狱也不过分。

Spring要去整合SpringMVC和Mybatis等等其他框架，还可能要整合三方框架。我们之前都说过了，Spring就是利用IOC来管理这些对象的，这些对象也被称为Bean。

那么问题来了，我怎么让Spring知道这个类的一个对象是一个Bean呢？

在最早期，Spring只能用XML的方式来配置：
```xml
<beans>
<bean>
//.....
</bean>

<bean>
//.....
</bean>

</beans>
```

这才是两个Bean的写法，如果Bean一旦多起来，并且Bean之间还有依赖关系【比如A对象作为B对象的一个属性，B对象又需要A对象作为属性，这种情况怎么解决？】【比如A对象作为B的属性，B对象又作为C的属性，然后我还要对C里面的其他属性进行默认赋值等等】，这样的写法将会非常复杂，看着眼睛都疼。

这样有些兄弟又要说了，着看着也没啥啊，不就是配置两个Bean吗，来，给你看看一个还不算复杂的基本SSM项目里面的配置：

```xml
Springmvc配置文件  
ajax.post的url${pageContext.request.contextPath}  
xml配置如下：  
<!--1.注册DispatcherServlet--><servlet><servlet-name>springmvc</servlet-name><servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class><!--关联一个springmvc的配置文件:【servlet-name】-servlet.xml--><init-param><param-name>contextConfigLocation</param-name><param-value>classpath:springmvc-servlet.xml</param-value></init-param><!--启动级别-1--><load-on-startup>1</load-on-startup></servlet><!--/ 匹配所有的请求；（不包括.jsp）--><!--/* 匹配所有的请求；（包括.jsp）--><servlet-mapping><servlet-name>springmvc</servlet-name><url-pattern>/</url-pattern></servlet-mapping><!--过滤器--><filter><filter-name>encoding</filter-name><filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class><init-param><param-name>encoding</param-name><param-value>utf-8</param-value></init-param></filter><filter-mapping><filter-name>encoding</filter-name><url-pattern>/*</url-pattern></filter-mapping>MVC拦截器配置  
<mvc:interceptors><mvc:interceptor><mvc:mappingpath="/**"/><beanclass="com.xxx.config.MyInterceptor"/></mvc:interceptor></mvc:interceptors>Spring整合SpringMVC  
<!-- 自动扫描包，让指定包下的注解生效,由IOC容器统一管理 --><context:component-scanbase-package="nuc.ss.controller"/><!-- 让Spring MVC不处理静态资源 --><mvc:default-servlet-handler/><!--注解驱动，以使得访问路径与方法的匹配可以通过注解配置--><mvc:annotation-driven/><!--乱码过滤器--><mvc:annotation-driven><mvc:message-converters><beanclass="org.springframework.http.converter.StringHttpMessageConverter"><constructor-argvalue="UTF-8"/></bean><beanclass="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter"><propertyname="objectMapper"><beanclass="org.springframework.http.converter.json.Jackson2ObjectMapperFactoryBean"><propertyname="failOnEmptyBeans"value="false"/></bean></property></bean></mvc:message-converters></mvc:annotation-driven><!--json乱码解决--><mvc:annotation-driven><mvc:message-convertersregister-defaults="true"><beanclass="org.springframework.http.converter.StringHttpMessageConverter"><constructor-argvalue="UTF-8"/></bean><beanclass="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter"><propertyname="objectMapper"><beanclass="org.springframework.http.converter.json.Jackson2ObjectMapperFactoryBean"><propertyname="failOnEmptyBeans"value="false"/></bean></property></bean></mvc:message-converters></mvc:annotation-driven><!-- 视图解析器 --><beanclass="org.springframework.web.servlet.view.InternalResourceViewResolver"id="internalResourceViewResolver"><propertyname="prefix"value="/WEB-INF/jsp/"/><propertyname="suffix"value=".jsp"/></bean><!--文件上传配置--><beanid="multipartResolver"class="org.springframework.web.multipart.commons.CommonsMultipartResolver"><!-- 请求的编码格式，必须和jSP的pageEncoding属性一致，以便正确读取表单的内容，默认为ISO-8859-1 --><propertyname="defaultEncoding"value="utf-8"/><!-- 上传文件大小上限，单位为字节（10485760=10M） --><propertyname="maxUploadSize"value="10485760"/><propertyname="maxInMemorySize"value="40960"/></bean>Mybatis配置：  
<?xml version="1.0" encoding="UTF-8" ?><!DOCTYPE configuration  
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"  
  "[http://mybatis.org/dtd/mybatis-3-config.dtd](http://mybatis.org/dtd/mybatis-3-config.dtd)">
  <configuration><environmentsdefault="development"><environmentid="development"><transactionManagertype="JDBC"/><dataSourcetype="POOLED"><propertyname="driver"value="${driver}"/><propertyname="url"value="${url}"/><propertyname="username"value="${username}"/><propertyname="password"value="${password}"/></dataSource></environment></environments><mappers><mapperresource="org/mybatis/example/BlogMapper.xml"/></mappers></configuration>

```


上面光就是Spring整合SpringMVC还有Mybatis的配置，还不说其他的三方整合。这下你还觉得简单吗？还没加Maven的pom依赖那些的。

每一个项目其实这些东西配置都差不多，但是大同小异。

而且项目就算开发好了，还需要打成war包，发布到Tomcat执行，那地方也是一堆配置，SSM就光是XML配置，新手都很劝退。

**我们想想，为什么需要那么多配置？**

>答案很简单，Spring要整合这些三方框架啊。首先，Java是啥语言？OOP的呗，不管是再怎么花里胡哨的三方框架，只要想在Java web后端项目里面发挥作用，那必须都是利用这个三方框架提供的核心对象，然后用这些核心对象的某些方法来实现三方框架的功能，这点没问题吧？
>
>那么要被Spring整合，肯定就需要把这些核心对象给初始化好，然后交给Spring的IOC容器进行管理，这不就是所谓的整合了吗。
>
>到这都没问题的话，所以现在知道我们为什么写那么多配置了吧？
>
>就是初始化这一个一个三方框架的核心组件对象，然后交给Spring的IOC管理啊！比如像我要用Mybatis，让他和Spring三方整合，那我是不是至少要一个数据库连接对象？要不然我Mybatis如何创建SQL Session呢？都不能连接数据库，所以Mybatis如何发挥作用呢？对吧

那既然大家整合某些三方框架都差不多，配置也是大同小异，那我能不能和大家协商，比如针对SpringMVC和Spring的整合，**我们首先约定好，某些对象**【比如SpringMVC中的文件上传解析器，Json解析，中文乱码处理器等等】**我们给出一个默认的配置。然后我们按照我们的公约，给你自动把这些核心组件的对象加入IOC当中**。

当然公约，是大多数项目整合三方框架时候的共性。对于每个不同的项目，肯定也有自己配置的特性。那么你如果要自定义修改某些公约的配置，你在哪里改呢？可以这样呗，**我在外部提供一个固定的配置文件**，比如就叫application.properties或者application.yml（yml是一种特殊的格式）文件。**你要是有自己想定义的配置，你去那里定义即可，覆盖原来的公约配置，完成自定义整合。**

这便是核心思想，约定大于配置。（自动化配置）

于是时局造英雄，大势所趋，大浪淘沙。

谁来了？看问题，和答主已经讲过的技术，猜都能猜到。

### 九、Spring Boot问世：

SpringBoot，这个框架，不是取代Spring，而是基于Spring，简化了Spring与其他任何框架整合的难度，核心思想也就是一点：**约定大于配置**。里面可以通过自动化配置的方式来大幅度简化一个Web应用程序的开发，并且自带Tomcat，不用像以前SSM那样打成war包然后部署到tomcat的webapps下面。

**SpringBoot把很多的场景都抽象为启动器【starter】，比如你要想快速搭建一个Web场景的应用，你只需要导入spring-boot-starter-web的Maven依赖即可，一切都是自动化配置好的，也就是约定大于配置，也就是说，你甚至可以0配置直接开发，专注你的业务逻辑。**

比如你希望启用定时调度功能，导入spring-boot-starter-quartz即可；启用入参检验，导入spring-boot-starter-validation即可；启用单元测试，导入spring-boot-starter-test即可；启用阿里[数据库连接池](https://www.zhihu.com/search?q=%E6%95%B0%E6%8D%AE%E5%BA%93%E8%BF%9E%E6%8E%A5%E6%B1%A0&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22answer%22%2C%22sourceId%22%3A2512335914%7D)，导入druid-spring-boot-starter即可；启用MybatisPlus框架，导入mybatis-plus-boot-starter即可；启用缓存Redis，导入spring-boot-starter-data-redis即；启用WebSocket服务时，导入spring-boot-starter-websocket就可以了，等等等等

Spring Boot自带很多starter，你懂了Spring Boot自动配置原理以后，你甚至可以封装属于你自己的starter。很多starter对应很多Web开发的场景，然后通过导入这些starter来启用自动化配置。当然，你要是对于约定配置不满意的话，你还是可以在一个外部配置文件里面更改你想要的配置信息，就如同上文所说，Spring Boot提供了application.properties(yml)文件，可以供你修改原有的默认配置信息。

还支持多环境profile，相当于你还可以写application-dev作为开发环境的自定义配置，application-test作为测试环境的配置，application-pro作为生产环境的配置。只要你用-Dspring.profiles.active指定了某个环境以后，跑你的项目，那么具体的配置文件将被激活，非常强大而且实用的功能。

诸如此类

---

但是这时候估计又有靓仔要问了，你这些Spring Boot的starter，又和Spring有啥关系呢？

>前面说了，Spring Boot就是为了简化其他框架和Spring整合开发的时候，那些繁琐的配置。
>
>其实你想想，我们Spring和三方框架整合，不就是利用Spring的IOC容器来管理那些三方框架里面实现核心功能的对象吗？然后利用Spring的AOP来对于IOC中的对象的功能进行无侵入式增强，实现功能扩展，对吧？
>
>AOP的概念，后面我给个链接说说。
>
>那么为什么Spring Boot里面你导入starter以后，就给你自动化配置好了呢？
>
>想想也知道，既然我们会导入某个环境的Starter，肯定就希望Spring自动和这个环境进行快速整合，然后我们几乎不用配置，就可以在项目中随便用了。
>
>那么纠其原理，肯定是导入starter以后，Spring默认去初始化了一些该框架的核心功能的组件作为Bean，然后加载入IOC中。
>
>说细点，肯定是导入starter以后，就会去加载一个地方的文件【其实核心就是META-INF/spring.factories文件，现在不详细展开了】，该文件中保存着整合该三方框架时候需要的所有核心对象。然后SpringBoot就会尝试初始化这些对象，并初始化成功完成以后加入到底层的IOC容器中。有一些核心对象的初始化由于有公约，可以直接初始化以后加入IOC——但是有一些，例如数据库连接对象，学过JDBC都知道，要初始化该对象，肯定需要数据库url，用户名，密码等等，这些配置只能我们手动在外部指定，和外部你写的配置文件绑定。
>
>然后Spring Boot就会通过这些配置，把那些场景下会用到的核心对象初始化完成，并且自动的加入IOC容器中。

这样，就给你一种感觉，好像就是导入了Starter以后，然后就可以直接在项目里面用了。 其实也离不开Spring的IOC，Spring Boot只是帮你做了一个自动化配置而已，核心思想也就是： 咋们对于任何三方框架的整合，约定大于配置，因为有了一个公约，Spring Boot才可以帮你自动配置，对吧，这也就是starter的一个浅薄理解。熟悉以后，你可以自己制定属于你的starter，你可以来指定：spring和该三方框架整合以后，如何初始化。

Spring Boot程序还集成了内部的Tomcat，这就意味着你可以把一个Web程序打包成一个可执行的jar包，然后在任何位置，java -jar xxxx.jar即可启动该Web程序，非常的方便。

Spring Boot有个问题，他不再支持JSP了。毕竟也不是以前的时代了，但是还是不能否定JSP对于JavaWeb这么多年的贡献，作为学习者，这一门坚持了那么久的技术，肯定还是有可学之处，只不过，他现在确实是过时了。**Spring Boot官方推荐已经开始使用模板引擎了，比如Thymeleaf，但是要用，别忘了也要导入starter哟**。

可以说，Spring Boot的强大力量，正是目前Spring生态圈能统一Java Web开发的理由。

Spring Boot那么强大，也不是一天能做出来的。没有Spring的IOC容器，没有Spring的对象生命周期管理，包括Spring的AOP功能，哪里有Spring Boot这种优秀的Web开发框架呢？可以说现在，Spring Boot已经变成了新手阶段学习Java web的终点，也是一个JavaWeb进阶的新起点。

>当然，Spring Boot也不是完美的，任何框架都有缺陷，Spring Boot也不例外。底层基于Spring，Spring基于Java，对于不了解Spring就直接上手Spring Boot的玩家来说，非常的难以理解底层运作规律。
>
>这样的结果就是导致，如果Spring Boot程序报了任何错误的话，没有Spring基础的新手，几乎靠百度或者StackOverFlow，Bing等，很难解决问题，解决的效率也很低。
>
>1、而且Spring Boot的自动化配置，很多东西的配置都是底层帮你做完了，作为新手如果不懂Spring Boot怎么实现自动化配置的，怎么自定义你自己的配置，全部用默认的配置，就知道几个AutoWired，RequestMapping的注解就开始使用Spring Boot的话，也就和直接把系统发布到服务器而不懂JVM调优一样，属于是不研究飞机结构和飞行轨道检测就直接起飞，结果就是分分钟坠机。
>
>2、而且学习成本太高，虽然号称简单，但是不懂底层原理，那也是完全没法胜任企业化开发的【个人学习开发也会被奇奇怪怪的bug卡的难受，比如循环依赖，自动注入失败，等等等等问题】，不知道怎么解决，怎么debug看方法栈去看底层的话，一旦访问就是满屏报错，实打实的新手噩梦了属于是。
>
>3、而且对于新手来说，一旦项目导入的starter变多，Maven依赖一旦变得复杂，很容易导致部分配置不可控的情况，甚至说比如有些功能，我都不知道我在哪里配置了但是他居然生效了的情况发生。

---

题主的问题回答也就结束了，从JavaWeb，到Spring FrameWork，到SpringMVC，到Spring Boot。

如果看官耐心能看到这里，相信也是不需要再去问任何学习路线了，毕竟，一切的学习路线，都是适应于技术历史的发展。技术的发展，其实本质上还是来源于人的懒，也来源于人的智慧。历史的书写，也来自技术的更迭。

说不定各位看官以后就是取代Spring Boot的创造者的一员呢？

### 十、前后端彻底分离的时代：

Spring Boot一经推出，后端开发得到了极大的便利，不过在以前，前端工程师为什么会处于后端工程师的鄙视链下面呢？

只是在以前哈，现在的前端早就变了天了。

以前在后端眼中，前端就是写写页面，偶尔玩一下JS，改改CSS的人，所以在鄙视链下面hhh

当前后端分离的概念推出来以后，前端就一直在思索，能不能彻底的告别后端，自己单开一个项目？毕竟像Thyme leaf那些，页面也是写在后端项目里面的。

于是前端项目化的风潮就来了，答主也不是前端从业人员，但是明显知道现在前端的要求，早就比以前的高的多了。

现在是Vue，React，Angular三大JS框架在前端三分天下，目前国内 Vue使用率占比多一些，是国人尤大佬开发并且免费开源的，文档也维护的很不错。

所以现在的主流开发模式已经转化为，前端单独一个前端项目，后端单独一个后端项目，前后端通过接口来进行数据交互，交互格式就是前面说的JSON。

前端处理用户操作逻辑，向后端接口发送请求获取数据或者响应。然后前端也可以存储一些数据【相当于一些操作状态】，但是没法涉及到持久化，毕竟没有数据库。用Vue的技术栈来说就是：

Vue【基于JS的MVVM基础框架】 + Vue-Router【前端路由】 + Vuex【状态管理】 + Axios【网络请求】

React和Angular的答主就知道的不是很多了，但是估计和Vue这种形式大同小异。像前端什么ES6语法规范，Promise回调啥的，答主也是一知半解，了解过一点，就不拿出来说了，毕竟这也不属于JavaWeb的学习路线了，有兴趣去了解一下前端也好，这样和前端对接时候会更方便一点。