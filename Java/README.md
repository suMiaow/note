# Java

## 数据类型

### 基本类型（值类型）

类型 | 中文名 | 字节数 | 取值范围
:---: | :---: | :---: | :---:
整数类型 |
`byte` | 字节型 | 1 | `-128 ~ 127`
`short` | 短整型 | 2 | `-2^15 ~ 2^15-1 _(32767)_`
`int` | 整型 | 4 | `-2^31 ~ 2^31-1 _(21亿)_`
`long` | 长整型 | 8 | `-2^63 ~ 2^63-1`
浮点数类型 |
`float` | 单精度浮点型 | 4 | `3.4e-45 ~ 1.4e38`
`double` | 双精度浮点型 | 8 | `4.9e-324 ~ 1.8e308`
字符类型 |
`char` | 字符型 | 2 | 取值 `'a'`, `'!'`, `'中'`
布尔类型 |
`boolean` |  | 4 (1) | `true` / `false`

### 类型提升现象

在做算术运算的时候，如果两边类型不一致，小类型会自动转换成大类型

布尔类型不能参与算术运算

```java
数值大小：byte < short < int < long < float < double
```

> `byte`，`short`，`int` 这些变量在赋值的时候首先会检查值的范围在不在数据类型的范围内。如果赋值的数据不在数据类型的范围内，则编译的时候( `javac` )就会报错

> boolean类型不参与转换

```java
类型提升： byte short char -> int -> long -> float -> double
```

```java
byte b1 = 127;
byte b2 = (byte)128 // -128
byte b3 = (byte)129 // -127
byte b4 = (byte)130 // -126
```

## 运算符

> 赋值运算符隐含了一个强制类型转换

```java
byte b = 20;
b = b + 1; // 不能编译通过
b += 1; // 编译可以通过
```

### 运算符优先级

    () > 算术运算符 > 比较运算符 > 逻辑运算符 > 赋值运算符

### 位运算符

```java
& | ^ ~
>> << >>>
```

常见面试题

1. 交换两个数
2. 用最有效率的方式计算 `3-8` 的结果： `3 << 3`

## 控制结构

`switch` 结构判断依据的类型：`byte`, `short`, `int`, `char`, `String`

- 1.5 之后支持枚举类型
- 1.7 之后支持String类型

`case` 后面跟的值必须是常量

`if-else` 使用场景：

1. 针对boolean类型判断
2. 针对某一个范围的判断
3. 针对常量的判断

`switch-case` 的场景

- 针对常量的判断

## 循环结构

规范：

1. 如果是一个确定次数的循环，建议使用 `for` 循环，比如 `1+...+100`
2. 如果是一个不确定次数的循环，而且可能一次都不执行，使用 `while` 循环
3. 不确定次数的循环，而且必须至少会执行一次，使用 `do-while` 循环

## 数组

```java
int[] a; // 定义一个int数组类型的变量a
int a[]; // 定义一个int类型的a数组
```

### 为数组赋值

1. 动态初始化：在堆中开辟一块指定长度的内存空间，由程序默认提供值

   ```java
   a = new int[5];
   ```

2. 静态初始化：由程序员提供数组元素的值，由程序计算出长度

   ```java
   a = new int[]{1,2,3};
   a = {1,2,3}
   ```

### 排序

1. 选择排序

   排序思路：(5个数)
   1. 先找到最小的数，把它和第0个数交换
   2. 找到后面4个数中最小的数，把它和第1个数交换
   3. 找到后面3个数中最小的数，把它和第2个数交换
   4. ……

2. 冒泡排序

### 多维数组

#### 声明：

```java
int[][] a; // 推荐
int a[][]; // 也可以
int[] a[]; // 不推荐
```

```java
int[] x,y[]; // 面试时小心
```

#### 初始化：

1. 动态初始化

   ```java
   a = new int[3][3];
   // OR
   a = new int[3][];
   a[0] = new int[1];
   a[1] = new int[2];
   a[2] = new int[3];
   ```

2. 静态初始化

   ```java
   int[][] a = {{1,2,3},{4,5,6},{7,8,9}};
   ```

## 面向对象编程

### 面向对象三大特征

1. 封装：维护性
2. 继承：拓展性
3. 多态：灵活性

### `this` 关键字：

1. 指代调用这个方法或者属性的对象本身（后面跟 `.` 的情况）
2. 指代本类的对应构造器 （跟的是 `()` 的情况），只能写在第一行

如果在成员方法中没有同名的变量或者方法，那么会默认加上 `this` 关键字

### 构造器（构造方法、构造函数）

明确一点，每个类都有构造器，就算你没有写

#### 分类

1. 隐式构造器

   如果没有显式的提供构造器，那么JVM会默认提供一个无参无实现过程的构造器

2. 显式构造器

   程序员手动书写在类中的构造器，

   但是如果显式的提供了构造器，那么JVM就不会再给你提供空构造器了

### `static` 静态修饰符

1. 修饰属性：修饰了这个属性，属性就不再属于对象，而是属于类

2. 修饰方法：方法就可以通过类名直接调用

   静态方法中没有 `this` 引用，不可以访问成员属性和成员方法

3. 修饰类

4. 修饰代码块

5. 静态导入

### 代码块：用 `{}` 包起来的代码

1. 局部代码块：方法内部的代码块
2. 构造代码块：在成员位置加入的代码块，在构造对象之前执行
3. 静态代码块：`static` 修饰的代码块，第一次访问到这个类的时候就会执行一次（可以理解为最先执行）

### 初始化顺序

1. 类的初始化 - 只有第一次用到这个类的时候才会初始化一次
   - 静态属性，静态代码块（初始化顺序就是它们的定义顺序）

2. 对象的初始化 - 只要 `new` 一个对象就会初始化
   1. 成员属性和构造块（初始化顺序就是它们的定义的顺序）
   2. 构造器

## 继承

把多个类中相同的部分抽取出来放在一个类中 (`extends`)

```java
class Student extends Person
```

- 好处：
  1. 提高了代码的可重用性
  2. 在升级代码时，不需要重复的书写以前的代码

- 坏处：
  - 增加类和类之间耦合

OOP程序设计思路：低耦合，高内聚

- 耦合：靠类和类之间的关系解决问题
- 内聚：靠自己的能力解决问题

### java中继承的特点

- 单线继承
  - 一个子类只能有一个直接父类
  - 但是支持多层继承
  - 一个父类可以有多个子类
- 子类可以通过继承得到父类的所有成员，除了私有的（构造器不会被继承）
- 构造子类对象前，会先构造父类对象

**注意**

1. 不要为了部分功能去强行使用继承
2. 继承其实体现了特殊与一般的关系，子类是一种特殊的父类 (is a)
3. 构造子类对象的时候会默认先调用父类的无参构造, 如果父类没有无参构造，就必须在子类的构造器中显式的指定调用父类的哪一个构造器

### 方法重写、复写、覆盖 `@Override`

在子类中写一个和父类中方法名，参数列表相同，实现过程不同的方法

**规范**：方法上面加上 `@Override`

注意和方法重载区分

*重载*：同一个类中同名不同参

### 变量的寻找顺序（就近原则）

