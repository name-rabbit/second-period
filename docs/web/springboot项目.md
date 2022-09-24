springboot项目

bootstrap模板

![image-20220924105403349](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20220924105403349.png)

department id departName

employee id lastName email gender departmennt birth

dao->mapper

自己造一个假的数据库 Dao层交给spring托管@Repository

![image-20220924110431050](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20220924110431050.png)

![image-20220924110835413](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20220924110835413.png)

造假的增删改查

![image-20220924111428586](H:%5CF%5Csecond-period%5Cdocs%5Cweb%5Cimg%5Cimage-20220924111428586.png)

链接：th:href="@{/css/bootstrap.css}"

文本：th:text="#{login.tip}"

提示：th:placeholder="#{login.password}"

按钮 与input输入框：[[#{login.btn}]]

国际化配置

```
<a class="btn btn-sm" th:href="@{/index.htm1(-'zh_CN')}">中文</a>
<a class="btn btn-sm" th:href="@{/index.htm1(1='en_us ' )} ">English</a>

```

1.首页配置:注意点，所有页面的静态资源都需要使用thymeleaf接管;@.页面国际化︰
1.我们需要配置i18n文件
2我们如果需要在项目中进行按钮自动切换，我们需要自定义一个组件LocaleResolver3.记得将自己写的组件配置到spring容器@Bean I

登录

密码错误  form表单的action请求 要有name

![image-20220924143958149](img/image-20220924143958149.png)

重定向

![image-20220924144412046](img/image-20220924144412046.png)

登录拦截器

在controller层把seesion.setAttribute("loginUser",username)

![image-20220924144936796](img/image-20220924144936796.png)

页面复用

th:fragment="sidebar"

![image-20220924150432213](img/image-20220924150432213.png)

激活

![image-20220924151130660](img/image-20220924151130660.png)

![image-20220924151207661](img/image-20220924151207661.png)

![image-20220924153131221](img/image-20220924153131221.png)

![image-20220924153301047](img/image-20220924153301047.png)