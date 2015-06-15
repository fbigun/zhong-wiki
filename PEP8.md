Python 编码风格指南

> Horin|贺勤
> Email: horin153@msn.com
> Blog: http://blog.csdn.net/horin153/

PEP:  8
Title:  Style Guide for Python Code
Version:  54700
Url:  http://www.Python.org/dev/peps/pep-0008/


译者：为了尽可能使译文保留原滋原味，译者尽可能进行直译；保留原始文档的布局、缩
> 进、换行风格 (阅读时请最大化)；尽量不在译文中穿插个人评注。
> 对有疑问的翻译，在译文后面的括号中给出原文；对部分标题和专业词汇，同时给出
> 原文和译文，以方便阅读。

> 感谢《Python 开发编码规范》一文及其作者，本文的很多句子、段落是对该文的直接
> 引用、或者略加修改。参见：
> http://wiki.woodpecker.org.cn/moin/PythonCodingRule

> 尽管逐词逐句都进行过认真推敲，但囿于能力，本文仍有很多不当、甚至错误的翻译
> ；请读者海涵，并敬请指正；联系方式：horin153@msn.com。


介绍

> 这篇文档所给出的编码约定，适用于在主要的 Python 发布版本中组成标准库的
> Python 代码。在 Python 的 C 实现中 C 代码风格指南的描述，请查阅姊妹篇
> PEP 7。

> 这篇文档改编自 Guido 最初的《Python Style Guide》一文。并从《Barry's style
> guide》中添加了部分内容。在有冲突的地方，Guide 的风格规则应该是符合本 PEP
> 的意图。这篇 PEP 可能仍是不完善的 (实际上，它可能永远不会完美)。


令人讨厌的小人物身上愚蠢的一致性
(A Foolish Consistency is the Hobgoblin of Little Minds)

> Guido 的主要洞察力 (key insights) 之一是：代码更多是用来读而不是写。故本
> 指南致力于改善 Python 代码的可读性、使不同的 (wide spectrum) Python 代码
> 保持一致性。正如 PEP 20 所说的可读性计算 (Readability counts)。

> 风格指南是关于一致性的。风格一致对本指南是重要的，对一个项目更重要。在一个
> 模块、或者函数内保持 (代码风格) 一致最重要。

> 但最重要的是：知道何时会不一致 -- 有时只是没有实施风格指导。当有疑惑时，运
> 用你的最佳判断。看看别的例子，然后决定怎样看起来更好。并且要不耻下问！

> 打破一条既定规则的两个好理由：

> (1) 当应用这条规则时将导致代码可读性下降，即便对某人来说，他已经习惯于按这
> > 条规则来阅读代码了。


> (2) 为了和周围的代码保持一致而打破规则 (也许是历史原因) -- 虽然这也是个清除
> > 其他混乱的好机会 (在真正的 XP 风格中)。


代码布局 (Code lay-out)


> 缩进 (Indentation)

> 每级缩进用 4 个空格。

> 为避免与旧代码混淆，可继续采用 8 个空格宽的 tab 缩进。

> Tab 还是空格 (Tabs or Spaces)？

> 绝不要混合使用 tab 和空格。

> 最流行的 Python 缩进方式是仅使用空格，其次是仅使用制表符。混合着制表符和空
> 格缩进的代码将被转换成仅使用空格。调用 Python 命令行解释器时使用 -t 选项，
> 可对代码中不合法的混用制表符和空格发出警告 (warnings)。使用 -tt 时警告将变
> 成错误。这些选项是被高度推荐的。

> 对新项目，强烈推荐只用空格，而不是用 tabs。大多数编辑器拥有使之易于实现的功
> 能。

> 最大行宽 (Maximum Line Length)

> 限制所有行的最大行宽为 79 字符。

> 周围仍然有许多设备被限制在每行 80 字符；而且，窗口限制在 80 个字符，使将多
> 个窗口并排放置成为可能。在这些设备上使用默认的折叠 (wrapping) 方式看起来有
> 点丑陋。 因此，请将所有行限制在最大 79 字符。对顺序排放的大块文本 (文档字符
> 串或注释 (docstrings or comments))，推荐将长度限制在 72 字符。

