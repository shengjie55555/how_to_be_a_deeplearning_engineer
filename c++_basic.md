# Learn C++ from Scratch
## array
1. 定义数组后，sizeof(arr)可以统计数组所占内存空间，但是如果作为函数的实参传入时，只是一个64bit的地址，不能用来统计数组所占内存空间。
2. 数组作为函数的形参或者返回值时：  

| 数组类型  | 定义                              | 调用            | 备注                          |
|-----------|-----------------------------------|-----------------|----------------------------|
| 1d        | void sort(int a[10]);             | sort(b);        | a和b为长度相同的1d数组        |
| 1d        | void sort(int a[], int size);     | sort(b, 10);    | b为1d数组                   |
| 2d        | void sort(int a[10][10]);         | sort(b);        | a和b为长度相同的2d数组        |
| 2d        | void sort(int a[][10], int row);  | sort(b, 10);    | b为2d数组，行数可变           |
| 2d        | void sort(int a[], int size);     | sort(*b, 100);  | a和b为2d数组，可转换为1d数组   |

## 指针
1. 空指针：指针变量指向内存中编号为0的空间。空指针指向的内存是不可以访问的，可以正常编译，执行会出问题。
2. 野指针：指针变量指向非法的内存空间。比如手动将一个地址赋值给指针变量。
3. const修饰指针：const修饰距离它最近的，const int *a, 那么指向int变量的值不能变，
   
| 常量指针：const修饰变量    | const int *a;         | 指针可以指向别的变量，但是不能改变指向变量的值。  |
|-------------------------|-----------------------|-------------------------------------------|
| 指针常量：const修饰指针    | int * const a;        | 指针指向不能变，但是指针指向变量的值可以变。      |
| const既修饰指针又修饰变量  | const int * const a;  | 指针指向的变量不能变，指向的变量的值也不能变。    |
4. 指针与数组：int a[4][4]; 那么a[1]与*(a+1)与&a[1][0]与&a[1]都是第一行的首地址。
   
## 引用
1. int &b = a; // b是a的别名。
2. int &b; // 错误，引用必须初始化，int &b = a; 初始化后不可以改变。
3. void swap(int &a, int &b); // 引用传递时，可以改变实参，本质上a是对传入实参的引用。 
4. 引用的本质在C++内部实现是一个指针常量：int &ref = a; ref = 10; 等同于int* const ref = &a; *ref = 10; 
5. void swap(const int &a, const int &b); // 用来修饰形参，防止误操作改变实参。 

## 结构体
1. 定义结构体的成员时，不能指定成员的存储类型为auto、register、extern，这是因为系统不为结构体类型分配任何存储空间，但是可以指定成员的存储类型为static。 
2. 定义结构体时: struct 数据类型 {int age; char[20] name;}；struct不可省略，创建变量可以省略。 
3. 结构体数组：结构体类型名 数组名[size] = {{}, {}, {}}; 
4. 结构体指针：struct_type *p = struct_valiable; 这时候用->访问结构体属性。 
   
## C++核心编程
1. C++程序在执行时，将内存大方向划分为4个区域： 
   1. 代码区：存放函数体的二进制代码，由操作系统进行管理； 
   2. 全局区：存放全局变量、静态变量和常量； 
   3. 栈区：由编译器自动分配释放，存放函数的参数值、局部变量等； 
   4. 堆区：由程序员分配和释放（new和delete），若程序员不释放，程序结束时由操作系统回收。 

| int* a = new int(10);    | delete a;      |
|--------------------------|----------------|
| int* arr = new int[10];  | delete[] arr;  |

2. 函数提高
   1. void func(int a, int b = 10; int c = 10;); // 函数形参列表可以有默认值，出现默认值的变量必须排到末尾，函数声明时有默认值，函数实现时就不能再写默认值。
   2. void func(int a, int); // 函数占位参数，调用时必须填补该位置
   3. 函数重载： 
      1. 同一个作用域； 
      2. 函数名称相同； 
      3. 函数参数类型不同、个数不同或者顺序不同；
      4. 函数的返回值不可以作为函数重载的条件，调用函数时确保**入口不同**；
      5. 函数形参有默认值和函数重载在调用时可能产生歧义。 
   
| void func();          | void func(int a);            |
|-----------------------|------------------------------|
| void func(double a);  | void func(int a, double b);  |

