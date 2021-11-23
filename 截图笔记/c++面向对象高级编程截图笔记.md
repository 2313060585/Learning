# c++面向对象高级编程截图笔记（1，上）

---

## 3、构造函数

![image-20210309203310582](C:\Users\珞\AppData\Roaming\Typora\typora-user-images\image-20210309203310582.png)

初始化和赋值是两个阶段，上图是构造函数的特有初始化写法。
		fun(参数) : 变量1(值), 变量2(值){ }

创建对象时自动调用构造函数，如果没写系统会各一个默认的空构造函数，构造函数名要与类名一致。

![image-20210309203854953](C:\Users\珞\AppData\Roaming\Typora\typora-user-images\image-20210309203854953.png)

![image-20210309203903245](C:\Users\珞\AppData\Roaming\Typora\typora-user-images\image-20210309203903245.png)

如上图构造函数可以有很多个重载。

<img src="C:\Users\珞\AppData\Roaming\Typora\typora-user-images\image-20210309204039359.png" alt="image-20210309204039359" style="zoom:50%;" />

注意上图两种构造函数冲突不可看做重载，因为同时都用了初始化值的写法。

## 4、参数传递与返回值

<img src="C:\Users\珞\AppData\Roaming\Typora\typora-user-images\image-20210309204400355.png" alt="image-20210309204400355" style="zoom:50%;" />

通常构造函数都是public的，但构造函数也可放在private中，这种情况通常出现在单例模式，用上图右边的写法调用。

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210309204631333.png" alt="image-20210309204631333" style="zoom:67%;" />

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210309204942207.png" alt="image-20210309204942207" style="zoom:67%;" />

不会改变数据内容的方法前要加const。否则在使用时，初始化一个常量的类，调用其中未添加const关键字的方法，编译器会报错。

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210309214132761.png" alt="image-20210309214132761" style="zoom:50%;" />

传递const类型的引用，接受的函数内不可对引用值修改，不然无法编译。
		**参数传递尽量都传递引用！**

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210309214651631.png" alt="image-20210309214651631" style="zoom:50%;" />

 **返回值类型也尽量都传递引用！**

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210309215406774.png" alt="image-20210309215406774" style="zoom:50%;" />

 友元可以取得类中private的数据。

 

## 7、三大函数

拷贝构造

![image-20210314162147637](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210314162147637.png)		拷贝赋值

![image-20210314162116799](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210314162116799.png)

检测自我复制是为了防止浅拷贝造成两块指针指向同一处，在一开始错误的清掉了自己指向的值。

析构

## 8、堆栈与内存管理

![image-20210316192545145](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210316192545145.png)

谁调用函数，this就是其对应的类型。

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210316192834129.png" alt="image-20210316192834129" style="zoom:50%;" />

**new**先分配内存，再转型，再调用构造函数。

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210316192646622.png" alt="image-20210316192646622" style="zoom:50%;" />

**delete**先调用析构函数，再释放内存。

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210316193506322.png" alt="image-20210316193506322" style="zoom:80%;" />

长的是调试模式下的，灰色部分内存用于方便回收调试占用的内存空间，开头可结尾各占4各字节，最后四位用于表示这个变量实际占用的字节长度和发送还是回收，1/0，发送/回收，他们占用8个字节，深绿色部分表示填充位，每个发送出去的变量都要占用十六的倍数个字节数，方便吧后四位都变成0用以携带其他表示发送、回收、字节长度等的信息。

![image-20210316213603617](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210316213603617.png)

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210316213446026.png" alt="image-20210316213446026" style="zoom:80%;" />

delete删除数组的指针时要在**delete**后加**[]**

9. #### 复习string类的实现过程

![image-20210316214248114](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210316214248114.png)



构造函数，存字符串

拷贝构造

拷贝复制

析构

返回指向本身的指针，用于putout

![image-20210316214617358](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210316214617358.png)

![image-20210316215051979](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210316215051979.png)

 函数全写inline就完事了

![image-20210316215436032](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210316215436032.png)

 

注意自我赋值的情况，字符串动态分配空间后面有个0，要多开一位

出现在typename后面的&叫引用。出现在变量前的&叫取地址，会得到一个指针。

## 10、扩展补充，类模板，函数模板及其他

static：在内存空间中只有一份的变量，静态函数没有this point，只能用于处理静态数据。

单例模式：

 ![image-20210317092501421](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317092501421.png)



函数模板

![image-20210317094916739](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317094916739.png)

 

## 11、组合与继承

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317095803131.png" alt="image-20210317095803131" style="zoom:67%;" />

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317095834516.png" alt="image-20210317095834516" style="zoom:67%;" />

上图表示queue中有deque这种东西，表示**组合**关系

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317100444882.png" alt="image-20210317100444882" style="zoom:67%;" />

![image-20210317100848380](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317100848380.png)



![image-20210317100744130](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317100744130.png)

上图表示string中有指向stringRep这种类型的指针，表**委托**关系

左边是个接口，右边是本体（pimpi，Handle/Body），也叫编译防火墙

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317102456246.png" alt="image-20210317102456246" style="zoom:67%;" />

