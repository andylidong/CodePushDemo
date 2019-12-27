## CodePushDemo

### 1、clone客户端代码
      $ git clone git@github.com:lidong/code-push-demo-app.git
 
### 2、cd到demo路径，执行npm install 安装node依赖包
 
### 3、用Android Studio打开code-push-demo-app/android目录

     到MainApplication.Java里面修改以下代码

     @Override
     protected List<ReactPackage> getPackages() {
       return Arrays.<ReactPackage>asList(
           new MainReactPackage(),
           new CodePush(
              "YourKey",  // code-push app add项目后生成的app 推送key
              MainApplication.this,
              BuildConfig.DEBUG,
              "YourCodePushServerUrl"   // config.js中配置的downloadUrl 地址 不需要/download后缀
           )
       );
     }
     下面是我的配置

     @Override
         protected List<ReactPackage> getPackages() {
           return Arrays.<ReactPackage>asList(
               new MainReactPackage(),
               new CodePush(getResources().getString(R.string.reactNativeCodePush_androidDeploymentKey),
                       getApplicationContext(),
                       BuildConfig.DEBUG,
                       "http://192.168.3.168:3000/")
           );
      }

### 4、终端操作
    打开命令终端，登录code-push-server服务器，这里配置为local，所以登录地址为http://127.0.0.1:3000 或者 http://192.168.3.168:3000/
    $ code-push http://127.0.0.1:3000  //账号密码为博主提供  account:  admin password:  123456
    登录成功之后获取token,将文本框中的key复制粘贴到登录终端，点击回车登录成功


### 5、添加推送app
     $ code-push app add Demo-android #android版
     添加完成之后可以用code-push app list命令查看创建好的app，并将测试的Staging key拷贝到MainApplication.java中的 “Your Key“ 的位置，
     推送的时  候通过key将app和服务器端关联
 

### 6、cd 到code-push-demo-app目录，允许React-native start 启动react-native 服务
 

### 7、Android Studio编译并将项目运行到手机上，reload更新到最新js包
 

### 8、测试
    在code-push-demo-app中首页随意做一些修改，这里添加了一段静态问题：“我是热更新内容" ,执行推送命令
    测试环境执行：
    $ code-push release-react Demo-android android
    生产环境执行：
    $ code-push release-react Demo-android android -d Production


### 9、到app中点击 “Start Sync!“ 执行完安装后，可以看到页面上多了“我是热更新内容". 