```
局部变量 -> 成员 -> 父类成员 -> 父类的父类成员 -> ... -> Object类
```

### 继承中的初始化顺序

- 先父类，后子类
- 先加载类，再构造对象

1. 类初始化：
   - 先初始化父类的静态块和静态属性，如果父类还存在父类的话，优先父类的父类；以此类推...
   - 最后初始化本类的静态块和静态属性

2. 对象初始化
   - 先构造父类对象，如果父类还存在父类的话，优先父类的父类；以此类推
   - 最后构造本类的对象

### `final` 关键字

1. 修饰基本类型：把变量变成常量（自定义常量）
   - 值不能被改变
   - 只能被赋值一次
   - 常量的命名规则：全部字母都用大写，多个单词用下划线隔开
2. 修饰引用类型：表示这个引用不能指向别的对象
3. 修饰方法：表示这个方法不能被子类所重写（覆盖）
4. 修饰类：表示类不能被继承

## 多态

允许不同的对象对同一种消息作出响应

操作方式相同，但是展现的效果随着对象的不同而不同

同样的方法调用，不同的对象展现出不同的特性

### 多态的条件

1. 必须要有继承
2. 必须要有方法重写
3. 必须要父类引用子类对象

多态实现了程序的灵活性，继承自同一父类的不同子类可以展示不同的特性

### 向上转型和向下转型

- 向上转型：父类引用子类对象，安全的转型
- 向下转型：子类引用 = (子类) 父类引用的子类对象
- 不安全的转型，有可能会在运行时报错

如何进行安全的向下转型呢？
> 通过 `instanceof` 关键字判断引用所指向的对象是否属于目标类型，如果返回 `true` 才能进行转换

### 抽象修饰符 `abstract`

1. 修饰方法
   - 抽象方法没有方法体
   - 有抽象方法的类就必须是抽象类
   - 专门用来被子类重写的

2. 修饰类
   - 抽象类不能被实例化
   - 专门用来被继承的

属性不能用 `abstract` 修饰

**注意**：

1. 继承一个抽象类，就必须实现抽象类中的所有抽象方法， 除非这个子类也是一个抽象类
2. 抽象类中可以有构造器，为了给子类调用初始化父类中的成员属性
3. 抽象类中可以没有抽象方法

总的来说，抽象类就是一个类，只不过不能实例化，可以有抽象方法

### 接口 `interface`

一系列常量和抽象方法的集合

```java
class Bird implements Flyable
```

1. 接口不能直接实例化，是专门用来被实现的
2. 接口中的方法只能是抽象方法，就算不写 `abstract` 也是抽象方法
3. 一个类可以在继承一个父类的同时实现接口
4. 接口中不能有变量，即使不写 `final`，定义出来也是常量
5. 接口中不能有构造器

#### 抽象类和接口的异同

- 相同点：
  1. 都不能被实例化
  2. 里面都可以抽象方法
  3. 作为他们的子类必须实现所有的抽象方法，除非子类也是抽象类或接口

- 不同点：
  1. 接口里只能有常量和抽象方法；抽象类中可以有成员属性和具体方法
  2. 接口里不能有构造器；抽象类可以有构造器
  3. 一个类只能继承于一个抽象父类，但是可以实现多个接口
  4. 接口也可以继承多个接口
  5. 设计方式不同，
     - 抽象类从具体类型中抽象得出，非常关心子类是什么东西
     - 接口是定义的一种规范

## 字符串

`String` - 不可变字符串

### 字符串的构造

在常量池中生成一个 `"abc"` 的常量，并把首地址赋值给栈中的变量 `s1`

```java
String s1 = "abc";
```

在常量池中生成一个 `"abc"` 的常量，在堆中生成一个字符串对象指向常量池中的 `"abc"` ， 再把堆中对象的首地址赋值给栈中的变量 `s2`

```java
String s2 = new String("abc");
```

### 字符串的比较

字符串内容的比较一定不能使用 `==`

使用 `==` 比较的是字符串的地址值

比较两个字符串的内容是否相等

```java
s1.equals(s2)
```

不区分大小写比较是否相等

```java
s1.equalsIgnoreCase(s2)
```

空串和 `null` 串

- 空串：长度为0的字符串
- null串：没有指向任何实例的字符串引用

```java
String s3 = null;

if(s3 != null && s3.length() > 0){
    System.out.println("字符串既不是空串，也不是null串");
}
```

> 字符串的内容是不可变的，任何一个看起来可以修改字符串内容的方法只不过是生成了一个新的字符串并把原来字符串的引用指向新的字符串实例而已

### 编辑字符串的方法

#### 可变字符串

`StringBuffer` 线程安全的可变字符串

`StringBuilder` 线程非安全的可变字符串

#### 基本类型和String的转化

基本类型 -> `String`

```java
String str = String.valueOf(1);
```

`String` -> 基本类型

```java
int i = Integer.parseInt("123");
```

整理代码的方式

1. 把功能相近的语句 -> 写成一个方法
2. 把功能相近的方法 -> 写成一个类
3. 把功能相近的类 -> 写在一个包里

## 包 `package`

`java` 提供的一种区别类的名字的命名空间的机制，是类的组织方式，是一组相关的类和接口的集合。

### 包的作用

1. 把功能相近的java文件放在一个文件夹里，便于管理，避免了命名冲突
2. 在java中，某些权限是和包有关系

### 包的命名规则

1. 全部字母都用小写
2. 多级文件夹的话，用.隔开

### 带包书写方式

1. `package` 语句必须是 `.java` 文件第一条可执行语句
2. `package` 语句最多有一条
3. 如果不写 `package` ，默认无包名

类带了包之后有2个主要结果

1. 包名会成为类名的一部分
2. class文件的路径和包路径必须完全一致

### 带包的class的运行方式

1. 把class文件放在包指定的路径下
2. 带包运行

```sh
javac -d out -cp src src/a/b/Demo1.java
```

#### 如何访问别的包中的公开类

1. 使用类的全名引用
2. 导包
3. 如果是访问本包中的类，则直接用简单类名即可

#### 访问修饰符

可以对类、接口、变量（常量）、方法进行访问权限控制的修饰符

修饰符 | 本类 | 包内 |子类 | 包外
--- | :---: | :---: | :---: | :---:
`public` | o | o | o | o
`protected` | o | o | o | x
`[default]` | o | o | x | x
`private` | o | x | x | x

### 内部类

在一个类的内部定义的类叫做内部类

内部类只不过是编译时的一个说法，一旦通过编译，就会变成2个完全不同的类

1. **Static Nested Classes*- 静态内部类，静态成员内部类，嵌套类

   修饰为 `static` 的内部类，不需要内部类对象和外部类对象之间的联系，可以直接构造内部类对象

   - 普通内部类不能有 `static`方法和属性，静态内部类都可以有
   - 普通内部类不能使用外部类的 `static` 属性和方法，静态内部类可以使用
   - 静态类一般都声明为 `public` ，方便直接调用

