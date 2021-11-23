# STL标准库和泛型编程

---

## 3、容器之分类与各种测试

vector的扩容过程是两倍增长的（1,2,4,8...），用vector.capacity可查目前容量，而vector.size查的是目前存了多少东西。

::表示全局变量

  ![image-20210320135600605](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210320135600605.png)

deque是分段连续存储的，看起来连续是由操作符重载实现的。

![image-20210320152204118](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210320152204118.png)

分配器还内存的时候当初要了多少个就要还对应的个数才行，因此不直接使用分配器。用malloc和free进行内存管理。

## 11、分配器

 allocators调用malloc和free管理内存

![image-20210321200116501](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210321200116501.png)

 ![image-20210321201918529](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210321201918529.png)

mallc分配时是从链表里往外分，每条链表看标号来判断它存多大的字节，然后分配器根据对应大小分到对应标号的链表中，链表内没内存可分时候才向系统要内存，这些表里内存都是用单向链表穿起来的。

## 13、深度探索list

![image-20210321205111406](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210321205111406.png)

![image-20210321204812286](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210321204812286.png)

前++里的node是一个指向本身的指针。

后++带一个无意义的参数，前++不带，且后++调用了重载后的拷贝构造和前++；

前++返回类型是&，后++是值。因为c++不允许整数进行两次后++动作但是可以两次前++，如上图左下角所示。

![image-20210321205513176](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210321205513176.png)

对*的重载就是让node取得本身的data值。

![image-20210321205900772](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210321205900772.png)

g2.9到g4.9修正了指针指向空的问题。

![image-20210321210223873](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210321210223873.png)

容器实际制作时候是环装的，为了实现前闭后开区间，因此会有一个不属于链表的节点夹在环中。这也就是为什么x.begin()可以取到但x.end()取不到的原因，因为end就是那个不属于容器的节点。

![image-20210321210650490](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210321210650490.png)

新版本链表实现的类间关系。

## 15、iterator Traits的作用与设计

Traits能萃取出iterator中一定的特性

![image-20210322085932346](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322085932346.png)

![image-20210322090255488](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322090255488.png)

iterator可以回答algorith提出的五种问题。

 收到的iterator可能是退化的，也就是收到了指针，就要用traits。



![image-20210322090739278](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322090739278.png)

traits的实现借助了偏特化。

![image-20210322091039013](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322091039013.png)

 

## 18、deque、queue、stack

deque是一个分段连续的数据结构，它的iterator是个类

cur：当前所在节点

first：node的初始点

last：node的结束点

node：当前所在连续的段的位置，这个是用来存分块区间的vector的位置，表示当前在第几段。

![image-20210322094352612](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322094352612.png)

![image-20210322100544133](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322100544133.png)

计算位置

![image-20210322102853940](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322102853940.png)

操作符重载

![image-20210322102944843](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322102944843.png)

ps：操作符重载一般写后++/--时调用前++/--；

![image-20210322103133570](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322103133570.png)

deque类的关系设计

![image-20210322103611368](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322103611368.png)

 

stack和queue

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322104522258.png" alt="image-20210322104522258" style="zoom:67%;" />



<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322105730494.png" alt="image-20210322105730494" style="zoom:67%;" />

## （ 番外）红黑树

https://zhuanlan.zhihu.com/p/79980618

红黑树的规则：

1.每个节点都有红色或黑色

2.树根始终要为黑色

3.没有两个相邻（连续）的红色节点

4.从任意节点到其任何后代NULL节点的每条路径都具有相同数量的**黑色**节点



变换规则主要两条：

1.recolor（改颜色）

2.rotation（旋转，类似于平衡二叉树的构造过程）



树的构建步骤如下：

1.将新插入的节点X标记为红色

2.如果X是根节点，那么将起标记为黑色（结束）

3如果X的parent不是黑色&&X也不是root（需同时满足才结束）（就说明出现了两个红色相连，此时判断要旋转还是改颜色）：

​	3.1--如果X的uncle节点为**红色**

​		3.1.1）将parent和uncle改为黑色

​		3.1.2）将grand parent(祖父)标记为红色

​		3.1.3）让X与它的祖父节点颜色相同。继续**重复公式 2、3**。确保根节点为黑色**注意，此时祖父节点将成为新的X**（因为虽然这时候在祖上三代看不到相连的两个红色节点了，但可能祖父和它的爸爸同时为红色，这时就需要对祖父进行上面的判断，若一直需要向上找，到根节点在第二步自然会停止）

