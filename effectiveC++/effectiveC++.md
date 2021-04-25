# 让自己习惯C++
## 条款01：视C++为一个语言联邦
*   C。区块、语句、预处理、内置数据类型、数组、指针等。
*   Object-Oriented C++。类、封装、继承、多态等
*   Template C++。
*   STL.容器、迭代器、算法、函数对象。
*   C++高效编程守则依据状态而变化。
## 条款02：尽量以const、enum、inline替换#define
*   对于单纯常量，最好以const对象或enums替换#define
*   对于形似函数的宏，最好改用inline函数替换#define
## 条款03：尽可能使用const
*   将某些东西声明为const可帮助编译器侦测出错误用法。const可被施加于任何作用域内的对象、函数参数、函数返回类型、成员函数本体
*   编译器强制实施bitwise constness，但编写程序时应，该使用概念上的常量。
*   当const和non-const成员函数有着实质等价的实现时，令non-const版本调用const版本可避免代码重复。

## 条款04：确定对象被使用前已先被初始化
*   为内置型对象进行手工初始化。因为C++不保证初始化它们。
*   构造函数最好使用成员初值列，而不要在构造函数本体内使用赋值操作。初值列列出的成员变量，其排列次序应该和它们在class中声明次序相同。
*   为免除“跨编译单元值之初始化次序”问题，请以local static对象替换non-local static对象。

#   构造、析构、赋值运算
##  条款05：了解C++默默编写并调用哪些函数
*   编译器可以暗自为class创建default构造函数、copy构造函数、copy assignment操作符、析构函数


##  条款06：若不想使用编译器自动生成的函数，就应该明确拒绝
*   为驳回编译器自动提供的机能，可将相应的成员函数声明为private并且不予实现。


##  条款07：为多态基类声明虚析构函数
*   带有多态性质的基类应该声明一个虚析构函数。如果类带有任何虚函数，它就应该拥有一个虚析构函数。

*   类的设计目的如果不是作为基类使用或不具备多态性，就不应该声明为虚函数。


##  条款08：别让异常逃离析构函数
*   析构函数绝对不要吐出异常。如果一个被析构函数调用的函数可能抛出异常，析构函数应该捕捉任何异常，然后吞下他或结束程序。

*   如果客户需要对某一个操作函数运行期间抛出的异常做出反映，那么类应该提供一个普通函数执行该操作。


##  条款09：绝不在构造和析构过程中调用虚函数
*   在构造和析构期间不要调用虚函数，因为这类调用从不下降至派生类。（比起当前执行的构造和析构函数的那一层）


##  条款10：令operator=返回一个refrence to *this
*   令赋值操作符返回一个reference to *this


##  条款11：在operator=中处理“自我赋值”
*   确保当对象自我赋值时operator=有良好行为。其中技术包括比较“来源对象”和“目标对象”的地址、精心周到的语句顺序、以及copy-and-swap

*   确定任何函数如果操作一个以上对象，而其中多个对象是同一个对象时，其行为仍然正确。


##  条款12：复制对象是勿忘每一个成分
*   copying函数应该确保复制“对象内的所有成员变量”及“所有基类成分”
*   不要尝试以某个copying函数实现另一个copying函数。应该将共同技能放进第三个函数中，并由两个copying函数共同调用。

#   资源管理
##  条款13：以对象管理资源
*   为防止资源泄漏，请使用RAII对象，它们在构造函数中获得资源并在析构函数中释放资源

*   两个常被使用的RAII classes分别时str1::shared_ptr和auto_ptr。前者通常时较佳旋转。因为其copy行为比较直观。

*   RAII时Resource Acquistion Is Initialzation即资源取得时机便是初始化时机。


##  条款14：在资源管理中小心copying行为
*   复制RAII对象必须一并复制它所管理的资源，所以资源的copying行为决定RAII对象的copying行为

*   普遍而常见的RAII class copying 行为时：抑制copying、施行引用计数法。不过其他行为可都可以能被实现。


##  条款15：在资源管理类中提供对原始资源的访问、
*   APIs往往要求访问原始资源，所以每一个RAII class应该提供一个“取得其所管理之资源”的办法
*   对原始资源的访问可能经由显示转换或隐式转换。一般而言显示转换比较安全，但隐式转换对客户比较方便。


##  条款16：成对使用new和delete时要采取相同形式
*   如果你在new表达式中使用\[\],必须在对应的delete表达式中也使用\[\]。如果你在new表达式中不使用\[\]，
    一定不要在对应的delete表达式中使用\[\]。


##  条款17：以独立语句将newed对象置入智能指针
*   以独立语句将newed对象存储与(置入)智能指针内。如果不这样做，一旦异常被抛出，有可能导致难以察觉的资源泄漏

#   设计与声明
##  条款18：让接口容易被使用，不易被误用
*   好的接口很容易被正确使用，不容易被误用。你应该在你的所有接口中努力达成这些性质。
*   “促进正确使用”的办法暴恐接口的一致性，以及与内置类型的行为兼容。
*   “阻止误用”的办法包括建立新类型、限制类型上的操作，束缚对象值，以及消除客户的资源管理责任。
*   tr1::shared_ptr支持定制删除器。这可以防范DLL问题，可被用来自动解除互斥锁。

##  条款19：设计class犹如设计type即设计class之前需要考虑的要素
*   新type的对象应该如何被创建和销毁？即构造函数、析构函数、内存分配函数、内存释放函数。
*   对象的初始化和对象的赋值应该有什么样的差别？即构造函数和赋值操作符的差异。
*   新type的对象如果被passed by value,意味着什么？记住，copy构造函数用来定义一个type的pass-by-value该如何实现。
*   什么是新type的“合法值”？ 需要进行错误检测。
*   你的新type需要配合某个继承图系吗？即析构函数是否为虚函数
*   你的新type需要什么样的转换?
*   什么样的操作符和函数对此新type而言是合理的？即那些是成员函数，那些是其他函数。
*   什么样的标准函数应该驳回？即哪些函数需要声明为私有
*   谁该取用新type的成员？
*   什么是新type的未声明接口？
*   你新的type有多么一般化？即可以用模板类吗？
*   你真的需要一个新type吗？即是否在原有类里面添加几个函数就行吗？

##  条款20：宁以pass-by-reference-to-const替换pass-by-value
*   尽量以pass-by-reference-to-const替代pass-by-value。前者通常比较高效并可避免切割问题。
*   以上规则并不适用于内置类型、stl迭代器和函数对象。

##  条款21：必须返回对象是，别妄想返回器reference
*   绝对不要返回pointer或reference指向一个local stack对象，或返回reference指向一个heap-allocated对象，
    或返回pointer或reference指向一个local static对象而有可能同时需要多个这样的对象。