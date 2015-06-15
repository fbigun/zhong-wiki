更新：Zhong Chen

## Quick Overview of GTK+ Concepts ##

如果你们有任何GTK+的编程经验，那么对于我将要阐述的一些概念你也许会听着犯迷糊。不过不用担心，在遇到这些概念的时候我回详细讲解，以便你能很好的阅读后面的内容。学完这一部分，对GTK+的基本概念有所了解后，你也许就能够有效的利用Glade进行开发了。

首先，GTK+并不是一门编程语言，而是一个开发工具套件，或者说是一个开发库，用来进行跨平台GUI应用程序开发，Linux, OSX, Windows或其它任何平台都能使用GTK+。GTK+就好比Windows上的MFC和Win32 API，JAVA上的Swing和SWT，或者Qt（KDE使用的GUI开发套件）。

尽管GTK+是使用C语言编写的，但是提供了其它各种语言的的捆绑，允许程序员选择自己喜欢的开发语言来开发GTK+应用程序，比如：C++, Python, Perl, PHP, Ruby等等。

GTK+开发套件基于三个主要的库：Glib, Pango和ATK，当然我们只需要关心如何使用GTK+即可，GTK+自己负责与这三个库打交道。Glib封装了大部分可移植的C库函数（允许你的代码移植到Windows和Linux上运行）。使用C或C++时，将大量使用Glib库函数，在我们用C语言的具体实现过程中我会详细解释它们。高级语言如：Python和Ruby却不用担心Glib的使用，因为它们有自己的标准库提供了相应的功能。

GTK+及相关的库是按照面向对象设计思想来实现的，至于这是如何实现的现在并不重要，不同的编程语言有不同的实现方法，重要的是要知道GTK+使用面向对象编程技术即可（似的，即使是C实现的）。

每一个 GTK+ 的 GUI 元素都是由一个或许多个 “ widgets ”对象构成的。 所有的 widgets 都从基类 GtkWidget 派生。例如， 应用程序的主窗口是 GtkWindow 类 widget ， 窗口的工具条是 GtkToolbar 类 widget 。 一个 GtkWindow 是一个 GtkWidget ， 但一个 GtkWidget 兵不是一个 GtkWindow ， 子类 widgets 继承自父类并扩展了父类的功能而成为一个新类， 这就是标准的面向对象 编程 OOP(Object Oriented Programming) 思想。
我们可以查阅 GTK+ 参考手册找到 widgets 直接的继承关系。 对于 GtkWindow 它的继承链看起来像这样：
GObject
> +----GInitiallyUnowned
> > +----GtkObject
> > > +----GtkWidget
> > > > +----GtkContainer
> > > > > +----GtkBin
> > > > > > +----GtkWindow
因此， GtkWindow 继承自 GtkBin ， GtkBin 继承自 GtkContainer ， 等等。在第一个程序中，你不需要担心 GtkWidget 对象。 各 widget 之间的继承链之所以重要是因为当你查找某个 widget 的函数， 属性和信号时， 你应该知道它的父类的函数，属性和信号也被此 widget 继承了，可以直接使用。在第二部分讲述此实例的代码时， 你能更清楚的认识到这一点。
我们来看命名规则， 命名规则带来的好处是非常便于使用。我们能够清楚 的看出对象或函数是哪个库中的。以 Gtk 开头的所有对象都是在 GTK+ 中定义的。 稍后我们会看到类似 Glade XML 以 Glade 开头的是 Libglade 库对象或函数， GError 以 G 开头的在 GLib 库定义。所有 Widgets 类都遵循标准 camelcase 命名习惯。所有操作函数都以下划线组合小写字母单词命名。如 gtk\_window\_set\_title （）设置 GtkWindow 对象的标题属性。
你需要的所有参考文档都可以从以下网站获得： library.gnome.org/devel/references ,
不过， 使用 Devhelp 更方便， 它甚至可以作为一个包来分发。 Devhelp 可以浏览或搜索任何安装在你系统上的库的相关文档， 当然前提是你必须安装了这些文档。