2. **Inner Classes*- 成员内部类

   作为外部类的成员，可以直接使用外部类中定义的成员属性和成员方法，即使是私有的

   - 成员内部类不能含有静态属性和静态方法
   - 成员内部类默认会保存外部类的引用，用外部类名 + `.this` 可以获取
   - 构造成员内部类对象需要先构造外部类对象

3. **Local Classes**局部内部类，方法内部类

   在方法内部定义的类，只在自己作用域范围内有效，出了作用域就无法被访问

   > 使用方法中局部变量的时候，这个局部变量（Java SE 8 以前， 必须被`final` 修饰，从 Java SE 8 以后，必须是 final 或 effectively final 的）

4. **Anonymous Classes*- 匿名内部类

   - 不能加访问修饰符
   - 要构造一个匿名内部类，首先要有一个父类或者一个接口

#### 内部类的继承

子类构造器中需要使用父类的外部类对象 `.super()`

而这个父类的外部类对象需要从外面创建并传递给构造方法形参

## IDE

### 编译和运行的版本修改

编译版本：java -> compiler
运行版本：项目中右键 -> java Build Path

建议编译版本和运行版本一致

- 编译版本低，运行版本高 -> 可以
- 编译版本高，运行版本低 -> 不可以

### 提高开发效率

- 自动生成构造器
- 自动生成 `getter` 和 `setter`
- 自动实现父类的抽象方法
- 代码自动补全 `Alt + /`
- 代码快速修复 `Ctrl + 1`

### 导入导出项目

- 查看项目的路径
- 项目区域中不能出现同名项目
- 自己随便建立的文件夹不能作为项目导入
- 不要随意修改项目的名字

### 导入导出jar文件

java中的类分为两种

1. Runnable class : 可运行类，有 `main` 方法的类
2. java Bean：没有 `main` 方法的类，往往作为一种数据类型被别的类所调用

## `Object` 类

`java.lang.Object`

1. `java.lang`

   java的语言包，使用这个包下的类都不需要导包

2. `Object` 是 `java` 所有类型的父类

   java中任意一个类型都直接或间接的继承自`Object`

### `Object` 方法

```java
protected Object void clone();
//创建并返回此对象的一个副本

boolean equals(Object obj);
// 默认实现就是 == ，比较的是引用类型地址是否相等

// 但是可以通过子类重写来达到比较对象内容的目的

// 重写的时候注意原则：
// 1. 自反性
// 2. 对称性
// 3. 传递性
// 4. 一致性
// 5. 非空型


protected void finalize();
// 由垃圾回收器在回收这个对象的时候会调用

// 默认无实现

// 实际开发中建议不重写，
// 因为回收垃圾的时候往往已经内存很满，电脑很卡了
// 你还要他额外执行很多代码，合理吗？

// 垃圾：没有引用指向的对象


Class<?> getClass(); // 返回此 Object 的运行时类。


int hashCode();
// 返回该对象的哈希码值。
// 默认实现，返回一个和这个对象的地址有关的一个整数

// 相当于hash码的结果就是对地址值的一个函数
// y = f(x)

// 常规协定:
// 1. 多次调用，结果一致
// 2. equals认为相等的对象，hashCode值必须相等
// 3. equals认为不相等的对象，hashCode值最好不相等。（为了提高性能）

// 要求：重写了equals，就一定要重写hashCode方法


void notify()


void notifyAll()
// 在并发控制的时候使用的方法


String toString();
// 返回该对象的字符串表示。

// 默认实现,对我们来说没有帮助

// 返回这个对象的 完整类名@哈希值的16进制表示


return getClass().getName() + "@" + Integer.toHexString(hashCode());

// 可以通过重写方法，来打印出对象中成员属性的值，方便调试程序

// 可以通过IDE自动生成 toString方法


void wait();
void wait(long timeout);
void wait(long timeout, int nanos);
// 在并发控制的时候使用的方法
```

## 包装类

java的设计师为每种基本类型都设计了对应的引用类型，就叫做基本类型的包装类

基本类型 | 包装类型
---: | :---
`byte` | `Byte`
`short` | `Short`
`int` | `Integer`
`long` | `Long`
`float` | `Float`
`double` | `Double`
`char` | `Character`
`boolean` | `Boolean`

1. 基本类型 -> 引用类型

   ```java
   Integer i1 = new Integer(1);     // 1. 不推荐
   Integer i2 = Integer.valueOf(2); // 2. 推荐 - 效率高
   ```

2. 引用类型 -> 基本类型

   ```java
   int i3 = i1.intValue();
   ```

面向对象程序员终极追求：

1. 解耦：降低类和类之间的关系
2. 通用：最好做到一种类型能完全完成一种类型的功能

1.5 新特性

泛型 - 参数化类型

1. 泛型类

2. 泛型方法

3. 泛型接口

4. 通配符

5. 类型擦除

   真正的原理是编译时类型检查，编译一旦完成，泛型就失去了作用

## Exception

Exceptional event

Definition: An *exception- is an event, which **occurs during the execution of a program**, that distrupts the normal flow of the program's instruction.

- `Throwable`
  - `Error`
  - `Exception`
    - `IOException`
      - `FileSystemException`
    - `RuntimeException`
      - `ArithmeticException`
      - `IllegalArgumentException`
      - `IndexOutOfBoundsException`
      - `NullPointerException`

### The Three Kinds of Exceptions

1. Checked Exception

   表示程序过程中发生的异常，如果经过了合适的处理，程序还是可以回归正常的指令流程

2. Error (unchecked exception)

   表示虚拟机内存发生的严重错误，一旦发生这样的错误，程序不可能再回到正常的指令流程

   如 `java.lang.StackOverflowError` 和 `java.lang.OutOfMemoryError`

3. Runtime Exception (unchecked exception)

### 处理异常

#### 捕获并解决

```java
try{

}catch(Exception e){

}finally{

}
```

`try`：可能发生异常的代码块，如果运行时发生了异常，就会捕获住这个异常对象

`catch`：处理具体异常问题的解决方案，当 `try` 块抓住了相应的异常对象就会把它交给相应的 `catch` 块进行处理

##### Catching More Than One Type of Exception with One Exception Handler (In Java SE 7 and later)

> If a `catch` block handles more than one exception type, then the catch parameter is implicitly final.

```java
catch (IOException|SQLException ex) {
    logger.log(ex);
    throw ex;
}
```

> In this example, the `catch` parameter `ex` is `final` and therefore you cannot assign any value to it within the `catch` block.

`finally`：最终执行的代码块，无论有没有发生异常，有没有遇到 `return` , `continue` , `break` 都会在最后执行

> If the JVM exits while the `try` or `catch` code is being executed, then the `finally` block may not execute. Likewise, if the thread executing the `try` or `catch` code is interrupted or killed, the `finally` block may not execute even though the application as a whole continues.

在以下特殊情况下，finally有可能会不执行

1. 在 `finally` 中发生了异常
2. 在前面的代码中使用了 `System.exit()` 退出了程序
3. 程序所在的线程死亡
4. 关闭CPU

##### The try-with-resources Statement (java SE 1.7)

**resource**: Any object that implements `java.lang.AutoCloseable`

- *`java.lang.AutoCloseable`*
  - *`java.io.Closeable`*


1.类集：指一组接口和类

