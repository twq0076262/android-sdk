# Android SDK 上手指南：应用程序数据

> 从广义上讲，Android 应用中的数据存储选项共有五种主要类型：将数据保存在应用的共享偏好当中、保存在内部存储（专属于应用本身）当中、保存在外部存储（向设备公开）当中、保存在数据库当中以及保存在可通过设备互联网连接访问的 Web 资源当中。

在本系列教程当中，我们将学习如何从零开始进行 Android SDK 开发。我们已经熟悉了 Android 应用程序的结构与基本组成元素，其中包括资源、清单与用户界面。在着手进行 Android 平台的功能性应用开发之后，大家肯定需要保存这样或者那样的数据信息。Android 平台提供多种选项，用于打理应用程序中的数据存储任务，而这正是今天这篇文章要讨论的核心内容。

**介绍**

从广义上讲，Android 应用中的数据存储选项共有五种主要类型：将数据保存在应用的共享偏好当中、保存在内部存储（专属于应用本身）当中、保存在外部存储（向设备公开）当中、保存在数据库当中以及保存在可通过设备互联网连接访问的 Web 资源当中。受篇幅所限，我们无法详细对这些选项作出论述，但会对每种方案的基础特性加以概括、从而帮助大家在需要使用持久化数据时理清存储问题的解决思路。

**1. 共享偏好**

**第一步**

共享偏好允许大家以键-值对的形式保存基本数据类型。应用程序的共享偏好文件通常被视为最简单的数据存储选项，但从本质上说它对于存储对象提出了一定程度的限制。大家可以通过它存储基本类型数字（如整数、长数以及浮点数字）、布尔值以及文本字符串。我们需要为自己保存的每个数值分配一个名称，从而在应用程序运行时据此对其进行检索。由于大家很可能在自己创建的第一款应用中就用到共享偏好，因此我们人把它作为讲解的重点、以更为详尽的方式（相较于其它选项）进行表述，从而帮助各位巩固必要知识。

大家可以在自己的主 Activity 类中尝试这些代码，并在稍后运行本系列教程的应用示例时对其加以测试。在理想情况下，共享偏好应该可以符合应用程序中的用户配置选项，如同选择外观设置一样。大家应该还记得，我们曾经创建过一个简单的按钮，用户点击它之后屏幕上会显示出“Ouch”文本内容。现在让我们假设自己希望用户在点击一次之后，该按钮上会持续显示“Ouch”字样，且该状态在应用程序运行过程中始终保持不变。这意味着按钮上的初始文本仅在用户首次点击操作之前存在。

让我们为应用程序添加共享偏好内容。在该类的起始位置、onCreate 方法之前，我们为共享偏好选择一个名称：

```
public static final String MY_APP_PREFS = &quot;MyAppPrefs&quot;; 
```

利用“public static”修饰符，我们可以访问处于应用内任何类中的这项变量，因此我们只需要将偏好名称字符串保存在这里即可。我们使用大写是因为该变量属于常数，“final”修饰符也是因此而存在。每一次检索或者在应用程序偏好当中设置数据条目时，大家都必须使用同样的名称。

**第二步**

现在我们来编写共享偏好内容。在我们的 onClick 方法中、按钮“Ouch”文本设置部分的下方，尝试通过名称取回这条共享偏好：

```
SharedPreferences thePrefs = getSharedPreferences(MY_APP_PREFS, 0); 
```

大家需要为“android.conent.SharedPreferences”类添加一条导入。将鼠标悬停在“SharedPreferences”文本上方，并利用 Eclipse 提示完成导入。第一项参数是我们所定义的偏好名称，第二项则是我们作为默认选项的基本模式。

现在我们需要为共享偏好指定一套编辑器，从而实现对其中数值的设定：

```
SharedPreferences.Editor prefsEd = thePrefs.edit(); 
```

现在我们可以向共享偏好当中写入值了：

```
prefsEd.putBoolean(&quot;btnPressed&quot;, true);
```

这里我们使用了布尔类型，因为当前状态只分为两种——用户已经或者尚未按下按钮。编辑器提供多种不同类型，我们可以从中选择以保存这套共享偏好，其中每种方法都拥有自己的名称与值参数。最后，我们需要提交编辑结果：

```
prefsEd.commit(); 
```

**第三步**

现在让我们利用已经保存的值来检测用户运行应用程序后，按钮应该显示什么样的内容。在 onCreate 中的现有代码之后添加共享偏好：

```
SharedPreferences thePrefs = getSharedPreferences(MY_APP_PREFS, 0); 
```

这一次我们不必使用编辑器，因为我们只需要获取一个值：

```
boolean pressed = thePrefs.getBoolean(&quot;btnPressed&quot;, false);
```
 