> 折叠长行的首选方法是使用 Python 支持的圆括号、方括号 (brackets) 和花括号
> (braces) 内的行延续。如果需要，你可以在表达式周围增加一对额外的圆括号，但是
> 有时使用反斜杠看起来更好。确认恰当地缩进了延续的行。一些例子：

> class Rectangle(Blob):

> def init(self, width, height,
> > color='black', emphasis=None, highlight=0):
> > if width == 0 and height == 0 and \
> > > color == 'red' and emphasis == 'strong' or \
> > > highlight > 100:
> > > > raise ValueError("sorry, you lose")

> > if width == 0 and height == 0 and (color == 'red' or
> > > emphasis is None):
> > > raise ValueError("I don't think so")

> > Blob.init(self, width, height,
> > > color, emphasis, highlight)


> 空行 (Blank Lines)

> 用两行空行分割顶层函数和类的定义。

> 类内方法的定义用单个空行分割。

> 额外的空行可被用于 (保守的 (sparingly)) 分割相关函数群 (groups of
> related functions)。在一组相关的单句 (related one-liners) 中间可以省略空行
> (例如一组哑元 (dummy implementations))。

> 在函数中使用空行时，请谨慎的用于表示一个逻辑段落 (logical sections)。

> Python 接受 contol-L (即 ^L) 换页符作为空白符 (whitespace)；许多工具视这些
> 字符为分页符 (page separators)，因此在你的文件中，可以用它们来为相关片段
> (sections) 分页。

> 编码 (Encodings) (PEP 263)

> Python 核心发布中的代码应该始终使用 ASCII 或 Latin-1 编码(又名ISO-8859-1)。

> 使用ASCII的文件不必有译码 cookie (coding cookie)。 Latin-1 仅当注释或文档字
> 符串涉及作者名字需要 Latin-1 时才被使用；另外使用 \x 转义字符是在字符串中包
> 含非 ASCII 数据的首选方法。


导入 (Imports)

> - 通常应该在单独的行中导入，例如：

> Yes: import os
> > import sys


> No:  import sys, os

> 但是这样也是可以的：

> from subprocess import Popen, PIPE

> - Imports 通常被放置在文件的顶部，仅在模块注释和文档字符串之后，在模块的全
> > 局变量和常量之前。


> Imports应该按照如下顺序成组安放：

  1. 标准库的导入
> 2. 相关的第三方包的导入
> 3. 本地应用/库的特定导入

> 你应该在每组导入之间放置一个空行。

> 把任何相关 all 说明的放在 imports 之后。

> - 对于内部包的导入是非常不推荐使用相对导入的。对所有导入总是使用包的绝对路
> > 径。即使现在 PEP 328 [7](7.md) 在 Python 2.5 中被完整实现了，其 explicit
> > relative imports 的风格也是不推荐的。绝对导入能更好的移植 (portable)，通
> > 常也更易读。


> - 从一个包含类的模块中导入类时，通常可以写成这样：

> from myclass import MyClass
> from foo.bar.yourclass import YourClass

> 如果这样写导致了本地名字冲突，那么就这样写：

> import myclass
> import foo.bar.yourclass

> 并使用 "myclass.MyClass" and "foo.bar.yourclass.YourClass"


在表达式和语句中的空格 (Whitespace in Expressions and Statements)

> 宠物的烦恼 (Pet Peeves)
> (注：即无伤大雅的小问题)

> 避免在下述情形中使用无关的空格：

> - 紧挨着圆括号、方括号和花括号：

> Yes: spam(ham[1](1.md), {eggs: 2})
> No:  spam( ham[1 ](.md), { eggs: 2 } )

> - 紧贴在逗号、分号或冒号前：

> Yes: if x == 4: print x, y; x, y = y, x
> No:  if x == 4 : print x , y ; x , y = y , x