2.Collection：添加add、删除remove、迭代iterator、清除clear、长度size、

3.List：新增了添加、查询get(int index)、删除、修改方法、获取元素首次或最后一次出现位置、列表迭代器listIterator
	（其实就是新增了根据索引位置操作元素的方法）

4.Set：同Collection一样，没有新增功能

5.ArrayList：ensureCapacity(int minCapacity)确保能容纳指定容量个数元素、受保护方法removeRange(int fromIndex, int toIndex) 
	、实际容量调整为当前列表大小trimToSize()（线程不安全）

6.LinkedList：新增了大量操作开头First和结尾Last元素的方法和逆向迭代方法(线程不安全)

7.Vector：功能同ArrayList基本相同，JDK1.2开始实现List接口，不过基本被ArrayList取代(线程安全)



1.Set的特点：
	不重复：内部通过equals方法来判断元素是否相等
	无序性：指的是元素的添加顺序和迭代出来的顺序不一定相等
2.HashSet：完全继承了Set或者Collection里的方法实现
	add、addAll、clear、isEmpty、size、contains、iteretor、remove等
3.TreeSet：对Set接口功能做了极大扩展，并且具有排序功能
	新增了很多方法：
		first(取第一个元素)、last(取最后一个元素)、
		pollFirst(获取并移除第一个元素)、pollLast(获取并移除最后一个元素)、
		ceiling(获取该Set中大于等于指定值的最小元素)、floor(获取该Set中小于等于指定值的最大元素)、
		higher(获取该Set中严格大于指定值的最小元素)、lower(获取该Set中严格小于指定值的最大元素)、
		headSet(开头一段子集)、tailSet(结尾一段子集)、subSet(中间一段子集)



1. TreeSet自定义排序的方式：
	1).元素本身实现排序算法，做法元素类。比如Person自身实现Comparable接口，实现抽象方法compareTo(Object o)
		这种方式实现类Person本身也要参与比较
	2).由TreeSet的对象来实现比较功能，做法，通过Comprator接口的实现类对象来构造TreeSet对象，
		实现compare(Object o1,Object o2)
		这种方式比较算法的实现类本身不参与比较

2.Map接口：映射接口,特点是以键值对形式来存放数据的
	常用方法：
		增(put)、删(remove)、改(put)、查(get)功能
		返回Set或者Collection的函数：返回所有key(keySet)、返回所有value(values)、返回所有的映射关系(entrySet)
		clear、containsKey、containsValue、size
3.HashMap：
	注意：
		1).key不能重复、value可以重复
		2).key和value都可以为null
		3).当get(key)中key不存在的时候，返回值也为null
		4).通常情况下我们都把key设置为String类型

555555555555555555555555555555555555555555555555555

【类之间的关系】

 1. 继承
  指的是一个类（称为子类，子接口）继承另外一个类（父类、父接口）的功能，
  并可以增加它自己新功能的能力，继承是类和类或者接口和接口之间最常见的关系。
  在java代码中通过关键字 extends 明确标识，在设计时一般没有争议性

  (class) A extends (class) B
  (interface) A extends (interface) B

 2. 实现
  指的是一个class类实现interface接口（或者是多个）的功能
  实现是类和接口之间最常见的关键，
  在java代码中通过关键字 implements 明确标识，在设计时一般没有争议性

 (class) A implements (interface) B

 3. 依赖
  简单的理解就是一个类A使用到了另一个类B，
  这种关系是具有偶然性，临时性，非常弱的
  但是B类的变化会影响到A
 
  （例）比如某人要过河，需要借用一条船，那此时人和船的关系就是依赖

 - 表现在代码层面，为类B作为参数被类A在某个方法中使用

  class A{
    void depend(B b){
	C c = new C();
    };
  }


 4. 关联
  体现的是两个类，或者类与接口之间语义级别的一种强依赖关系

  （例）我和我朋友
  这种关系比依赖更强，不存在依赖关系的偶然性、关系也不是临时性的
  一般是长期性、而且双方的关系是平等的，关联可以是单向、双向的；

  - 表现在代码层面，为被关联类B是以类属性的形式出现在关联类A中，
   也可能是关联类A引用了一个类型为被关联类B的全局变量

  class A{
    B b;
  }


 5. 聚合
  聚合是关联关系的一种特例，它表示的是部分与整体、拥有的关系，
  即has-a的关系，此时整体和部分是可以分离的

  他们可以用各自的生命周期，部分也可以属于多个整体对象。 
  
 （例）计算机与CPU，公司与员工

  - 表现在代码层面，只能通过语义区分


 6. 组合
  组合也是关联关系的一种特例
  它表示的是一种 contains-a的关系
  这种关系比聚合更强，也称为强聚合
  它同样体现整体与部分的关系，但此时整体和部分是不可分离的
  整体的生命周期结束也意味着部分的生命周期结束

  （例）你和你的大脑

  - 表现在代码层面，只能通过语义区分

---
 ### 对于继承、实现这两种关系没多少疑问，他们体现的是一种类与类、或者类与接口间的纵向关系；
  其他的四者关系则体现的是类与类、或者类与接口间的引用、横向关系，是比较难区分的，
  有很多事物间的关系要想准确定位是很难的，前面也提到，这几种关系都是语义级别的，
  所以从代码层面并不能完全区分各种关系；

  但总的来说，后几种关系所表现的强弱程度依次为：组合>聚合>关联>依赖；

 ### 举例：
  聚合关系 雁群 & 大雁
  组合关系 大雁 & 翅膀

 聚合关系的类里含有另一个类作为参数 
 雁群类（GooseGroup）的构造函数中要用到大雁（Goose）作为参数把值传进来 
 大雁类（Goose）可以脱离雁群类而独立存在  

 组合关系的类里含有另一个类的实例化 
 大雁类（Goose）在实例化之前 一定要先实例化翅膀类（Wings） 
 两个类紧密耦合在一起 它们有相同的生命周期 翅膀类（Wings）不可以脱离大雁类（Goose）而独立存在 

 信息的封装性不同 
 在聚合关系中，客户端可以同时了解雁群类和大雁类，因为他们都是独立的 
 而在组合关系中，客户端只认识大雁类，根本就不知道翅膀类的存在，因为翅膀类被严密的封装在大雁类中。

---


【六大设计原则】

 1. 单一职责原则

  不要存在多于一个导致类变更的原因。
  通俗的说，即一个类只负责一项职责。

  遵循单一职责原的优点有：

  1）可以降低类的复杂度，一个类只负责一项职责，其逻辑肯定要比负责多项职责简单的多；

  2）提高类的可读性，提高系统的可维护性；

  3）变更引起的风险降低，变更是必然的，
     如果单一职责原则遵守的好，当修改一个功能时，可以显著降低对其他功能的影响。

  - 需要说明的一点是单一职责原则不只是面向对象编程思想所特有的，只要是模块化的程序设计，都适用单一职责原则。

