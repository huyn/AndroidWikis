android studio ndk 笔记
搜索关键字：androidstudio 自定义 android.mk

密码：32569958

http://stackoverflow.com/questions/27833530/how-to-use-my-own-android-mk-file-with-android-sudio
http://blog.gaku.net/ndk/

这一篇最有价值：https://www.crystax.net/cn/blog/3


这个教程时针对windows环境：
http://david740204.pixnet.net/blog/post/412169557-android-studio%E8%A3%A1%E8%87%AA%E5%AE%9Aandroid.mk%E5%92%8Capplication.mk

这一篇讲解了neon的配置：
http://blog.csdn.net/fengbingchun/article/details/37766607
http://www.tuicool.com/articles/673mIn
http://www.bkjia.com/Androidjc/834441.html
http://developer.android.com/ndk/guides/cpu-arm-neon.html

普通的androidstudio编译ndk教程，依靠gradle配置
http://blog.csdn.net/sodino/article/details/41946607

最全的macos下的ndk工作介绍
http://blog.csdn.net/ashqal/article/details/21869151


1.如果采用as的ndk自动模式，在gradle中配置
ndk {
            moduleName "app"
            ldLibs "log", "z", "m"
            abiFilters "armeabi", "armeabi-v7a", "x86"
        }

即可

2.因为ndk options只有5个基本配置，所以如果想定义其他参数，如：我只想适配arm64-va这个平台，就没办法来，只有通过自定义的方式来实现，这样，就需要配置gradle文件

配置ndk需要配置系统环境变量
macos下配置环境变量如下：
http://www.cnblogs.com/mokey/p/3542389.html
这个还没试过：
http://blog.csdn.net/greenbird811/article/details/7543305
http://my.oschina.net/weichou/blog/374227
http://hdu104.com/23

正常解压ndk后，配置.bash_profile后是这样的： 
http://hathaway.cc/post/69201163472/how-to-edit-your-path-environment-variables-on-mac 这里教你怎么配置.bash_profile
export PATH=${PATH}:/Users/huyaonan/Library/Android/sdk/platform-tools/
export PATH=${PATH}:/Users/huyaonan/dev/android-ndk-r10e/
export ANDROID_SDK=/Users/huyaonan/Library/Android/sdk
export ANDROID_HOME=/Users/huyaonan/Library/Android/sdk
export NDK=/Users/huyaonan/dev/android-ndk-r10e

官网：
https://developer.android.com/ndk/downloads/index.html

小技巧：
显示文件路径：
http://sspai.com/26273


提升：JNI_OnLoad