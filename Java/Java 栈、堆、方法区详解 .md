## java栈、堆、方法区详解

java中的栈（stack）和堆（heap）是java在内存（ram）中存放数据的地方

### 堆区

存储的全部是对象，每个对象都包含一个与之对应的class的信息。 （class的目的是得到操作指令）； jvm只有一个heap区，被所有线程共享，不存放基本类型和对象引用，**只存放对象本身**。

**堆的优劣势**： 堆的优势是可以动态的分配内存大小，生存期也不必事先告诉编译器，java的垃圾收集器会自动收取这些不在使用的数据， 但缺点是，由于要在运行时动态分配内存，存取速度慢。

### 栈区

每一个线程包含一个stack区，只保存基本数据类型的对象和自定义对象的引用（不是对象），对象都存放在共享heap中；

每个栈中的数据（基本数据类型和对象引用）都是私有的，其他栈不能访问；

栈分为3部分：基本类型变量区、执行环境上下文、操作指令区（存放操作指令）

**栈的优劣势**： 存取速度比堆要快，仅次于直接位于CPU的寄存器，但必须确定的是存在stack中的数据大小与生存期必须是确定的，缺乏灵活性。单个stack的数据可以共享。

stack是一个**先进后出**的数据结构，通常保存方法中的参数，局部变量。

在java中，所有基本类型和引用类型都在stack中储存，栈中数据的生存空间一般在当前scopes内

### 方法区

- 又叫静态区，跟堆一样，被所有的线程共享。方法区包含所有的class和static变量；

- **方法区中包含的都是在程序中永远的唯一的元素**

### 在JAVA中，有六个不同的地方可以存储数据：

1\. 寄存器（register）。这是最快的存储区，因为它位于不同于其他存储区的地方----处理器内部。但是寄存器的数量极其有限，所以寄存器由编译器根据需求进行分配。你不能直接控制，也不能在程序中感觉到寄存器存在的任何迹象。

2\. 堆栈（stack）。位于通用RAM中，但通过它的"堆栈指针"可以从处理器哪里获得支持。堆栈指针若向下移动，则分配新的内存；若向上移动，则释放那些 内存。这是一种快速有效的分配存储方法，仅次于寄存器。创建程序时候，JAVA编译器必须知道存储在堆栈内所有数据的确切大小和生命周期，因为它必须生成 相应的代码，以便上下移动堆栈指针。这一约束限制了程序的灵活性，所以虽然某些JAVA数据存储在堆栈中----特别是对象引用，但是JAVA对象不存储其中。

3\. 堆（heap）。一种通用性的内存池（也存在于RAM中），用于存放所以的JAVA对象。堆不同于堆栈的好处是：编译器不需要知道要从堆里分配多少存储区 域，也不必知道存储的数据在堆里存活多长时间。因此，在堆里分配存储有很大的灵活性。 当你需要创建一个对象的时候，只需要new写一行简单的代码，当执行这行代码时，会自动在堆里进行存储分配。当然，为这种灵活性必须要付出相应的代码。用堆进行存储分配比用堆栈进行存储存储需要更多的时间。

4\. 静态存储（static storage）。这里的"静态"是指"在固定的位置"。静态存储里存放程序运行时一直存在的数据。你可用关键字static来标识一个对象的特定元素是静态的，但JAVA对象本身从来不会存放在静态存储空间里。

5\. 常量存储（constant storage）。常量值通常直接存放在程序代码内部，这样做是安全的，因为它们永远不会被改变。有时，在嵌入式系统中，常量本身会和其他部分分割离开，所以在这种情况下，可以选择将其放在ROM中

6\. 非RAM存储。如果数据完全存活于程序之外，那么它可以不受程序的任何控制，在程序没有运行时也可以存在。 就速度来说，有如下关系： 寄存器 < 堆栈 < 堆 < 其他

**运行类过程：方法区找到方法--堆中实例化对象--调用栈（指向堆中实例）**