> - 紧贴着函数调用的参数列表前的开式括号：

> Yes: spam(1)
> No:  spam (1)

> - 紧贴在索引或切片 (indexing or slicing) 开始的开式括号前：

> Yes: dict['key'] = list[index](index.md)
> No:  dict ['key'] = list [index](index.md)

> - 在赋值 (或其他) 运算符周围的用于和其他语句对齐的一个以上的空格：

> Yes:

> x = 1
> y = 2
> long\_variable = 3

> No:

> x             = 1
> y             = 2
> long\_variable = 3


> 其他建议 (Other Recommendations)

> - 始终在这些二元运算符两边放置一个空格:
> > assignment (=), augmented assignment (+=, -= etc.),
> > comparisons (==, <, >, !=, <>, <=, >=, in, not in, is, is not),
> > Booleans (and, or, not).


> - 在数学运算符两边使用空格：

> Yes:

> i = i + 1
> submitted += 1
> x = x **2 - 1
> hypot2 = x** x + y **y
> c = (a + b)** (a - b)

> No:

> i=i+1
> submitted +=1
> x = x\*2 - 1
> hypot2 = x\*x + y\*y
> c = (a+b) **(a-b)**

> - 不要在用于指定关键字参数 (keyword argument) 或默认参数值的 '=' 号周围使用
> > 空格。


> Yes:

> def complex(real, imag=0.0):
> > return magic(r=real, i=imag)


> No:

> def complex(real, imag = 0.0):
> > return magic(r = real, i = imag)


> - 复合语句 (Compound statements) (多条语句写在同一行) 一般不推荐。

> Yes:

> if foo == 'blah':
> > do\_blah\_thing()

> do\_one()
> do\_two()
> do\_three()

> Rather not:

> if foo == 'blah': do\_blah\_thing()
> do\_one(); do\_two(); do\_three()

> - 虽然有时可以在 if/for/while 的同一行跟一小段代码，但绝不要对多条子句
> > (multi-clause statements) 也这样做。也避免折叠这样的长行。


> 最好不要 (Rather not)：

> if foo == 'blah': do\_blah\_thing()
> for x in lst: total += x
> while t < 10: t = delay()

> 明确不要 (Definitely not)：

> if foo == 'blah': do\_blah\_thing()
> else: do\_non\_blah\_thing()

> try: something()
> finally: cleanup()

> do\_one(); do\_two(); do\_three(long, argument,
> > list, like, this)


> if foo == 'blah': one(); two(); three()


注释 (Comments)

> 同代码不一致的注释比没注释更差。当代码修改时，始终优先更新注释！

> 注释应该是完整的句子。如果注释是一个短语或句子，首字母应该大写，除非它是一
> 个以小写字母开头的标识符 (永远不要修改标识符的大小写)。

> 如果注释很短，可以省略末尾的句号。注释块通常由一个或多个段落组成，段落是由
> 完整的句子构成的，每个句子应该以句号结尾。

> 你应该在结束语句的句点 (a sentence-ending period) 后使用两个空格。

> 用英语书写时，断词和空格是可用的 (When writing English, Strunk and White
> apply)。

> 非英语国家的 Python 程序员：请用英语书写你的注释，除非你 120% 的确信代码永
> 远不会被不懂你的语言的人阅读。


> 注释块 (Block Comments)

> 注释块通常应用于跟随其后的一些 (或者全部) 代码，并和这些代码有着相同的缩进
> 层次。注释块中每行以 '#' 和一个空格开始 (除非它是注释内的缩进文本)。

> 注释块内的段落以仅含单个 '#' 的行分割。

> 行内注释 (Inline Comments)

> 节俭使用行内注释。

> 一个行内注释是和语句在同一行的注释。行内注释应该至少用两个空格和语句分开。
> 它们应该以一个 '#' 和单个空格开始。

> 行内注释不是必需的，事实上，如果说的是显而易见事，还会使人分心。不要这样做
> ：

> x = x + 1                 # Increment x