---

 2. 里氏替换原则

  任何基类可以出现的地方，子类一定可以出现

  当使用继承时，遵循里氏替换原则。类B继承类A时，
  除添加新的方法完成新增功能P2外，尽量不要重写父类A的方法，也尽量不要重载父类A的方法。

  继承作为面向对象三大特性之一，在给程序设计带来巨大便利的同时，也带来了弊端。
  比如使用继承会给程序带来侵入性，程序的可移植性降低，增加了对象间的耦合性，
  如果一个类被其他的类所继承，则当这个类需要修改时，必须考虑到所有的子类，并且父类修改后，所有涉及到子类的功能都有可能会产生故障。

  里氏替换原则通俗的来讲就是：子类可以扩展父类的功能，但不能改变父类原有的功能。它包含以下4层含义：

  1）子类可以实现父类的抽象方法，但不能覆盖父类的非抽象方法。

  2）子类中可以增加自己特有的方法。

  3）当子类的方法重载父类的方法时，方法的前置条件（即方法的形参）要比父类方法的输入参数更宽松。

  4）当子类的方法实现父类的抽象方法时，方法的后置条件（即方法的返回值）要比父类更严格。

  看上去很不可思议，因为我们会发现在自己编程中常常会违反里氏替换原则，
  程序照样跑的好好的。所以大家都会产生这样的疑问，
  假如我非要不遵循里氏替换原则会有什么后果？

  后果就是：你写的代码出问题的几率将会大大增加。

---

 3. 依赖倒转原则

  高层模块不应该依赖低层模块，二者都应该依赖其抽象；
  抽象不应该依赖细节；细节应该依赖抽象。

  类A直接依赖类B，假如要将类A改为依赖类C，则必须通过修改类A的代码来达成。
  这种场景下，类A一般是高层模块，负责复杂的业务逻辑；类B和类C是低层模块，负责基本的原子操作；
  假如修改类A，会给程序带来不必要的风险。
  
  在实际编程中，我们一般需要做到如下3点：

  1）低层模块尽量都要有抽象类或接口，或者两者都有。
  2）变量的声明类型尽量是抽象类或接口。
  3）使用继承时遵循里氏替换原则。

  - 依赖倒置原则的核心就是要我们面向接口编程，理解了面向接口编程，也就理解了依赖倒置。

---

 4. 接口隔离原则

  使用多个隔离的接口，比单个接口要好

  采用接口隔离原则对接口进行约束时，要注意以下几点：

  1）接口尽量小，但是要有限度。对接口进行细化可以提高程序设计灵活性是不争的事实，
     但是如果过小，则会造成接口数量过多，使设计复杂化。所以一定要适度。

  2）为依赖接口的类定制服务，只暴露给调用的类它需要的方法，它不需要的方法则隐藏起来。
     只有专注地为一个模块提供定制服务，才能建立最小的依赖关系。

  3）提高内聚，减少对外交互。使接口用最少的方法去完成最多的事情。
  
 - 运用接口隔离原则，一定要适度，接口设计的过大或过小都不好。
  设计接口的时候，只有多花些时间去思考和筹划，才能准确地实践这一原则。

---

 5. 迪米特法则（最少知道原则）

  一个对象应该对其他对象保持最少的了解。
 
  类与类之间的关系越密切，耦合度越大，当一个类发生改变时，对另一个类的影响也越大。

  自从我们接触编程开始，就知道了软件编程的总的原则：低耦合，高内聚。
  无论是面向过程编程还是面向对象编程，只有使各个模块之间的耦合尽量的低，才能提高代码的复用率。
  低耦合的优点不言而喻

  迪米特法则还有一个更简单的定义：只与直接的朋友通信
  每个对象都会与其他对象有耦合关系，只要两个对象之间有耦合关系，我们就说这两个对象之间是朋友关系。
  耦合的方式很多，依赖、关联、组合、聚合等。
  其中，我们称出现成员变量、方法参数、方法返回值中的类为直接的朋友，
  而出现在局部变量中的类则不是直接的朋友。
  也就是说，陌生的类最好不要作为局部变量的形式出现在类的内部。

```java
  class A{
   main(){
     new b();
      b
   }
  }

  class B{
   public void b(){
    b1
    b2
    b3
   }
   private void b1();
    private void b2();
    private void b3();
  }
```

---
  
 6. 开闭原则
  一个软件实体如类、模块和函数应该对扩展开放，对修改关闭。

  在软件的生命周期内，因为变化、升级和维护等原因需要对软件原有代码进行修改时，
  可能会给旧代码中引入错误，
  也可能会使我们不得不对整个功能进行重构，
  并且需要原有代码经过重新测试。

  所以当软件需要变化时，尽量通过扩展软件实体的行为来实现变化，而不是通过修改已有的代码来实现变化。


【设计模式】
  设计模式代表了最佳的实践，通常被有经验的OOP程序员所采用
  开发过程中面临一般问题的解决方案，
  这种解决方案是软件开发人员经过相当长的一段时间的实验和错误中总结出来的

  使用设计模式的用途
   1. 最佳的实践
    设计模式已经经历了相当长的一段时间的发展
    它提供了软件开发过程中面临一般问题的最佳解决方案
    学习这些模式有助于经验不足的开发人员通过一种简单快捷的方式来学习软件设计

   2. 开发人员的共同平台 
    设计模式提供了一个标准的术语系统，具体到特定的场景



【单例模式】

  这种模式涉及到一个单一的类，该类负责创建自己的对象，同时确保只有单个对象被创建。
  这个类提供了一种访问其唯一的对象的方式，可以直接访问，不需要实例化该类的对象。

  1. 单例的类只能有一个实例
  2. 单例类必须能自己创建自己的实例
  3. 必须给其他所有类提供这一实例

  - 饿汉模式 & 懒汉模式
777777777777777777777777777777777777777777777777777777777

java.io.File

 表示一个文件或者文件夹

 1. 文件的创建、删除、重命名

  - 不能创建一个父目录不存在的文件

 2. 文件夹的创建、删除、重命名 

  - mkdir 是创建单级目录
    mkdirs 可以创建多级目录

  - 不能删除一个非空的文件夹

 3. 查看文件的基本信息

	相对路径：相对于当前位置开始的路径
	绝对路径：从盘符位置开始的路径


 高级用法：
  1. 遍历文件夹
    用递归实现，如果是文件夹的话，再次调用自身做遍历

  2. 删除多级文件夹
    用递归实现，要先删除内部的所有文件，最后才能删除自己。


IO流
 连接内存与硬盘的桥梁

 根据方向来分
 输入流: 从硬盘到内存
 输出流：从内存到硬盘

## `I/O`

### `java.io`

---

- *`DataInput`*
  - *`ObjectInput`*
- *`DataOutput`*
  - *`ObjectOutput`*

---

- `InputStream` *`Closeable`* *`AutoCloseable`*
  - `FileInputStream`
  - `FilterInputStream`
    - `BufferedInputStream`
    - `DataInputStream` *`DataInput`*
    - `LineNumberInputStream`
  - `ObjectInputStream`
- `OutputStream` *`Closeable`* *`AutoCloseable`* *`Flushable`*
  - `FileOutputStream`
  - `FilterOutputStream`
    - `BufferedOutputStream`
    - `DataOutputStream` *`DataOutput`*
    - `PrintStream` (`System.out`, `System.err`)
  - `ObjectOutputStream`