3. 类和对象 
   1. 封装的意义：将属性和方法作为一个整体；将属性和方法加以权限控制。struct默认权限为public，class默认权限为private 
   2. 构造函数：类名() {} 
      1. 没有返回值也不用写void；
      2. 函数名称和类名相同； 
      3. 构造函数可以有参数，因此会发生重载;
      4. 程序在调用对象时会自动调用构造函数，无需手动调用，而且只调用一次;
      5. 默认情况下，C++编译器会提供默认构造函数、默认拷贝函数（浅拷贝）和默认析构函数。（1）如果用户定义有参构造函数，C++不提供默认无参数构造函数，但是会提供默认拷贝构造函数；（2）如果用户自定义拷贝构造函数，C++不再提供其他构造函数，这时候如果没有定义其他构造函数，Cube cube(10); 和 Cube cube；都会出错;
      6. 深拷贝和浅拷贝：如果类的属性中有指针，初始化后，指针会指向某个内存空间，浅拷贝只会将这个内存空间的地址赋值给新对象的指针，而不会重新在堆区开辟空间，这会导致两个问题：（1）如果原来的对象是函数内部作用域的局部变量，退出函数后，该变量会销毁，那么新对象指针指向的内存空间也被释放了；（2）如果析构函数里面用delete释放堆区空间，浅拷贝会导致多次释放同一个空间;
      7. 初始化列表：构造函数(int a, int b) : m_a(a), m_b(b){…} //其中m_a, m_b为类的属性;
      8. B类成员中有A类的对象，那么创建B类对象时，先调用A的构造函数再调用B的，析构时先B的再A的;
      9. 赋值时，比如c1 = Cube(1, 1, 1);右边的临时对象创建后会直接调用析构函数。静态成员（public权限）和函数可以通过类名:: 和对象. 两种方法访问;
   3. 析构函数：~类名() {} 
      1. 没有返回值，也不用写void； 
      2. 函数名称与类名相同，在名称前加上符号~； 
      3. 析构函数不可以有参数，所以不能重载； 
      4. 程序在对象销毁前会自动调用析构函数，无需手动调用，而且只会调用一次。 
   4. C++对象模型和this指针 
      1. 类内的成员变量和成员函数分开存放，只有非静态成员变量才属于类的对象空间。每一个非静态成员函数只会诞生一份函数实例，多个对象公用这一块代码。 
      2. this指针指向被调用的成员函数所需的对象。当形参和成员变量同名时：this->age = age; 可以用于返回对象本身：return *this; 
      3. 常函数：成员函数后加const，比如：void get_value() const {…} // 此时不能修改成员属性，可以获取成员属性，当成员属性声明时加入mutable，在常函数中可以修改。常对象：声明对象前加const，比如：const class_type c; 此时该对象只能调用常函数。
   5. 友元函数：可以在类外访问类中的私有属性。全局函数、其他类和其他类中的成员函数都可以做友元。需要在被访问的类中添加函数声明：friend void googGay(class_type c); 
   6. 运算符重载：加号运算符重载、左移运算符重载、递增运算符重载、赋值运算符重载等。C++编译器至少给一个类添加了4个函数：（1）默认构造函数（无参，函数体为空）（2）默认析构函数（无参，函数体为空）（3）默认拷贝构造函数，对属性进行值拷贝（4）赋值运算符operate=，对属性进行值拷贝。无论是默认的拷贝构造函数还是赋值运算，只有存在指针（有属性指向堆区），就会出现深浅拷贝的问题。赋值运算符重载格式：Class_type& operate=(Class_type c) {…; return *this;} //把形参c的属性赋值给this对象后，返回 *this 
   7. 继承：可以减少重复的代码。 
      1. class A: public B{…};A类为子类或派生类，B类为父类或基类。 
      2. 继承中，先调用父类构造函数，再调用子类构造函数，析构顺序先子类再父类。 
      3. 当子类中出现和基类同名成员时，可以通过设定基类中该成员的属性为private来避免，也可以通过作用域来访问基类成员，比如：this->Base::a; 如果出现同名成员函数，子类会隐藏基类中同名成员函数，加作用域可以访问到父类同名函数。
      4. 菱形继承时，若要使公共的基类在派生类中只有一个拷贝，则可以将这种基类说明为虚基类。比如：class ClassName: virtual public ClassName{…};并且需要在子类的构造函数中直接调用基类的构造函数。 
   8. 多态 
      1. 静态多态：函数重载和运算符重载属于静态多态，复用函数名，静态多态的函数地址在编译阶段确定
      2. 动态多态：派生类和虚函数实现运行时多态；动态多态的函数地址在运行阶段确定 
   9. 有继承关系，子类中重写了父类中的虚函数：virtual void print(){…}，子类中不需要加关键字：void print(){…}。父类的指针指向子类对象，子类的对象可以用于初始化基类对象。 
   10. 多态中，通常父类的虚函数实现是没有意义的，主要是调用子类重写的内容，因此可以将父类的虚函数定义为纯虚函数：virtual < type > FuncName(< ArgList >) = 0; 把至少包含一个纯虚函数的类称为抽象类，这种类只能用于派生的基类，不能产生对象，但是可以产生基类指针，指向其派生类，调用派生类中重写的虚函数。实际使用时一般通过一个基类派生多个子类，每个子类重新实现虚函数，然后定义基类指针，指向某一个子类，则调用该类的虚函数。如果子类中在堆区开辟了空间，基类指针无法释放子类对象，可以在基类中用虚析构函数或者纯虚析构函数实现。 

