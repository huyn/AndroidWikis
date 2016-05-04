* According to [http://gold.xitu.io/entry/57200b9371cfe400573d84fa]

* 1.Install maven
* 2.Set Environmental Variables
```
MAVEN_HOME=/Users/huyaonan/apache-maven-3.3.9
PATH=$PATH:$MAVEN_HOME/bin

export MAVEN_HOME
export PATH
```
* 3.change maven/conf/settings.xml

make 
```
<localRepository>/Users/huyaonan/maven-repo</localRepository>
```
visible
This is your self-created maven repo

* 4.follow the tutor
* 5.When execute 
`./gradlew -p basenetworkframework clean build uploadArchives --infoc`

`bash: ./gradle: permission denied` would happen

execute `chmod +x gradlew` and continue

If any other errors happen, follow the log and fix it

when you success, you will find some surprise int you filr /Users/huyaonan/maven-repo

* 6.Continue folling the tutor...

`$ ./gradlew -p modulename clean build uploadArchives --info`