- `Reader` *`Closeable`* *`AutoCloseable`* *`Readable`*
  - `BufferedReader`
  - `InputStreamReader`
    - `FileReader`
- `Writer` *`Closeable`* *`AutoCloseable`* *`Flushable`* *`Appendable`*
  - `BufferedWriter`
  - `OutputStreamWriter`
    - `FileWriter`
  - `PrintWriter`

### `java.nio.file`

如何在文件中保存一个对象呢？

新建一个文本文件
1,苹果,5,2.5
2,香蕉,10,3

序列化
 把一个对象的状态信息转化成二进制方式进行保存或者传输的过程

 序列化：对象 -> 二进制
 反序列化：二进制 -> 对象

XML 可扩展标记语言
Extensible Markup Language

 将数据格式化成XML之后，可以真正的实现数据的跨平台共享
 在不同的语言中，XML的解析方式都是一致的


语法规则：
 1. 所有的元素都叫做标记，标记必须有开始和结束标签
  <a />
  <a></a>

 2. 大小写敏感
 <A /> <a />不是同一种标记

 3. 必须正确的嵌套
 <a></a><b></b>  兄弟关系
 <a><b></b></a>  父子关系

 错误的关系
 <a><b></a></b>

 4. 必须有根元素，（所有元素必须有个统一的父亲）

 <root>
 	<a>
		<c />
	</a>
	<b></b>
 </root>

## Concurrency

**Program or Application*- 应用程序（程序）

为了完成特定的任务而编写的一组指令代码 - 静态的代码

**Processes*- 进程

操作系统分配资源和调度的基本单位，例如linux 32位，每一个进程都会默认分配4G的内存空间

> 一个程序可以同时开启多个进程

> 多进程 目的：提高内存的使用率

**Threads*- 线程

- 程序执行的最小单元
- 线程是依赖于进程的
- 一个进程可以有一个或多个线程
- 是CPU调度的基本单位

> 多线程 目的：提高CPU的使用率

并行：多个CPU实例或多个计算机同时执行一段处理逻辑，是真正的同时

并发：通过CPU调度算法，让用户看上去好像是同时在执行，其实从CPU操作层面来看
不是真正的同时，只是切换的速度非常非常快。

java如何实现多线程呢？

 1. 


 2. 


线程的名字

 1. 使用Thread(String)构造器
 2. 使用 setName(String)

线程的调度

 sleep 
  睡眠
  让线程休眠指定的时间，在这个时间内不再运行

 yield
  让步
  让当前线程暂时退出CPU，给别的线程执行的机会

 interrupt
  中断线程

  不是真正的立即停止，而是仅仅改变一个标志位，Thread.interrupted() = true
  正常运行的线程是不会被中断的
  如果当前线程正处于sleep wait等超时状态中，会使得这个线程进入异常状态，
  可以在异常状态出退出线程
  循环中的线程，可以在循环中加入判断!Thread.interrupted()，就可以在中断后退出循环

 - 如何中断一个正在运行的线程？
 标准的错误答案：close stop destroy suspend
 

 join
   强势加入
   阻塞当前的线程，让加入的线程执行完毕之后自己再执行


线程的优先级
每当调度器有机会重新选择要执行的线程时，它会考虑线程的优先级
可以调用setPriority方法设置线程的优先级


线程的状态
如果想知道线程的状态，可以调用getState()

 1. 新创建 new 
  当用new运算符创建了一个线程对象时，
  该线程还没有启动
  当一个线程处于新创建状态时，程序还不会执行里面的代码

 2. 可运行 runnable
   一旦调用了start方法，线程就处于runnable状态
   一个可运行的线程可能正在运行也可能没有
   这取决于操作系统给该线程提供运行的时间

   一旦一个线程开始运行，它不必始终保持运行
   运行中的线程被中断，目的是为了让别的线程获得调度的机会
   抢占式调度系统给每个可运行的线程一个时间片来执行任务
   当时间片用完，操作系统就会剥夺线程的运行权，给另一个线程提供机会

   - 当选择下一个线程时，操作系统会考虑一下线程的优先级

 3. 被阻塞 blocked
   当线程处于阻塞或等待状态时，它暂时不活动
   不运行任何代码并且消耗最少的资源，直到线程调度器重新激活它
   重新激活的时机取决于它是如何达到这个状态的
  

 4. 等待 waiting

 5. 计时等待 timed_waiting
   方法中有一个超时参数，调用就会让线程进入计时等待状态
   这个状态会保持到超时期满或收到适当的通知

 6. 终止 terminated
  线程因为如下两个原因之一而被终止
  a. 因为run方法正常退出而死亡
  b. 因为一个没有捕获的异常导致run方法异常终止而死亡


线程同步
 java中的线程同步指的是通过人为的控制和调度使得对共享资源的多线程访问成为线程安全

 - 线程安全：用来描述一段程序，在并发环境下执行，线程调度的顺序不会影响最终结果的准确性

 注意：要保证结果准确的同时，提高性能才是好的程序

 synchronized 用法

 1. 同步方法
  通过在方法声明中加入synchronized来表示这是一个同步方法
  每个synchronized 方法都必须获得调用该方法的对象的实例对应的锁才能执行和方法，
  否则线程就会阻塞，方法一旦执行，就会占用该锁，直到从该方法返回才会把锁归还，
  被阻塞的线程才有可能可以获取锁对象

  给一个成员方法加锁的意义往往是因为保证成员变量的线程安全
  （一个对象一把锁）

  一个类也对应一把锁，给static方法加锁，相当于锁在这个类对象的实例上，
  给静态方法加锁的意义往往是为了保证静态成员变量的线程安全
  
 2. 同步代码块
   只有拿到同步代码块锁住的那个对象的实例才能执行代码块中的代码
   相比同步方法来说，它的粒度更小
   

 - synchronized 不能修饰变量





【Timer和TimerTask】

 1. 基本概念

 其实就Timer来讲就是一个调度器
 而TimerTask呢只是一个实现了run方法的一个类
 而具体的TimerTask需要由你自己来实现

---

 2. 常用方法

 public void schedule(TimerTask task, long delay)
 调度一个task，经过delay(ms)后开始进行调度，仅仅调度一次

 public void schedule(TimerTask task, Date time)
 在指定的时间点time上调度一次。

 public void schedule(TimerTask task, long delay, long period)
 这个方法是调度一个task，在delay（ms）后开始调度，每次调度完后，最少等待period（ms）后才开始调度。

 public void schedule(TimerTask task, Date firstTime, long period)
 和上一个方法类似，唯一的区别就是传入的第二个参数为第一次调度的时间。

 public void scheduleAtFixedRate(TimerTask task, long delay, long period)
 调度一个task，在delay(ms)后开始调度，然后每经过period(ms)再次调度