## 八股文
1. 智能指针
   1. 作用：
      * 管理一个指针，避免程序员申请的空间在函数结束的时候忘记释放，造成内存泄漏
      * 智能指针本质就是就是一个类，当超出类的作用域，类会自动调用析构函数，析构函数会自动释放资源。
   2. 常用接口
      ```C++
      T* get();
      T& operator*();
      T* operator->();
      T& operator=(const T& val);
      T* release();
      void reset(T* ptr=nullptr);
      ```
   3. unique_ptr
      1. 实现独占式拥有或严格拥有概念，保证同⼀时间内只有⼀个智能指针可以指向该对象.
         ```C++
         unique_ptr<string> p(new string("hello world"));
         ```
   4. shared_ptr
      1. 实现共享式拥有概念，多个智能指针可以指向相同对象，该对象和其相关资源会在"最后⼀个引⽤被销毁"时候释放。它使⽤计数机制来表明资源被⼏个指针共享。
   5. weak_ptr
      1. 是⼀种不控制对象⽣命周期的智能指针，它指向⼀个shared_ptr管理的对象。进⾏该对象的内存管理的是那个强引⽤的shared_ptr。weak_ptr只是提供了对管理对象的⼀个访问⼿段。
      2. 它只可以从⼀个shared_ptr或另⼀个weak_ptr对象构造，它的构造和析构不会引起引⽤记数的增加或减少。
      3. 可⽤来解决shared_ptr相互引⽤时的死锁问题，如果说两个shared_ptr相互引⽤，那么这两个指针的引⽤计数永远不可能下降为0，也就是资源永远不会释放。（和python里面的循环引用是一样的）
