# Android SDK 上手指南：Activity 与生命周期

> Activity 生命周期并不仅仅在用户运行应用程序之后才开始生效，事实上它也影响着用户切出以及切回应用时得到的不同反馈。当我们开发一款应用时，首先需要牢记一点：用户会经常在执行过程中、在我们的应用与其它应用之间频繁切换。

**介绍**
Activity 生命周期并不仅仅在用户运行应用程序之后才开始生效，事实上它也影响着用户切出以及切回应用时得到的不同反馈。当我们开发一款应用时，首先需要牢记一点：用户会经常在执行过程中、在我们的应用与其它应用之间频繁切换。取决于用户的操作方式，同一款应用程序有时在前台运行、有时则在后台运行。大家必须保证自己的应用能够就会这类情况，并在此类切换过程中及时保存并恢复数据。再次提醒各位，这一过程对于某些特定应用程序略有不同——例如功能性组件。

**1.回调方法**
**第一步**
为了控制 Activity 处于不同状态下时应用程序的运行方式，例如当用户切出或者切回应用，大家可以选择多种处理方法。这类方法也就是 Activity 生命周期回调方法。Android 系统会在我们的 Activity 进入某种特定状态后调用这些方法，从而通过一系列步骤确保我们的应用程序能够继续起效、不至于丢失数据而且在用户不与之交互时不会使用非必要性资源。每一种回调方法都会让我们的应用进入一种可能的状态。

如果大家之前曾经接触过 Java 应用程序的编程工作，那么应该已经发现 Android 应用程序的启动遵循另一种方式。与 Java 应用直接使用主方法不同，Android 在启动后会首先执行主 Activity 类中的 onCreate 方法。请记住，我们已经在清单中将该类指定为主启动 Activity。Activity 会首先回调 onCreate 方法，相当于重复用户启动应用程序后的流程。这时候 onCreate 方法会使应用程序进入 Created 状态。

开发者指南当中通过示意图以直观方式介绍了生命周期、回调方法以及状态的概念。其中 onResume 方法负责提供 Resumed 状态，这时我们的应用程序可以接受用户的直接操作。其它各类回调方法都以 onResume 为核心，即将应用程序引导至 Resumed 状态或者从该状态脱离、启动该状态或者将其停止。

对于大部分应用程序来说，我们只需要使用一部分回调方法，但最起码要用到 onCreate。虽然使用频率不高，但了解全部回调及状态的作用将帮助我们了解自己的应用程序在运行及停止运行时，Android 系统会受到怎样的影响。一般情况下，大家需要保证用户能够在任何操作过程切换出去之后、都能顺利恢复到之前的运行状态；如果他们通过导航选择前进或者后退，应用则需保存全部必要数据并释放不必要占用的硬件资源。

**第二步**
我们的应用程序可能处于以下五种状态，分别为：Created、Started、Resumed、Paused 以及 Stopped。另有七种回调方法能够让应用进入或者脱离上述状态，它们分别是：onCreate、onStart、onRestart、onResume、onPause、onStop 以及 onDestroy。这些方法能够让我们的应用程序在可能的状态之间进行切换，而且某些情况下切换速度会很快。通常来说，大家可以认为自己的应用程序始终处于 resumed、paused 或者 stopped 这三种状态之下，因为其它状态都是暂时性的。

当我们的应用程序正处于运行当中且用户与之进行操作交互，这时的应用状态为 Resumed；当另一个 Activity 处于前台但仅仅使我们的应用被部分隐藏时，这时的应用状态为 Paused——在这种状态下用户无法再与应用进行交互。当我们的应用完全处于后台之下，而且用户既无法操作、也无法观看到它时，其状态即为 Stopped。在这种状态下 Activity 会保留之前的所有数据，但无法加以执行。

**2.进入 Resumed 状态**
如我们所知，主 Activity 会在应用程序启动时开始运行，onCreate 方法也将执行、从而让我们准备该类所需要的 Activity UI 以及全部数据条目。我们创建的大部分应用当中都包含不只一个 Activity，其它 Activity 会在用户与应用程序进行操作交互时启动。大家可以利用以下代码通过 Intent 类启动另一个非主 Activity：

这代表着应用程序包中另一个名为“About”的 Activity 类。大家可以通过选择自己的源码包而后选择“文件”、“新建”、“类”的方式在 Eclipse 当中创建一个新 Activity，而后将该 Android Activity 类选定为超级类。请记住，每一个 Activity 都必须在我们的应用程序清单当中列出。大家还可以利用 Intent 类实现不同 Activity 之间的数据转移。

当一个 Activity 处于运行当中时，onCreate 方法也在同时执行，因此除了把其它 Activity 类列入清单之外、大家也能够以与主 Activity 类似的方式在应用程序当中处理这些类。我们也可以为每个 Activity 创建一个布局文件，并通过设置让其使用与主 Activity 同样的技术机制。

在某个 Activity 的 onCreate 方法开始执行之后，onStart 与 onResume 两个方法也将开始执行， 从而使该 Activity 处于 Resumed 状态、并在后续执行过程中根据情况转换为 Created 以及 Started 状态。