---

 ### schedule 和 scheduleAtFixedRate 区别

 schedule在计算下一次执行的时间的时候，是通过当前时间（在任务执行前得到） + 时间片
 而scheduleAtFixedRate方法是通过当前需要执行的时间（也就是计算出现在应该执行的时间）+ 时间片
 前者是运行的实际时间，而后者是理论时间点

 例如：schedule时间片是5s，那么理论上会在5、10、15、20这些时间片被调度，
 但是如果由于某些CPU征用导致未被调度，假如等到第8s才被第一次调度，
 那么schedule方法计算出来的下一次时间应该是第13s而不是第10s，
 这样有可能下次就越到20s后而被少调度一次或多次，
 而scheduleAtFixedRate方法就是每次理论计算出下一次需要调度的时间用以排序，
 若第8s被调度，那么计算出应该是第10s，
 所以它距离当前时间是2s，
 那么再调度队列排序中，会被优先调度，那么就尽量减少漏掉调度的情况。
  

【Callable、Future和FutureTask】

 创建线程的方式有继承Thread类和实现Runnable接口
 这2种方式都有一个缺陷就是：在执行完任务之后无法获取执行结果

 如果需要获取执行结果，就必须通过共享变量或者使用线程通信的方式来达到效果，这样使用起来就比较麻烦。
 而自从Java 1.5开始，就提供了Callable和Future，通过它们可以在任务执行完毕之后得到任务执行结果

---

 1. java.util.concurrent.Callable<V>

public interface Callable<V> {
    V call() throws Exception;
}

 这是一个泛型接口，call()函数返回的类型就是传递进来的V类型

 那么怎么使用Callable呢？
 一般情况下是配合ExecutorService来使用的，在ExecutorService接口中声明了若干个submit方法的重载版本

 <T> Future<T> submit(Callable<T> task);
 <T> Future<T> submit(Runnable task, T result);
 Future<?> submit(Runnable task);

 一般情况下我们使用第一个submit方法和第三个submit方法，第二个submit方法很少使用

---

 2. java.util.concurrent.Future<V>
 Future就是对于具体的Runnable或者Callable任务的执行结果进行取消、查询是否完成、获取结果。
 必要时可以通过get方法获取执行结果，该方法会阻塞直到任务返回结果。

public interface Future<V> {
    boolean cancel(boolean mayInterruptIfRunning);
    boolean isCancelled();
    boolean isDone();
    V get() throws InterruptedException, ExecutionException;
    V get(long timeout, TimeUnit unit)
        throws InterruptedException, ExecutionException, TimeoutException;
}

 cancel方法用来取消任务，如果取消任务成功则返回true，如果取消任务失败则返回false。
 参数mayInterruptIfRunning表示是否允许取消正在执行却没有执行完毕的任务，
 如果设置true，则表示可以取消正在执行过程中的任务。
 如果任务已经完成，则无论mayInterruptIfRunning为true还是false，此方法肯定返回false，
 即如果取消已经完成的任务会返回false；
 如果任务正在执行，若mayInterruptIfRunning设置为true，则返回true，
 若mayInterruptIfRunning设置为false，则返回false；
 如果任务还没有执行，则无论mayInterruptIfRunning为true还是false，肯定返回true。

 isCancelled方法表示任务是否被取消成功，如果在任务正常完成前被取消成功，则返回 true。

 isDone方法表示任务是否已经完成，若任务完成，则返回true；

 get()方法用来获取执行结果，这个方法会产生阻塞，会一直等到任务执行完毕才返回；

 get(long timeout, TimeUnit unit)用来获取执行结果，如果在指定时间内，还没获取到结果，就直接返回null。
　　也就是说Future提供了三种功能：

　　1）判断任务是否完成；

　　2）能够中断任务；

　　3）能够获取任务执行结果。

 - 因为Future只是一个接口，所以是无法直接用来创建对象使用的，因此就有了下面的FutureTask。

----------------------------------------------------------------------------------------------------------------------

 3. FutureTask

 public class FutureTask<V> implements RunnableFuture<V>

 public interface RunnableFuture<V> extends Runnable, Future<V> {
    void run();
 }

 可以看出RunnableFuture继承了Runnable接口和Future接口，
 而FutureTask实现了RunnableFuture接口。
 所以它既可以作为Runnable被线程执行，又可以作为Future得到Callable的返回值。

 - 事实上，FutureTask是Future接口的一个唯一实现类。


【阻塞队列】

 使用非阻塞队列的时候有一个很大问题就是：它不会对当前线程产生阻塞，
 那么在面对类似消费者-生产者的模型时，就必须额外地实现同步策略以及线程间唤醒策略，这个实现起来就非常麻烦。

 但是有了阻塞队列就不一样了，它会对当前线程产生阻塞，比如一个线程从一个空的阻塞队列中取元素，此时线程会被阻塞直到阻塞队列中有了元素。
 当队列中有元素后，被阻塞的线程会自动被唤醒（不需要我们编写代码去唤醒）。这样提供了极大的方便性。

----------------------------------------------------------------------------------------------------------------------

 1. 主要的阻塞队列
 ArrayBlockingQueue：基于数组实现的一个阻塞队列
  在创建ArrayBlockingQueue对象时必须制定容量大小。并且可以指定公平性与非公平性
  默认情况下为非公平的，即不保证等待时间最长的队列最优先能够访问队列。

 LinkedBlockingQueue：基于链表实现的一个阻塞队列
  在创建LinkedBlockingQueue对象时如果不指定容量大小，则默认大小为Integer.MAX_VALUE。

 PriorityBlockingQueue：
  以上2种队列都是先进先出队列，而PriorityBlockingQueue却不是，
  它会按照元素的优先级对元素进行排序，按照优先级顺序出队，每次出队的元素都是优先级最高的元素。
  注意，此阻塞队列为无界阻塞队列，即容量没有上限（通过源码就可以知道，它没有容器满的信号标志），前面2种都是有界队列。

 DelayQueue：基于PriorityQueue，一种延时阻塞队列
  队列中的元素只有当其指定的延迟时间到了，才能够从队列中获取到该元素。
  DelayQueue也是一个无界队列，因此往队列中插入数据的操作（生产者）永远不会被阻塞，而只有获取数据的操作（消费者）才会被阻塞。

----------------------------------------------------------------------------------------------------------------------

 2. 主要方法

　put(E e) 
  向队尾存入元素，如果队列满，则等待；

  take()   
  从队首取元素，如果队列为空，则等待；

  offer(E e,long timeout, TimeUnit unit)  
  向队尾存入元素，如果队列满，则等待一定的时间，当时间期限达到时，如果还没有插入成功，则返回false；否则返回true；

  poll(long timeout, TimeUnit unit)   
  从队首取元素，如果队列空，则等待一定的时间，当时间期限达到时，如果取到，则返回null；否则返回取得的元素；

