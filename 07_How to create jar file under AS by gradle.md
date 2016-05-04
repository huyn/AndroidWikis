* 1. 方法一
```
task makeJar(type: Copy) {
    delete 'build/libs/mysdk.jar'
    from('build/intermediates/bundles/release/')
    into('build/libs/')
    include('classes.jar')
    rename ('classes.jar', 'mysdk.jar')
}

makeJar.dependsOn(build)
//在终端执行生成JAR包
// gradlew makeJar
```

execute command:

`./gradlew -p basenetworkframework clean build makeJar --info`

TESTED

* 2.BY JAVA COMMAND [http://blog.csdn.net/beijingshi1/article/details/38681281]
open command terminal
go to your module file and execute
`./gradlew clean build`

you will generate classes files under 'build/intermediates/classes/release'
then execute 'jar cvf myJar.jar -C  build/intermediates/classes/release .'
you will get myJar.jar under current folder

If you want to generate .jar by gradle
add this block to build.gradle:
```
//定义一个函数，target是生成jar包的文件名，classDir是class文件所在的文件夹  
def makeJar(String target,String classDir){  
    exec{  
        executable "jar"   //调用jar  
        args "cvf",target  
        args "-C", classDir  
        args "","."  
    }  
}  
  
//新建一个task,名为buildLib,依赖build(build是一个自带的task)  
task buildLib(dependsOn:['build'])<< {  
    makeJar("MyJar.jar","build/intermediates/classes/release")  
} 
```

then execute `./gradlew buildLib` by terminal and you will get MyJar.jar under the folder

* 3.jar with proguard
http://android.jobbole.com/81235/
