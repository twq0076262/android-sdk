# Android SDK 上手指南：用户界面设计

> 我们将为应用程序项目添加布局方案，在这方面 XML 与 Eclipse ADT 接口将成为工作中的得力助手——不过在后面两节中还会用到一部分 Java 开发知识。

**内容简介**

我们将为应用程序项目添加布局方案，在这方面 XML 与 Eclipse ADT 接口将成为工作中的得力助手——不过在后面两节中还会用到一部分 Java 开发知识。XML 与 Java 在 Android 平台的开发工作当中可谓无处不在，如果大家对二者还缺乏基本的了解，请尽快想办法补补课。对于刚刚入门的读者朋友来说，本文所介绍的要点将成为各位日后开发工作的重要基础。

**1. XML 基础知识**

在我们开始讨论布局之前，先来梳理作为标记语言的 XML 的基础知识。如果大家对于 XML 已经很熟悉，可以直接跳过本节。XML 是一种用于保存数据值的语言。XML 文件在多个领域发挥作用。它们在某些项目中的功能与数据库非常相近，而且通常被作为网页的输出机制。如果大家之前曾经使用过 HTML，应该会对 XML 的基本功能感到熟悉。

在 XML 中，数据值被保存在元素当中。单一元素通常包含一个开始标记与一个结束标记，如下所示：

```
<product>Onion</product> 
```

如大家所见，开始标记与结束标记几乎完全一样，惟一的区别在于结束标记中多了一个“/”符号。在上面的例子中，数据值也就是元素内容，即文本字符串“Onion”。开始标记也可以容纳与数据项目相信的其它属性信息，如下所示：

```
<product type="vegetable">Onion</product>
```
 
每项属性都有一个名称与一个值，其中值就是引号内的部分。元素中还可以包含其它元素：

```
<section name="food"><font></font> 
<product type="vegetable">Onion</product><font></font> 
<product type="fruit">Banana</product><font></font> 
</section><font></font> 
```

在这种结构中，我们将 section 元素称为主元素、products 元素则被称为子元素。两个子元素之间属于“兄弟关系”。在 XML 文档当中，必须存在一个 root 元素作为主元素，或者被称为“嵌套”。这就构成了一种 tree 结构，其中子元素作为自主元素延伸出去的分支。如果某个子元素之下还包含其它子元素，那么它本身同时也具有主元素属性。

大家还会遇到另一种自结束元素，其中开始与结束标记并非独立存在：

```
<order number="12345" customerID="a4d45s"/> 
```

其中元素末尾的“/”符号代表结束。

我们在 Android 平台上所使用的全部资源文件都要用到 XML 标记，其中包括布局文件、可绘制元素、数据值以及 Manifest。

**2. Android 布局**

**第一步**

当大家在安装了 ADT 的 Eclipse IDE 当中使用 XML 时，输入过程中显示的相关背景提示能让编码过程变得更轻松一些。在编辑器中打开新应用中的主布局文件，确保 XML 编辑标签已经被选中，这样我们就能直接对代码进行编辑了。我们首先要处理的是用于主屏幕的布局方案，用户在启动应用之后最先看到的就是它。Eclipse 会提供一套基础布局，供我们进行个性化修改：

```
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"<font></font> 
    xmlns:tools="http://schemas.android.com/tools"<font></font> 
    android:layout_width="match_parent"<font></font> 
    android:layout_height="match_parent"<font></font> 
    android:paddingBottom="@dimen/activity_vertical_margin"<font></font> 
    android:paddingLeft="@dimen/activity_horizontal_margin"<font></font> 
    android:paddingRight="@dimen/activity_horizontal_margin"<font></font> 
    android:paddingTop="@dimen/activity_vertical_margin"<font></font> 
    tools:context=".MainActivity" ><font></font> 
    <TextView<font></font> 
        android:layout_width="wrap_content"<font></font> 
        android:layout_height="wrap_content"<font></font> 
        android:text="@string/hello_world" /><font></font> 
</RelativeLayout><font></font> 
```

如大家所见，root 元素是一项布局元素，在上面的示例中为 RelativeLayout。Android 当中还提供其它几种布局类型，我们可以将一种布局嵌套到另一种当中。这里的 root 布局元素拥有几项额外属性且与布局效果密切相关，例如宽度、高度以及边距等等。布局元素当中的 TextView 允许开发人员显示一条文本字符串。TextView 是 View 的一种，View 属于可见及交互性元素，用以构成我们的应用程序 UI。因此，应用程序中的每套分屏方案都要选择一种 View，并在其中包含一种或者多种布局机制。在 Android 系统中，这些布局被称为 ViewGroup 对象，每个 ViewGroup 内包含一套或者多套 View。