我们的 Activity 可以通过不只一种方式进入 Resumed 状态，应用程序启动只是其中最基本的途径。如果 Activity 处于 Paused 或者 Stopped 状态，则应用程序切换至当前之后该 Activity 将直接进入前台运行模式，且无需重复调用 onCreate 方法。如果大家的应用从 Paused 状态切换回 Resumed 状态，则 Activity 的 onResume 方法将开始执行。如果该应用由 Stopped 状态切换回运行状态，则执行 onRestart 方法、而后依次为 onStart 与 onResume 方法。

**3.进入 Destroyed 状态**
**第一步**
当我们的应用程序处于退出或者隐藏状态下，则 Resumed 就会转变为 Destroyed。这时候，onPause 方法会将应用的 Activity 由运行时的 Resumed 状态转换为 Paused 状态。在 onPause 当中，大家应当停止任何需要占用资源的任务，例如动画播放、传感器数据处理以及广播接收等等。如果 onPause 正在执行，那么 onStop 也可以开始执行，因为用户此时通常已经通过导航退出了我们的应用程序。大家还可以利用 onPause 方法进行数据保存——虽然通常来说数据保存工作由 onStop 方法来负责最为妥当。

正如我们之前曾经提到，大家的 Activity 能够通过 onResume 方法从 Paused 状态重新回归至 Resumed 状态。这意味着我们可以利用 onResume 来恢复任何我们之前在 onPause 当中停止或者发布过的内容。不过大家还需要记住一点，onResume 在其它情况下也会付诸执行，例如在应用程序启动时。

**第二步**
在 onPause 之后，如果应用程序进入 Stopped 状态，那么 onStop 也将开始执行。在这种情况下，onRestart、onStart 以及 onResume 等方法仍然能够使应用程序重新回到 Resumed 状态。在 onStop 中，大家应当尽可能压缩只在必要数据的操作量，例如向数据库中写入内容。请大家确保在 onStop 当中囊括了所有应用程序所使用的资源，从而避免该应用在被彻底关闭之后导致内存溢出问题。

这套系统会在应用程序从 resumed 状态切换至 stopped 状态后保存特定数据，例如视图中需要显示的内容。当某个 Activity 从 Stopped 状态恢复到 Resumed 状态时，onRestart、onStart 以及 onResume 方法都会开始执行。不过 onStart 与 onResume 的执行情况有所不同——例如在应用程序启动之时。而 onRestart 方法只会在应用程序从 Stopped 状态恢复至前台之后才会执行，这样大家就能利用它来恢复任何保存在 onStop 当中的运行内容。

提示:当大家从一个 Activit 之下启动另一个 Activity 时，前者会进入 Stopped 状态。如果用户随后利用后退按钮再次由后者返回先前的 Activity 当，那么前者的 onRestart 方法就会开始执行。

**第三步**
如果大家的应用程序即将彻底关闭，例如我们的当前 Activity 被从系统当中移除，则 onDestroy 方法会开始执行。尽管这是在我们的 Activity 完全消失之前执行的最后一个方法，大家仍然不应该简单地将所有内容一股脑清除。事实上，我们需要利用 onStop 或者 onPause 来处理结束工作。当然也有例外情况，如果应用程序的后台进程仍然处于运行状态，那么这时候大家应该在 onDestroy 当中将其停止。

在 onDestroy 执行之后，如果用户通过导航返回应用程序 Activity，则对应 onCreate 方法将再次被启动。一般情况下，大家可以假设 onPause 与 onStop 会在 onDestroy 之前执行。不过如果大家明确调用 finish 方法来结束一个 Activity，则只有 onDestroy 会被执行。

在多数情况下，我们并不需要为应用程序当中的生命周期回调问题投入过多精力，因为大家完全可以利用 onCreate 方法的参数实现数据保留效果。在 Activity onCreate 方法当中，Bundle 参数负责如前所述自动进行视图信息保存。不过大家也可以利用该对象保存更多数据内容，例如记录用户与应用程序之间的交互所产生的变量更新。要实现这一目标，大家可以在 Activity 类当中使用 onSaveInstanceState 方法，完成数据键值对的编写之后、我们就可能在 onCreate 当中将其恢复。

提示:当用户改变设备显示模式时，也就是在纵向及横向模式间进行切换，我们的 Activity 实际上会经历重新创建、onCreate 也会被再次执行。这一过程被我们称为配置变化。在这种情况下，系统会假设大家需要重新创建 Activity，例如大家在每种显示模式下使用不同的布局方案。不过在多数情况下，大家可能不希望系统照此办理。为了避免我们的 Activity 在显示模式转换时发生重新创建，大家可以从两种解决方式中作出选择：向清单内的 Activity 添加“android:configChanges”属性，或者调整我们的 Activity 结构、利用我们在配置变量时所保留的 Fragments。

**总结**
当大家开始学习如何为 Android 平台开发应用程序时，Activity 当中所涉及的大量状态与回调方法可能会成为很多难题乃至混乱的根源。然而在大多数情况下，我们只需要采用最低数量的方法以确保自己的应用程序有能力提供用户所预期的功能与效果。在本系列教程的下一篇当中，我们将共同了解部分常用 Android 类，大家很可能会在自己的第一款应用当中与它们打交道。在此之后，我们将着眼于 Android 代码示例、需要了解的应用程序发布知识以及其它一些关于今后进一步学习的建议。

原文链接：

http://mobile.tutsplus.com/tutorials/android/android-sdk-activities-lifecycle/