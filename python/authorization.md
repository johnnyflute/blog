#授权模式
最近在cloudmgr项目中，需要将集群和主机的restful接口加上授权功能，使用户通过token的方式来使用接口，总结了下授权模式，供以后参考。

授权简单地说就是资源的拥有者提供授权给第三方应用，也就是客户端来访问用户的资源。授权模式分为四种
1. authorization code
2. implicit
3. resource owner password credentials
4. client credentials
这四种按照user和client的关系可以划分为两种：显示和隐式授权。显式授权一般在用户不信赖client的时候，需要授权服务器提供一个授权页面给用户，由用户输入密码并授权。对应类型1和类型2；如果用户信赖客户端，将密码告诉client，那就是隐式授权，表明同意client直接访问token endpoint获取token