现在我们利用已经设置过的名称检索该值，并读取变量中的结果。如果该值尚未被设置，返回的则为第二项参数，也就是默认值——代表否定含义。现在让我们使用该值：

```
if(pressed) theButton.setText(&quot;Ouch&quot;);
```
 
如果用户在应用程序运行之后按下该按钮，则按钮直接显示“Ouch”字样。在本系列的后续文章当中，大家会看到我们在应用运行中进行这一操作的情况。这个简单的例子很好地诠释了共享偏好的使用过程。大家会发现，共享偏好在帮助应用程序通过外观及使用感受迎合用户喜好方面具有重要的作用。

**2. 私有内部文件**

**第一步**

大家可以将文件保存在用户设备的内部以及外部存储当中。如果将文件保存在内部存储中，Android 系统会将其视为专属于当前应用的私有数据。这类文件基本上属于应用程序的组成部分，我们无法在应用程序之外直接对其进行访问。再有，如果应用程序被移除、这些文件也会同时被清空。

大家可以利用以下输出例程在内存存储中创建一个文件：

```
FileOutputStream fileOut = openFileOutput(&quot;my_file&quot;, Context.MODE_PRIVATE);
```
 
大家需要为“java.io.FileOutputStream”类进行导入添加。我们提供了文件名称与模式，选择私有模式意味着该文件将只能被该应用程序所使用。如果大家现在就把这部分代码加入到 Activity 当中，例如 onClick 方法中，Eclipse 将弹出错误提示。这是因为当我们进行输入/输出操作时，应用程序可能遭遇一些需要应对的错误。如果大家的输入/输出操作无法解决这类错误，Eclipse 就会提示异常状况、应用程序也会中止运行。为了保证应用程序在这种情况下仍能正常运行，我们需要将自己的输入/输出代码封装在 try 代码块当中：

```
try{     FileOutputStream fileOut = openFileOutput(&quot;my_file&quot;, Context.MODE_PRIVATE); 
} catch(IOException ioe){     
Log.e(&quot;APP_TAG&quot;, &quot;IO Exception&quot;, ioe); } 
```

如果输入/输出操作导致异常，那么 catch 块中的上述代码就会付诸执行，从而将错误信息写入到日志当中。大家今后会经常用到应用程序中的 Log 类（导入‘android.util.Log’），它会记录代码执行时所发生的具体情况。我们可以为字符串标签定义一个类变量，也就是上述代码中的第一条参数。这样一旦出现错误，大家就可以在 Android LogCat 中查看异常信息了。

**第二步**

现在回到 try 块，在创建了文件输出例程之后，大家可以尝试将以下代码写入文件：

```
String fileContent = &quot;my data file content&quot;; fileOut.write(fileContent.getBytes()); 
```

在将所有必要内容写入数据文件之后，利用以下代码作为结尾：

```
fileOut.close(); 
```

**第三步**

当大家需要检索内部文件中的内容时，可以通过以下流程实现：

```
try{    
 FileInputStream fileIn = openFileInput(&quot;my_file&quot;);     
//read the file } catch(IOException ioe){     
Log.e(&quot;APP_TAG&quot;, &quot;IO Exception&quot;, ioe); } 
```

在 try 块当中，利用利用缓冲读取器读取文件内容：

```
InputStreamReader streamIn = new InputStreamReader(fileIn); 
BufferedReader fileRead = new BufferedReader(streamIn); 
StringBuilder fileBuild = new StringBuilder(&quot;&quot;); 
String fileLine=fileRead.readLine(); while(fileLine!=null){    
 fileBuild.append(fileLine+&quot;\n&quot;);     
fileLine=fileRead.readLine(); } 
String fileText = fileBuild.toString(); streamIn.close(); 
```

大家不要被其中所涉及的大量不同对象所吓倒，这其实属于标准的 Java 输入/输出操作。其中的 while 循环会在文件中的每一行执行一次。在执行完成后，“fileText”变量将把文件内容保存为字符串、以备我们直接使用。

**3. 公共外部文件**

**第一步**

只要用户设备支持，我们的应用程序也可以将文件保存在外部存储当中。外部存储种类繁多，包括 SD 卡、其它便携式介质或者用户无法移除但被系统认定为外部类型的内存存储机制。当我们将文件保存在外部存储中时，其内容将完全公开、大家也无法以任何方式阻止用户或者其它应用对其进行访问。

在我们尝试将数据保存在外部存储中之前，必须首先检查对应存储机制是否可用——尽量避免意外状况绝对是种好习惯：

```
String extStorageState = Environment.getExternalStorageState(); 
```

系统会将信息以字符串的形式返回，大家可以对其进行分析、并与 Environment 类中的外部存储状态字段加以比对：

