# 调试工具Stetho


Stetho，来自Facebook，它能做什么？无需root，借助Chrome可以查看SharePreferences和数据库中的数据，此外还有网络抓包以及查看View树等。

[github地址](http://facebook.github.io/stetho/)

[使用教程](http://www.jianshu.com/p/03da9f91f41f)

### 配置说明
我们希望只在debug情况下使用这个开源库。

* 所以在build.gradle中添加依赖

```
dependencies {
	debugCompile 'com.facebook.stetho:stetho:1.4.2'
	debugCompile 'com.facebook.stetho:stetho-okhttp3:1.4.2'
}
```
* 在build.gradle android节点下设置sourceSets

```
sourceSets {//源集
        main {
            java.srcDirs = ['src/main/java']
        }
        debug{
            java.srcDirs = ['src/main/javaDebug']
        }
        release{
            java.srcDirs = ['src/main/javaRelease']
        }
}
```
* 在src/main/javaDebug中创建初始化类StethoUtils

```
public class StethoUtils {

    public static void install(Application application){
        Stetho.initializeWithDefaults(application);
    }

    public static void addNetworkInterceptor(OkHttpClient.Builder builder){
        builder.addNetworkInterceptor(new StethoInterceptor());
    }

}
```
* 在src/main/javaRelease中创建同名类StethoUtils

```
public class StethoUtils {
    public static void install(Application application){
    }
    public static void addNetworkInterceptor(OkHttpClient.Builder builder){
    }
}
```
* 在Application中的onCreate中初始化

```
if(BuildConfig.DEBUG){
	StethoUtils.install(this);
}
```
* 在OkHttpClient初始化的地方添加

```
OkHttpClient.Builder builder = new OkHttpClient.Builder();
if(BuildConfig.DEBUG){
	StethoUtils.addNetworkInterceptor(builder);
}
```

如果工程里使用的网络库不是okhttp，请参考官网设置




