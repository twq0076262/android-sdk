# 剖析 Android SDK：Android 组件详解

> 在本系列教程当中，我们了解了在进行应用程序创建过程中需要使用到的各种 Android 基础开发功能。到目前为止，我们已经一同学习了 Android 应用程序中的结构与典型元素，其中包括用户界面元素以及数据存储。

在本系列教程当中，我们了解了在进行应用程序创建过程中需要使用到的各种 Android 基础开发功能。到目前为止，我们已经一同学习了 Android 应用程序中的结构与典型元素，其中包括用户界面元素以及数据存储。利用当下已经掌握的知识，大家完全可以着手创建自己的 Android 应用。不过在实际操作之前，我们还要梳理一遍部分常用 Android 组件——这也正是今天这篇文章的主要内容。在本系列的下一篇文章中，我们将探讨 SDK 示例代码。

**介绍**
Android 应用程序当中包含四大组件：Activity、Service、Content Provider 以及 Broadcast Receiver。只要大家创建或者使用其中的任何一种，就必须将对应元素添加到项目清单当中。我们之前已经跟 Activity 打了不少交道，因此在今天的文章中我就不再浪费篇幅加以介绍了。现在让我们把注意力集中在另外三种主要应用程序组件身上。需要强调的是，我还将介绍大家在应用程序当中最可能用到的其它一些资源，其中包括 fragment 以及 action bar。

**1.Service**
在 Android 系统当中，一项 Service 就相当于一个后台进程。Service 通常被用于那些正在进行或者需要持续很长一段时间的进程。事实上 Service 并不具备用户界面，因此它们通常需要与其它组件结合起来以实现功效，例如与 Activity 联手。最典型的例子就是，在应用程序当中 Activity 会在用户操作的同时启动一项 Service，这项 Service 也许会将数据上传至 Web 资源当中。用户可以继续与该 Activity 进行交互，但与此同时 Service 的运作却不受影响——因为它的执行一直在后台完成。

提示:如果大家希望执行获取互联网数据之类的后台进程，其中也不一定非要使用 Service 类。根据应用实际需求的不同，大家可能更适合在自己的 Activity 中利用内部 AsyncTask 类来解决问题。它能让后台进程与用户界面彻底分离，但我们的 Activity 仍然可以接收来自 AsyncTask 的运作结果并将其上更新至用户界面当中。

要将一项 Service 组件添加到清单当中，我们需要利用以下语法及其元素取代应用程序元素：

大家可以在 Eclipse 当中创建一个 Service 类，其过程与之前介绍过的 Activity 一样、只不过这次是把 Service 选择为超级类。Service 与 Activity 组件的区别我们之前已经谈到过，二者之间存在多种重大差异。如果我们以 Activity 为起点启动一项 Service，而用户又通过导航从该 Activity 切换到了其它应用程序处，那么该 Service 仍将继续运行。因此，Service 拥有的生命周期与我们所熟知的 Activity 完全不同，大家需要将这一点牢记于心、从而确保自己的应用程序能够有效运转。

其它应用程序组件可以与 Service 绑定，并向其请求并接收数据。如果一项绑定 Service 正处于运行当中，那么所有与之相绑定的组件停止之后它也将同时进入停止状态。尽管 Service 与应用程序的用户界面并无关联，但随 Activity 启动的 Service 会与之运行在同一线程当中。然而，如果大家的 Service 需要使用大量处理资源，那么我们最好为其创建一个独立的运行线程。请大家 点击此处 查看更多来自《Android 开发者指南》中关于 Service 的说明。

**2.Content Provider**
另一种组件 Content Provider 用于管理数据集。这里指的数据集既可以单纯归属于我们的应用程序，也可以与其它应用所共享、能够对数据进行查询及修改。如果大家为自己的应用程序创建了一个用于管理数据的 Content Provider，那么我们的 UI 组件（例如 Activity）就能够使用该 Content Provider，通常是利用 Content Resolver 类来实现与数据的交互。当被其它应用程序使用时，该 Content Provider 则通过标准方法来访问数据、从而与数据库等结构化数据集实现交互。

如果大家对于关系类数据库已经非常熟悉，那么应该非常了解 Content Provider 所使用的数据访问方法。数据会被 Content Provider 提交给一系列包含行与列的表格，其中每行（或者每条记录）中的列都包含一个单独的数据值。因此，处理通过 Content Provider 返回的数据与处理数据库查询结果非常相似。