```
if(Environment.MEDIA_MOUNTED.equals(extStorageState)){     
//ok to go ahead and read/ write to external storage } 
else if(Environment.MEDIA_MOUNTED_READ_ONLY.equals(extStorageState)){    
 //can only read } else{     //cannot read or write } 
```

即使设备上确实存在外部存储，我们也不能先入为主地假定应用可以向其写入数据。

**第二步**

在证实了我们确实能够向外部存储写入数据之后，大家接下来需要检索目录以指定文件保存的位置。以下应用程序设置内容指向八级及更高 API：

```
File myFile = new File(getExternalFilesDir(null), &quot;MyFile.txt&quot;); 
```

这样大家就可以对该文件进行写入与读取了。不过也别忘了在项目的清单文件中添加以下仅限：

```
&lt;uses-permission android:name=&quot;android.permission.WRITE_EXTERNAL_STORAGE&quot; /&gt; 
```

随着我们开发的应用程序变得愈发复杂，大家可能希望将自己保存得到的文件与其它应用共享。在这种情况下，大家可以使用公共目录下的各类通用条目，例如图片以及音乐文件。

**4. 数据库**

随着我们的应用程序所涉及的复杂结构数据越来越多，共享偏好或者内部/外部文件可能已经无法满足实际需求，这时候大家就应该考虑使用数据库方案了。Android 支持开发人员在应用程序内部创建并访问 SQLite 数据库。在我们创建一套数据库时，其将作为私有组件服务单纯服务于相关应用程序。

在 Android 应用中利用 SQLite 数据库的方法多种多样，推荐大家使用扩展 SQLiteOpenHelper 的类来实现这方面需求。在该类当中，我们需要定义数据库属性、创建各种类变量（包括我们所定义的数据库列表名称及其 SQL 创建字符串），具体代码如下所示：

```
private static final String NOTE_TABLE_CREATE =     &quot;CREATE TABLE Note (noteID INTEGER PRIMARY KEY AUTOINCREMENT, &quot; +     &quot;noteTxt TEXT);&quot;;
```
 
这里所举的例子只涉及一套非常简单的表格，其中包含两列，一列内容为 ID、另一列内容为文本；两列都用于记录用户注释信息。在 SQLiteOpenHelper 类当中，大家可以重写 onCreate 方法来创建自己的数据库。在应用程序的其它部分当中，例如 Activity 类中，大家可以通过 SQLiteOpenHelper 实现对数据库的访问，并利用 WritableDatabase 方法插入新记录、利用 getReadableDatabase 方法来查询现有记录，而后将结果显示在应用程序 UI 当中。

在对查询结果进行迭代时，我们的应用程序将使用 Cursor 类——该类会依次引用结果集中的每一行内容。

**5. 互联网数据**

很多应用都会使用互联网数据资源，而且某些应用甚至基本是由一套界面与大量 Web 数据源所构成。大家可以利用用户设备上的互联网连接来存储并检索来自 Web 的数据，只要网络连接有效、这一机制就能正常运作。为了实现这一目标，我们需要在自己的清单文件中添加“android.permission.INTERNET”权限。

如果我们希望自己的应用能够从互联网中获取数据，则必须保证这一流程脱离应用主 UI 线程。利用 AsyncTask，大家可以通过后台进程的方式从 Web 源获取数据、在数据下载完成后将结果写入 UI、最后让 UI 正常执行自身功能。

大家还可以将一个内部 AsyncTask 类添加到 Activity 类当中，并在需要获取数据的时候在该 Activity 中创建一个 AsyncTask 实例。通过在 AsyncTask 中引入 doInBackground 与 onPostExecute 两种方法，大家可以检索 Activity 中所获取到的数据并将其写入用户界面。

获取 Web 数据在应用开发工作当中属于中等难度的任务，大家最好在熟练掌握了 Android 开发知识之后再进行尝试。不过大家可能很快就会发现，这样的数据获取机制对不少应用都非常适合，因为这能有效利用用户设备的连接资源。Java 与 Android 都提供相关工具，用于处理返回的结构化数据——例如 JSON feed。

**结论**

在今天的文章中，我们基本了解了开发 Android 应用程序时需要接触到的数据存储方案。无论大家最终选择哪种方案，都应该以实际需求作为参考标准，因为不同的方案只适合特定需求。在本系列教程的下一篇当中，我们将共同探讨如何将物理设备与已安装的 Eclipse 相连、同时学习如何创建虚拟设备。在此之后，我们还将探索如何让应用程序运行在这两种类型的设备之上。顺便向大家报告，再有两篇文章本系列教程就将彻底结束；在最后一篇文章中，我们将研究通用类以及 Android Activity 生命周期，从而帮助大家做好开发应用程序的一切准备。

原文链接： http://mobile.tutsplus.com/tutorials/android/android-sdk-app-data/