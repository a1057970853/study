# C++Primer
## 表达式
    表达式由一个或多个运算对象组成，对表达式求值将获得一个结果。字面值和变量是表达式。
### 基础
#### 基础概念
*   组合运算符和运算对象
*   运算对象转换
*   重载运算符
*   左值和右值
    c++表达式不是左值就是右值。左值可以位于赋值语句的左侧，右值则不能。
    左值代表对象的值
    右值代表对象的内存的位置
*   优先级与结合律
*   求值顺序:求值顺序与优先级和结合律无关
#### 算术运算符
#### 逻辑和关系运算符
#### 赋值运算符
#### 递增和递减运算符
#### 成员访问运算符
#### 条件运算符
     ?:;
#### 位运算符
#### sizeof运算符
    sizeof运算符的结果部分地依赖于其作用类型
*   对char或类型为char的表达式执行sizeof运算，结果为1
*   对引用类型执行sizeof运算得到被引用对象所占空间大小
*   对指针执行sizeof运算得到指针所占空间的大小
*   对解引用指针执行sizeof运算得到指针所指向的对象所占空间大小，指针不需有效
*   对数组执行sizeof运算得到整个数组所占空间的大小，等价于对数组中所有的元素各执行一次sizeof运算并将所得结果求和。注意，sizeof运算不会把数组转化成指针处理
*   对string对象或vector对象执行sizeof运算，只返回给类型固定部分的大小，不会计算对象中元素占用多少空间
#### 逗号运算符
#### 类型转换
    隐式转换
*   在大多数表达式中，比int类型小的整型值首先提升为较大的整型类型。
*   在条件中，非布尔类型转化为布尔类型。
*   初始化过程中，初始值转换成变量的类型；在赋值语句中，右侧运算对象转换成左侧运算对象的类型。
*   如果算术运算或关系运算的运算对象有多种类型，需要转换成同一类型
*   其他见第六章
### 算术转换
    算术转化是把一种算术类型转换成另一种算术类型。
    整型提升是负责把小整数类型转化为较大的整数类型。
### 运算符优先级表
