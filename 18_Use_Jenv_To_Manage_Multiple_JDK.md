1、安装jenv
执行：curl -s get.jenv.io | bash
jenv参考（关键是方便别的java工具管理）：https://github.com/linux-china/jenv/wiki/Chinese-Introduction
2、进入jenv目录,然后建相关目录：
Java代码  收藏代码
cd ~/.jenv/candidates/  
mkdir java  
cd java  
mkdir 1.6  
mkdir 1.7  
mkdir 1.8  
 
3、执行以下命令：
Java代码  收藏代码
ln -s /System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home/bin ~/.jenv/candidates/java/1.6  
ln -s /Library/Java/JavaVirtualMachines/jdk1.7.0_45.jdk/Contents/Home/bin ~/.jenv/candidates/java/1.7  
ln -s /Library/Java/JavaVirtualMachines/jdk1.8.0_25.jdk/Contents/Home/bin ~/.jenv/candidates/java/1.8  
 
大功告成：
1、最先默认的jdk一般是你最后安装的那jdk。
2、切换版本：jenv use java 1.8
3、设置缺少版本：jenv default java 1.6

参考：http://chessman-126-com.iteye.com/blog/2162466
