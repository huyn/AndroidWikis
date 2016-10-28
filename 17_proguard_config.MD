最常用的配置选项 
-dontwarn 缺省proguard 会检查每一个引用是否正确，但是第三方库里面往往有些不会用到的类，没有正确引用。如果不配置的话，系统就会报错。 
-keep 指定的类和类成员被保留作为 入口 。 
-keepclassmembers 指定的类成员被保留。 
-keepclasseswithmembers 指定的类和类成员被保留，假如指定的类成员存在的话。

-optimizationpasses 5 ［指定代码的迭代优化次数］
-dontusemixedcaseclassnames 【混淆时不会产生形形色色的类名 】 
-dontskipnonpubliclibraryclasses 【指定不去忽略非公共的库类。 】 
-dontpreverify 【不预校验】 
-verbose [混淆时是否纪录日志]
-optimizations !code/simplification/arithmetic,!field/,!class/merging/ 【优化】 

-dontobfuscate 不混淆输入的类文件
-printmapping {filename}
-applymapping {filename} 重用映射增加混淆
-obfuscationdictionary {filename} 使用给定文件中的关键字作为要混淆方法的名称
-overloadaggressively 混淆时应用侵入式重载
-useuniqueclassmembernames 确定统一的混淆类的成员名称来增加混淆
-flattenpackagehierarchy {package_name} 重新包装所有重命名的包并放在给定的单一包中
-repackageclass {package_name} 重新包装所有重命名的类文件中放在给定的单一包中
-dontusemixedcaseclassnames 混淆时不会产生形形色色的类名
-keepattributes {attribute_name,…} 保护给定的可选属性，例如LineNumberTable, LocalVariableTable, SourceFile, Deprecated, Synthetic, Signature, and InnerClasses.
-renamesourcefileattribute {string} 设置源文件中给定的字符串常量