**第二步**

为了专注于一套布局的基础创建工作，我们要把主布局文件中的现有内容全部删掉，这样才能从零开始着手设计。正如我们之前所提到，大家可以利用 Java 代码创建自己的布局或者 View，不过 Android 上的多种工具允许开发者利用 XML 设计自己的应用 UI——这样各位就可以在创建元素的同时直接观察设计效果了。在某些实例中，大家可能见过单纯通过 Java 代码创建一些或者全部 UI 的做法，但现实情况下大部分创建工作还是要由 XML 完成的。这种做法还能保证应用程序逻辑与显示元素彼此独立。

```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"<font></font> 
    android:layout_width="fill_parent"<font></font> 
    android:layout_height="fill_parent"<font></font> 
    android:orientation="vertical" ><font></font> 
    <!-- views go here --><font></font> 
</LinearLayout><font></font> 
```

LinearLayout 会沿横向或者纵向显示我们打算使用的 View。在以上示例中显示方向为垂直，因此每个 View 都会沿屏幕下方依次排列。如果采取横向布局，那么各个 View 将由左至右依次排列。如果使用“layout width”与“layout height”两种属性（在 Android 当中，它们往往被称为布局参数），那么布局会被拉伸至横向与纵向的最大长度。

在“layout height”声明行之后再添加一条新行，通过键入“android：”准备开始输入属性。当大家输入对应内容，Eclipse 就会提供一套与该属性相关的列表。大家可以继续输入内容以缩小属性列表，也可以直接在列表中用鼠标进行点选。现在我们选择“android：gravity”属性。

键入“center_horizontal”作为 gravity 值，这样其中包含的元素就会以 X 轴为中心加以显示：

```
android:gravity="center_horizontal" 
```

这种方式适用于布局中的一切元素。我们可以添加其它几种额外显示属性，例如填充、边距以及背景等。不过在今天的文章中，我们先从最简单的项目入手。

**3. 添加 View**

**第一步**

正面我们开始向布局中添加 View。所谓 View，是指 UI 当中的可见元素。让我们首先添加一些文本内容和一个按钮。进入 LinearLayout 元素（在开始忹结束标记之间），输入“<”之后 Eclipse 就会提示大家与属性相关的可用元素列表。

在列表中选择 TextView。请注意，与大部分 View 一样，这是一种自结束元素。为 TextView 设置两种属性，分别为 layout width 与 layout height（键入‘android：’并选择对应提示）：

```
<TextView<font></font> 
    android:layout_width="wrap_content"<font></font> 
    android:layout_height="wrap_content" /><font></font>
```
 
通过“wrap_content”，我们可以保证 View 的宽度足以容纳其显示内容——这就避免了像布局那样以填充方式显示元素。现在再为 TextView 添加另一项属性，这一次通过列举文本字符串实现显示功能：

```
android:text="Hello there" 
```

在保存文件之后，大家会看到 Eclipse 显示出一条警告消息。如果将鼠标悬停在消息之上，编辑器的边框处将显示该文本——这部分内容也会同时显示在 Problem 视图当中。警告内容为“Hardcoded string……should use @string resource（硬编码字符串……应使用@string 资源）。”系统推荐的做法是将每一个文本字符串值保存为一项值资源，而不应将其直接包含在布局 XML 当中。尽管从起步阶段来看这样的处理方式既麻烦又毫无意义，但一旦养成良好习惯、大家会在今后的工作中逐渐发现其在大型项目中的价值。通过 Package Explorer 找出“res/values/strings.xml”文件并打开，切换到“strings.xml”标签并对代码进行编辑。

可以看到，Eclipse 已经添加了几条字符串。要另行添加，只需为其设定名称与值：

```
<string name="hello">Hello there</string> 
```

这意味着如果大家需要在应用程序 UI 当中不止一次使用同一条字符串，而且稍后又需要对其进行修改，则只需在一处做出变更即可。保存字符串文件并切换到布局文件。将 TextView 的“text”属性引用到值文件的对应字符串中：

```
android:text="@string/hello" 
```

