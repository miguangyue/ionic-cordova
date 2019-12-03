# ionic-cordova
环境搭建布局:
（1）jdk 安装后
     系统环境变量配置： JAVA_HOME =》 C:\Program Files\Java\jdk1.8.0_202
（2）android-sdk 安装后 E盘  
                    ANDROID_HOME =》 E:\android-sdk_r24.4.1-windows\android-sdk-windows
（3）gradle安装后 pth =》%JAVA_HOME%\bin
                      E:\android-sdk_r24.4.1-windows\android-sdk-windows\tools
                      E:\android-sdk_r24.4.1-windows\android-sdk-windows\platform-tools   
                      C:\Program Files\nodejs\
                      C:\Windows\system32
                      C:\Windows
                      C:\Windows\System32\Wbem
                      C:\Windows\System32\WindowsPowerShell\v1.0\
                      E:\gradle-4.1-all\gradle-4.1\bin
 （4）npm install -g cordova@3 ionic@8.1.2
      建项目
      ionic start myApp --type=ionic-angular
      配置Android环境
      ionic platform add android
      打包 ionic build android
      签名流程：
        生成无签名文件
        (1)ionic build android --release --prod
        生成签名
       （2）  keytool -genkey -v -keystore spilledyear.keystore -alias spilledyear.keystore -keyalg RSA -validity 36500 
         -genkey：产生密钥
         -keystore: 签名文件名称（这里是 demo.jks，demo 可以自定义，jks 是 Android studio 生成的签名文件的后缀）
         -alias：签名文件的别名（这里是 demo，可自定义）
          -keyalg：使用 RSA 算法对签名加密（默认 RSA ）
         -validity 有效期限（这里是 10000 天，可自定义）
          把上面两个文件生成的 app-release-unsigned.apk，spilledyear.keystore放一起后往下执行（3）
        （3）jarsigner -verbose -keystore spilledyear.keystore -signedjar zmjj.apk android-release-unsigned.apk spilledyear.keystore
        jarsigner是工具名称 
        -verbose表示将签名过程中的详细信息打印出来，显示在dos窗口中
        -keystore spilledyear.keystore 表示签名所使用的数字证书所在位置，没有写路径表示在当前目录下
        -signedjar zmjj.apk android-release-unsigned.apk 表示给android-release-unsigned.apk文件签名，签名后的文件名称为zmjj.apk 
        spilledyear.keystore 表示证书的别名，对应于生成数字证书时-alias参数后面的名称


