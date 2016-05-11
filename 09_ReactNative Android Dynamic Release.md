几个案例
* http://richardcao.me/2015/12/03/React-native-Android-%E7%83%AD%E6%9B%B4%E6%96%B0/
* https://github.com/fengjundev
* https://github.com/vczero/react-native-lesson (iOS)
* https://github.com/race604/ZhiHuDaily-React-Native
* http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html


思路总结：
首先翻到了这一片博客［http://richardcao.me/2015/12/03/React-native-Android-%E7%83%AD%E6%9B%B4%E6%96%B0/］
讲到了两个方案：
* 方案一：通过反射的模式，`recreateReactContextInBackground`实现JsBundleFile的动态更新。代码存在一个一点问题
```
private void recreateReactContextInBackground(
      JavaScriptExecutor.Factory jsExecutorFactory,
      JSBundleLoader jsBundleLoader) {
    UiThreadUtil.assertOnUiThread();

    ReactContextInitParams initParams =
        new ReactContextInitParams(jsExecutorFactory, jsBundleLoader);
    if (!mIsContextInitAsyncTaskRunning) {
      // No background task to create react context is currently running, create and execute one.
      ReactContextInitAsyncTask initTask = new ReactContextInitAsyncTask();
      initTask.execute(initParams);
      mIsContextInitAsyncTaskRunning = true;
    } else {
      // Background task is currently running, queue up most recent init params to recreate context
      // once task completes.
      mPendingReactContextInitParams = initParams;
    }
  }
```
实际上`recreateReactContextInBackground`的两个参数分别是`JavaScriptExecutor.Factory`和`JSBundleLoader`
所以反射部分代码修改为：
```
Class<?> RIManagerClazz = mReactInstanceManager.getClass();
            Method method = RIManagerClazz.getDeclaredMethod("recreateReactContextInBackground",
                    JavaScriptExecutor.Factory.class, JSBundleLoader.class);
            method.setAccessible(true);
            method.invoke(mReactInstanceManager,
                    new JSCJavaScriptExecutor.Factory(),
                    JSBundleLoader.createFileLoader(getApplicationContext(), JS_BUNDLE_LOCAL_PATH));
```
* 方案二：也就是博主自己的方案，直接替换文件，但是没谈到怎么刷新的问题，我也还没有做测试


既然解决了离线动态加载的方案，我们接下来将正式打包的部分做完，以下几步必须：
* `ndk`部分。build.gradle中加入：
```
        ndk {
            abiFilters "armeabi-v7a", "x86"
        }
```
  根据自身需要，编译动态库
  `gradle.properties`中加入`android.useDeprecatedNdk=true`
  安装好ndk后在`local.properties`中加入`ndk.dir=/Users/huyaonan/android-ndk-r10e`

* @race604的知乎日报项目写了个很赞的gradle脚本，能将bundle在打包的时候写一份到`assets`文件夹当中，这样，才真正的可以当做一个正式包发布出去，再结合以上动态更新的代码，一个完整的热加载功能就实现了。附`ReactInstanceManager`实例化部分代码：
```
mReactInstanceManager = ReactInstanceManager.builder()
                .setApplication(getApplication())
                .setJSBundleFile("assets://ReactNativeDevBundle.js")
                .setJSMainModuleName("index.android")
                .addPackage(new MainReactPackage())
                .addPackage(new CustomReactPackage())
                .setUseDeveloperSupport(BuildConfig.DEBUG)
                .setInitialLifecycleState(LifecycleState.RESUMED)
                .build();
```


PS:之前reactnative上的一个issue［https://github.com/facebook/react-native/pull/3189］描述的部分是有问题的，到现在为止，`ReactInstanceManager`根本就没有`setJsBundleLoader`这个方法