> 但是有时，这样是有益的:

> x = x + 1                 # Compensate for border


文档字符串 (Documentation Strings)

> 书写好的文档字符串 (又名"docstrings") 的约定，在 PEP 257 [3](3.md) 中是永存的。

> - 为所有公共模块、函数、类和方法书写文档字符串。文档字符串对非公开的方法不
> > 是必要的，但你应该有一条注释来描述这个方法做什么；这条注释应该出现在
> > "def" 行之后。


> - PEP 257 描述了好的文档字符串约定。一定注意，多行文档字符串结尾的 """ 应该
> > 单独成行，并推荐在其前加一空行，例如：


> """Return a foobang

> Optional plotz says to frobnicate the bizbaz first.

> """

> - 对单行的文档字符串，结尾的 """ 在同一行也可以。


版本注记 (Version Bookkeeping)

> 如果你必须把 Subversion、CVS、or RCS crud 包含在你的源文件中，按如下做：

> version = "$Revision: 54700 $"
  1. $Source$

> 这些行应该包含在模块的文档字符串之后，任何其他代码之前，上下各用一个空行分
> 隔 。


命名约定 (Naming Conventions)

> Python 库的命名约定有点混乱，所以我们将永远不能使之变得完全一致。不过还是有
> 普遍推荐的命名规范的。新的模块和包 (包括第三方的框架) 应该根据这些标准书写
> ，但对有不同风格的已有的库，保持内部的一致性是首选的。

> 描述：命名风格 (Descriptive: Naming Styles)

> 有许多不同的命名风格。以下的有助于辨认正在使用的命名风格，这独立于它们的作
> 用。

> 以下的命名风格是众所周知的：

> - 单个小写字母 (b)

> - 单个大写字母 (B)

> - 小写串 (lowercase)

> - 带下划线的小写串 (lower\_case\_with\_underscores)

> - 大写串 (UPPERCASE)

> - 带下划线的大写串 (UPPER\_CASE\_WITH\_UNDERSCORES)

> - 首字母大写单词串 (CapitalizedWords) (或 CapWords、CamelCase -- 因其字母看
> > 起来错落有致，故得此名)。有时这也被称作 StudlyCaps。


> 注意: 在 CapWords 中使用缩写，需要把缩写的所有字母大写。故
> HTTPServerError 比 HttpServerError 更好。

> - 混合大小写串 (mixedCase) (与首字母大写串不同之处在于第一个字符是小写的！)

> - 带下划线的首字母大写串 (Capitalized\_Words\_With\_Underscores) (丑陋！)

> 还有一种风格，使用特别的短前缀来将相关的名字分成组。这在 Python 中不常用，
> 但是出于完整性要提一下。例如，os.stat() 函数返回一个 tuple，其元素传统上有
> 象 st\_mode, st\_size, st\_mtime 等等这样的名字。(这样做是为了强调与 POSIX 系
> 统调用结构体的相关性，这有助于程序员熟悉那些相关性。)

> X11 库的所有公开函数以 X 开头。在 Python 中，这个风格通常认为是不必要的，因
> 为属性和方法名以对象作前缀，而函数名以模块名作前缀。

> 另外，以下用前导或后置下划线的特殊形式是被公认的 (通常这些可以和任何习惯相
> 组合):

> - **single\_leading\_underscore:
> > (单前导下划线): 弱的 "内部使用 (internal use)" 标志。
> > 例如，"from M import _" 不会导入以下划线开头的对象。_


> - single\_trailing\_underscore_:
> > (单后置下划线): 习惯上用于避免与 Python 关键词的冲突。
> > 例如：
> > Tkinter.Toplevel(master, class_='ClassName')**


> - double\_leading\_underscore:
> > (双前导下划线): 当用于命名 class 属性时，会触发名字重整 (name mangling)。
> > (在类 FooBar 中，boo 变成 _FooBar__boo；参加下面)。_