我们通过在字符串名称前加上“@string”的方式告知 Android 工具需要在哪里寻找字符串资源。这样一来，警告信息就不会再出现了。Eclipse 通常会在我们编码的过程中发出这些提醒，从而通知我们当前存在的错误或者警示问题。大家可以选择遵循或者忽略警告信息的内容，但对于错误则必须加以调整，否则应用程序将无法正常工作。

**第二步**

在 TextView 之后添加一个 Button：

```
<Button<font></font> 
    android:layout_width="wrap_content"<font></font> 
    android:layout_height="wrap_content"<font></font> 
    android:text="@string/click" /><font></font> 
```

在我们的示例中，Button 使用的属性与 TextView 相同。不过在其它情况下，它可能会使用更多属性，而且一般来说不同视图需要配合不同属性。按钮上显示的是“text”属性值。将这条字符串同之前一样添加到我们的“res/values/strings.xml”文件当中：

```
<string name="click">Click Me!</string> 
```

在接下来的教程中，我们将处理按钮的点击效果。切换到布局文件，查看编辑器右侧的 Outline 视图——它显示的是另一套指向文件元素的界面。双击列出的项目以跳转到对应代码位置。大家也可以展开或者折叠主元素。当布局变得更加复杂时，这种处理方式就变得非常实用。

提示:要整理 Eclipse 编辑中所打开的全部文件，我们只需按下“Ctrl+A”对其进行全选，然后按下“Ctrl+I”即可。

**4. Graphical Layout**

**第一步**

确保我们的布局文件已经正确保存，然后切换到 Graphical Layout 标签。

大家可以看到自己所设计的布局已经能够直接查看。界面左侧的 Palette 区域允许我们选择 UI 项目并将其拖动到布局当中。不过我们应该首先使用 XML，直至对基本框架拥有初步概念。XML 能帮助我们控制细节设计，所以即使在使用图形化工具的时候，我们也可能需要对 XML 结果进行编辑。

在 Graphical Layout 视图上方是一套下拉清单，我们可以从中选择用于查看布局效果的设备类型，其中也提供切换显示方向及缩放效果的工具。大家需要在设计布局的过程中不断利用 Graphical Layout 对效果加以控制。另外，这里也提供其它一些值得尝试的布局元素与设置。

**第二步**

大家可能已经注意到，在这一次的布局设计当中可见元素的显示位置与屏幕上边缘靠得比较近。下面就来解决这个问题。切换到 XML 编辑标签并向 LinearLayout 当中添加边距属性：

```
android:layout_margin="10dp" 
```

我们使用“dp”来设置像素的独立密度，这样设计就会让像素密度自动与用户设备相匹配。保存文件并切换到 Graphical Layout 以查看实际效果。

在我们进行布局设计时，Graphical Layout 是一款非常实用的参考工具，但只能起到引导的效果。要了解我们的布局在应用程序运行时以怎样的方式显示、又能实现怎样的功能，大家需要将其载入虚拟或者物理设备进行实际难。我们会在后续文章中进一步讨论这个话题。

**5. 选项**

大家可以在应用程序屏幕中包含各类布局类型以及 View，但其基本处理方式都是一致的。我们前面所使用的是 LinearLayout，但还有其它多种方案可供选择，其中比较常见的有 RelativeLayout、FrameLayout、AbsoluteLayout 以及 GridLayout。大家可以在 LinearLayout Palette 当中找到这些类型，建议各位放松心态、在自己的 View 中任意选择并观察其显示效果。当添加来自 Graphical Layout 工具的元素时，请务必切换到 XML 以观察新元素的加入会产生什么样的标记代码。

Android 平台针对多种常见需求提供 View 方案，例如单选按钮、复选框以及文本输入区等。这些方案能够大大节约我们需要手动执行的功能数量；但如果各位需要使用非自带 UI 元素，则需要创建一个自定义 View 类。一般来说，最好是在没有其它选择时再这样处理，毕竟标准化 UI 元素在用户设备上的表现更为可靠，同时也能节约开发及测试的时间。

**结论**

在今天的教程中，我们讨论了 Android 平台上用户界面布局的基本设计流程，但并未做深层次挖掘。在本系列文章的下一部分，我们将尝试在应用程序添加用户交互元素、检测并响应按钮点击。接下来，我们将着眼于同 Android 开发关系最密切的 Java 相关概念，并进一步探讨应用程序开发过程中所涉及的要素及实践方式。

原文链接：

http://mobile.tutsplus.com/tutorials/android/android-sdk-user-interface-design/

原文标题：Android SDK: User Interface Design