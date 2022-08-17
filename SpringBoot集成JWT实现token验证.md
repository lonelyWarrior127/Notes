# SpringBoot集成JWT实现token验证

全称是Json web token。它将用户信息加密到token里，服务器不保存任何用户信息。

服务器通过使用保存的密钥验证token的正确性，只要正确即通过验证。

【优点】

1. 简洁：通过URL、POST参数或者HTTP header发送。因数据小，传输速度快
2. 自包含：负载中可包含用户所需要的信息，避免多次查询数据库
3. 跨语言：token是以JSON加密的形式保存在客户端，原则上任何web形式都支持
4. 不需要服务端保存会话信息。特别适用于分布式微服务

【缺点】

1. 无法作废已颁布的令牌
2. 不易应对数据过期

### 1 JWT消息构成

token = 头部 + 载荷+ 签证。

三部分之间用.号做分隔

<img src="https://img-blog.csdnimg.cn/img_convert/e09666b21315063aac3363de97d2a21b.png" alt="Encoded JWT" style="zoom:50%;" />

<img src="https://img-blog.csdnimg.cn/53ac86dfeab94c87a57b47652fe0e10b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA54Ot5rKz5LiN5piv5rKz,size_20,color_FFFFFF,t_70,g_se,x_16" alt="img" style="zoom: 67%;" />

#### 1.1 头部header

- Jwt的头部承载两部分信息：

​       声明类型，这里是Jwt
​      声明加密的算法 通常直接使用 HMAC SHA256
Jwt里验证和签名使用的算法列表如下：

| JWS   | 算法名称 |
| :---- | :------- |
| HS256 | HMAC256  |
| HS384 | HMAC384  |
| HS512 | HMAC512  |
| RS256 | RSA256   |
| RS384 | RSA384   |
| RS512 | RSA512   |
| ES256 | ECDSA256 |
| ES384 | ECDSA384 |
| ES512 | ECDSA512 |

#### 1.2 载荷playload

- 载荷就是存放有效信息的地方。基本上填2种类型数据：标准中注册的声明的数据；自定义数据。由这2部分内部做base64加密。

   **标准中注册的声明** (建议但不强制使用)
  			   iss: jwt签发者
				sub: jwt所面向的用户
				aud: 接收jwt的一方
				exp: jwt的过期时间，这个过期时间必须要大于签发时间
				nbf: 定义在什么时间之前，该jwt都是不可用的.
				iat: jwt的签发时间
				jti: jwt的唯一身份标识，主要用来作为一次性token,从而回避重放攻击。
 **自定义数据**: 存放我们想放在token中存放的key-value值

#### 1.3  签名signature

Jwt的第三部分是一个签证信息，这个签证信息由三部分组成
base64加密后的header和base64加密后的payload连接组成的字符串，然后通过header中声明的加密方式进行j检验secret组合加密，然后就构成了Jwt的第三部分。