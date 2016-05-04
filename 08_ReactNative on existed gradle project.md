* 基于 ReactNative 植入原生应用［http://reactnative.cn/docs/0.20/embedded-app-android.html#content］

一步一步按照教程执行，直至执行真机调试那个步骤，这个时候在手机上打开app，发现会闪退，原因是：

`Error: Requiring unknown module "ReactPerf"`

提示我没有这个模块，google之，发现这是react的一个模块，用来调试性能的

执行`npm list`

log说`peer dep missing: react@^0.14.5`

那么在package.json中加入：
`"react":"0.14.5"`

执行`npm install`

然后重新启动
`npm start`

打开app

完美

有时候启动的时候会报`8081`端口被占用的log

如果你同时开发安卓和iOS应用，或者有时在不同的应用之间进行切换，编译时可能会遇到端口8081被占用的问题，这时可以运行：
`lsof -n -i4TCP:8081`，检查端口的使用情况，必要时可以通过：`kill -9 <端口号>`，杀死当前占用`8081`端口的进程
