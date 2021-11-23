# Shell命令：

who：查询有哪些用户

sudo：以最高权限执行某个命令

apt-get update：自检更新下载资源

apt-get upgrade：安装更新

apt-get dist-upgrade：内核更新（相当于windows系统更新）

pwd：打印出当前在哪个目录下面

cd：进入下一级目录（~到主目录下）

相对路径：cd . ：当前目录	cd .. : 到上一级目录

ls：列出当前目录下文件

ls -i：查看文件号

ls -F：列出当前目录下文件夹用 **xxx/** 表示

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210417152321462.png" alt="image-20210417152321462" style="zoom:50%;" />  

ls -l：列出详细信息：

目录 拥有者权限-与你同一组的用户的权限-其他用户权限  文件的硬连接数 文件归属谁 归属者的组 文件大小 上一次修改时间 文件名字

硬链接必须在同一块硬盘上（因为涉及文件号）才能使用

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210417152420948.png" alt="image-20210417152420948" style="zoom:50%;" /> 

ls a* ： 列出以a开头的文件

ls *.txt：列出后缀为txt的文件

ls a?b：？占用一个未知字符



touch：创建一个文件，touch已经创建的文件会更改文件的时间信息

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210417152537525.png" alt="image-20210417152537525" style="zoom:50%;" /> 

cp （-i） aaa.txt aaa.bak：拷贝aaa.txt到aaa.bak(发生覆盖的时候-i会触发询问是否操作）

cp -l aaa.txt bbb.txt：会改变文件aaa和bbb的硬链接数，bbb相当于对aaa的引用，也就是起了个别名，改变两个文件中一个的内容，另一个也会同步改变(类似共享指针)

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210417154457688.png" alt="image-20210417154457688" style="zoom:50%;" /> 

rm aaa.txt：删除aaa.txt

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210417154554838.png" alt="image-20210417154554838" style="zoom:50%;" /> 

mkdir doc： 建立一个名字叫做doc的目录

rmdir doc： 删除目录doc

当目录下有文件时候会提示不让删

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210417155010337.png" alt="image-20210417155010337" style="zoom:50%;" /> 

rm -r doc： 递归删除doc下所有内容

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210417155128872.png" alt="image-20210417155128872" style="zoom:50%;" /> 

stat  abc.txt：查看文件详细信息

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210417155502611.png" alt="image-20210417155502611" style="zoom:50%;" /> 

file abc.txt：查看文件详细信息

<img src="C:/Users/珞/AppData/Roaming/Typora/typora-user-images/image-20210417155715449.png" alt="image-20210417155715449" style="zoom:50%;" />  

cp -s abc.txt aaa.txt：软连接拷贝

调用aaa.txt时候系统会默认认为你在调用abc.txt（可以关联到多个硬盘）

缺点：可能会出现空引用（软连接失效，被指向文件被删除了），和循环引用（软连接之间相互指，类似于共享指针的循环引用）。

ln：建立文件间的连接（默认硬链接）

mv a b：更改文件名字