虽然有时候我们可能会创建一个专门的 Content Provider 程序，但在最初着手开发自己的第一款应用时、大家基本上还是会直接使用由其他开发者或者 Android 系统本身所提供的 Content Provider——例如设备日程表或者联系人。Content Provider 能够定义客户端应用所需要的权限，从而实现内容使用。为了在应用程序当中使用 Content Provider，大家需要在清单当中为其添加相应的权限。

提示:如果大家只是需要一套应用程序当中的结构化数据源，那么我们通常并不需要单独创建 Content Provider。大家可以创建一套只适用于我们应用程序本身的 SQLite 数据库，而完全不需要使用 Content Provider 类。我们需要创建 Content Provider 的惟一情况在于，大家希望从我们的应用程序当中将结构化数据复制到其它应用处，或者大家希望使用搜索框架。

**3.Broadcast Receiver**
Android 系统能够发出多种应用程序能够响应的广播信息。大家也可以开发出应用程序来发出这些广播，但这种可能性与监听现有广播相比要低得多，至少对我们的第一款应用来说是这样。系统通知当中包含关于设备硬件的各类信息，例如电池电量、屏幕关闭以及充电器是否接入插座等等。

为了接收来自 Android 系统的广播通知，我们的应用程序需要使用 Broadcast Receiver。举个典型的例子，电池电量工具会在电池电量发生实际变化时更新显示结果。在这种情况下，大家可以将 Service 类与 Broadcast Receiver 配合使用，从而保证应用程序始终在后台监听通知内容。

Android 系统将广播通知称为 intent，它能够被用于启动 Activity。作为系统执行的操作，intent 可以实现 Activity 启动或者发出通知。要使用 Broadcast Receiver，我们的应用程序必须在清单中对其作出声明；此外还有一套备选 intent filter，用于指示我们想要接收的操作：

通过以上代码，我们应用中的 Broadcast Receiver 就能够接收“battery low（电池电量低）”这一 intent。请注意，我们无法通过在清单中声明 action 这种方式接收全部系统通知。在某些情况下，大家必须完成注册来实现通知接收，例如在 Java 当中使用 BATTERY_CHANGED action。

**4.其它类**
正如大家所见，Android 组件的设计初衷在于为不同应用程序提供彼此之间的交互效果。正如广播通知可用于系统之上的任何应用，Android 还提供其它一系列 action、帮助我们在应用程序中完成各类常见任务——例如拨打电话号码。同样，大家也可以使用由其他开发人员所提供的功能，从而快速实现预定处理流程、节约代码开发量并帮助自己将更多精力集中在应用程序的独特之处上。当我们启动一项 intent 时，可以通过设置使其向启动中的 Activity 返回一个结果——即使所启动的 intent 并非我们应用程序的组成部分。这就使我们的应用能够在要求操作完成之后继续运行。

其它值得关注的 Android 组件还包括 fragment 以及 action bar。下面就让我们简单对二者进行探讨：

**Fragment**
比起单纯利用 Activity 以及布局配置来定义应用程序中各个屏幕下的用户界面，使用 fragment 的话效率可能会更高一些。在 fragment 的帮助下，大家可以将自己的用户界面拆分为逻辑部分，甚至在应用程序的多个屏幕之间重复使用同样的部分。这样一来，我们不仅能够节约大量花在实现同样视觉/交互元素上的重复劳动，同时也实现了修改一点即完成对整款应用变更的效果。Fragment 在 Android 系统中属于 Activity 中的组成部分，因此每个 fragment 都要与其所在的 Activity 生命周期相适应。

**Action Bar**
在应用程序开发过程中，action bar 也是我们经常需要用到的关键性用户界面元素。它的作用在于为我们的应用程序提供足以作用于整套 Android 系统的用户界面，这也使它成为该平台用户们最熟悉的元素。一般来说，action bar 当中所显示的条目包括用户在应用程序当中所处的位置以及应用程序各个部分之间的导航系统。要在 Activity 当中使用 action bar，大家需要保证自己的类当中包含 ActionBarActivity 类，并在清单当中将 AppCompat 主题应用在该 Activity 当中。

**总结**
具体使用哪一种 Android 类及组件取决于大家的应用程序到底要执行哪些任务。不过经过文章的论述，相信应该能够帮助大家对类与组件的类型及数量有所了解，并根据实际情况作出正确选择。对于特定特性或者功能来说，我们往往很难决定具体该使用哪款组件或者类，因此请大家在判断之前确保自己对它们的作用拥有清晰的了解。在接下来的教程当中，我们将探讨 Android 示例代码以及应用程序的发布流程。

原文链接：

http://mobile.tutsplus.com/tutorials/android/android-sdk-common-android-components/