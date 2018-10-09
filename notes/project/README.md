# 面试总结（截止20180921）

## 一、项目技术点深挖

- [x] 单点登录

  共享Redis会话服务器

- [ ] 扫码登录

  token

- [ ] 接口验证，涉及到 RESTful API 和 HTTP、HTTPS 相关

- [ ] 接口验证，这里涉及到网络安全，别拦截了怎么处理，如二次 token 等怎么做，需要深入

当用户登录成功后，返回一个由Token签名生成的秘钥信息(Token可使用base64编码和md5加密，可以放在请求的Header中)，然后对每次后续请求进行Token的封装生成，服务器端在验证是否一致来判断请求是否通过。

（1）常规的方法：用户登陆后生成token，返回客户端，然后服务器使用AOP拦截controller方法，校验token的有效性，每次token是一样的；

（2）用户登陆后生成临时token，存到服务器，并返回客户端，客户端下次请求时把此token传到服务器，验证token是否有效，有效就登陆成功，并生成新的token返回给客户端，让客户端在下一次请求的时候再传回进行判断，如此重复。 这种方法有性能问题，但也有一个漏洞，如果用户在一次请求后，还未进行下一次请求就已被黑客拦截到登录信息并进行假冒登录，他一样可以登录成功并使用户强制下线，但这种方法已大大减少被假冒登录的机会。

（3）两层token：一般第一次用账号密码登录服务器会返回两个token，时效长短不一样，短的时效过了之后，发送时效长的token重新获取一个短时效，如果都过期，那么就需要重新登录了。当然更复杂你还可以做三层token，按照业务分不同token。

- [ ] 数据库同步，线程池工作原理和设计思想，ETL
- [ ] 分布式高可用，水平拆分，垂直拆分。设计到数据一致性得问题
- [ ] 数据库分库分表，主从复制，Redis数据库缓存
- [ ] 消息队列（发布订阅），消息通信（RESTful）。可能会涉及到 Kafka、RabbitMQ
- [ ] Redis 集群部署，Master-slave 和 哨兵模式
- [ ] MySQL 数据库定时备份，这个怎么做的

mysqldump



## 二、后台核心知识点扫盲

- [ ] 线程池工作原理与设计
- [ ] 类加载机制
- [ ] 动态代理  和 Cglib
- [ ] 多并发编程怎么理解的
- [ ] 锁的类型
- [ ] 虚拟内存