上图表示**继承**关系



## 12、虚函数与多态

vitural-虚函数关键字。表示子类在继承父类时，父类是否希望子类重新定义它已有的函数。

**非虚函数**：父类不准子类重新定义

**虚函数**：父类希望子类重新定义，当然不重新定义也行

**纯虚函数**：父类要求子类一定要重新定义才能使用，因为服了没有对其进行定义

![image-20210317103524417](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317103524417.png)

  

子类(C)同时存在继承父类(A)和组合其他类(B)时候，构造函数的构造顺序如下：

A->B->C

![image-20210317112306365](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317112306365.png)

**观察者模式**



## 13、委托相关设计

c+中vector内放的东西一定要一样大小，要存动态大小的东西就存指针。

![image-20210317160712496](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317160712496.png)

组合模式，可用于建立文件树

![image-20210317161718852](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317161718852.png)

图中表示：

+public

#proticted

-private



# c++程序设计（1、下）

---

## 1转换函数

![image-20210317164804312](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317164804312.png)

转换函数的返回类型就是名称类型，同时不准有参数，默认参数就是隐藏的this，而且通常函数都会将加const，因为不会改变被转换函数的值。

## 3、non-explicit-one-argument ctor

C++中的**explicit**关键字只能用于修饰**只有一个参数**的类**构造函数**, 它的作用是表明该构造函数是显示的, 而非隐式的, 

跟它相对应的另一个关键字是**implicit,** 意思是隐藏的,类构造函数默认情况下即声明为implicit(隐式).

![image-20210317170241594](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317170241594.png)

这时如果定义Fraction d1 = 4 + f会通过，如果是Fraction d2 = f + 4会报错，有二义性

 智能指针类的内部一定有真正的指针，并且一定有对操作符*和->的重载。

迭代器不光要重载操作符*和->，还有++，--等操作符。

![image-20210317213620139](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317213620139.png)



## 5、function-like classes

![image-20210317214118450](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317214118450.png)

类中如果有对操作符（）的重载，那么就意味着这个对象是个**仿函数**对象，为了让它用起来像个一个function。

![image-20210317214459781](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210317214459781.png)

这两个函数大小理论上内存大小为0，因为里面没塞任何数据，因为技术实现的关系，实际为1。



## 6、namespace

用以区分不同人写的同名变量。





## 7、class template

将不确定的变量或函数类型指定为**T**的用法就是模板

```c++
template<typename T>
class complex{
    public:
    	complex (T r = 0,T i = 0)
        :re (r),im (i)
        {}
    	complex& operator += (const complex&);
    	T real () const{return re;}
    	T imag () const{return im;}
    private:
    	T re,im;
    	
    	friend complex& __doapl (complex*, const complex&);
}

int main(){
    complex<double> c1(2.5, 1.5);
    complex<int> c2(2, 6);
}
```



![image-20210318100849678](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210318100849678.png)

函数模板不必制定type，因为编译器会做实参推导

## 9、member template

![image-20210318101712256](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210318101712256.png)

使用成员模板可以使构造函数更有弹性。

上图中通过时用成员模板达到了可以让所有子类赋值给父类构建对象的效果。

![image-20210318102336545](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210318102336545.png)

智能指针要达到和指针同样的效果，因此也使用了成员模板

 

## 10、模板特化

 ![image-20210318103234821](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210318103234821.png)

偏特化

![image-20210318103452759](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210318103452759.png)

**个数上的**：绑定一部分模板的参数

![image-20210318103533168](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210318103533168.png)

**范围上的**：针对不同类型调用不同的泛化模板，如上就针对变量是否为指针调用了不同的模板类

## 12、template template paramember

模板的模板，用于不确定的容器中套了不确定的变量类型。

![image-20210318104000528](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210318104000528.png)





上述XCLs<string, list> mylst1编译无法通过的原因是容器还有不可兼得默认参数，而上述模板不能自动填充多个默认参数。

using Lst = list<T,allocator<T>>可以解决上述问题。

## 14、 variadic templates

![image-20210318114746774](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210318114746774.png)

 

 

## 15、reference

![image-20210318133932728](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210318133932728.png)

（&）reference常用于传参。

![image-20210318134559715](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210318134559715.png)

不能同时存在同名的传引用和传递实参的函数，因为&不是签名的一部分。

但可以同时存在一个带const和一个不带const的，因为const是函数签名的一部分。

## 16、复合、继承关系下的构造和析构

构造由内而外，析构由外而内。  

## 17关于虚函数和虚表

vptr

vtbl

![image-20210318140529104](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210318140529104.png)

含有虚函数的类中都会有个虚指针，虚指针指向一份虚表。 

## 21、重载::operator new  ::operator delete

![image-20210318152117300](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210318152117300.png)

![image-20210318152346274](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210318152346274.png)

上图是编译时new和delete的真正执行过程，重载的new和delete会在上面箭头出发点被调用。

![image-20210318161648441](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210318161648441.png)

![image-20210318191855427](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210318191855427.png)