> - double\_leading\_and\_trailing\_underscore:
> > (双前导和后置下划线)：存在于用户控制的 (user-controlled) 名字空间的
> > "magic" 对象或属性。例如:
> > init, import or file
> > 决不要发明这样的名字，仅像文档中那样使用即可。


> 说明：命名约定 (Prescriptive: Naming Conventions)

> 避免采用的名字 (Names to Avoid)

> 决不要用字符 'l' (小写字母 el)，'O' (大写字母 oh)，或 'I' (大写字母 eye)
> 作为单个字符的变量名。

> 在一些字体中，这些字符不能与数字 1 和 0 区别开。当想要使用 'l' 时，用'L'
> 代替它。

> 包和模块名 (Package and Module Names)

> 模块名应该是简短的、全部小写的名字。可以在模块名中使用下划线以提高可读性
> 。Python 包名也应该是简短的、全部小写的名字，尽管不推荐使用下划线。

> 因为模块名被映射到文件名，有些文件系统大小写不敏感并且截短长名字，所以把
> 模块名选择为相当短就很重要了 -- 这在 Unix 上不是问题，但当把代码迁移到
> Mac、Windows 或 DOS 上时，就可能是个问题了。

> 当一个用 C 或 C++ 写的扩展模块，有一个伴随的 Python 模块来提供一个更高层
> (例如，更面向对象) 的接口时，C/C++ 模块名有一个前导下划线 (如：_socket)。_

> 类名 (Class Names)

> 几乎没有例外，类名使用首字母大写单词串 (CapWords) 的约定。
> 内部使用的类使用一个额外的前导下划线。

> 异常名 (Exception Names)

> 因为异常应该是类，故类命名约定也适用于异常。然而，你应该对异常名添加后缀
> "Error" (如果该异常的确是一个错误)。

> 全局变量名 (Global Variable Names)

> (让我们希望这些变量只打算用于一个模块内部。) 这些约定与那些用于函数的约
> 定差不多。

> 对设计为通过 "from M import **" 来使用的模块，应采用 all 机制来防止导
> 出全局变量；或者使用旧的约定，为该类全局变量加一个前导下划线 (可能你想表
> 明这些全局变量是 "module non-public")。**

> 函数名 (Function Names)

> 函数名应该为小写，必要时可用下划线分隔单词以增加可读性。

> 混合大小写 (mixedCase) 仅被允许用于这种风格已经占优势的上下文 (如:
> threading.py)，以便保持向后兼容。

> 函数和方法的参数 (Function and method arguments)

> 对实例的方法，总是用 'self' 做第一个参数。

> 对类的方法，总是用 'cls' 做第一个参数。

> 如果函数的参数名与保留关键字冲突，在参数名后加一个下划线，比用缩写、错误
> 的拼写要好。因此 "print_" 比 "prnt" 好。(也许使用同义词来避免冲突更好。)_

> 方法名和实例变量 (Method Names and Instance Variables)

> 采用函数命名规则：小写单词，必要时可用下划线分隔单词以增加可读性。

> 仅对 non-public 方法和实例变量采用一个前导下划线。

> 为避免与子类命名冲突，采用两个前导下划线来触发 Python 的命名重整规则。

> Python 用类名重整这些名字：如果类 Foo 有一个属性名为 a， 它不能以
> Foo.a 访问。(执著的用户还是可以通过 Foo._Foo__a 得到访问权。) 通常，双
> 前导下划线仅被用来避免与基类的属性发生名字冲突。_

> 注：关于 names 的作用存在一些争论 (见下面)。

> 继承的设计 (Designing for inheritance)

> 总是确定类的方法和实例变量 (统称为属性) 是否应该被公开或者不公开。如果有
> 疑问，选择不公开；今后把其改为公开比把一个公开属性改为非公开要容易。

> 公开属性是那些你期望你的类的不相关的客户使用，并根据你的承诺来避免向后不
> 兼容变更。非公开属性是那些确定不给第三方使用的；你不保证非公开属性不变、
> 甚至被移除。

