# Android SDK 上手指南：知识测试(1)

> 在从零开始学习 Android 开发系列教程当中，我们已经了解了为 Android 平台创建应用程序过程中需要涉及的各种基本概念及知识要点。一路走来，我们探讨了关于 Android 开发的各方面内容，其中包括 Java 开发、XML 使用、用户界面设计、项目结构、数据存储以及发布流程等。为了检验我们的学习效果，在今天的文章中请大家接受一份结业测试、看看自己是否掌握了前面提到的各项知识。

![](images/38.png)

**教程说明**
完成时间:十五分钟

执行难度:简单

在[从零开始学习 Android SDK 系列教程](http://mobile.51cto.com/android-420819.htm)当中，我们已经了解了为 Android 平台创建应用程序过程中需要涉及的各种基本概念及知识要点。一路走来，我们探讨了关于 Android 开发的各方面内容，其中包括 Java 开发、XML 使用、用户界面设计、项目结构、数据存储以及发布流程等。为了检验我们的学习效果，在今天的文章中请大家接受一份结业测试、看看自己是否掌握了前面提到的各项知识。

**问题一**

我们的 Java 类被保存在以下哪个 Android 应用程序目录之下？

res
layout
src
values

**问题二**

我们不会在项目清单文件中执行以下哪项内容？

在应用程序当中声明 activity。
设定最低 API 支持级别。
定义按钮被点击后执行何种事件。
列出应用程序运行所需要的权限。

**问题三**

为了在 Java 当中利用“@+id/how”语法检索 XML 中某个视图集的 id，我们应该使用以下哪条语句？

R.how
R.view.how
findViewById(how)
R.id.how

**问题四**

我们应该使用以下哪条语句在 XML 当中设定 TextView 所显示的文本字符串？

android:text='@string/info'
android:string='info'
android:text='@text/info'
android:value='@string/info'

**问题五**

以下哪一种才是我们用于定义用户点击某个按钮时所执行事件的标准方法？

onClickListener
onViewClick
onClick
onButtonClick

**问题六**

我们需要将以下哪种 XML 属性添加到视图当中，从而指定用户进行点击时所执行的方法 ？

android:onClick
android:click
android:clickListener
android:clicked

**问题七**

我们需要使用以下哪条语句在 ImageView 当中设置一个可绘制显示图形？

android:img='@drawable/my_shape'
android:shape='@drawable/my_shape'
android:drawable='@drawable/my_shape'
android:src='@drawable/my_shape'

**问题八**

我们需要将以下哪种 activity 元素包含在清单当中，从而在应用程序从设备菜单中启动时执行该 activity？

包含在某个属性当中的应用程序名称。
主要及启动器属性。
主 action 以及启动器类型元素。
主类型与启动器 action 元素。

**问题九**

我们需要在哪个元素当中声明应用程序在清单中所要求的权限？

permission
request-permission
permission-required
uses-permission

**问题十**

应用程序的 Shared Preferences 是用来干什么的？

保存原始数据项的键值对。
在表当中以行和列的方式保存结构化数据。
检索互联网数据。
将数据保存在用户设备上的外部文件中。

**问题十一**

应用程序在读取并写入文件时，我们需要如何处理 I/O 错误？

仔细检查文件名字符串。
将我们的 I/O 代码放置在一个独立的类当中。
尝试并获取与 I/O 代码相关的数据块。
向用户输出警告信息。

**问题十二**

在尝试向外部存储机制进行写入之前，我们的应用程序不需要执行以下哪个步骤？

检查外部存储机制是否可用。
检查外部存储机制的写入访问。
使用清单内用于向外部存储写入操作的权限。
使用警告对话框，要求用户为数据写入提供权限。

**问题十三**

在从互联网源获取数据时，我们需要坚持做到以下哪一点？

使用一个 service 类来获取数据。
使用一个单独的进程、而不要利用用户界面进程进行数据获取。
在主 activity 类中的一个方法内获取数据。
将检索数据保存在 SQLite 数据库当中。

**问题十四**

以下哪种说法存在错误？

即使是在启动某 service 的 activity 停止运行之后、该 service 仍将继续处于运行状态。
除非用户利用后退按钮进行退出操作，否则 activity 将始终处于运行状态。
某个绑定 service 在任何与之相绑定的组件停止运行后、也将一同停止运行。
当某个 activity 的指向发生变化时、其在默认情况下将进行重新创建。

**问题十五**

要在某个 activity 当中启用另一个 activity，我们需要使用以下哪种类？

Intent
Thread
View
Service

**问题十六**

当一款应用程序启动并处于 resumed 状态时，以下哪种回调方法不会执行？

onCreate
onPause
onStart
onResume

**问题十七**

当用户在暂停之后重新返回我们的应用程序时，以下哪种回调方法会付诸执行？

onRestart
onResume
onStart
onCreate

**问题十八**

我们需要利用当种方法将状态数据保存在 activity 的 onCreate 与 onRestoreInstanceState 方法当中、以备未来访问？

onDestroy
onSaveInstanceState
onStateChange
onSaveState

**问题十九**

哪个类允许我们定义可重复使用的用户界面部分？

Fragment
Service
Activity
View

**问题二十**

在向 Google Play 发布应用程序时，我们不需要进行以下哪个步骤？

在清单当中包含应用程序的版本与名称。
利用 release key 进行 APK 签名。
为应用程序选择内容分级以及产品定价。
为应用程序创建一段视频介绍。

正确答案：
1、C；
2、C；
3、D；
4、A；
5、C；

6、A；
7、D；
8、C；
9、D；
10、A；

11、C；
12、D；
13、B；
14、B；
15、A；

16、B；
17、B；
18、B；
19、A；
20、D。