【线程池】

 如果并发的线程数量很多，并且每个线程都是执行一个时间很短的任务就结束了，
 这样频繁创建线程就会大大降低系统的效率，因为频繁创建线程和销毁线程需要时间。
 那么有没有一种办法使得线程可以复用，就是执行完一个任务，并不被销毁，而是可以继续执行其他的任务？
 
 1 ThreadPoolExecutor 构造器参数含义

 corePoolSize：核心池的大小
  这个参数跟后面讲述的线程池的实现原理有非常大的关系。
  在创建了线程池后，默认情况下，线程池中并没有任何线程，而是等待有任务到来才创建线程去执行任务，
  除非调用了prestartAllCoreThreads()或者prestartCoreThread()方法，
  从这2个方法的名字就可以看出，是预创建线程的意思，即在没有任务到来之前就创建corePoolSize个线程或者一个线程。
  默认情况下，在创建了线程池后，线程池中的线程数为0，当有任务来之后，就会创建一个线程去执行任务，
  当线程池中的线程数目达到corePoolSize后，就会把到达的任务放到缓存队列当中；

 maximumPoolSize：线程池最大线程数
  这个参数也是一个非常重要的参数，它表示在线程池中最多能创建多少个线程；

 keepAliveTime：表示线程没有任务执行时最多保持多久时间会终止。
  默认情况下，只有当线程池中的线程数大于corePoolSize时，keepAliveTime才会起作用，
  直到线程池中的线程数不大于corePoolSize，即当线程池中的线程数大于corePoolSize时，
  如果一个线程空闲的时间达到keepAliveTime，则会终止，直到线程池中的线程数不超过corePoolSize。
  但是如果调用了allowCoreThreadTimeOut(boolean)方法，在线程池中的线程数不大于corePoolSize时，
  keepAliveTime参数也会起作用，直到线程池中的线程数为0；

 unit：参数keepAliveTime的时间单位
  有7种取值，在TimeUnit类中有7种静态属性：
  TimeUnit.DAYS;              //天
  TimeUnit.HOURS;             //小时
  TimeUnit.MINUTES;           //分钟
  TimeUnit.SECONDS;           //秒
  TimeUnit.MILLISECONDS;      //毫秒
  TimeUnit.MICROSECONDS;      //微妙
  TimeUnit.NANOSECONDS;       //纳秒

 workQueue：一个阻塞队列，用来存储等待执行的任务
  这个参数的选择也很重要，会对线程池的运行过程产生重大影响，一般来说，这里的阻塞队列有以下几种选择：
  ArrayBlockingQueue;  基于数组的先进先出队列，此队列创建时必须指定大小
  LinkedBlockingQueue; 基于链表的先进先出队列，如果创建时没有指定此队列大小，则默认为Integer.MAX_VALUE
  SynchronousQueue;    这个队列比较特殊，它不会保存提交的任务，而是将直接新建一个线程来执行新来的任务
  一般使用LinkedBlockingQueue和Synchronous。线程池的排队策略与BlockingQueue有关。

 threadFactory：线程工厂，主要用来创建线程；

 handler：表示当拒绝处理任务时的策略，
  有以下四种取值：
  ThreadPoolExecutor.AbortPolicy:丢弃任务并抛出RejectedExecutionException异常。 
  ThreadPoolExecutor.DiscardPolicy：也是丢弃任务，但是不抛出异常。 
  ThreadPoolExecutor.DiscardOldestPolicy：丢弃队列最前面的任务，然后重新尝试执行任务（重复此过程）
  ThreadPoolExecutor.CallerRunsPolicy：由调用线程处理该任务 

---

 2. 重要方法

 execute()方法实际上是Executor中声明的方法，在ThreadPoolExecutor进行了具体的实现，
 这个方法是ThreadPoolExecutor的核心方法，通过这个方法可以向线程池提交一个任务，交由线程池去执行。

 submit()方法是在ExecutorService中声明的方法，在AbstractExecutorService就已经有了具体的实现，在ThreadPoolExecutor中并没有对其进行重写，
 这个方法也是用来向线程池提交任务的，但是它和execute()方法不同，它能够返回任务执行的结果，
 去看submit()方法的实现，会发现它实际上还是调用的execute()方法，只不过它利用了Future来获取任务执行结果

 shutdown()和shutdownNow()是用来关闭线程池的
 shutdown()：不会立即终止线程池，而是要等所有任务缓存队列中的任务都执行完后才终止，但再也不会接受新的任务
 shutdownNow()：立即终止线程池，并尝试打断正在执行的任务，并且清空任务缓存队列，返回尚未执行的任务

---

 3. 任务执行策略
 任务提交给线程池之后
 如果当前线程池中的线程数目小于corePoolSize，则每来一个任务，就会创建一个线程去执行这个任务；

 如果当前线程池中的线程数目>=corePoolSize，则每来一个任务，会尝试将其添加到任务缓存队列当中，
 若添加成功，则该任务会等待空闲线程将其取出去执行；
 若添加失败（一般来说是任务缓存队列已满），则会尝试创建新的线程去执行这个任务；

 如果当前线程池中的线程数目达到maximumPoolSize，则会采取任务拒绝策略进行处理；

 如果线程池中的线程数量大于 corePoolSize时，如果某线程空闲时间超过keepAliveTime，线程将被终止，直至线程池中的线程数目不大于corePoolSize；
 如果允许为核心池中的线程设置存活时间，那么核心池中的线程空闲时间超过keepAliveTime，线程也会被终止。

---

 - 不过在java doc中，并不提倡我们直接使用ThreadPoolExecutor，而是使用Executors类中提供的几个静态方法来创建线程池：
  Executors.newCachedThreadPool();        //创建一个缓冲池，缓冲池容量大小为Integer.MAX_VALUE
  Executors.newSingleThreadExecutor();   //创建容量为1的缓冲池
  Executors.newFixedThreadPool(int);    //创建固定容量大小的缓冲池

---
 ## 合理分配线程池大小

 一般需要根据任务的类型来配置线程池大小：

 如果是CPU密集型任务，就需要尽量压榨CPU，参考值可以设为 N(CPU)+1

 如果是IO密集型任务，参考值可以设置为2*N(CPU)


 
222222222222222222222222222222222222222222222



 
计算机网络
 将地理位置不同的独立计算机，通过通信线路连接起来
 在网络操作系统，网络应用软件以及网络通信协议的管理和协调下
 实现网络信息资源共享和信息传递的计算机系统

构成计算机网络的三要素
 1. 计算机
 2. 通信介质（导线、无线）
 3. 网络软件

网络编程三要素
 1. IP地址：用于定位网络上的一台计算机的位置
   本机的ip地址：127.0.0.1

 2. 端口号：计算机上的每一个进程都有一个唯一的端口号

 3. 通信协议：
  TCP协议：是一种面向连接的、可靠的、基于字节流的传输层通信协议
  UDP协议：用户数据报协议，是一种无连接的协议


网络编程
java的网络编程 -> Socket 编程 （套接字） 理解为电话

服务端：提供服务的计算机
客户端：希望获取服务的计算机

网络软件的实现原理：
1. 服务端开启监听
2. 客户端发送请求给服务器
3. 服务器返回结果给客户端

类似于QQ这样的聊天也是这样的原理
A和B聊天
是不是A直接发消息给B呢？
是A先把消息发给服务器，由服务器转发给B


telnet客户端
如何打开功能呢？
1. 控制面板
2. 程序
3. 打开或关闭windows功能
4. telnet功能 勾上 确定

如何使用呢？

1. 重启CMD
2. 打开服务器
3. telnet localhost 10086

333333333333333333333333333333333333333333333

## Date Time

### `java.time`

---

## Dynamic Proxy Classes
