* armeabi下面的so文件有时候会自动被ignore，下面是重新add到svn的命令  
`svn add * --force --no-ignore`

`--no-ignore`是取消忽略   
`* --force`是添加当前目录及所有子目录下所有文件
