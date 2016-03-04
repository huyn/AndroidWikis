react native学习笔记

环境配置：http://www.csdn.net/article/2015-09-24/2825787-react-native    
1，安装brew：http://brew.sh/index_zh-cn.html

终端窗口输入
```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```    
开始安装    
有可能一次安装不成功，没关系   
```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)”
```  
卸载后重新install一次

2,接着安装nvm：  
```
brew install nvm
```
但是nvm的github站点https://github.com/creationix/nvm#installation明确表示
```
Homebrew installation is not supported
```
fuck

正确步骤是先
```brew install nvm```

按照终端输出的log，配置好环境变量

log如下：
```
You should create NVM's working directory if it doesn't exist:

  mkdir ~/.nvm

Add the following to ~/.bash_profile or your desired shell
configuration file:

  export NVM_DIR=~/.nvm
  . $(brew --prefix nvm)/nvm.sh

You can set $NVM_DIR to any location, but leaving it unchanged from
/usr/local/Cellar/nvm/0.31.0 will destroy any nvm-installed Node installations
upon upgrade/reinstall.

Type `nvm help` for further information.

Bash completion has been installed to:
  /usr/local/etc/bash_completion.d
···


然后
```curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.30.2/install.sh | bash
```
这时候在终端输入 
```nvm help```   正常显示就安装好了


3，接着安装node.js
```
nvm install node && nvm alias default node
```
完了 
```
node -v 
```输出正常版本号
`npm -v` 输出正常版本号
表示node安装成功


4.安装watchman 和flow
这两个包分别是监控文件变化和类型检查的。安装如下：

```brew install watchman```
```brew install flow```
5.最后安装react native
```npm install -g react-native-cli```
Android需要配置环境变量
```export ANDROID_HOME=/Users/huyaonan/Library/Android/sdk```
