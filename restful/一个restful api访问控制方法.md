# 一个restful api访问控制方法


新浪的API访问控制使用的是AccessToken，有两种方式来使用该AccessToken：
- 1、API请求 URL 的后面加上一个AccessToken
- 2、Http头里面加一个字段AccessToken=xxx
这种AccessToken是写死在程序里面的，在每次请求的时候附带上，对于这种AccessToekn新浪那边有过期时间，过期之后就无法再使用了。
- 很明显这种方式是不安全的，一旦别人获取到这个AccessToekn 就可以伪装身份使用该API，这个访问控制就形同虚设了。但是新浪也知道这一点，所以利用这种方式使用的接口都是较为基础的接口，高级一点的接口需要使用Oauth 2.0进行二次认证的访问控制。

### 在我的项目中大致想了下面这种访问控制的办法。
- 1、为每个应用颁发一个账号（user）和密码（password），相当于（公钥和私钥）。
- 2、服务器后台存储该账号和密码（密文存储 MD5加密）
- 3、应用端在通过HTTP请求该接口的时候，需要在HTTP HEADER 附带下面几个字段
时间date=unix时间戳
签名sign=sign
该sign的生成算法是这样的
String sign = HTTPMETHOD（GET/POST）+ api_uri（API的访问URI）+date（即上面的UNIX时间戳）+length（发送body的数据长度）+password（后台颁发的密码）
sign = MD5(sign)
sign = user+":"+sign
### 后台服务器在接收到请求后
- 1、比对HTTP头中的时间戳，比对服务器时间，如果超过某个阈值，则拒绝访问，同时返回请校准你的应用时间。
- 2、如果没有超过时间阈值，则从sign中取出user然后在数据库中查找对应的password，然后同样根据上面的sign生成算法，来生成sign进行身份认证，认证成功则执行API，失败则返回认证失败。