> 这里我们不使用术语 "private"，因为在 Python 中没有属性是真正私有的 (没有
> 通常的无用功 (unnecessary amount of work))。

> 另一类属性是 "subclass API" 的一部分 (在其他语言中通常称为 "protected")。
> 一些类被设计为基类，要么被扩展，要么类的某些行为被修改。当设计这样的类时
> ，注意明确决定哪些属性是公开的，哪些是子类 API 的一部分，及哪些是真正仅被
> 你的基类使用。

> 谨记这些 Python 特色的指导方针：

> - 公开属性应该没有前导下划线。

> - 如果公开属性名和保留关键字冲突，在你的属性名后添加一个后置下划线。这比
> > 缩写或者错误的拼写更可取。(然而，尽管这条规则，对任何已知是类的变量或者
> > 参数，尤其是类方法的第一个参数，'cls' 是首选拼写方式。)


> 注1：参见上面对类方法的参数名的建议。

> - 对简单的公开数据属性 (data attribute)，最好只暴露属性名，没有复杂的访问
> > /修改方法 (accessor/mutator methods)。谨记 Python 为将来增强提供了一条
> > 容易的途径，你应该发现简单数据属性需要增加功能行为。在那种情况，用特性
> > (properties) 把功能实现隐藏在简单数据属性访问语法后面。


> 注1：特性仅工作于 new-style 的类。

> 注2：尝试不管功能行为的副作用，尽管像 cache 之类副作用通常是好的。

> 注3：避免对费时的计算操作使用特性；属性符号使调用者相信访问是 (相对)
> > 廉价的。


> - 如果确定你的类会被子类化，并且你有不希望子类使用的属性，考虑用两个前导
> > 下划线、但没有后置下划线命名它们。这将触发 Python 的名字重整算法，把类
> > 名整合进属性名中。当子类无意中包含了相同名字的属性时，这有助于避免属性
> > 名冲突。


> 注1：注意仅使用简单类名来重整名字，因此，如果子类使用相同的类名和属性名
> > ，你仍然会名字冲突。


> 注2：名字重整使一些应用稍有不便，例如调试和 getattr()。然而名字重整
> > 算法有良好的文档，也容易手工执行。


> 注3：不是每个人都喜欢名字重整。尝试在避免意外的名字冲突需求和高级调用者
> > 的可能应用之间平衡。


设计建议 (Programming Recommendations)


> - 某种程度上，代码不应该不利于其他 Python 实现 (PyPy, Jython, IronPython,
> > Pyrex, Psyco, 等等)。


> 例如，对 a+=b or a=a+b 形式的语句，不要依赖 CPython 对就地 (in-place) 字
> 符串连接的高效实现。那些语句在 Jython 中运行很慢。对库的性能敏感部分，应
> 该改用  ''.join() 语句。这将保证对不同的实现，字符串连接表现为线性时间。

> - 与 None 之类的单件比较，应该总是用 'is' or 'is not'，绝不要用等号操作符。

> 同样，当你本意是 "if x is not None" 时，对写成 "if x" 要小心 -- 例如，当
> 测试一个默认为 None 的变量或参数是否被设置为其他值时,这个其他值可能是一种
> 在布尔上下文中为假的类型 (例如容器)！

> - 使用基于类的异常。

> 在新代码中，禁止使用字符串异常 (String exceptions)，因为这一语言特征将在
> Python 2.6 中被移除。

> 模块和包应该定义它们自己的特定域的异常基类，该异常基类应该是内建异常类的
> 子类。还始终包含一个类的文档字符串。例如：

> class MessageError(Exception):
> > """Base class for errors in the email package."""


> 类命名约定也适用于这里，尽管当异常是错误时，你应该添加 "Error" 后缀到你的
> 异常类。非错误类异常不需要特殊后缀。

> - 当 raise 一个异常时，使用 "raise ValueError('message')" 代替旧的 "raise
> > ValueError, 'message'"。


> 首选采用使用圆括号的形式，因为当异常参数很长或者包括格式化字符串时，你不
> 需要使用行延续符，感谢包含的圆括号。在 Python 3000 中将移除旧的形式。

