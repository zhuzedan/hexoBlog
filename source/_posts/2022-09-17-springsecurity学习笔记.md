springsecurity学习笔记

### 前后端交互的登录流程

![用户登录流程](https://zhuzedan.oss-cn-hangzhou.aliyuncs.com/img/%E7%94%A8%E6%88%B7%E7%99%BB%E5%BD%95%E6%B5%81%E7%A8%8B.png)

springsecurity就是一个过滤器链，内置了关于springsecurity的16个过滤器。

```java
@SpringBootApplication
public class SecurityStudyApplication {

    public static void main(String[] args) {
        ConfigurableApplicationContext run = SpringApplication.run(SecurityStudyApplication.class, args);
        System.out.println("hello");
    }

}
```

![image-20220915090018330](https://zhuzedan.oss-cn-hangzhou.aliyuncs.com/img/image-20220915090018330.png)

### 用户名密码过滤器运行机制

![image-20220915102222764](https://zhuzedan.oss-cn-hangzhou.aliyuncs.com/img/image-20220915102222764.png)

自定义登录

![image-20220915103835244](https://zhuzedan.oss-cn-hangzhou.aliyuncs.com/img/image-20220915103835244.png)

登录：

1. 自定义登录接口 调用providemanager方法，登录成功生成jwt，存入redis

	2. 自定义userdetailamanager实现类  从数据库中访问系统用户

访问资源：自定义认证过滤器

1. 获取token
2. 从token中获取userid
3. 从redis中通过userid获取用户信息
4. 村SecurityContextHolder

### JWT

jsonwebtoken，无状态登录模型

优点：不需要服务器端存session

组成：头部+载荷+签名

### 自定义登录接口

分析需求：

1. 定义一个controller登录接口
2. 放行自定义登录接口
3. 使用ProviderManager的auth方法进行验证
4. 生成自己的jwt给前端
5. 系统用户所有信息放入redis