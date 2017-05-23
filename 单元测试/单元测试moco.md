
# 单元测试

## 1.为什么进行单元测试？

[可以参考这个链接](http://chriszou.com/2016/04/16/android-unit-testing-about-why.html)


## 2.android默认依赖的测试框架

[junit介绍](http://blog.csdn.net/yaodong379/article/details/55113388)

[UI测试-Espresso](http://blog.sunofbeaches.com/archives/552)


## 3.mock & mockserver

mock测试就是在测试过程中，对于某些不容易构造或者不容易获取的对象，用一个虚拟的对象来创建以便测试的测试方法。
mockserver 就是构建一个测试环境。

[moco项目地址](https://github.com/dreamhead/moco)

[moco使用方式](http://blog.csdn.net/sanjay_f/article/details/50204883)

[开发者的专访](http://www.csdn.net/article/2013-08-23/2816684-Moco-Java-framework)

## 4.流程示例 

1.[下载moco.jar](https://repo1.maven.org/maven2/com/github/dreamhead/moco-runner/0.11.0/moco-runner-0.11.0-standalone.jar)

2.[[编写本地json文件nav-list.json]]

3.启动本地服务
java -jar moco.jar start -p 5638 -c nav-list.json

4.这时可以在电脑查看运行结果
http://localhost:5638/nav-list

5.修改代码，把命令地址改为本地ip（注意是电脑ip地址，不是手机ip地址）

String server = mVideoServerUrl + "api/nav-list.htm?";

改为

String server = "http://192.168.20.237:5638/nav-list";