2. const和static
   1. static：控制变量的存储方式和可见性
      1. 修饰局部变量：⼀般情况下，对于局部变量在程序中是存放在栈区的，并且局部的⽣命周期在包含语句块执⾏结束时便结束了。但是如果⽤static关键字修饰的话，该变量便会存放在静态数据区，其⽣命周期会⼀直延续到整个程序执⾏结束。但是要注意的是，虽然⽤static对局部变量进⾏修饰之后，其⽣命周期以及存储空间发⽣了变化，但其作⽤域并没有改变，作⽤域还是限制在其语句块。
      2. 修饰全局变量：对于⼀个全局变量，它既可以在本⽂件中被访问到，也可以在同⼀个⼯程中其它源⽂件被访问(添加 extern进⾏声明即可)。⽤static对全局变量进⾏修饰改变了其作⽤域范围，由原来的整个⼯程可⻅变成了本⽂件可⻅。
      3. 修饰函数：⽤static修饰函数，情况和修饰全局变量类似，也是改变了函数的作⽤域。
      4. 修饰类中的成员：如果C++中对类中的某个函数⽤static修饰，则表示该函数属于⼀个类⽽不是属于此类的任何特定对象，存储空间中只存在⼀个副本，可以通过类和对象去调⽤。静态⾮常量数据成员，其只能在类外定义和初始化，在类内仅是声明⽽已。
         ```C++
         class Person {
         private:
            static int _nationality;
            static const string _sex = "male";
         };

         int Person::_nationality = "CHINA";

         int main() {
            return 0;
         }
         ```
      5. 注意事项：
         1. 函数体内static变量的作⽤范围为该函数体，不同于auto变量，该变量的内存只被分配⼀次，因此其值在下次调⽤时仍维持上次的值。
         2. static类对象必须要在类外进⾏初始化，static修饰的变量先于对象存在，所以static修饰的变量要在类外初始化。
         3. 由于static修饰的类成员属于类，不属于对象，因此static类成员函数是没有this指针，this指针是指向本对象的指针，正因为没有this指针，所以static类成员函数不能访问⾮static的类成员，只能访问static修饰的类成员。
         4. static成员函数不能被virtual修饰，static成员不属于任何对象或实例，所以加上virtual没有任何实际意义；静态成员函数没有this指针，虚函数的实现是为每⼀个对象分配⼀个vptr指针，⽽vptr是通过this指针调⽤的，所以不能被virtual修饰；虚函数的调⽤关系this->vptr->ctable->virtual function。
   2. const
      1. 修饰基本数据类型：基本数据类型，修饰符const可以⽤在类型说明符前，也可以⽤在类型说明符后，其结果是⼀样的。在使⽤这些常量的时候，只要不改变这些常量的值即可。
      2. const修饰指针变量：[详见指针](c++_basic.md##指针)
      3. const应用到函数中：按照const所修饰的部分进⾏常量化，保护了原对象的属性。通常⽤于参数为指针或引⽤的情况。
      4. const在类中的用法：
         1. const成员变量，只在某个对象⽣命周期内是常量，⽽对于整个类⽽⾔是可以改变的。因为类可以创建多个对象，不同的对象其const数据成员值可以不同。所以不能在类的声明中初始化 const数据成员，因为类的对象在没有创建时候，编译器不知道const数据成员的值是什么。const数据成员的初始化只能在类的构造函数的初始化列表中进⾏。
         2. const成员函数：const成员函数的主要⽬的是防⽌成员函数修改对象的内容。要注意，const关键字和static关键字对于成员函数来说是不能同时使⽤的，因为static关键字修饰静态成员函数不含有this指针，即不能实例化，const成员函数⼜必须具体到某⼀个实例。
      5. const修饰类对象，定义常量对象：常量对象只能调⽤常量函数，别的成员函数都不能调⽤。
   3. C和C++的区别（函数/类/struct/class）
      1. C++新增语法和关键字
         1. 语法的区别有头⽂件的不同和命名空间的不同
         2. 关键字⽅⾯⽐如C++与C动态管理内存的⽅式不同，C++中在malloc和free的基础上增加了new和delete，⽽且C++中在指针的基础上增加了引⽤的概念，关键字例如C++中还增加了auto，explicit体现显示和隐式转换上的概念要求，还有dynamic_cast增加类型安全⽅⾯的内容。
      2. 函数⽅⾯C++中有重载和虚函数的概念：C++⽀持函数重载⽽C不⽀持，是因为C++函数的名字修饰与C不同，C++函数名字的修饰会将参数加在后⾯，例如int func(int, double)经过名字修饰之后会变成_func_int_double，⽽C中则会变成_func，所以C++中会⽀持不同参数调⽤不同函数。C++还有虚函数概念，用以实现多态。
      3. 类⽅⾯，C的struct和C++的类也有很⼤不同：C++中的struct不仅可以有成员变量还可以成员函数，⽽且对于struct增加了权限访问的概念，struct的默认成员访问权限和默认继承权限都是public，C++中除了struct还有class表示类，struct和class还有⼀点不同在于class的默认成员访问权限和默认继承权限都是private。
      4. C++中增加了模板，提供了更加强⼤的STL标准库。
   4. 指针与引用的区别
      1. 指针是一个变量，存储的是指向对象的地址，在编译的时候，则是将“指针变量名-指针变量的地址”添加到符号表中，所以说，指针包含的内容是可以改变的，允许拷⻉和赋值，有const和⾮const区别，甚⾄可以为空，sizeof指针得到的是指针类型的⼤⼩（64位电脑就是8字节）。
      2. 引用只是⼀块内存的别名，在添加到符号表的时候，是将"引⽤变量名-引⽤对象的地址"添加到符号表中，符号表⼀经完成不能改变，所以引⽤必须⽽且只能在定义时被绑定到⼀块内存上，后续不能更改，也不能为空，也没有const和⾮const区别。
      3. sizeof引⽤得到代表对象的⼤⼩。⽽sizeof指针得到的是指针本身的⼤⼩。另外在参数传递中，指针需要被解引⽤后才可以对对象进⾏操作，⽽直接对引⽤进⾏的修改会直接作⽤到引⽤对象上。作为参数时也不同，传指针的实质是传值，传递的值是指针变量保存的地址；传引⽤的实质是传地址，传递的是变量的地址。
   5. 野（wild）指针与悬空（dangling）指针有什么区别？
      * 野指针是没有被初始化过的指针。
      * 悬空指针是指最初指向的内存已经被释放了的一种指针。 
   6. 函数指针：指向函数的指针变量
      * 在编译时，每⼀个函数都有⼀个⼊⼝地址，该⼊⼝地址就是函数名。
         ```C++
         // 函数返回值类型 (* 指针变量名) (函数参数列表);
         int Func(int x) { return x;} // 某个函数
         int (*p)(int x);  // 定义了一个函数指针，返回值和参数列表都是int变量
         p = Func;  // 函数名就是函数的入口地址，
         p(10);
         (*p)(10);
         ```
      * 函数指针在调用时，两种方式都是等价的。
   7. new/delete和malloc/free区别
      * new: 分配未初始化的内存空间（malloc）；使用对象的构造函数对空间进行初始化；返回空间的首地址。
      * delete：使用析构函数对对象进行析构；回收内存空间（free）。
      * new/delete可以自动调用构造和析构函数。
   8. 虚函数
      * 当⼀个类中包含虚函数时，编译器会为该类⽣成⼀个虚函数表，保存该类中虚函数的地址，同样，派⽣类继承基类，派⽣类中⾃然⼀定有虚函数，所以编译器也会为派⽣类⽣成⾃⼰的虚函数表。
      * 当我们定义⼀个派⽣类对象时，编译器检测该类型有虚函数，所以为这个派⽣类对象⽣成⼀个虚函数指针，指向该类型的虚函数表，这个虚函数指针的初始化是在构造函数中完成的。
      * 如果有⼀个基类类型的指针，指向派⽣类，那么当调⽤虚函数时，就会根据所指真正对象的虚函数表去寻找虚函数的地址，也就可以调⽤派⽣类的虚函数表中的虚函数以此实现多态。
   9. 静态绑定和动态绑定
      * 静态绑定，⼜名早绑定，绑定的是静态类型，所对应的函数或属性依赖于对象的静态类型，发⽣在编译期间。
      * 动态绑定，⼜名晚绑定，绑定的是动态类型，所对应的函数或属性依赖于动态类型，发⽣在运⾏期间。
      * virtual函数是动态绑定的，⾮虚函数是静态绑定的，缺省参数值也是静态绑定的。
         ```C++
         class Person {
         public:
            virtual void func(int a=10) {cout << a << endl;}
         };

         class Man: public Person {
         public:
            virtual void func(int a=12) {cout << a << endl;}
         };

         int main()
         {
            Person* p = new Man();
            p->func();  // 会调用Man类中的func，但是缺省值是静态绑定的结果仍为10
            return 0;
         }
         ```
   10. 为什么拷贝构造函数必须引用传递，不能是值传递？
       * 为了防止递归调用。当⼀个对象需要以值⽅式进⾏传递时，编译器会⽣成代码调⽤它的拷⻉构造函数⽣成⼀个副本（因为会将实参赋值给形参，调用的是=，存储在栈区），如果类A的拷⻉构造函数的参数不是引⽤传递，⽽是采⽤值传递，那么就⼜需要为了创建传递给拷⻉构造函数的参数的临时对象，⽽⼜⼀次调⽤类A的拷⻉构造函数，这就是⼀个⽆限递归。
   11. 内存泄漏
       * 内存泄漏简单的说就是申请了⼀块内存空间，使⽤完毕后没有释放掉。 它的⼀般表现⽅式是程序运⾏时间越⻓，占⽤内存越多，最终⽤尽全部内存，整个系统崩溃。由程序申请的⼀块内存，且没有任何⼀个指针指向它，那么这块内存就泄漏了。
   12. 预处理，编译，汇编，链接程序
       * ⼀段⾼级语⾔代码经过四个阶段：预处理→编译→汇编→链接，生成可执⾏的⽬标⼆进制代码。
       * **预处理阶段**：写好的⾼级语⾔的程序⽂本⽐如hello.c，预处理器根据#开头的命令，修改原始的程序，如#include<stdio.h>将把系统中的头⽂件插⼊到程序⽂本中，预处理后通常是以.i结尾的⽂件。
       * **编译阶段**：编译器将hello.i⽂件翻译成⽂本⽂件hello.s，这个是汇编语言程序。高级语言是源程序。所以注意概念之间的区别。汇编语⾔程序是⼲嘛的？每条语句都以标准的⽂本格式确切描述⼀条低级机器语言指令。不同的⾼级语言翻译的汇编语言相同。
       * **汇编阶段**：汇编器将hello.s翻译成机器语言指令。把这些指令打包成可重定位⽬标程序，即.o文件。hello.o是⼀个⼆进制⽂件，它的字节码是机器语⾔指令，不再是字符。前⾯两个阶段都还有字符。
       * **链接阶段**：⽐如hello程序调⽤printf程序，它是每个C编译器都会提供的标准库C的函数。这个函数存在于⼀个名叫printf.o的单独编译好的⽬标⽂件中，这个⽂件将以某种⽅式合并到hello.o中。链接器就负责这种合并。得到的是可执⾏⽬标⽂件。
   13. 动态编译和静态编译
       * 静态编译，编译器在编译可执⾏⽂件时，把需要⽤到的对应动态链接库中的部分提取出来，连接到可执⾏⽂件中去，使可执⾏⽂件在运⾏时不需要依赖于动态链接库。
       * 动态编译，可执⾏⽂件需要附带⼀个动态链接库，在执⾏时，需要调⽤其对应动态链接库的命令。所以其优点⼀⽅⾯是缩⼩了执⾏⽂件本身的体积，另⼀⽅⾯是加快了编译速度，节省了系统资源。缺点是哪怕是很简单的程序，只⽤到了链接库的⼀两条命令，也需要附带⼀个相对庞⼤的链接库；⼆是如果其他计算机上没有安装对应的运⾏库，则⽤动态编译的可执⾏⽂件就不能运⾏。


## STL (Standard Template Library)
1. 简介
   1. Container  
      1. Category
         1. Sequence containers  
            1. 每个元素都有固定的位置，取决于插入时机和地点，和元素值无关
            2. vector, list, stack, queue, deque
         2. Associated containers
            1. 元素位置取决于特定的排序准则，和插入顺序无关
            2. set, multiset, map, multimap
   2. Iterator  
      1. 定义：迭代器是一种检查容器内元素并且遍历容器内元素的数据类型
      2. 作用：提供对一个容器内对象的访问方法，并且定义了容器内对象的范围
      3. 意义
         1. STL每种容器的实现原理各不相同，如果没有迭代器需要记住每一种容器中对象的访问方法，显然很麻烦。
         2. STL为了统一对所有容器的访问方式，对每个容器都实现了一个迭代器，虽然实现方式不一样，但是操作方法是一致的。
         3. 比如：无论哪个容器，访问当前元素的下一个元素，我们可以通过迭代器自增进行访问。
2. vector  
   1. 将元素置于一个动态数组中加以管理的容器，可以随机存取元素，增删数据O(n)，尾部增删数据O(1)
   2. 初始化方式
      1. 默认构造```vector<T> arr;```
      2. 带参数构造
      ```c++
      vector<T> arr(begin, end);  // begin和end都是addr，左闭右开
      vector<T> arr(n, elem);  // n个elem拷贝给arr
      vector<T> arr(v);  // 将v拷贝给arr
      ```
   3. 赋值
   ```c++
   vector<T> v1;
   v1.assign(begin, end);  // begin和end都是addr，左闭右开
   v1.assign(n, elem);  // 将n个elem拷贝赋值给本身
   v1.swap(v2);  // 将v2和v1的元素互换
   ```
   4. 长度
   ```c++
   vector<int> v;
   int size = v.size();  // v的长度
   bool is_empty = v.empty();  // 判断是否为空
   v.resize(new_size);  // 重新指定长度，如果变长则默认填充，边短则删除超出长度的元素
   ```
   5. 访问方式
   ```c++
   vector<int> v = {1, 2, 3, 4};
   v.at(2) == v[2];  // 采用at如果越界会抛出std::out_of_range异常
   v[0] == v.front();
   v[v.size() - 1] == v.back();
   ```
   6. 末尾的插入移除
   ```c++
   vector<int> v;
   v.push_back(10);
   v.pop_back();  // 需要自己判断vector对象是否为空
   ```
   7. 任意位置插入: 可以插入元素，多个重复元素，一段连续空间的values
   ```c++
   vector<int> v = {1, 2, 3, 4};
   vector<int> v1 = {5, 6};
   v.insert(v.begin() + 1, -1);  // param: (addr, elem), return: (std::vector<int>::iterator)
   int idx = v.insert(v.begin() + 1, -1) - v.begin();
   v.insert(v.begin(), 3, -100);  // param: (addr, n, elem)
   v.insert(v.end(), v1.begin(), v1.end());  // param: (addr, addr, addr)
   ```
   8. 迭代器
   ```c++
   vector<int> v;
   vector<int>::iterator iter;  // iterator是一个类
   iter = v.begin();
   iter = v.end();
   ```
      1. 迭代器内部是通过指针来访问容器中的元素，如果发生扩容，那么本质是new了一块新的内存空间，那么原先定义的迭代器中的指针就变成了野指针，即指向的内存空间是非法的。
      ```c++
      vector<int> v = {1, 2, 3, 4};
      auto it = v.begin() + 2;
      v.insert(it, -1);  // 此时it内的指针指向的内存空间存储的不是-1
      it = v.insert(it, -1);  // insert函数返回的是新开辟的内存空间中对应的迭代器
      ```
      2. 如果改变容器的size，比如insert/erase之类的操作，需要注意更新iterator对象
3. deque
   1. double-ended queue, 在头部和尾部增删元素都是O(1), 中间是O(n)
   2. 头部的插入和移除
   ```c++
   deque<int> dq;
   dq.push_front(1);
   dq.pop_front();
   ```
4. list
   1. 双向链表容器，可高效进行插入删除元素，不可以随机存取，不支持at函数与[]操作符，只能iter++，不能+=n
   2. list对象的构造
   ```c++
   list<int> lst;
   list<int> lst(n, elem);  // 将n个elem拷贝给list对象
   list<int> lst(begin, end);  // 将[begin, end)区间内的元素拷贝给自身，可以是其他容器的起终迭代器
   list<int> lst(lst_1);  // 拷贝构造函数
   ``` 
   3. 赋值：不是追加，会直接覆盖原先的元素
   ```c++
   list<int> lst;
   lst.assign(begin, end);  // 将[begin, end)区间内的元素拷贝给自身，可以是其他容器的起终迭代器
   lst.assign(n, elem);  // 将n个elem拷贝给list对象
   lst.swap(lst_1);  // 将lst和lst_1的元素互换
   ```
   4. 长度
   ```c++
   int size = lst.size();
   bool is_empty = lst.empty();
   lst.resize(n, elem);  // 如果n>原长度则填充elem，否则删除超过指定容器长度的元素
   ```
   5. 头尾的增删操作
   ```c++
   list<int> lst;
   lst.push_back(elem);
   lst.pop_back();
   lst.push_front(elem);
   lst.pop_front();
   cout << lst.front();  // front(), back() 可以访问和修改头尾节点的value
   lst.front() = elem;
   ```
   6. 插入
   ```c++
   lst.insert(pos, elem);  // param: (addr, elem), return: (list<int>::iterator)
   lst.insert(pos, n, elem);
   lst.insert(pos, begin, end);
   ```
   7. 删除
   ```c++
   lst.clear();  // 清空
   lst.earse(begin, end);  // 删除[begin, end)区间的数据，返回下一个元素的位置
   lst.earse(pos);  // 删除pos位置的元素，返回下一个元素的位置
   lst.remove(elem);  // 删除容器中所有等于elem的元素
   ```
   8. 反转
   ```c++
   lst.reverse();
   ```
   9.  迭代器
   ```c++
   list<int>::iterator = lst.begin();  // 如果list<int>对象是const，那么iterator对应需要声明为const_iterator
   list<int>::iterator = lst.end();
   list<int>::reverse_iterator iter = lst.rbegin();  // 指向最后一个元素的反向迭代器，但是用for循环遍历时，还是用++来指向下一个元素的地址
   list<int>::reverse_iteratoriter = lst.rend();  // 指向第一个元素之前一个位置的反向迭代器
   ```
      1. ```lst.earse(pos);  // 返回指向下一个node的iterator```删除list中某个节点，首先需要记录next_ptr,否则iterator++操作会出问题 
5. stack
   1. stack是队栈容器，是一种“先进后出”的容器，没有迭代器，不能直接遍历
   2. stack对象的构造
   ```c++
   stack<int> st;
   stack<int> st_1(st);
   stack<int> st_2 = st_1;
   ```
   3. push & pop
   ```c++
   stack<int> st;
   st.push(elem);  // 入栈
   st.pop();  // 出栈
   st.top();  // 返回栈顶元素
   ```
   4. 长度
   ```c++
   st.size();
   st.empty();
   ```
6. queue
   1. queue是队列容器，是一种“先进先出“的容器，没有迭代器，不能直接遍历
   2. queue对象的构造
   ```c++
   queue<int> q;
   queue<int> q_1(q);
   ```
   3. push & pop
   ```c++
   queue<int> q;
   q.push(elem);  // 在队尾添加元素
   q.pop();  // 从队头移除元素
   q.front();  // 返回队头元素
   q.back();  // 返回队尾元素
   // 维护一个定长的queu
   for (int i = 0; i < 100; i++) {
      q.push(i);
      while (q.size() > 10) {
         std::cout << q.front() << '~' << q.back() << std::endl;
         q.pop();
      }
   }
   ```
   4. 长度
   ```c++
   q.size();
   q.empty();
   ```
7. set & multiset
   1. 基础知识
      1. set是一个集合容器，包含的元素是唯一的，集合中的元素按照一定的顺序排列。元素插入过程是按排序规则插入，所以不能指定插入位置。
      2. set采用**红黑树**变体的数据结构实现，红黑树属于平衡二叉树。在插入和删除操作上比vector快。
      3. set不可以直接存取元素，不可以使用at(pos)与[]操作符。
      4. multiset和set的区别在于前者中同一值可以出现多次。
      5. 不可以直接修改set和multiset容器中的元素值，因为该类容器是自动排序的，如果希望修改一个元素值，必须先删除原有的，再插入一个新的元素。
   2. set对象的构造
   ```c++
   set<int> s;
   set<int> s_1(s);
   s_1.swap(s);
   ```
   3. 插入和迭代器
   ```c++
   s.insert(elem);  // 在容器中插入元素elem
   s.begin();  // set<int>::iterator
   s.end();
   s.rbegin();  // set<int>::reverse_iterator
   s.rend();
   ```
   4. 大小
   ```c++
   s.size();
   s.empty();
   ```
   5. 删除
   ```c++
   s.clear();  // 清空所有元素
   s.erase(pos);  // param: (set<int>::iterator), return(set<int>::iterator)
   s.erase(begin, end);  // param(set<int>::iterator, set<int>::iterator), [begin, end)
   s.erase(elem);  // 删除特定的元素
   ```
   6. 排序
   ```c++
   #include <set>
   #include <string>

   class Person{
   public:
      Person() = default;
      ~Person() = default;
      Person(int age, std::string name): age(age), name(name) {}
      Person(const Person& p) {
         this->age = p.age;
         this->name = p.name;
      }
      int get_age() const {
         return this->age;
      }
      
      std::string get_name() const {
         return this->name;
      }
   private:
      int age;
      std::string name;
   };

   class PersonFunctor{
   public:
      bool operator() (const Person& p1, const Person& p2) const {
         return p1.get_age() > p2.get_age();
      }
   };

   int main() {
      // Write C++ code here
      std::cout << "Hello world!\n";

      set<int, less<int>> s1;  // 默认的升序
      set<int, greater<int>> s2;  // 降序
      
      Person p1(10, "wsj");
      Person p2(11, "cmf");
      Person p3(12, "xye");
      std::cout << p1.get_name() << ' ' << p1.get_age() << std::endl;
      
      std::set<Person, PersonFunctor> s;
      s.insert(p1);
      s.insert(p2);
      s.insert(p3);
      
      for (auto it = s.begin(); it != s.end(); it++) {
         std::cout << it->get_name() << " " << it->get_age() << std::endl;
      }
      
      std::cout << "End world!\n";
      return 0;
   }
   ```
   7. 查找
   ```c++
   s.find(elem);  // 查找elem元素，返回指向elem元素的迭代器，如果找不到，返回的是s.end()
   s.count(elem);  // 返回容器中值为elem的元素个数，对于set，要么是0要么是1,对于multiset，可能大于1
   s.lower_bound(elem);  // 返回第一个 >= elem元素的迭代器
   s.upper_bound(elem);  // 返回地一个 > elem元素的迭代器
   ```
8. map & multimap
   1. map对象的构造
   ```c++
   map<int, int> m;
   ```
   2. 插入和迭代器
   ```c++
   // insert不会去覆盖原来的键值对
   m.insert(pair<int, int>(3, 3));  // 通过pair方式
   m.insert(map<int, int>::value_type(1, 1));  // 通过value_type方式
   m[2] = 2;  // 类内重载了[]，如果不存在则插入，如果存在则修改，m[key]作为右值时，如果key不存在，那么则会创建一个pair<int, int>(key, default_value)的键值对

   // 循环遍历
   for (std::map<int, int>::iterator it = m.begin(); it != m.end(); it++) {
      std::cout << (*it).first << ' ' << (*it).second << std::endl;
   }
   ```
   3. 获取键值对
   ```c++
   cout << m[1];  // 如果1不存在，会自动创建一个默认的键值对
   map<int, int>::iterator it = m.find(2);  // 返回一个迭代器，如果找不到则返回m.end()
   cout << m.at(1);  // 区别于第一种，在于如果找不到会抛出std::out_of_range异常，而不是自动创建一个默认的键值对
   ```