> - 在捕获异常时，尽可能写出明确的异常，而不是使用空的 'except:' 子句。

> 例如使用：

> try:
> > import platform\_specific\_module

> except ImportError:
> > platform\_specific\_module = None


> 空的 'except:' 子句将捕获 SystemExit and KeyboardInterrupt 异常，这使得用
> Control-C 中断程序变得困难，也会掩饰其他问题。如果你想捕获全部导致程序错
> 误的异常，就使用 'except StandardError:'。

> 一个好的经验方法是把空的 'except' 子句限制用在两种情况：

  1. 如果异常处理器将打印出或者日志记录 traceback，至少用户将知道有错误
> > 发生。


> 2) 如果代码需要做一些清除工作，但然后用 'raise' 来向上传播异常。对这种
> > 情况，'try...finally' 是一种更好的处理方法。


> - 另外，对所有 try/except 子句，把 'try' 子句限制在有需要的绝对最少量代码。
> > 这再次避免掩饰 bugs。


> Yes:

> try:
> > value = collection[key](key.md)

> except KeyError:
> > return key\_not\_found(key)

> else:
> > return handle\_value(value)


> No:

> try:
    1. Too broad!
> > return handle\_value(collection[key](key.md))

> except KeyError:
    1. Will also catch KeyError raised by handle\_value()
> > return key\_not\_found(key)


> - 使用字符串方法代替 string 模块。

> 字符串方法总是很快，而且和 unicode 字符串共用同样的 API。如果必须向后兼容
> Python 2.0 以前的版本，可不考虑此规则。

> - 使用 ''.startswith() and ''.endswith() 代替字符串切片，来检查前缀和后缀。

> startswith() and endswith() 更清晰易读，也倾向于减少错误。例如：

> Yes: if foo.startswith('bar'):

> No:  if foo[:3] == 'bar':

> 如你的代码必须工作在 Python 1.5.2 (希望不是！)，则除外。

> - 对象类型的比较应该始终用 isinstance() 代替直接比较类型。

> Yes: if isinstance(obj, int):

> No:  if type(obj) is type(1):

> 检查一个对象是否是字符串时，紧记它也可能是 unicode 字符串！在 Python 2.3
> 中，str 和 unicode 有公共的基类 basestring，所以你可以这样做：

> if isinstance(obj, basestring):

> 在 Python 2.2 中，types 模块为此定义了 StringTypes 类型，例如：

> from types import StringTypes
> if isinstance(obj, StringTypes):

> 在 Python 2.0 和 2.1 中，你应该这样做：

> from types import StringType, UnicodeType
> if isinstance(obj, StringType) or \
> > isinstance(obj, UnicodeType) :


> - 对序列 (字符串 (strings)，列表 (lists)，元组 (tuples))，使用空序列为假这
> > 个事实。


> Yes: if not seq:
> > if seq:


> No: if len(seq)
> > if not len(seq)


> - 不要书写依赖于有意义的后置空白字符的文本字符串。这种后置空白字符在视觉上
> > 不可区分，并且有些编辑器 (或者最近，reindent.py) 会将它们裁剪掉。


> - 不要用 == 来把布尔值与 True 或 False 进行比较。

> Yes:   if greeting:

> No:    if greeting == True:

> Worse: if greeting is True:


References
> [1](1.md) PEP 7, Style Guide for C Code, van Rossum

> [2](2.md) http://www.python.org/doc/essays/styleguide.html

> [3](3.md) PEP 257, Docstring Conventions, Goodger, van Rossum

> [4](4.md) http://www.wikipedia.com/wiki/CamelCase

> [5](5.md) Barry's GNU Mailman style guide
> > http://barry.warsaw.us/software/STYLEGUIDE.txt


> [6](6.md) PEP 20, The Zen of Python

> [7](7.md) PEP 328, Imports: Multi-Line and Absolute/Relative


Copyright
> This document has been placed in the public domain.