​	3.2--如果X的uncle是**黑色**（下面的左右依次都是从祖父节点算起往下数）

​		3.2.1）X在左左，（祖父）P设为黑色PP设为红色，右旋，

​		3.2.2）X在左右，（父亲）左旋，（祖父）P设为黑色PP设为红色，右旋

​		3.2.3）X在右左，（父亲）右旋，（祖父）P设为黑色PP设为红色，左旋

​		3.2.4）X在右右，（祖父）P设为黑色PP设为红色，左旋。

​		记起来就是，左左右，右右左，左右，右左，数的时候从上数，转的多的时候从下转，祖父旋转父黑祖红再旋转



关于删除先马一下：

![img](https://upload-images.jianshu.io/upload_images/2392382-edaf96e55f08c198.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp)

## 20、RB-tree深度搜索







## 20、RB-tree深度搜索

红黑树是平衡二叉搜索树。

![image-20210322110003016](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322110003016.png)

 

红黑树在标准库的定义（key和data合成value）

![image-20210322144143941](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322144143941.png)

例子

![image-20210322144415607](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322144415607.png)

 

## 21、set

![image-20210322150612841](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210322150612841.png)

set在其实现的类中有一个红黑树，它把所有的事情都转交给内部的红黑树完成，因此set也可以被看做是适配器。

##  25、各种哈希

hash_map中使用了数组，链表，红黑树来实现。

当链表长度大于等于8时候转为红黑树，树的节点数小于6时候转为链表，因为链表查找时间复杂度为n/2，红黑树为log8

红黑树线程不安全，当AB插入值相同且同时进行put时会产生覆盖。



## 29、迭代器分类对算法的影响

![image-20210323160209606](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210323160209606.png)

iterator_traits用来回答问题，通常会返回个类型。

上面的return __ distance就是通过traits得到的category来确定要调用哪个__distence

type_traits的影响

![image-20210323163941195](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210323163941195.png)

## 30、算法源码分析

### accumulate

![image-20210323165537119](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210323165537119.png)

### for_each

![image-20210323165613741](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210323165613741.png)

### count

下面8的自己带有count的函数和其他函数租户要区别是他们是用哈希表和红黑树实现的，有独特的查找方式。

![image-20210323195220113](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210323195220113.png)

![image-20210323195227334](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210323195227334.png)

### find

![image-20210323195517415](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210323195517415.png)

![image-20210323195511858](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210323195511858.png)

### sort

关联式容器本身就已经排序了，不需要sort，链表不能跳也不能sort

![image-20210323195943247](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210323195943247.png)

![image-20210323195711374](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210323195711374.png)

上图调用rbegin和rend相当于反向与begin和end排序

![image-20210323200101808](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210323200101808.png)

![image-20210323200133400](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210323200133400.png)

### binary_search

使用了lower_bound

![image-20210323200423307](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210323200423307.png)

## 31、仿函数和函数对象

自己写的functors要继承binary_function（两个操作数）或unary_function（一个操作数），用以融入到STL

![image-20210324125549777](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210324125549777.png)

## 32、adapter适配器‘

adapter用组合的方式来实现。不使用继承。

![image-20210324140305860](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210324140305860.png)

adapter可能也会向他内涵的东西提问。

type name后直接加（）作用是创建临时对象。



## 35、bind用法：

绑定第二参数或未确定的模板参数。

![image-20210324143551102](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210324143551102.png)

迭代器适配器inserter

通过重载绑定的额外参数的操作符重载，可以改变函数的执行行为

![image-20210324153413775](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210324153413775.png)

## 37、ostream_iterator

可以把迭代器绑定到cout上输出，还可以指定分隔符。

![image-20210324161129933](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210324161129933.png)



## 39、istream_istream



![image-20210327094105221](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210327094105221.png)

##  40、hash function

![image-20210328155001003](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210328155001003.png)

## 41、tuple

可以用多种类型的变量构造出一个变量。

用法如下：

tuple<tupename1,typename2... ...typenamen> t;//定义

auto t2 = make_tuple(22,44,"???");//auto直接推导出赋值的类型

sizeof(t);//看大小

cout<<get<0>(t)<<get<1>(t)<<... ... << get<n>(t)<<endl;

cout<<tuple_size<TupleType>::value<<endl;



![image-20210328155814654](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210328155814654.png)

 

![image-20210328162714660](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210328162714660.png)

 

## 42.type traits

![image-20210328170219769](C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210328170219769.png)

一个类是否该有**虚析构函数**要看他是否会被当做**父类**。

