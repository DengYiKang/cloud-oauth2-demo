这是一个关于OAuth2授权码方式的入门级demo，数据全部保存在内存中。
分为三个部分，auth-server（授权服务器）,user-server（资源服务器）,client-app（客户端）。

auth-server保存有:
+ client-id, client-secret, 及授权类型
+ username, password, role

user-server保存有:
+ token检验地址
+ client-id, client-secret
+ 资源与角色的对应关系
+ 资源

流程如下：
访问client-app的index界面，点击第三方登录链接，发送
http://localhost:8080/oauth/authorize?client_id=javaboy&response_type=code&scope=all&redirect_uri=http://localhost:8082/index.html
请求，跳转至auth-server的登录页。

用户在auth-server上进行登录，确定给client授权，然后auth-server返回code给client，client拿着code到auth-server请求token，成功后拿着token去访问user-server的某个资源，
若token解析成功则资源获取成功。
