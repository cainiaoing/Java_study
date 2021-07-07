## 第一章

### 1、安装EditPlus

学习前线安装好一点的文本编辑器，这里是EditPlus5

   * 安装好之后取消自动备份，否则会出现.bak后缀的文件（以后缀.bak结尾的文件是备份文件）
     取消方式；工具 --> 首选项 --> 文件 --> 保存是船舰备份文件给去掉即可
   * 设置字体等一系列选项

### 2、懂得DOS命令

作为程序员，要求掌握最基本的windows 相关DOS命令

1、DOS命令操作的位置：在DOS命令窗口编写DOS命令（即终端 ； 命令提示符）
       2、打开方式；windows + r键 --> 在输入cmd

3、定义：最初的windowns计算机中没有图形界面，只能通过DOS窗口完成对文件的新建、编辑、保存、删除等一系列操作

4、常见的DOS命令；

```markdown
- exit 退出当前DOS窗口
- cls（等价于clear screen) 清除当前DOS窗口的信息
- DOS窗口中的内容怎么复制
      在DOS窗口中任意位置，赋值粘贴即可，
      
- dir 列出当前目录下的所有子文件/子目录。
- cd 命令
      * cd 命令表示：change directory[改变目录]
      * cd 命令怎么用？
        cd 目录的路径
      * 但是路径包括绝对路径和相对路径
        1、绝对路径：表示该路径从某个磁盘的盘符下作为出发点的路径
        2、相对路径：表示该路径从当前所在的路径下作为出发点的路径
        3、假设是这样写的：C:\Users\28929，那么在此时输入cd Desktop,那么Desktop就是一个相            对路径，从当前所在的C:\Users\28929 作为出发点开始找Desktop目录
        4、假设是这样写的：cd C:\Users\28929\Desktop,其中C:\Users\28929\Desktop路径就是            一个绝对路径。
 - cd .. 回到上级目录
 - cd \  直接回到根目录
 - 怎么切换盘符
   c: 回车，就到了c盘
   d: 回车 ， 就到了D盘
   e: 回车， 就到了E盘
   f: 回车， 就到了F盘
- ipconfig 是用来查询ip地址的

- del *.class 表示删除掉后缀名为class的文件。

- del 文件名.文件后缀名（删除单个指定文件）

- cd . 那个.代表当前路径，..代表上级路径

-ping (看看电脑能否正常的上网，通信)
  格式
     ping IP地址
     ping 域名  （ping www.baidu.com / ping www.google.com
```

### 3、显示文件扩展名

我的电脑 –> 菜单栏 –> 查看 –> 勾中显示文件扩展名

### 4、JDK目录的介绍

- bin目录：存放一些可执行文件（想java.exe,Java编译器等，javac.exe负责编译，java.exe负责运行）
- db目录：是一个小型的数据库
- jre目录：Java程序运行时的环境
- include目录：存放c语言一些头文件
- src.zip文件；这个文件可以查看JDK的核心源代码
- lib目录：Java的类库库文件（图书馆简称）

### 5、编译阶段

```markdown
1、程序员需要在硬盘的某个位置新建一个.java扩展名的文件，该文件被称为Java源文件，Java里编写的是Java源程序/源代码，一个Java源文件，可以编写生成多个.class文件/字节码文件，而.class文件是最终要执行的文件。Java源文件的删除最终不会影响Java文件的执行。

2、Java程序员需要使用JDK当中自带的javac.exe命令进行Java程序的编译。
3、javac怎么用，在哪里用？
   在DOS窗口中使用
  
4、编译结束之后，可以拷贝.class文件，到其他操作系统中去执行（跨平台）
```

### 6、运行阶段

```mardkown
1、JDK中的Java.exe命令主要负责运行阶段

2、- Java.exe在DOS里用使用方法为；java 类名
   例如；硬盘上有个A.class,那就这样用java A;硬盘上有个B.class,那就这样用 java B;但是这种方式错误的；java A.class.
3、
```

### 7、安装JDK

```c
官网下载JDK,默认下一步
到了jre时候，要知道；JDK;java开发工具包
                   JRE;java的运行时环境,只要有这个环境，就可以运行java程序
                   JVM;java的虚拟机
三者的关系是；JDK > JRE > JVM，所以，JDK中都会自带一个JRE,可以不选择目录去安装它，取消 -》 关闭即可，也可以去更换位置去某任下一步安装他。
                       
```



### 8、path环境变量的配置

```markdown
将HelloWorld.java源程序文件通过javac工具进行编译；
- 首先需要解决的问题是：javac命令是否能用

- 打开DOS命令窗口，直接数据javac，然后回车，会出现以下问题：“‘javac’ 不是内部或外部命令，也不是可运行的程序或批处理文件”， 出现此问题是因为windowns操作系统无法找到javac命令文件，但是只能在JDK,中的bin目录下，进入到该目录，才可以用javac命令，否则用不了。没有指定path路径，而直接在别处搜索，都会出现这样的的问题

- javac是一个工具，一个命令，也是一个版本号，查询javac版本号方式，输入：javac -version 回车即可

- 解决javac在任意位置不能用的问题；
  在环境变量中去设置path里面的bin目录，把bin目录下的路径放到环境变量中，便可以去使用bin下的javac了
  path环境变量是专门给windows系统指路的。
  
- 系统变量；是针对全电脑都能找到改命令，而个人用户环境变量，只能针对改用户

- 环境变量中，path，会有多个路径，路径与路径之间，用因为转态下的分号分开，
```

```markdown
windows操作系统是如何搜索硬盘上某个命令的呢？
- 首先会从当前目录下搜索
- 当前目录搜索不到的话，会从环境变量path指定的路径去搜索某个命令
- 如果搜索不到就会报错
例如：当javac在把bin目录放到DOS窗口中，在去执行javac命令，不会出错，因为当前目录是能找到javac的，但是直接在C:\Users\28929> 搜索javac，就会报错，因为当前目录是:\Users\28929，没有改行营的bin目录，这是剧照path指定的路径，因为没有在path环境变量去配置改bin目录，所以还是找不到，依然报错。当在path环境变量设置了bin目录，这是就能直接用javac命令了
```



### 9、开启第一个java程序

1、保证计算机中安装EditPlus

2、安装JDK,一般从官网上下载即可

3、建立一个文件HelloWorld.java,在对此文件用EditPlus打开

4、在编译器输入

```c
public class HelloWorld{
    public static void main(String[] args){
        System.out.println("Hello World!");
    }
}
```

5、在DOS中输入javac 把该文件的绝对路径放过来回车，当看到生成.class时，说明编译成功

6、在把路径切换到HelloWorld.java之前，回车，在我输入dir确定有这样的文件，在按java helloWorld,回车即可输出

### 10、classpath

> ==在那个位置去搜索xxx.class字节码文件呢==实在classpath环境变量数据java语言的环境变量，不属于windows系统环境变量，path属于windowns系统的环境变量

```c
配置好classpath环境变量后，就可以直接运行class字节码文件了
classpath=. ，那个点代表从当前路径下去搜索class字节码文件，可以加;去从其他路径找class文件
```



### 11、注释

```markdown
1、单行注释
//

2、多行注释
/*

*/

3、javadoc注释
/**
* javacdoc注释
* javacdoc注释
* javacdoc注释
* javacdoc注释
* javacdoc注释
*/

注意；该注释是比较专业的注释，该注释会被javadoc.exe工具解析，并生成帮助文档
```

### 12、HelloWorld程序解释

```java
//public 表示公开的
//class 表示一个类
//HelloWorld 表示一个类名

public class HelloWorld{ //定义一个公开的类，起名HelloWorld
/*
    public 表示公开的
    static 表示静态的
    void 表示空
    main 表示方法名时main
    (String[] args) 是一个main方法的形式参数列表
*/ 
    //下面是类体,类体中不允许直接编写java语句，除声明变量之外
    public static void main(String[] args){ //表示一个公开的静态的主方法，是程序的入口
        //方法体
        System.out.println("Hello World!");
        //在输入
        System.out.println("我是一名程序员");
    }
}
```

```markdown
//总结，需要记忆的
* public
* class
* static
* void
* System.out.println();//向控制台输出消息
* 类体
* 方法体
* 类体中不允许直接编写java语句，除声明变量之外
* 方法体种可以编写多条java语句
* 一个java语句必须以‘;’ 结尾
```

### 13、public class 和 class的区别

```markdown
1、一个java源文件当中可以定义多个class类
2、一个java源文件当中public的class不是必须的
3、一个java源文件中定义几个class,就会有几个xxx.class字节码文件
4、一个java源文件当中定义公开类的话，只能有一个，该类名称必须和java源文件名称一致
5、每一个class当中都可以编写main方法，都可以设定程序的入口，想执行B.class中的main方法：java B, 想执行X.class中的main方法：java X;
6、注意点：在命令窗口中执行 java Hello,那么必须要求Hello.class必须有主方法（main）,否则会报错
```

基本框架

```java
public class HelloWorld{ //HelloWorld是一个类名，可以修改，但是必须跟文件名一致
    //main是一个方法名，不可以改
    public static void main(String[], args){//args是一个变量名，可以改
        
    }
    
}
```

自定义环境变量

```java
//在环境变量中，系统路径中的path 把jdk的bin目录复制进去（仅仅只是可以编译，不可运行）
//打开的DOS窗口再 设置set classpath=bin的目录（临时的）-这样就可以运行了
//若要永久性的，把路径弄进去就可以了
```





## 第二章 标识符

### 1、标识符

1、定义

```c
1、在源文件中，可以自己命令的都是标识符
2、标识符在EditPlus中，已黑色高亮显示
3、标识符可以表示什么？
    类名
    方法名
    变量名
    接口名
    常量名……
```

2、命名规则

```c
1、有数字，字母，下划线，美元符号$,组成，
2、但开头不能有数字
3、严格区分大小写
4、关键字不能做标识符
```

3、命名规范

```markdown
1、最好见名知意

2、遵循驼峰命名方式，即每个单词之间首字母大写，可以知道由几个单词组成，例如：SystemService,UserService

3、类名、接口名：首字母大写，后面的每个单词首字母大写

4、变量名、方法名：首字母小写，后面的每个单词首字母大写

5、常量名：全部大写
```

### 2、字面值

```mardkown
关于字面值，在c语言叫常量，但是在java中常量有其他的意思。常见的字面值种类
- 10、100
- 3.14
- “abc"
- 'a'
- true、false
字面值就是数据

```

### 3、关键字总结

```markdown
访问控制  private protected public
类/修饰符 abstact class extends final implements interface native
         new static strictfp synchronized trunsient volatile
         
         
程序控制 break continue return case defalut

错误处理 try catch throw throws finally
包 import package
基本类型：boolean byte char double float int short 
         null true false
         
变量引用super this void 

保存字 goto const
  

```



### 4、数据类型

```markdown
数据类型  占用字节数 取值范围           缺省默认值
byte         1     -128 - 127          0
short        2     -2^15 - 2^15 - 1    0
int          4     -2^31 - 2^31 - 1    0
long         8                         0L
float        4                         0.0f
double       8                         0.0
boolean      1     ture false          false
char         2    (0 ~ 65535)        '\u0000'
                   0-2^16-1
long 建议用大写L,小写的l和1分不清

switch语句中的条件表达式的数据类型只能是
  char、int 、short、byte类型，其他的都不行会报错。
  
```

```markdown
整数型数据类型（共四种byte short int long）他们的字节为1、2、4、8
1字节 = 8个二进制位
1byte = 8bit

进制的写法 十进制： + 10
          八进制   + 010
          十六进制 0x10
          二进制   0b10
```

```java
//long数据类型应当注意的是

public class Test{
    public static void main(String[] args){
        //编译器会报错，因为再java中数据类型字面值一上来就会被看成int类型
        //而2147483648已经超出了int范围，所以再没赋值之前就出错了
        //不是e放不下2147483648，e时long类型，完全可以容纳2147483648，只不过2147483648本身超出了int类型范围
        //一次再处理比较大的数据时，一定要加后缀符号
        //long e = 2147483648;
        long e = 2147483648L; //只要让2147483648不看成int类型就行
        System.out.println(e);
    }
}

//byte 、char 、short在坐混合运算的时候
/*
结论：byte 、char 、short在坐混合运算的时候，各自先转换成int在坐运算
*/
public class IntTest{
    public static void main(String[] args){
        char c1 = 'a';
        byte b = 1;
        System.out.println(c1 + b);
        
        //错误，不兼容的类型：从int转换成short可能会丢损失
        //short s = c1 + b;//编译器不知道这个加法最后的结果是多少，只知道是int类型。
        
        //这样修改也不行
        //错误，不兼容的类型：从int转换成short可能会丢损失
        //short s = (short)c1 + b;//b是int类型
        
        short s = short(c1 + b); //没毛病
        
        int a = 1;
        //short = 1;可以，但是short = a;不行
        //short x = a;//高数据类型不能不强制类型转换就变为底数据
        short x = 1;
        System.out.println(x);
        
    }
}

//多种数据类型做混合运算的时候
/*
   结论：多种数据类型在混合运算的时候，最终的结类型是“最大容量”对应的类型
   char + short + byte 除外
*/
public class IntTest{
    public static void main(String[] args){
        long a = l0L;
        char c = 'a';
        short s = 100;
        int i = 30;
        System.out.println(a + c + s + i);
        
        //int x = a + c + s + i;//错误，int不是最大的数据类型在这四个变量中
        int x = (int)(a + c + s + i);
        System.out.println(x);
    }
}
//布尔类型

/*
   1、在java语言中boolean类型只有两个值（true/false），没有其他值
   不想c/c++ 0/1也可以表示布尔类型
   2、用于充当条件

*/
```

### 5、猜数字小游戏

```java
import java.util.Random;
import java.util.Scanner;

public class GuessNumber {
    public static void main(String[] args) {
        //通过Random类中的nextInt方法生成一个0-9的随机数
        int randomNumber = new Random().nextInt(10);
        System.out.println("随机数已经生成");
        //2猜数子
        System.out.println("---请输入你要猜的数字----");
        Scanner s = new Scanner(System.in);
        int number = s.nextInt();//输入数字
        while(number != randomNumber){
            if(number > randomNumber){
                System.out.println("对不起，您猜大了，");
            }else if(number < randomNumber){
                System.out.println("对不起，您猜小了");
            }
            System.out.println("请你重新猜");
            number = s.nextInt();
        }
        System.out.println("恭喜你，你猜对了");
    }
}
```







## 第三章 方法

### 1.方法

```mardkown
方法定义：
- 使某个功能代码只需要写一遍
- 要使用这个功能，只需要给这个功能传入具体的数据
- 这个功能完成之后返回一个最终结果
- 代码可以重复利用了，提高代码的复用性
在使用这个方法，我们称之为调用/invoke
```

```markdown
方法的本质是：
- 方法就是一段代码片段，并且该片段可以完成某个特定的功能，并且可以重复使用
- 英文单词Method, 在c语言叫做函数
- 方法只能定义在类体当中，方法体之外
- 一个类当中可以定义多个方法，方法的编写位置没有先后顺序，可以随意
- 方法体当中，不可以在定义方法
```

```c
关于java语言中的方法：
    1、方法定义形式，语法结构
       [修饰符列表] 返回值类型 方法名（形式参数列表）{
             方法体；
       }
    2、对以上结构进行解释；
        2.1、关于修饰符列表
             * 可选项，不是必须的
             * 目前统一写成public static
             * 方法种有static 关键字的时候，怎么调用
             类名.方法名（实际参数列表）- 具体含义：类名的方法名
        2.2、方法名：
             * 首字母小写，后面的每个单词首字母大写
             * 见名知意
        2.3、方法调用
             * 方法定义后，不去调用时不会执行的，只有调用后才会去执行
```

实列

```java
//公开的定义了一个类，该类的类名为MethodTest2（且与文件名要一致）
public class MethodTest2
{
	//类体
	//类体中不可直接编写java语句，除了声明变量外
	//方法体应当出现在类体中

	//方法
    //公开的， 静态的 ， 返回类型为空的， 方法名（该方法为主方法）时程序的入口（sun公司规定的）
	//(String[] args): 形式参数列表，其中String[]是一种引用数据类型，args是一个局部变量的变量名
	//所以只有args这个局部变量的变量名是随意的
	public static void main (String[] args){
		//这里的程序一定会执行的，main方法是有JVM负责调用的，是一个入口位置
		//从这里作为起点开始执行程序
		//在这里编写调用java语句（该语句自顶向下，有顺序）
		//调用MethodTest2方法的sumInt方法，传递两个实参
		MethodTest2.sumInt(9302,92002);

		MethodTest2.sumInt(2839,2823); //一个方法可以重复使用，重复被调用

		MethodTest2.sumInt(820,9202);

		MethodTest2.sumInt(82,92);
	}
    
    //自定义方法，不是程序的入口
	//方法作用：计算两个int类型的数据的和，不要求返回结果，但是要求结果直接输出到控制台
	//修饰符列表
	//方法名
	//形式参数列表（int x, int y）
	//方法体：主要任务是求和之后输出结果
	public static void sumInt(int x, int y){
		int a = x + y;
		System.out.println(x + "+" + y + "=" + a);
	}
}
```

参数类型(注意问题)

```java
public class MethodTest3
{
	public static void main(String[] args){
		int a = 0, b = 0;

		double c = 0, d = 8;
		float e = 9, f = 7;
        //MethodTest3.sum(c, d); //错误，会报错，因为double到float没有强制类型转化（会出现编译错误）

		MethodTest3.sum(e,f); //正确
        MethodTest3.sum(34.3f, 32.2f); //整形数据默认为是double类型，所以一定要加后缀
        
        MethodTest3.sumLong(92L, 93L); //末尾任为是ing形变量
	}
    //传参数要注意，会后强制类型转换，小的会自动变成大的（如过你传入的数据不与形参类型形同的话）
	//float - > double,所以再
	public static void sum(float x, float y){
		float c = x + y;
		System.out.println(x + "+" + y + "=" + c);
	}
    
    public static void sumLong(long a, long b){
        long c = a + b;
        System.out.println(a + "+" + b + "=" + c);
    }
}
```

### 2、方法的内存机制

> 方法再执行的过程中，在JVM中的内存是如何分配的，内存是如何变化的？（JVM是java虚拟机）1、方法只定义，不调用，是不会执行的，并且在JVM中也不会分配“运行所属”的内存空间
>
> 2、在JVM中内存的划分有这样三块的内存空间：
>
> * 方法区内存
> * 堆内存
> * 栈内存
>
> 3、方法代码片段存在哪里？方法执行的时候执行过程在哪里分配？
>
> 方法代码片段属于.class字节码文件的一部分，字节码文件在类加载的时候，将其方法区当中，所以JVM中的三块主要的内存空间中，方法区内存最先有数据，存放了代码片段
>
> 代码片段虽然在方法区内存中，只有一份，但是可以重复被调用，每一次调用这个方法的时候，需要给该方法分配独立的活动场所，在栈内存中分配。【占内存中分配方法运行的所属内存空间】
>
> 4、方法在调用的瞬间，会给该该方法分配内存空间，会在栈中发生压栈动作，方法执行结束后，会给方法分配的内存空间全部释放，此时会发生弹栈动作。
>
> 5、局部变量在“方法体”中声明，局部变量在运行阶段内存在栈中分配

```java
注意：在EditPlus当中，字体颜色为红色时，表示一个类的名字，并且该类是javaSE类库自带的
//我们自定义的类，字体是黑色的，是标识符
在JavaSE类库中自带的类，例如：String.class、System.class,这些类也是标识符，只要是类名就一定是标识符
```





### 3、==方法的重载机制==

```java
//缺点程序（没使用重载机制）
//缺点：sumInt, sumLong, sumDounle方法虽然功能不同，但是功能相似，都是求和。
//以下程序当中功能相似的方法，分别起了三个不同的名字，对于程序员来说，调用的时候不方便，需要记忆更多的函数，才能完成调用
//并且代码不美观

public class OverloadTest1
{
	//入口
	public static void main(String[] args){
		//调用
		int change = sumInt(89, 76); //调用方式一
		System.out.println(change);

		double change1 = sumDouble(89.2, 90.4);
		System.out.println(change1);

		long change2 = sumLong(89L, 8983L);
		System.out.println(change2);

	}

	//对两个整形数据求和
	public static int sumInt(int a, int b){
		int c = 0;
		c = a + b;
		return c;
	}

	//传两个双精度数据
	public static double sumDouble(double a, double b){
		double c = 0.0;
		c = a + b;
		return c;
	}

	//传两个长整型数据
	public static long sumLong(long a, long b){
		long c = 0;
		c = a + b;
		return c;
	}
}
```

> 方法的重载：功能虽然不同，但是“功能相似”的时候，程序员在使用这些方法的时候，就像在使用同一种方法一样，这种机制叫Overload
>
> 主要是，方法名一样，但是参数不一样，通过传参的不同，来确定是用的是哪一种功能的方法。

```c
//缺点：sumInt, sumLong, sumDounle方法虽然功能不同，但是功能相似，都是求和。
//以下程序当中功能相似的方法，分别起了三个不同的名字，对于程序员来说，调用的时候不方便，需要记忆更多的函数，才能完成调用
//并且代码不美观

public class OverloadTest1
{
	//入口
	public static void main(String[] args){
		//调用（重载）
		int change = sum(89, 76); //调
		System.out.println(change);

		double change1 = sum(89.2, 90.4); //默认的是double类型的数据
		System.out.println(change1);

		long change2 = sum(89L, 8983L); //默认的不加后缀的是int类型的变量
		System.out.println(change2);

	}

	//对两个整形数据求和
	public static int sum(int a, int b){
		int c = 0;
		c = a + b;
		return c;
	}

	//传两个双精度数据
	public static double sum(double a, double b){
		double c = 0.0;
		c = a + b;
		return c;
	}

	//传两个长整型数据
	public static long sum(long a, long b){
		long c = 0;
		c = a + b;
		return c;
	}
}
```

```java
/*
   方法重载：
     1、方法重载又被称为：overload
	 2、什么时候考虑使用方法重载？
	    * 功能相似的时候，尽可能地方法名相同
		【但是：功能不同/不相似的时候，尽可能地让方法名不同】

	 3、什么条件满足之后构成了方法重载
	    *在同一类当中
		*方法名相同
		*参数列表不同
		  — 数量不同
		  - 顺序不同(数据类型，类型相同的就不行，否则会发生类型的重复)
		  - 类型不同
	 4、方法重载和什么有关系，和什么没关系？
         * 方法重载和方法名 + 参数列表有关系
		 * 方法重载和 返回值类型 无关
		 * 方法重载和 修饰符列表无关




*/
public class OverloadTest1
{
	//入口
	public static void main(String[] args){
		//调用（重载）
		m1();
		m1(1);

		m2(1,2.0);
		m2(2.0,1);

		m3(4);
		m3(4.0);

	}
	//以下两个方法构成重载
	public static void m1(){}
    public static void m1(int a){}

	////以下两个方法构成重载
	public static void m2(int a, double b){}
	public static void m2(double b, int a){}

	//以下两个方法构成重载
	public static void m3(int x){}
	public static void m3(double x){}

	/*
	以下不构成方法的重载，发生了方法的重复
	public static void m4(int a, int b){}
	public static void m4(int b, int a){}
	*/

	/*方法重载和返回值了类型无关
	public static void m5(int b){}
	public static int m5(int c){}
	*/

	/*方法重载和修饰符列表无关
	public static void m6(){}
	void m6(){}
	*/
}
```

应用实例

```java
//方法重载的应用实例
public class Overload
{
	//入口
	public static void main(String[] args){
		工具.m("我是一名程序员");
		工具.m(89);
		工具.m(893.2);
		工具.m(9893.2f);
		工具.m(true);
		工具.m(89293L);
	}
	
}

//自定义类（该类会生成字节码文件.class，任何java程序都可以调用它）
//前提是必须有该字节码文件，这样就算没有在源程序中定义类，也可以调用它(把其装入u盘即可),这样以来，
//把该类在主方法中调用的时候，只需要有这个字节码文件即可，不需要重新定义了
//每一个类都会生成后缀名为.java文件，并且会有.class的字节码文件
class 工具 //可以是public class 工具(类名，可以是中文)
{
	//重载类
	public static void m(byte b){
		System.out.println(b);
	}

	public static void m(short b){
		System.out.println(b);
	}

	public static void m(long b){
		System.out.println(b);
	}

	public static void m(float b){
		System.out.println(b);
	}

	public static void m(double b){
		System.out.println(b);
	}

	public static void m(boolean b){
		System.out.println(b);
        //传入的参数只能是true和false,这是与c语言不同的地方
	}

	public static void m(char b){
		System.out.println(b);
	}

	public static void m(String b){
		System.out.println(b);
	} 
    
}
```



## 第四章 面向对象(上)

### 1、特征

- 封装
- 继承
- 多态

> 采用面向对象的方式开发一个软件，生命周期当中：
>
> * 采用面向对象的分析：OOA
> * 采用面向对象的设计：OOD
> * 采用面向对象的编程：OOP

2、类与对象的概念

```java
1、什么是类？
    - 类在显示世界中是不存在的，是一个模板，是一个概念，是一个人类大脑思考的结果
    - 类代表一类事物，
    - 在现实世界中，对象A和对象B之间的共同的特征，进行抽象，总结出来的一个模板，这个模板被称为类
2、什么是对象？
    - 对象是实际存在的个体，现实世界中实际存在
    
3、描述一个软件开发的过程：
    * 程序员先观察这个世界，从现实生活中寻找对象
    * 寻找了N多个对象之后，发现所有对象的共同特种
    * 程序员在大脑中形成了一个模板【类】
    * java程序员可以通过java代码来表述一个类
    * java程序员中有了类的定义
    * 然后通过类就可以创建对象
    *有了对象之后，可以让对象直接协作起来形成一个系统
4、类到对象的过程：称之为  实例化
   * 类又叫做 实例/instance
   * 对象 -> 类的过程叫做：（抽象）
5、重点：
    类描述的是对象的共同特征。
    共同特征：身高特征
    这个身高特征在访问的时候，必须先创建对象，通过对象去访问特征
6、一个类主要描述什么信息呢？
    一个类主要描述的是 状态 + 动作
    状态信息：名字，身高，性别、年龄
    动作信息：吃、唱歌、跳舞、学习
    
    状态-> 一个类的属性
    动作-> 一个类的方法
    类{
       属性;//描述对象的状态信息
       方法;//描述对象的动作信息
}

7、类的定义
    语法结构;
    [修饰符列表] class 类名{
        属性;
        方法;
    }
    学生类，描述所有对象的共同特征；
        学生对象有哪些状态信息;
         * 学号【int】
         * 名字【string】
         * 性别【boolean】
         ……
        学生对象有哪些动作信息
          * 吃饭
          * 睡觉
          * 完
          ……
    重点：属性通常是通过采用变量的方式来定义【描述对象的状态信息】
//定义一个类，类名为Student(学生类，属于引用类型)
//Student 是一类，代表所有学生对象，是一个学生模板
public class Student{ //公开的类，起名为Student
    //属性
    //属性通常采用变量的方式定义
    //在类体中，方法体之外定义的变量叫：成员变量
    //成员变量没有赋值，系统赋默认值，一切向0看齐
    //学号
    String no;
    //姓名
    String name; //引用这些成员变量得创建对象。
    //性别
    boolean sex;
    //年龄
    int age;
    
    //方法，描述对象动作信息
}

8、- 基本数据类型
    byte
    short
    int 
    long 
    float
    double
    boolean
    char
    
    _ 引用数据类型
    String.class//sun公司提供
    System.class
    Student.class //自定义
    User.class//自定义
    Product.class//自定义
    Customer.class//自定义
    
    * 所有定义的class都属于引用类型（不属于基本数据类型）
```

### 2、对象的创建

```java
//java类
//学生类是一个模板
//描述了所有学生的共同特征【状态 + 行为】
public class Student{
    //类体 = 属性 + 方法
    //属性【存储数据采用的变量形式】
    //由于变量定义在类体当中，方法体之外，这种变量成为成员变量
    //所有的学生信息都有学号信息，但是每个学生的学号是不同的
    //所以要访问这个学号，必须先去创建对象，通过对象去访问学号信息
    //学号信息不能直接通过类去访问，所以这种成员变量又叫做实例变量
    //对象又被称为实例，实例变量又被称为对象变量【对象级别的变量】
    //不创建1对象，这个no变量的内存空间是不存在的，只有创建了对象，这个no变量内存才会创建
    int no;
    //姓名
    String name;
    //年龄
    int age;
    boolean sex;
    //住址
    String addr;
}
/*成员变量没有手动赋值的话，系统会赋默认值
默认值
数据类型              默认值
--------------------------
byte short int long    0
float double           0,0
boolean                false
char                   \u0000
引用数据类型            null
*/
```

>  ==对象的创建和使用==

```java
public class OOTest01{
    public static void main(String[] args){
        //int 是基本数据类型
        //i是一个变量名
        //10是一个int类型的字面值
        int i = 10;
        //通过一个类可以实例化N个对象
        //实例化对象的语法：new 类名（);
        //new是java语言中一个运算符，new运算符的作用是创建对象，在JVM堆内存当中开辟新的内存空间
        //方法区内存：在类加载的时候，class字节码片段被加载到该内存空间中。
        //栈内存（局部变量）;方法代码片段执行的时候，会给该方法分配内存空间，在栈内存中压栈
        //堆内存：new的对象在堆内存中存储
        //Student 是一个引用数据类型
        //s是一个变量名
        //new Student()是一个学生对象
        //s是局部变量，在栈内存中存储，（s被称为引用，而不是对象）
        //什么是对象？new运算符在堆内存开辟的内存空间成称为对象
       //什么叫引用？引用是一个变量，只不过这个变量保存了一个java中内存地址
        //java语言当中，程序员只能通过‘引用’去访问堆内存当中对象内部的实例变量
        Student s = new Student();//如果在类中没有定义Student的话，那Student字节码文件必须存在
        //访问实例变量的语法格式
        //读取数据；引用.变量名
        //修改数据；引用.变量名 = 值
        int stuNum = s.no;
        int stuAge = s.age;
        String name = s.name;
        boolean stuSex = s.sex;
        String stuAddr = s.addr;
        //访问方式一
        System.out.println("访问方式一:");
        System.out.println("学号 = " + stuNum);
        System.out.println("年龄 = " + stuAge);
        System.out.println("姓名 = " + name);
        System.out.println("性别 = " + stuSex);
        System.out.println("住址 = " + stuAddr);
        //访问方式二
        System.out.println("访问方式二:");
        System.out.println("学号 = " + s.no);
        System.out.println("年龄 = " + s.age);
        System.out.println("性别 = " + s.sex );
        System.out.println("姓名 = " + s.name);
        System.out.println("住址 = " + s.addr);
        //修改对象
        s.no = 89;
        s.age = 21;
        s.name = "孔德华";
        s.sex = true;
        s.addr = "河北省武安市马家庄乡神南峪村96号";
        System.out.println("修改后的对象:");
        System.out.println("学号 = " + s.no);
        System.out.println("年龄 = " + s.age);
        System.out.println("性别 = " + s.sex );
        System.out.println("姓名 = " + s.name);
        System.out.println("住址 = " + s.addr);
        
        //再通过实例化一个全新的对像
        //stu是一个引用，stu同时是一个局部变量，student是变量的数据类型
        Student stu = new Student();
        System.out.println("新增对象:");
        System.out.println("学号 = " + stu.no);
        System.out.println("年龄 = " + stu.age);
        System.out.println("性别 = " + stu.sex );
        System.out.println("姓名 = " + stu.name);
        System.out.println("住址 = " + stu.addr);
        
        //System.out.println(Student.no);
        //编译报错，no这个实例变量不能直接‘类名’的方法访问，因为通过no是实例变量，对象级别的变量，变量存储在java对象的内部，必须现有对象
        //通过对象才能访问no这个实例变量，不能够直接通过类名访问
    }
}
/*局部变量在栈内存中存储，成员变量中的实例变量在堆内存中的java对象内部存储
实例变量是一个对象一份，100个对象有100份。
*/
```

以上的在JVM程序执行图的内存表示

![image-20210404172706103](java%E5%AD%A6%E4%B9%A0.assets/image-20210404172706103.png)

> ==示例二==

```java
//用户类
public class User{
    //属性[以下都是成员变量之实例变量]
    //用户编号，no是一个实例变量
    int no;
    //用户名
    //String 是一个引用数据类型，代表字符串
    //name是一个实例变量，name是一个引用
    String name;
    //家庭住址
    //Address是一个引用数据类型，代表家庭住址
    //addr是一个实例变量，同时也是一个引用
    Address addr;
}
//引用可以是局部变量也可以是成员变量
public class Address{
    //属性【成员变量值实例变量】
    //城市，String 是一个引用，保存内存地址一个变量，该变量保存内存地址指向了堆内存当中的的对象
    String city;
    //街道
    String street;
    //邮编
    String zipcode;
}

public class OOTest02{
    public static void main(String[] args){
        //创建User对象
        //u是一个局部变量，是一个引用
        User u = new User();
        System.out.println(u.no);
        System.out.println(u.neme);
        System.out.println(u.addr);
        //修改User对象内部的实例变量的值
        u.no = 389;
        u.name = "jake";//jake是一个对象，类型为String对象
        u.addr = new Address();
        u.addr.city = "武安市";
        u.addr.street = "神南峪村";
        u.addr.zipcode = "9919393";
        System.out.println(u.name + "居住的城市为 " + u.addr.city);
        System.out.println(u.name + "所在村落 " + u.addr.street);
        System.out.println(u.name + "家庭邮编 " + u.addr.zipcode);
    }
}
```

![image-20210404181054401](java%E5%AD%A6%E4%B9%A0.assets/image-20210404181054401.png)



> ==示例三==

```java
public class OOTest03{
    public static void main(String[] args){
        User u = new User();
        //上一个版本是
        //u,addr = new Address();
        
        //a是一个引用，局部变量
        Address a = new Address();
        u.addr = a;
        System.out.println(u.addr.city);
        a.city = "天津";
        System.out.println(u.addr.city);
    }
}
```

![image-20210404182622378](java%E5%AD%A6%E4%B9%A0.assets/image-20210404182622378.png)

> ==实例4==

```java
//丈夫类
class Husband{
    //姓名
    String name;
    //丈夫对象中含有妻子引用
    Wife w;
}
//妻子类
class Wife{
    //姓名
    String name;
    //妻子对象中含有丈夫引用
    Husband h;
}
//测试程序
public class OOTest04{
    public static void main(String[] args){
        //创建一个丈夫对象
        Husband kongdehua = new Husband();
        kongdehua.name = "孔德华";
        //创建一个妻子对象
        Wife lijing = new Wife();
        lijing.name = "李菁";
        //结婚【通过妻子能找到丈夫，通过丈夫能找到妻子】
        kongdehua.w = lijing;
        lijing.h = kongdehua;
        //输出关系
        System.out.println("孔德华的妻子是 " + kongdehua.w.name);
        System.out.println("李菁的丈夫是 " +  lijing.h.name);
    }
}
```

![image-20210404205719391](java%E5%AD%A6%E4%B9%A0.assets/image-20210404205719391.png)

==JVM==

```markdown
1、JVM（java虚拟机）主要包括三块内存空间，分别是：占内存，堆内存，方法区
2、堆内存和方法区内存各有一个：一个线程一个栈内存
3、方法调用的时候，该方法所需要的内存空间在栈内存中分配，成为压栈。方法执行结束之后，该方法所属的内存空间释放，成为弹栈
4、栈中主要存储的是方法体当中的局部变量。
5、方法的代码片段以及整个类的代码片段都被存储到方法区内存当中，在类加载的时候这些代码片段会载入。
6、在程序执行的过程中使用new运算符创建java对象，存储在堆内存当中，对象内部有实例变量，所以实例变量存储在堆内存当中
7、变量的分类
   — 局部变量【方法体中声明】
   — 成员变量【方法体外声明】
     * 实例变量【前面没有修饰符static】
     * 静态变量【前面修饰符中有static】

8、静态变量存储在方法区内存当中
9、三块内存当中变化最频繁的是栈内存，最先有数据的是方法区内存，垃圾回收器主要针对的是堆内存
10、垃圾回收器【自动垃圾回收机制、GC机制】什么时候会考虑将该某个java对象的内存回收呢？
   * 当堆内存当中的java对象成为垃圾数据的时候，会被垃圾回首器回收。
   * 什么时候堆内存中的java对象会变成垃圾？
     这个对象无法被访问，因为访问对象只能通过引用方式方式访问
     没有更多的引用指向它的时候。
```

> ==实例五; 空指针异常==

```java
class Customer{
    int id;
}
public class OOTest05{
    public static void main(String[] args)
    {
        Customer c = new Customer();
        System.out.println(c.id);
        
        //以下程序编译可以通过，因为符合语法
        //运行出现空指针异常
        //空引用访问‘实例’相关的数据一定会出现空指针异常
        //java.lang.NullPointerException
        c = null;
        System.out.println(c.id);
    }
}
/*
“实例相关的数据”表示：这个数据访问的时候必须有对象的参与，这种数据就是实例相关的数据。
*/
```

![image-20210404212816576](java%E5%AD%A6%E4%B9%A0.assets/image-20210404212816576.png)



> ==实例六：内存分析==

```java
/*
  需求：
     定义一个计算机类【电脑/笔记本】
       * 颜色
       * 型号
       * 品牌
     定义一个学生类，学生类有属性
       * 学号
       * 姓名
       * 学生有一台笔记本电脑
     编写一个程序来表示以上的类，然后分别将类创建为对象，对象的数量不限，然后让其中的一个学生去使用其中的一台笔记本电脑
*/
//计算机类
class Computer
{
    String brand;
    String style;
    String color;
}
//学生类
class Student
{
    int no;
    String name;
    Computer notepad;
}

//测试类
public class OOTest06
{
    public static void main(String[] args){
        //创建笔记本对象
        Computer bijiben = new Computer();
        bijiben.brand = "联想";
        bijiben.style = "拯救者";
        bijiben.color = "黑色";
        //创建学生对象
        Student zhangsan = new Student();
        zhangsan.no = 9300283;
        zhangsan.name = "张三";
        zhangsan.notepad = bijiben;
        
        System.out.println("输出信息如下");
        System.out.println("学生姓名 " + zhangsan.name);
        System.out.println("学生学号 " + zhangsan.no);
        System.out.println("学生使用电脑类型 " + zhangsan.notepad.style);
        System.out.println("学生使用电脑品牌 " + zhangsan.notepad.brand);
        System.out.println("学生使用电脑颜色 " + zhangsan.notepad.color);
    }
}
```

### 3、eclipse的使用

```markdown
* workspace: 工作区
  ——当myeclipse打开的时候，大多数会提示选则工作区
  ——这个工作区可以是已经存在的工作区，也可以是新建的工作区
  ——选则工作区后，将来编写的java代码，自动编译的class文件都会在工作区中找到
  
* 创建一个项目，所有程序是基于项目编写的
- 选则java project, 如果不是，则在other里找到java project
* 写入工程名称，finish即可
* 在包资源管理器中，工程项目下的src（所有的编写的程序都会在此下面）
* 对src 右击 -> new -> Package(新建一个包)
* 包名默认的写法；cn.itcase.工程名
* 对新建好的包名右击 -> new -> class
* 编写类名即可
* 编写好之后，可以通过上方的编译按钮来显示结果
* 如果要显示行号的话，对显示行号的滑轮列 -> 右击 -> show Line Numbers

java中，包是专门存放类的，相同功能的类存放到相同的包中

—— 一个项目中可能会使用很多包，当一个包中类需要调用另一个包中的类时，要使用import关键字引入需要的类，使用方法如下
   import 包名.类名;
   通常import出现在package语句之后，类定义之前
   import 包名.* 导入改包下的所有类
```

### 4、面向对象的封装性

```java
class User{
    int age;
    
}
/*
对于当前程序来说：
User类中的age属性在外部程序中可以随意访问，导致age属性的不安全。
一个User对象表示一个用户，用户的年龄不能为负数，以下程序年龄为负数，程序运行时并没有报错，这是当前程序存在的缺陷，所以要封装

封装的好处；
    1、封装之后，对于那个事物，看不到事务复杂的一面，只能看到事物简单的一面
    
    2、封装之后才会形成真正的‘对象’，真正的‘独立体’
    3、封装就意味着以后的程序可以重复使用，并且这个事物应该是应性比较强，在任何场合下都可以使用
    4、封装后，对于事物的本身，提高了安全性
    

*/
public class UserTest{
    
    public static void main(String[] args){
        //创建User对象
        User user = new User();
        //访问age
        
        System.out.println("该用户的年龄是 ；" + user.age);
        
        //修改年龄
        //此方法不合适，因为不安全
        user.age = 20;
        System.out.println("该用户的年龄是 ；" + user.age);
        
        //修改年龄
        user.age = -100;
        System.out.println("该用户的年龄是 ；" + user.age);
   } 
}
```

修改后的

```java
/*
封装的步骤
  1、将所有的属性私有化，使用private关键字进行修饰，private表示私有的，所有数据只能在本类中访问
  
  2、对外提供的简单操作入口，也就是以后外部程序想要访问get属性，必须通过这些简单的入口进行访问
    - 对外提供两个公开的方法，分别是set方法和get方法
    - 想要修改age属性，调用get方法
    - 想要读取age属性，调用set方法
  3、set方法命名规则；
    public void set+属性名首字母大写(形参){
        //因为是修改，所以无返回类型
    }
    
  4、get方法命名规范
    public int(返回值类型) get+属性名首字母大写（形参）{
       return int(返回值类型);//因为要读取放到其他类当中，所以要有返回值类型
    }
  5、一个属性对应两个（读取和修改方法）


****************************************
- setter 和getter方法没有static关键字
- 有static关键字的方法调用方式；类名.方法名（实参）
- 没有static关键字的方法怎么调用，引用.方法名(实参)
*/

public class User{
    //属性私有化
    private int age;
    //set,修改
    public void setAge(int a){
        //编写业务逻辑代码进行安全控制
        if(a < 0 || a > 150){
            System.out.println("年龄是不合法的");
        }
        else {
          age = a;
        }
        return ;
    }
    
    //getter
    public int getAge(){
        return age;
    }
}

public class UserTest{
    public static void main(String[] args){
        User user = new User();
        //以下就会报错，因为age属性彻底在外部访问不到了
        //System.out.println(user.age);
        
        //修改
        user.setAge(-100);
        //读取
        System.out.println("用户年龄 " + user.getAge());
    }
}
```

### ==5、构造方法==

```java
/*
关于java类中的构造方法：
    1、构造方法又被称为构造函数/构造器/Constructor
    2、构造方法语法结构;
       [修饰符列表]构造方法名（形式参数列表）{
           构造方法体;
       }
    3、普通方法语法结构；
       [修饰符列表] 返回值类型 方法名（形式参数列表）{
           方法体;
       }
       
    4、对于构造方法来说，’返回值类型‘不需要指定，并且也不能写void,只要写上void,那么这个方法就成为了普通方法了。
    5、对于构造方法来说，构造方法的方法名必须和类名保持一致
    
    6、构造方法的作用;
       构造方法存在的意义是，通过构造方法的调用，可以创建对象
    7、构造方法怎么调用？
       - 普通方法是这样调用的：方法修饰符中有static的时候，类名.方法名（实参列表）、方法修饰符列表中没有static的时候：引用.方法名（实参列表）
       - 构造方法的调用
         new 构造方法名（实参列表）
         
    8、构造方法调用执行后，有返回值吗？
       每一个构造方法实际上结束之后都有返回值，但是这个retrun；这样的语句不需要填写，构造方法结束时候java程序自动返回值。
       并且返回值类型是构造方法所在的类的类型，由于构造方法的返回值就是类本身，所以返回值类型不需要编写
       
    9、注释和取消注释：ctrl + /, 多行注释ctrl + shift + /
    10、当一个类中没有定义任何构造方法的话，系统会默认该该类提供一个无参的构造方法，这个构造方法被称为缺省构造器
    11、当一个类显示的将构造方法定义出来，那么系统不在默认认为这个类提供缺省构造器
    
    12、构造方法支持重载机制。在一个类当中编写多个构造方法，这多个构造方法显然已经构成方法冲重载机制
    13、当用构造方法重载机制的时候，必须定义一个无参数的构造方法，否则有参数的构造方法也是使用不了的。

*/
public class ConstructorTest01{
    public static void main(String[] args){
        //创建USer对象
        //调用User类的构造方法来完成对象的创建
        //以下四个程序创建了4个对象，只要构造函数调用就会创建对象，并且一定是在“堆内存”开辟空间的
        new User();//不可以用了，因为在User中定义了个有参数的构造方法
        User u = new User();
        User u1 = new User(9); //new后面是一个构造方法的方法名
        User u2 = new User("张三");
        
        //调用带有static的方法：类名
        ConstructorTest01.doSome();
        
        //调用没有static的方法：引用
        //doOther方法在ConstructorTest01类当中，所需要创建ConstructorTest01对象
        //创建ConstructorTest01对象，条用无参数构造方法发
        ConstructorTest01 t = new ConstructorTest01();
        t.doOther();
    }
    public static void doSome(){
        System.out.println("do some");
    }
    
    public void doOther(){
        System.out.println("do Other");
    }
}

class User{
    //一般默认的情况下系统会自动生成一个无参数且无任何类型的构造方法
    public User(){
        System.out.println("这个无参的构造方法");
    }
    //当你重新构造一个方法后，此方法会代替默认的构造方法，且默认的构造方法不能使用了
    public User(int i){
         System.out.println("这个int类型的构造方法");
    }
    public User(String name){
        System.out.println("这个String类型的构造方法");
    }
}
```

```java
/*构造方法作用
   1、创建对象
   2、创建对象的同时，初始化实例变量的内存空间
   
成员变量之间的实例变量，属于对象级别的变量，这种变量必须先有对象才有实例变量
  
  
*/
```

### 6、this关键字

```java
/*
关于java语言中的this关键字：
    1、this是一个关键字，翻译为这个
    2、this是一个引用，this是一个变量，this变量保存了内存地址指向了自身，this存储在JVM堆内存java对象内部。
    3、创建100个java对象，每一个java对象都有一个this,也就是有100个不同的this
    4、this可以出现在“实例方法”当中，this指向当前正在执行的这个动作的对象(this代表当前对象)
    5、this在多数情况下都是可以省略不写的
    6、this不能使用带有static的方法当中
*/
public class Customer{
    //姓名【推内存对象内部存储，所以访问该数据的时候，必须先创建对象，通过引用方式访问】
    String name;
    //构造方法
    public Customer(){
        
    }
    
    //不带有static关键字的一个方法
    //顾客购物行为
    //每一个顾客最终的结果是不一样的
    //所以购物这个行为属于对象级别的行为
    //由于每个一对象在执行购物这个动作的时候，最终结果不同，所以购物这个动作必须有’对象‘的参与
    //重点：没有static关键字的方法被称为‘实例方法’，实例方法怎么访问？“引用.”
    //重点：没有static关键字的变量成为“实例变量”
    //注意当一个行为/动作执行的过程当中是需要对象参与的，那么这个方法一定要定义为“实例方法”，不要带有static关键字
    //以下方法定义为实例方法，因为每一个顾客在真正购物的时候，最终结果是不同的，所以这个动作在完成的时候必须有对象的参与
    public void shopping(){
        //当张三购物时候，输出：张三在购物
        //当李四购物时候，输出李四在购物
        //System.out.println(name + "在购物");
        
        /*
        由于name是一个示例变量，所以这个name访问的时候一定访问的是当前对象name
        所以多数情况下“this”是可以省略掉的   
        */
        //完整写法
        System.out.println(this.name + "在购物");
    }
    
    //带有static
    public static void doSome(){
        //这个执行过程中没有“当前对象”，因为带有static的方法是通过类名的方式访问的
        //或者说这个“上下文”当中没有“当前对象”，自然也不存在this(this代表当前正在执行的这个动作的对象)
        //以下的这个程序为什么会出错呢》
        //doSome方法调用不死对象去调用，是一个类名区调用，执行的过程中没有“当前对象”
        //name是一个“实例变量”，以下代码的含义是：访问当前对象的name,没有当前的对象，自然也不能访问当前的对象name
        //System.out.println(name);
        //static的方法调用不需要对象，直接使用类名，所以执行的过程中没有当前对象，所以不能直接使用this
        //System.out.println(this);
    }
    
    public static void doOther(){
        //假设像访问name这个实例变量的话，因该怎么做?
        //可以采用以下方案，但是以下的方案，绝对不是访问的当前对象的name
        //创建name
        Customer c = new Customer();
        System.out.println(c.name); //这里访问的nam是c引用指向对象的name//默认为空NULL
        
    }
}

public class CustomerTest{
    public static void main(String[] args){
        Customer c1 = new Customer();
        c1.name = "zhangsan";
        c1.shopping();
        Customer c2 = new Customer();
        c2.name = "lisi";
        c2.shopping();
        //调用doSome方法（修饰符列表上有static）
        //采用“类名.”的方法访问，显然这个方法在执行的时候不需要对象的参加
        Customer.doSome();
        //调用doOther
        Customer.doOther();
    }
}
```

![image-20210406091921849](java%E5%AD%A6%E4%B9%A0.assets/image-20210406091921849.png)



实例

```java
/*
最终结论：
    在带有static的方法中不能直接访问实例变量和实例方法
    因为实例变量和实例方法都需要对象的存在
    而static的方法中是没有this的，也就是说当前对象是不存在的
    而然也是无法访问当前对象的实例变量和实例方法
    但是不带有static的方法中可以直接访问实例变量和实例方法
*/

public class ThisTest{
    int num = 10; //实例变量，访问的话是以“引用.num”
    public static void main(String[] args){
        //在static中不能使用static，那怎么访问num
        ThisTest u = new ThisTest();
        System.out.println(u.num);
        
        ThisTest.doThis();
        doThis();
        //doOther是实例方法，实例方法必须有对象的存在
        //以下代码表示含义：调用当前对象的doOther方法
        //但是由于main方法中没有this,所以不能以下方法调用
        //doOther();
        //this.doOther();//编译错误
        ThisTest u1 = new ThisTest();
        u1.doOther();
        
    }
    public static void doThis() {
    	System.out.println("doThis"); //类名.方法名
    }
    public void doOther() {
    	System.out.println("doOther");//引用.方法名
    }
}
```

实例

```c++
public class User{
    private int id; //实例变量
    private String name;
    //Setter ans getter
    //以下程序的id和实例变量id无关，不能采用这种方式
    /*
    public void setId(int id)
    {
        id = id; //id的就近原则
    }
    
    */
    //this什么时候不能省略？
    //用来区分局部变量和实例变量的时候，“this.”不能省略(只有这一种情况不能省略)
    public void SetId(int id){
        this.id = id;
    }
    
    public int GetId(){
        return id;
    }
}
```

实例

```java
/*
this可以用在哪里
    1、可以使用在实例方法种，代表当前对象【语法格式：this】
    2、可以使用在构造方法当中，通过当前的构造方法调用其他的构造方法[语法格式：this(实参);]
       
重点[记忆]: this ()这个语法只能出现在构造函数的第一行。

*/

public class Date{
    //属性
    private int year;
    private int month;
    private int day;
    
    //构造方法
    //有参
    public Date(int year, int month, int day){
        this.year = year;
        this.month = month;
        this.day = day;
    }
    //无参
    /*
    需求：当程序员调用以下无参数的构造方法是，默认的创建日期是“1970 - 1 -1”
    
    */
    public Date(){
        /*this.year = 1970;
        this.month = 1;
        this.day = 1;
        */
        //以上代码可以通过调用李刚一个构造方法来完成
        //但前提是不能直接创建新的对象，以下代码表示创建了一个全新的对象
        //new Date(1970,1,1);
        
        //需要采用以下的语法来完成构造方法的调用
        //这种方式不会创建新的java对象，但可以达到调用其他的构造方法
        this(1970,1,1);
    }
    
    //setter and getter
    public int getYear(){
        return year;
    }
    public void serYear(int year){
        this.year = year;
    }
    public int getMonth(){
        return month;
    }
    public void setMonth(int Month){
        this.month = month;
    }
    public int getDay(){
        return day;
    }
    public void setDay(int day){
        this.day = day;
    }
    
    //对外提供一个方法可以将日期打印输出到控制台
    public void print(){
        System.out.println("year = " + year + "month = " + month + "day = " + day);
    }
    
}
public class DateTest{
    public static void main(String[] args){
        //创建日期对象1
        Date time1 = new Date();
        time1.print();
        //创建日期对象2
        Date time2 = new Date(1999,4,22);
        time2.print();
    }
}
```

实例

```java
public class Test{
    //没有static的变量
    int i = 10;
    //带有static的方法
    public static void doSome(){
        System.out.println("do Some!");
    }
    //没有static的方法
    public void doOther(){
        System.out.println("do other");
    }
    //带有static的方法
    public static void methodd1(){
        //调用doSome
        //完整的调用方式
        Test.doSome();
        //省略方式的调用
        doSome(); //类名可以省略
        
        //调用doOther
        //完整的调用方式
        Test t = new Test();
        t.doOther();
        //省略方式调用不了
        
        //调用i
        //完整的方式访问
        System.out.println(t.i);
        //省略的方式访问不了
    }
    //不带有static的方法
    public void method2(){
        //调用doSome
        //完整的调用方式
        Test.doSome();
        //省略方式的调用
        doSome(); //类名可以省略
        
        //调用doOther
        //完整的调用方式
        this.doOther();
        doOther();
        //省略方式调用不了
        
        //调用i
        //完整的方式访问
        System.out.println(this.i);
        //省略的方式访问
        System.out.println(i);
    }
    public static void main(String[] args){
        //要求在这里编写程序调用method1
        //使用完整方式调用
        Test.method1();
        //省略方式调用
        method1();
        //调用method2
        //使用完整方式调用
        Test t = new Test();
        t.method2();
        //使用省略方式调用
        //调用不了
    }
    //mei
}
```

实例：

```java
/*
什么时候程序会出现空指针异常呢》
    空指针访问实例相关的数据，因为实例相关的数据就是对象相关的数据
    这些数据在访问的时候，必须有对象的参与，当空引用的时候，对象不存在，访问这些实例数据一定会
    出现空指针异常

*/
public class Test{
    public static void main(String[] args){
        Test.doSome();
        doSome();
        
        Test t = new Test();
        t.doSome();
        
        //引用是空
        t = null;
        //带有static的方法，其实可以采用类名的方式访问，也可以采用引用的方式访问
        //但是即使采用引用的方式区访问，实际上执行的时候和引用指向的对象无关
        //在eclipse中开发的时候，使用引用的方式访问带有static的方法，程序会出现警告
        //所以带有static的方法还是使用“类名.”的方法访问。
        t.doSome();//这里不会出现空指针异常
    }
}
```

### ==7、static关键字==

```jAVA
/*
带有static关键字的，都是类级别的，不带有static关键字的都是对象级别的，需要每次都给对象赋值
什么时候成员变量声明为实例变量呢？ 
    - 所有对象都有这个属性，但是这个属性的值会随着对象的变化而变化[不同的对象，这个属性的值不同]
    
什么时候成员变量声明为静态变量呢？
    - 所有的对象都有这个属性，并且所有的对象的这个属性的值是一样的，建议定义为静态变量，节省内存的开销
    
静态变量在类加载的时候初始化，内存在方法区中开辟，访问的时候不需要创建对象，直接使用”类名.静态变量名“的方法访问。

java中的static关键字：
   1、static修饰的方法为静态方法
   
   2、static修饰的变量为静态变量
   
   3、所有的static修饰的元素都称为静态的，都可以使用”类名.“方式访问，当然也可以采用”引用.“的
      方式访问【但是不建议】
      
   4、static修饰的所有元素都是类级别的特征，和具体的对象无关。
*/

public class Chinese{
    //身份证号[每个对象的身份证号不同]；实例变量
    String id;
    
    //姓名【每个对象的姓名不同】 ，实例变量
    String name;
    
    //国籍
    //无论Chinese类实例化多少java对象，这些java对象的国籍都是“中国”
    //实例变量【实例变量是一个java对象的一份，100个对象就有100个countory】
    //实例变量存储在java对象内部，在堆内存当中，在构造方法执行的时候初始化。
    String country;
    
    //构造方法
    public Chinese(){
        this.id = null;
        this.name = null;
        this.country = null;
    }
    //构造方法
    public Chinese(String id, String name, String country){
        this.id = id;
        this.name = name;
        this.country = country;
    }
}
public class ChineseTest{
    public static void main(String[] args){
        //创建中国人对象1
        Chinese zhangsan = chinese("1","zhangsan","中国");
        System.out.println("id = " + zhangsan.id + "name = " + zhangsan.name + "country = " + zhangsan.country);
        //创建中国人对象2
        Chinese lisi = chinese("2","lisi","中国");
        System.out.println("id = " + lisi.id + "name = " + lisi.name + "country = " + lisi.country);
    }
}
//以上的country太浪费，定义以下的方法会比较好一些（较少内存的消耗）

//-----------------------------------------------------------------------------------
public class Chinese{
    //身份证号[每个对象的身份证号不同]；实例变量
    String id;
    
    //姓名【每个对象的姓名不同】 ，实例变量
    String name;
    
    //国籍【所有的国际一样，这种特征属于类级别的特征，可以提升为整个模板的特征，可以在变量前添加static关键字修饰】
    //静态变量，在类加载的时候初始化，不需要创建对象，内存就开辟了。
    //静态变量存储在方法区内存当中。
    
    static String country = "中国"; //类级别的变量，访问类名.变量名
    
    //构造方法
    public Chinese(){
        this.id = null;
        this.name = null;
        //this.country = null;
    }
    //构造方法
    public Chinese(String id, String name){
        this.id = id;
        this.name = name;
        //this.country = country;
    }
}
public class ChineseTest{
    public static void main(String[] args){
        //创建中国人对象1
        Chinese zhangsan = chinese("1","zhangsan");
        System.out.println("id = " + zhangsan.id + "name = " + zhangsan.name + "country = " + Chinese.country);
        //创建中国人对象2
        Chinese lisi = chinese("2","lisi");
        System.out.println("id = " + lisi.id + "name = " + lisi.name + "country = " + Chinese.country);
        System.out.println(Chinese.country);
        System.out.println(zhangsan.country);
        zhangsan.country = null;
        //所有的静态数据都是可以采用类名. 也可以采用引用. ， 但是建议采用类名. 的方式访问。
        //采用引用. 的方式访问的时候，即使引用时null, 也不会出现空指针异常，因为访问静态的数据不需要对象的存在。
        System.out.println(zhangsan.country);
    }
}
```

![image-20210407092113340](java%E5%AD%A6%E4%B9%A0.assets/image-20210407092113340.png)

### 8、静态代码块&实例代码块



```java
/*
可以使用static关键字来定义“静态代码块”
    1、语法格式;
       static{
          java语句;
       }
    2、静态代码块在类加载时执行，并且只执行一次(类加载，而不是类中的main函数执行之后)
    
    3、静态代码块在一个类中可以编写多个并且遵循自上而下的顺序依次执行
    
    4、静态代码块的作用是什么？怎么用?用在哪儿？什么时候用？
    - 这当然和具体的需求有关，例如项目中要求在类加载的时候，执行代码完成日志的记录。
    
    - 静态代码块是java为程序员准备的特殊的时刻，这个时刻被称为类加载时刻，若希望在此时刻执行
      一段特殊的程序，这个程序可以直接放到静态代码块当中、
    
    5、通常在静态代码块中完成预备工作，先完成数据的准备工作，例如：初始化连接池，解析XML配置文
       件……
*/

public class StaticTest01{
    static{
        System.out.println("类加载-->1");
    }
    static{
        System.out.println("类加载-->2");
    }
    static{
        System.out.println("类加载-->3");
    }
    public static void main(String[] args){
        System.out.println("main begin");
    }
}
```

```java
/*
实例语句块/代码块
  1、实例代码块可以编写多个，也是遵循自上而下的顺序依次执行
  
  2、实例代码块在构造方法执行之前执行，构造方法执行一次，实例代码块执行一次
    （构造方法不执行，不申请对象，实例代码块不执行）
    
  3、实例代码块也是java语言为程序员准备的一个特殊时机，这个特殊时机被称为：对象初始化时机。

*/
public class Test{
    //构造函数
    public Test(){
        System.out.println("Test类的缺省构造器执行");
    }
    //实例代码块
    {
        System.out.println("1");
    }
    //实例代码块
    {
        System.out.println("2");
    }
    //实例代码块
    {
        System.out.println("3");
    }
    //主方法
    public static void main(String[] args){
        System.out.println("main Begin");
        new Test();
        new Test();
    }
}
```

```java
public  static HelloWorld{
    public static void main(String[] args){
        //主方法的重载
        main(10);
        main("hello world");
    }
    public static void main(int i){
        System.out.prinln(i);
    }
    public static void main(String args){
        System.out.println(args);
    }
    
}
```

```java
/*
方法什么时候定义为静态的方法？
    方法的描述是动作，当所有的对象执行这个动作的时候，最终产生的影响是一样的，那么这个动作已经不再属于某一个对象的动作了，可以将这个动作提升为类级别的动作，模板级别的动作。
    
    静态方法中无法直接访问实例变量和实例方法。
    
    大多数方法都定义为实例方法，一般一个行为或者一个动作正在发生的时候，都需要对象的参与
    但是也有例外，例如：大多数“工具类”都是静态方法，因为工具类就是方便编写，为了方便调用，，
    自然也不需要new对象是最好的。
*/
public class StaticTest{
    public static void main(String[] args){
        //实例变量
        int i = 100;
        
        //实例方法
        public void doSome(){
            
        }
        //静态方法【静态上下文】
        public static void main(String[] args){
            //System.out.println(i);
            //doSome();
            StaticTest st = new StaticTest();
            System.out.println(st.i);
            st.doSome();
        }
    }
}
```



## 第五章 面向对象（下）

### 1、继承

```java
/*
关于java语言当中的继承
    1、继承是面向对象三大特称征之一
    
    2、继承“基本”作用是：代码复用。但是继承的最"重要"的作用是:有了继承才有了以后的“方法覆
       盖”和“多态机制”。
       
    3、继承语法格式：
       [修饰符列表] class 类名 extends 父类名{
           类体 = 属性 + 方法
       }
       
    4、java语言当中的继承只支持单继承，一个类不能同时继承很多类，但是c++可以支持多类
    
    5、关于继承中的一些术语：
       B类继承A类，其中
          A类称为：父类、基类、超类、superclass
          B类称为：子类、派生类、subclass
          
     6、在java语言中子类继承父类都继承哪些数据呢？
       - 私有的不支持继承
       - 构造方法不支持继承
       - 其它数据都可以被继承
       
     7、虽然java语言当中只支持单继承，但是一个类可以间接继承其它类
         c extends b{
         
         }
         b extends a{
         
         }
         a extends t{
         
         }
         c直接继承b类，但是c类间接继承t、a类
         
     8、java语言中假设一个类没有明显的继承任何类，该类默认继承javaSE库当中提供的
        java.lang.Object类
     所以，对于public class Account{
        Account 继承了JVM中的很多类（只是不显示而已）
     }
     java语言中，任何一个类都有Object类的特征
 
*/
public class Account{
    private String actno; //账号
    private double balance; //余额
    //在此处右击 ->源码（source）->Generate Constructor using Fields
    //(使用字段生成构造函数)- >勾选参数/不勾选参数 -> 生成无参构造函数/有参构造函数
    //还有右击 score -> 生成set函数和getter函数（一下代码一键生成）
    public Account(String actno, double balance) {
		this.actno = actno;
		this.balance = balance;
	}
	public Account() {
	}
	public String getActno() {
		return actno;
	}
	public void setActno(String actno) {
		this.actno = actno;
	}
	public double getBalance() {
		return balance;
	}
	public void setBalance(double balance) {
		this.balance = balance;
	}
}
public class CreditAccount extends Account{
    private String actno;
    private double balance;
    private double credit;
   
	public creditAccount() {
		
	}
	
	public double getCredit() {
		return credit;
	}
	public void setCredit(double credit) {
		this.credit = credit;
	}
}
public class ExtendsTest{
    //快捷键：查找类型【Open Type】 -->ctrl + shift + t
    //超诈资源【Open Resorece】 -->ctrl + shift + r
    public static void main(String[] args){
        creditAccount act = new creditAccount();
        act.setActno("act-001");
        act.setBalance(-1000.0);
        act.setCredit(0.99);
        System.out.println(act.getActno() + " ," + act.getBalance() + ", " + act.getCredit());
    }
}
```

### 2、方法的覆盖

```java
/*
关于java语言当中的方法覆盖：
    1、方法覆盖又被称为重写，英语单词override[官方的] / overwrite
    
    2、什么时候使用方法重写？
       当父类中的方法已经无法满足当前子类的业务需求
       子类有必要将父类中继承过来的方法进行重新白编写
       这个重新编写的过程称为方法重写/发放覆盖

    3、什么条件满足后方法会发生重写呢？【代码满足什么条件之后，就构成方法的覆盖呢？】
       * 方法重写的发生在具有继承关系的父子类之间
       * 方法重写的时候：返回值类型相同，方法名相同，形参列表相同
       * 方法重写的时候：访问权限不能更低，可以更高。
       * 方法重写的时候，抛出异常不能更多，可以更少。
       
    4、建议方法重写的时候，尽量复制粘贴，不要编写，容易出错，导致没有产生覆盖
      （或者右键Score 的override 中工具生成）
      
    5、注意：
        私有方法不能继承，所以不能覆盖
        构造方法不能继承，所以不能覆盖
        静态方法不存在覆盖，
        覆盖只针对方法，不存在属性/方法
*/
public class Animal{
    //动物可以移动的
    public void move(){
        System.out.println("动物在移动")；
    }
    
}
//猫科类继承动物类
public class Cat extends Animal{
    //方法的覆盖
    public void move(){
        System.out.println("猫在走猫步");
    }
}
//飞禽类继承动物类
public class Bird extends Animal{
    //方法的覆盖
    public void move(){ //名字一样的会发生方法的覆盖
        System.out.println("鸟儿在飞翔");
    }
}

public class OverrideTest{
    public static void main(String[] args){
        //创建动物对象
        Animal a = new Animal();
        a.move();
        
        //创建猫科类动物对象
        Cat c = new Cat();
        c.move();
        //创建飞禽类动物对象
        Bird b = new Bird();
        b.move();
    }
        
}
```

### 3、多态

```c++
/*
关于java语言当中的多态语法机制：
    1、Animal、Cat、Bird三类之间的关系：
       Cat继承Animal
       Bird继承Animal
       Cat和Bird之间没有任何继承关系
       
    2、关于多态中涉及到几个概念：
       * 向上转型(upcasting)
         子类型 --> 父类型
         又被称为：自动类型转换
       * 向下转型（downcasting）
          父类型 --> 子类型
          又被称为：强制类型转换【要加强制类型转换符】
          【八大数据类型种，除了boolean外其它都可以互相转换】
          
       * 需要记忆：
             无论是向上转型，还是向下转型，两种类型之间必须要有继承关系。
             没有继承关系，程序是无法编译通过的

*/

public class Animal{
    public void move(){
        System.out.println(”动物在移动“);
    }
}

public class Cat extends Animal{
    public void move(){
        //重写父类种继承过来的方法
        System.out.println(”猫在移动“);    
    }
    
    //不是从父类种继承过来的方法
    //这个方法是子类对象特有的行为【不是所有的动物都有此方法】
    public void catchMouse(){
        System.out.println("猫抓老鼠");
    }
}

public class Bird extends Animal{
    public void move(){
        //重写父类种继承过来的方法
        System.out.println(”飞禽在飞翔“);
    }
    public void fly(){
        System.out.println("bird fly");
    }
}

public class Test{
    public static void main(String[] args){
        //以前的程序
        Animal a1 = new Animal();
        a1.move();
        
        Cat c1 = new Cat();
        c1.move();//调用的一定是继承后重写之后的方法（如果存在方法重写的话）
        c1.catchMouse();
        
        Bird b1 = new Bird();
        b1.move();
        
        //使用多态语法机制
        
        /*
        1、Animal和Cat之间存在继承关系，Animal是父类，Cat是子类
        
        2、Cat is a Animal【合理的】
        
        3、new Cat()创建的对象类型是Cat,a2这个引用的数据类型是Animal,可见他们进行了类型转换
           子类型转换成父类型，称为向上转型/upcasting,或者称为自动类型转换
        
        4、Java种允许这种语法：父类型引用指向子类型对象
        
        */
        Animal a2 = new Cat();
        /*Bird b2 = new cat();编译报错，因为这两种类型之间不存在任何继承关系，无法向上或者
          向下转型
        */
        
        /*
        1、java程序永远都分为编译阶段和运行阶段
        
        2、先分析编译阶段，在分析运行阶段，编译无法通过，根本是无法运行的。
        
        3、编译阶段编译器检查a2这个引用的数据类型为Animal,由于Animal.class字节码当中都有
           move()方法，所以编译通过了。这个过程我们称为静态绑定，编译阶段绑定
           只有静态绑定成功之后，才有后续的运行阶段
        
        4、在程序运行阶段，JVM堆内存当中真实创建的对象是Cat对象，那么以下程序在运行阶段一定会
           条用Cat对象的move（）方法，此时放生了程序的动态绑定，运行阶段绑定
        
        5、无论是Cat类有没有重写move方法，运行阶段一定调用的是Cat对象的move方法，因为在底层
           真实对象就是Cat对象。
        
        6、父类型引用指向子类型对象这种机制导致程序存在编译阶段绑定和运行阶段绑定两种不同的形
           态/状态。
        */
        a2.move();
        
        /*
        分析以下程序为什么不能调用？
            因为编译阶段编译器检查到a2的类型是Animal类型，
            从Animal.class字节码文件当中绑定失败了，没有绑定成功
            也就是编译失败了。别谈运行了。
        
        */
        
        //a2.catchMouse();
        
        /*
        需求：
            假设想让以上的对象执行catchMouse()方法怎么办？
                a2是无法直接调用的，因为a2的类型Animal，Animal中没有catchMouse()方法。
                我们可以将a2强制类型转换为Cat类型
                a2的类型是Animal(父类)，装换成Cat类型（子类），被称为
                向下转型/downcasting/强制类型转换。
        注：向下转型也需要两种类型之间必须有继承关系，不然编译报错。强制类型转换需要加强制类型
            转换符。
        
        什么时候需要使用向下转型呢？
            当调用的方法是子类型中特有的，在父类型中不存在，必须进行向下转型
        */
        Cat c2 = (Cat)a2;
        c2.catchMouse();
        
        //父类型引用指向子类型对象【多态】
        Animal a3 = new Bird();
        /*
        1、以下程序编译没有任何问题，因为在编译器检查到a3的数据类型是Animal，Animal和Cat
           之间存在继承关系，并且Animal是父类型，Cat是子类型，父类型转换成子类型叫做向下转
           型，语法合格
           
        2、程序虽然编译通过了，但是程序在运行阶段会出现异常，因为在JVM堆内存当中真实存在的对
           象是Bird类型，Bird对象无法转换成Cat对象，因为这两种之间不存在任何继承关系，此时出
           现了著名的异常：
               java.lang.ClassCastException
               类型转换异常，这种异常总是在”向下转型“的时候会发生。
        */
        Cat c3 = (Cat)a3;
        
        /*
        1、以上的异常只有在强制类型转换的时候会发生，也即是说”向下转型“存在隐患
          （编译过了，但是运行错了）
          
        2、向上转换只要编译通过，运行一定不会出现问题：Animal a = new Cat();
        
        3、向下转型编译通过了，运行可能错误：Animal a = new Bird(); Cat c3 = (Cat)a3;
        
        4、如何能避免向下转型出现的ClassCastException错误呢？
           使用instanceof(instance;实例，of:的)运算符可以避免出现以上的异常。
        
        5、instanceof怎么用？
           5、1：语法格式：
                 (引用 instanceof 数据类型)
                 
           5、2：以上的运算符的执行结果类型为布尔类型，结果可能是false/true;
           
           5、3：关于结果的true/false;
                假设（a instanceof Animal)
                true表示：
                    a这个引用指向的对象是一个Animal类型。
                false表示：a这个引用的对象不是一个Animal类型。
                
        6、Java规范要求中：在进行强制类型转换之前，建议才采用instanceof运算符进行判断，
           避免ClassCastException异常的发生。
              
        */
        if(a instanceof Cat){ //a3是一个Cat类型的对象
            Cat c3 = (Cat)a3;
            //调用子类中特有的方法
            c3.catchMouse();
         }else if(a3 instanceof Bird){//a3是一个Bird类型的对象
            
            Bird b2 = (Bird)a3;
            //调用子类中特有的方法
            b2.fly();
         }
    }
}

public class Test2{
    public static void main(String[] args){
        //父类型引用指向子类型对象
        //向上转型
        Animal a1 = new Cat();
        Animal a2 = new Bird();
        
        //向下转型【只有当访问子类型对象中特有的方法】
        if(a1 instanceof Cat){
            Cat c1 = (Cat)a1;
        }
        if(a2 instanceof Bird){
            Bird b1 = (Bird)a2;
        }
    }
}
```

![image-20210412093439399](java%E5%AD%A6%E4%B9%A0.assets/image-20210412093439399.png)

```java
/*
多态在实际开发中的作用，以下是主人喂养宠物为例说明多态的作用
  1、分析：主人可以喂养宠物，这个场景要实现需要进行类型的抽象：
     - 主人【类】
     - 主任可以喂养宠物，所以主人有喂养的这个动作
     - 宠物【类】
     - 宠物可以吃东西，所以宠物要有吃东西的这个动作
     
2、面向对象编程的核心：定义好类，然后将类实例化对象，给一个环境驱使一下，让各个对象之间协作起
   来形成一个系统。

3、多态的作用是什么？
      降低程序的耦合度，提高程序的扩展力。
      能使用多态尽量使用多态。
      父类型引用指向子类型对象。
   
   核心：面向抽象编程，尽量不要面向具体编程。
*/
public class Test{
    public static void main(String[] args){
        //创建主人对象
        Master zhangsan = new Master();
        //创建猫对象
        Cat tom = new Cat();
        //主任喂养猫
        zhangsan.feed(tom);
        //创建小狗对象
        Dog erHa = new Dog();
        //主人喂养小狗
        zhangsan.feed(erHa);
    }
}
//宠物猫类
public class Cat extends Pet{
    public void eat(){
        System.out.println("小猫正在吃鱼");
    }
}

/*
这种方式没使用java语言当中的多态机制，存在的缺点：Master扩展能力很差，因为只要加一个宠物，Master类就需要添加新的方法。

//主人的一个类（面向具体的编程）
public class Master{
    public void feed(Cat c){
        c.eat();
    }
    public void feed(Dog d){
        d.eat();
    }
}

//Master和Cat.Dog这两个类型的关联程度很强，耦合度很高，扩展力差。
*/
//降低程序的耦合度【解耦合】，提高程序的扩展力【软件开发的一个很重要的目标】
public class Master{
    //Master主人类面向的是一个抽象的Pet,不在面向具体的宠物
    //提倡：面向抽象的编程，不要面向具体编程。
    //面向抽象编程的好处是，耦合度低，扩展里强
    public void feed(Pet pet){//Pet pet 是一个父类型的引用
        pet.eat();
    }
    
}
public class Dog extends Pet{
    public void eat(){
        System.out.println("小狗正在啃骨头");
    }
    
}

public class Pet(){
    public void eat(){
        
    }
}
```

### 4、final 关键字

```c++
/*
关于java语言中final关键字：
    1、final是一个关键字，表示最终的，不可变的
    
    2、final修饰的类无法被继承
    
    3、final修饰的方法无法被覆盖
    
    4、final修饰的变量“一旦”赋值后，不可重新赋值【不可重新赋值，即二次赋值】
    
    5、final修饰的实例变量
       java语言最终规定实例变量使用final修饰之后，必须手动赋值，不能采用系统默认赋值
       
    6、final修饰的引用
       final修饰的引用，一旦指向某个对象后，不能再指向其他对象，那么被指向其它对象无法被垃圾回收器回收
       final修饰的引用虽然指向某个对象之后，不能再指向其它对象，但是所指向的内部的内存是可以被修改的
       
    7、final修饰的实例变量，一般和static联合使用，被称为常量。

对于以后大家所学习的类库，一般都是包括三部分的
    - 源码【可以看源代码来理解程序】
    - 字节码 【程序开发的过程中使用的就是这个部分】
    - 帮助文档【对开发提供帮助】
*/

public class FinalTest01{
    public static void main(String[] args){
        int i = 10;
        System.out.println(i);
        i = 20;
        System.out.println(i);
        final int k = 10;
        //编译错误，无法为最终变量k分配值
        //k = 200;
        
        final int m;
        m = 200;
        //编译错误，无法为最终变量m分配值
        //m = 300;
    }
}
public class C{
    public final void m1(){
        
    }
}
public class B extends C{
    /*
    public void m1() {
        //重写不了，因为是final修饰了父类，重写不了
    }
    */
}
```

```java
public class FinalTest02{
    //成员变量值实例变量
    //实例变量有默认值 + final修饰的变量一旦赋值不能重新赋值
    //综合考虑，java语言最终规定实例变量使用final修饰之后，必须手动赋值，不能采用系统默认赋值
    
    //final int age;
    
    //第一种解决方案
    final int age = 10;
    
    //第二种解决方案
    public FinalTest02(){
        this.age = 200;
        
    }
    //以上的两种解决方案：其实本质上是一种方式，都是在构造方法执行的过程当中给实例变量赋值
    
    public static void main(String[] args){
        final int a;
        a = 100;
        //不可二次赋值
        //a = 200;
    }
    
}
```

```java
public class User{
    private int id;
    
    public int getId(){
        return id;
    }
    public void setId(int id){
        this.id = id;
    }
    public User(){
        
    }
    public User(int id){
        this.id = id;
    }
}

public class FinalTest03{
    public static void main(String[] args){
        //创建用户对象
        User u = new User(100);
        
        //又创建了一个新的User对象
        //程序执行到此处，表示以上的对象已变成垃圾数据，等待垃圾回收器回收。
        u = new User(200);
        
        //创建用户对象
        final User zhangsan = new User(30);
        
        //一下是报错程序，原理跟局部量一个道理，不可二次创建对象
        //zhangsan = new User(40);//final修饰的引用，一旦指向某个对象后，不能再指向其他对象，那么被指向其它对象无法被垃圾回收器回收
    }
}
```

```java
public class User{
    int id;
    
    public User(){
        
    }
    public User(int id){
        this.id = id;
    }
}

public class FinalTest03{
    public static void main(String[] args){
        
        final User zhangsan = new User(30);
        Stetem.out.println(user.id);
        User.id = 50;//final修饰的引用虽然指向某个对象之后，不能再指向其它对象，但是所指向的内部的内存是可以被修改的
        Stetem.out.println(user.id);
    }
}
```



实例

```java
//中国人
class Chinese{
    //国籍
    //需求：每一个中国人的国籍都是中国，而且国际不会发生改变，为了防止国籍被修改，建议加上final修饰
    //final修饰的实例变量是不可变的，这种变量一般和static联合使用，被称为“常量”
    //常量的定义语法格式：
    //    public static final 类型 常量名 = 值;
    //java规范中要求所有的常量名字全部大写，每个单词之间使用下划线连接
    //static final String country = "中国";
    
    public static final String GUO_JI = "中国";
}

public class FinalTest04{
    public static void main(String[] args){
        System.out.println(Chinese.GUO.JI);
        System.out.println("圆周率 = " + Math.PI);
    }
}

class Math{
    public static final double PI = 3.1415936;
}
```

### 5、package,import

```java
/*
关于java语言当中的包机制
    1、为什么要使用package?
    包又被称为package,java中引用package这种语法机制主要是为了方便程序的管理。不同的功能的类被放到不同的软件包当中，查找比较方便，管理比较方便，易维护
    2、怎么定义package呢？
       - 再java源程序中的第一行编写package语句
       - package只能编写一个语句
       - 语法结构
         package 包名;
    3、包名的命名规范
       公司域名倒序 + 项目名 + 模块名 + 功能名
       采用这种机制，重名的几率很低，因为公司域名具有全球唯一性
       例如：
           com.bjpwoernode.oa.user; //company
           org.apache.tomcat.core; //organization
    4、包名要求全部小写，包名也是标识符，必须遵守表示符命名规则
    5、一个包对应一个目录
    6、是用来package机制之后，类名不再是Test01了，类名是：com.bjpowernode.javase.day11.Test01
    7、是用来package机制之后，应该怎么编译？怎么运行呢？(在终端里，非程序里eclipse里)
     - 使用了package机制后，类名不再是Test01了，类名是：com.bjpowernode.javase.day11.Test01
     - 编译：javac java源文件路径（在硬盘上生成一个class文件：Test01.class）
     - 手动方式创建了目录，将Test01.class字节码文件放到指定的目录下
     - 运行：java com.bjpowernode.javase.day11.Test01
     

*/
package com.bjpowernode.javase.day11; //4个目录【目录之间使用.隔开】

public class Test01{
    public static void main(String[] args){
        System.out.println(Test01 is main method execute);
    }
}
```

````java
package com.bjpowernode.javase.day11;
public class Test02{
    public static void main(String[] args){
        //完整类名是：com.bjpowernode.javase.day11.Test01
        com.bjpowernode.javase.day11.Test01 t = new com.bjpowernode.javase.day11.Test01();
        System.out.println(t);
        
        //可以省略包名，因为Test01和Test02在同一目录下（软件包）
        Test01 tt = new Test01();
        System.out.println(tt);
    }
}
````

```java
//当类在不同的目录下，用import去调用要使用的类，因为该类在此目录下找不到
/*
    import语句用来完成导入其他类，同一个包下的类不需要导入
    不在同一个包下需要手动导入
    
    import语法格式：
       import 类名;
       import 包名.*;
       
    import语句需压编写在package语句之上，class语句之上
    
    当在main主函数里，直接使用
    Cat c = new Cat();
    System.out.println(c);会报错，直接在package之下，按住ctrl + shift + o,看看缺少那个包，将其点击，系统导入即可。
*/

package com.bjpowernode;
import  com.bjpowernode.javase.day11.Test01;
//import  com.bjpowernode.javase.day11.*;

public class Test03{
    public static void main(String[] args){
        com.bjpowernode.javase.day11.Test01 t = new com.bjpowernode.javase.day11.Test01();
        System.out.println(t);
        //以上程序可以就是麻烦
        //当用import去调用其它包是，就不用这样繁琐
        Test01 x = new Test01();
        System.out.println(x);
        
        //java.lang.*;不需要手动引入，系统会自动引入
        //lang:language语言包，是java语言的核心类，不需要手动导入
        String s = "abc";
        System.out.println(s);
        //直接编写一下代码编译错误，因为Date类没找到
        ///Date d = new Date();
        //java.util.Date d = new java.util.Data ;
        Date d = new Data();
    }
}
/*
   最终结论；
       什么时候需要import？
         *不是java.lang包下，并且不在同一包下的时候，需要使用import进行引入,java.lang.*;这个包下的类不需要导入。
         A类中使用B类。
         A和B类在同一包下，不需要import
         A和B类不在同一包下，需要使用import
       
       import怎么用？
          import语句只能出现在package语句之下，class声明语句之上。
          import语句还可以采用星号的方式
*/
```

### 6、访问控制权限

```java
/*
访问控制权限修饰符：
    1、访问控制权限修饰符来控制元素的访问范围
    
    2、访问控制权限修饰符包括：
       public    表示公开的，再任何位置都可以访问
       protected 同包，子类
       缺省(不写) 同包
       private   表示私有的，只能再本类中访问
       
    3、访问控制权限修饰符可以修饰类、变量、方法……
    
    4、当某个数据值希望子类使用，使用protected进行修饰
    5、修饰符的范围：
       private < 缺省（default） < protected < public
       
    6、类中能用public 和缺省关键字（default）进行修饰

访问控制修饰符   本类   同包   子类    任意位置
———————————————————————————————————————————
public          可以   可以  可以      可以
protected       可以   可以  可以      不行
默认            可以   可以  不行       不行
private         可以   不行  不行       不行
*/
```

### 7、super关键字

```java
/*
  1、super 是一个关键字，全部小写。
  2、super 和this对比着学习
  this
      this能出现在实例方法和构造方法中。
      this的语法是：“this.”“this()”
      this不能使用在静态方法中。
      this.大部分情况下是可以省略的。
      this.什么时候不能省略呢？在区分局部变量和实例变量的时候不能省略。
          public void setName(String name){
               this.name = name;
          }
      this()只能出现在构造方法的第一行，通过当前的构造方法取调用“本类”中的其它构造方法，目的是：代码复用
   
   super:
      super能出现在实例方法和构造方法中。
      super的语法是：“super.”“super()”
      super不能使用在静态方法中。
      super.大部分情况下是可以省略的。
      super.什么时候不能省略呢？在区分局部变量和实例变量的时候不能省略。
          
      super()只能出现在构造方法的第一行，通过当前的构造方法取调用“父类”中的其它构造方法，目的是：创建子类对象的时候，先初始化父类型特征。
      
  3、super()
     表示通过子类的构造方法调用父类的构造方法。
     模拟现实世界中的这种场景：要想现有儿子，需要先有父亲
     
  4、重要结论：
     当一个构造方法第一行：
          既没有this()有没有super()的话，默认会有一个super();
          表示通过当前子类的构造方法调用父类的无参构造方法。
          所以必须保证父类的无参数构造方法是存在的。
    5、注意：
       this()和super()不能共存，他们都是只能出现在构造方法中的第一行。
          有super()就没有this(),有this()就没有super();前提是得手动写出来。
       当一个继承后的类中，构造方法第一行既没有this()有没有super()，默认的认为有super();
       
    6、this()和super()得区别
       this()调用的是本类中的构造方法，但是super调用的是继承父类的构造方法
       
    7、无论怎么折腾，父类的构造方法一定会被执行的。
    8、在java语言中，不管是new什么对象，最后老祖宗Object类的无参数构造方法一定会执行（Object类的无参数构造方法一定会最先执行）
     
*/

public class SuperTest01{
    public static void main(String[] args){
        //创建子类对象
        /*
           结果为如下
           A类的无参数构造方法
           B类的无参数构造方法
        */
        new B();
    }
}
//方法的覆盖针对的是方法，而此处针对的是构造函数。
class A{ //此处默认继承得是Object
    //建议将一个类的无参构造方法写出来，防止子类的构造方法super()调用的是无参的构造方法，防止出错
    public A(){
        //此处得super()调用的是Object中的构造方法
        System.out.println("A类的无参数构造方法");
    }
    
    public A(int i){
        System.out.println("A类中的有参数构造方法，（int）")
    }
    //一个类如果没有手动提供任何构造方法，系统会默认的提供一个无参数的构造方法
    //一个类如果手动提供了一个构造方法，那么无参数构造系统将不在提供。
}

class B extends A{
     public B(){
        //默认有一个super()去调用父类的无参构造方法，且只能出现在构造方法的第一行。
        System.out.println("B类的无参数构造方法");
    }
    /*
    public B(){
        //super(123); //调用父类中的有参数构造方法
        this("zhangsan"); //调用本类中的有参数的构造方法。
        System.out.println("B类中的")
    }
     //super作用是先去调用父类种相对应的构造方法，在去执行本类中的构造方法中的语句
    */
    public B(String name){
        super();
        System.out.println("B类种的String类型的构造方法");
    }
}
```

```java
/*
   举个例子：在恰当的时间里使用：super(实际参数列表)
   
   3、思考：“super(实参)”到底是干啥的？
   super(实参)的作用是：初始化当前对象的父类型给特征。并不是创建新的对象，实际上对象只创建了一个
*/
public class Account{
    private String actno; //账号
    private double balance; //余额
   
    public Account(String actno, double balance) {
		this.actno = actno;
		this.balance = balance;
	}
	public Account() {
	}
	public String getActno() {
		return actno;
	}
	public void setActno(String actno) {
		this.actno = actno;
	}
	public double getBalance() {
		return balance;
	}
	public void setBalance(double balance) {
		this.balance = balance;
	}
}
public class CreditAccount extends Account{
    private String actno;
    private double balance;
    private double credit;
   
	public CreditAccount() {
		
	}
    //构造方法
	public CreditAccount(String actno, double balance, double credit){
        /* 不能这么干，私有的属性，只能在本类中访问
        this.actno = actno;
        this.balance = balance;
        */
        //默认调用无参的super();调用父类的对应的构造方法
        super(actno, balance);
        //以上的子类通过恰当的super()完成上面的私有变量在子类中取访问了（间接）
        this.credit = credit;
    }
	public double getCredit() {
		return credit;
	}
	public void setCredit(double credit) {
		this.credit = credit;
	}
}
public class ExtendsTest{
    
    public static void main(String[] args){
       CreditAccount ca1 = new CrditAccount();
        System.out.println(ca1.getActno() + "," + ca1.getBalance() + "," + ca1.Credit());//默认值
        CreditAccount ca2 = new CreditAccount("11111",100.00,0.9999);
        System.out.println(ca2.getActno() + "," + ca2.getBalance() + "," + ca2.Credit());
    }
}
```

```c++
public class SuperTest04{
    public static void main(String[] args){
        Vip v = new Vip("张三");
        v.shopping();
    }
}
class Customer{
    String name;
    public Customer(){}
    public Customer(String name){
        this.name = name;
    }
}

class Vip extends Customer{
    public Vip(){}
    public Vip(String name){
        super(name);
    }
    //super和this都不能出现在静态方法中
    public void shopping(){
        //this表示当前对象
        System.out.println(this.name + "正在购物");
        //super表示得是当前对象的父类型特征
        System.out.println(super.name + "正在购物");
        System.out.println(name + "正在购物");
    }
}
```

![image-20210426231517578](java%E5%AD%A6%E4%B9%A0.assets/image-20210426231517578.png)

```c++
/*
   1、“this.”和"super."大部分情况下都是可以省略的
   2、this. 什么时候不能省？
    public void setName(String name){
       this.name = name;
    }
    
   3、super.什么时候不能省略？
       父中有，子中也有，如果想在子访问“父的特征”，super.（一般是同名的属性出现，不可省略）
*/

public class SuperTest05{
    public static void main(String[] args){
        Vip v = new Vip("张三");
        v.shopping();
    }
}
class Customer{
    String name;
    public Customer(){}
    public Customer(String name){
        this.name = name;
    }
}


class Vip extends Customer{
    //假设子类也有一个同名的属性
    String  name;//实例变量
    //java中允许在子类中出现和父类一样的同名变量
    public Vip(){//如果构造方法中什么也不写的话，会给该类中的每个变量赋空值
        super();
        //默认的会执行
        //this.name = null;
    }
    public Vip(String name){
        super(name);
    }
    //super和this都不能出现在静态方法中
    public void shopping(){
        /*
          java是怎么样来区分子类和父类的同名属性的？
             this.name:当前对象的name属性
             super.name:当前对象的父类型特征中的name属性
        
        */
        //this表示当前对象
        System.out.println(this.name + "正在购物");//null正在购物
        //super表示得是当前对象的父类型特征
        System.out.println(super.name + "正在购物");//张三正在购物
        System.out.println(name + "正在购物");//null正在购物（什么也不写，默认为this.name）
    }
}
```

![image-20210426233419873](java%E5%AD%A6%E4%B9%A0.assets/image-20210426233419873.png)

```c++
/*
   通过这个测试得出结论：
      super不是引用，super也不保存内存地址，super也不指向任何对象
      super只是代表对象内部的那一块父类型特征
*/


public class SuperTest06{
    //实例方法
    public void doSome{
        System.out.println(this);
        //输出“引用.”的时候，会自动调用toString()方法,等价于下面的输出语句
        //System.out.println(this.toString());
        //编译错误：需要‘.’
        //System.out.println(super);
    }
    public static void main(String[] args){
        Super.Test06() st = new SuperTest06();
        st.doSome();
   }
}
```

```java
/*
   在父和子中有同名的属性，或者说有相同的方法，
   如果此时想在子类中访问父中的数据，必须使用“super.”加以区分。
   
   super.属性名  【访问父类中的属性】‘
   super.方法名  【访问父类中的方法】
   super(实参)   【调用父类中的构造方法】

*/


public class SuperTest07{
    public static void main(String[] args){
        Cat c = new Cat();
        c.yiDong();
    }
}

class Animal{
    public void move(){
        System.out.println("Animal move1");
    }
}

class Cat extends Animal{
    //对move进行重写
    public void move(){
        System.out.println("Cat move!");
    }
    
    //单独编写一个子类的特有的方法
    public void yiDong(){
        this.move();
        move();
        //super.不仅可以访问属性，也可以访问方法
        super.move();
    }
}
```





## IDEA

```markdown
Create New Project (创建工程)
Import Project (导入工程)
Open(打开工程)
Get from Version Control (从某个地方获取工程)

第一步：点击create new project
   注意：在IDEA当中一个project相当于eclipse当中的一个wordspace

第二步：新建一个Empty Project
   新建一个空的工程，选则创建工程窗口下面的“最后一项”，Empty Project
   
第三步：给空的工程起一个名字，：javase,并存储到相应的位置，点击Finish

第四步：自动弹出一个每日提示，这个每日提示可以取消掉，以后每一次打开就不再提示了

第五步：会自动弹出一个：project structure(项目重构),先取消掉

第六步：在空的工程下新建Module(模块)，IDEA中模块类似于eclipse当中的project.
   eclipse的组织方式：
     workspace -> project
   idea的组织方式：
     project -> module
   怎么创建module？
     file菜单 -> new -> Module
     
第七步：在New Module窗口上点击左上角的java,然后next

第八步：给module起一个名字：chapter15

第九步：编写代码，在src目录下新建类，写代码，并运行
```

```markdown
关于IEDA工具的快捷键以及一些简单的设置
  1、字体：file -> Settings -> (搜索栏搜：font（字体)）输入font -> 设置字体样式以及字号大小
  2、快速生成main方法;
    psvm回车
  
  3、快速生成System.out.println()
    sout回车
    
  4、IDEA是自动保存，不需要ctrl + s
  
  5、运行的机制：
     代码上右键-> run
     或者点击左侧数字栏的绿色箭头
     ctrl + shift + F10
     
  6、左侧窗口中的列表怎么展开？怎么关闭？
     左箭头关闭
     右箭头展开
     上下箭头移动
     
  7、idea中，退出任何窗口，都可以使用esc键盘。
  
  8、窗口变大变小：ctrl + stift + F12
  
  9、任何新增/新建/添加的快捷键是：
     alt + insert（笔记本电脑是要alt + Fn + insert(F12）)
     
  10、切换java程序：从一个类切换到另一个类
     alt + 左/右箭头
     
  11、IDEA,自动纠错的快捷键（Alt + 回车），前提是光标得再红线错误出，再按快捷键
  
  12、更改主题
     file -> settings -> Editor -> Color Scheme
     
  13、包的显示方式
     设置按钮 -> Compact Middle Packages
     
  14、如果使用IDEA 给主程序String传入参数
      Run -> Edit configurations…… -> 输入想用的参数，各个字符串之间用空格隔开（如果使用文本编译器，直接输入文件名.后缀名 字符串1 字符串2 ……）
      
  15、如何再IDEA中出现API帮助文档
      双击两次shift，输入包名即可。
      
  16、如何给IDEA增加背景
      文件 -> 设置 -> 外观&行为 -> 外观 -> UI选项 -> Background image... -> 在电脑中选则自己喜欢的图片 -> 并设置相应的透明度 -> 应用即可
```



## 抽象类

1、抽象类的理解

![image-20210427121518028](java%E5%AD%A6%E4%B9%A0.assets/image-20210427121518028.png)

```java
/*
   抽象类：
     1、什么是抽象类？
       类和类之间具有共同特征，将这些共同特征提取出来，形成的就是抽象类
       类到对象是：实例化， 对象到类是抽象
       类本身不存在，所以抽象类无法创建对象【无法实例化】
       
     2、抽象类属于什么类型？
        抽象类也属于引用数据类型
        
     3、抽象类定义？
       语法：
          [修饰符类列表] abstract class 类名{
              类体；
          }
    4、抽象类是无法实例化的，无法创建对象的，所以抽象类是用来被子类继承的。
    
    5、final 和abstract是对立的，不能联合使用，final是子类不能被继承，而abstarct是专门让子类继承的。
    
    6、抽象类的子类可以是抽象类
    7、抽象类虽然无法实例化，但是抽象类有构造方法，这个构造方法是供子类使用的。
    
    8、抽象类关联到一个概念：抽象方法。什么是抽象方法？
       抽像方法表示没有实现的方法，没有方法体的方法。例如：
       public abstract void doSome();
       抽象方法特点是：
          特点1：没有方法体,以分号结尾。
          特点2：前面修饰符列表中有abstract关键字
          
    9、抽象类中不一定有抽像方法，但抽象方法必须出现在抽象类里面。

*/
public class AbstractTest01{
    public static void main(String[] args){
        //错误：Acount是抽象的，无法实例化
        //Account act = new Account();
    }
}
//银行账户类
abstract class Account{
    public Account(){
        
    }
    public Account(String name){
        
    }
}

//子类继承抽象类，子类可以实例化对象
class CreditAccount extends Account{
    public CreditAccount(){
        super();
    }
}

//抽象类的子类可以是抽象类吗？可以
/*
abstract class CreditAccount extends Account{
    
}
*/
```

```java
/*
  抽象类：
      1、抽象类中不一定有抽象方法，抽象方法必须出现再抽象类中
      2、重要结论：总要结论：（必须记住）
         一个非抽象的类继承抽象类，必须将抽象类中的抽象方法实现了。
         这是java语法上强制规定的，必须的，不然编译器就报错了。
         这里的覆盖或者重写，也可以叫做实现（对抽象的实现。）

*/

public class AbstractTest02{
    public static void main(String[] args){
        //能不能使用多态？
        //父类型引用指向子类型的对象。
        Animal a = new Bird();
        //这就是面向抽象编程。
        //以后调用都是调用的a.xxx
        //a的类型是Animal ,Animal是抽象的
        //面向抽象编程，不要面向具体编程，降低程序的耦合度，提高程序的扩展力
        a.move();
        //编译用的是Animal的抽象类，运行的时候，用的是Bird中的move方法。
    }
}
//动物类
abstract class Animal{
    //抽象方法
    public abstract void move();
}
//子类(非抽象的)
//错误：BIrd不是抽象的，并且没有覆盖Animal中的抽象方法。
/*
class Bird extends Animal{
    
}
*/
class Bird extends Animal{
    //需要将父类中的继承过来的抽象方法进行覆盖/重写，或者也可以叫做实现
    //把抽象方法实现了
    public void move(){}
}
/*
  有些内容不要死机硬背，讲讲道理。
  分析：
      Animal 是父类，并且是 抽象的。
      Animal 这个抽象类中有一个抽象方法move.
      
      BIrd是子类，并且是 非抽象的。
      Bird继承Animal之后，会将抽象方法继承过来。
*/

/*
   如果Bird是抽象类的话，那么这个Animal中继承过来的抽象方法也可以不去重写/覆盖/实现。
   abstract class Bird extends Animal{
   
   }
*/
```

## 接口

> 接口基础语法

```java
/*
   接口：
     1、接口也是一种“引用数据类型”，编译之后也是一个字节码（.class）文件
     2、接口时完全抽象的，（抽象或者半抽象），或者可以说是接口时特殊的抽象类。
     3、接口的定义方式，语法式什么？
        [修饰符列表] interface 接口名{}
        //抽象类
        [修饰符列表] abstract class 类名{}
        //类
        [修饰符列表] class 类名{}
     4、接口支持多继承，一个接口可以继承多个接口。
     5、接口中只包含两部分内容，一部分式：常量，一部分是：抽象方法，接口中之后这两个内容，没有其它内容了。
     6、接口中的抽象方法定义时：public abstract 修饰符可以省略。
     7、接口中的所有元素都是public 修饰的（都是公开的）
     8、接口中的方法都是抽象方法，所以接口中的方法不能有方法体。
     9、接口常量中的public static final可以省略
*/
public class Test01{
    public static void mian(String[] args){
        //访问接口的常量
        System.out.println(MyMath.PI);
    }
}
//定义接口(接口与接口之间的继承)
interface A{
    
}
//定义接口，接口支持继承
interface B extends A{
    
}
//一个接口可以继承多个接口（支持多继承）
interface C extends A,B{
    
}
interface MyMath{
    //常量
    public static final double PI = 3.1415926;
    //抽象方法
    //public abstract int sum(int a,int b);
    
    //接口中既然都是抽象方法，那么再编写代码的时候，public abstract 可以省略吗？可以
    int sum(int a, int b);
    //接口中的方法不可以有主体
    /*
    void doSome(){
    
    } //不能把封号去掉改成大括号
    
    */
}
```

## 类实现接口

### 1、接口的基础语法

```java
/*
  接口的基础语法：
      1、类和类之间叫做继承，类和接口之家叫做实现
         别多想：你任然可以将“实现”看作是“继承”。
         继承使用extends关键字完成的
         实现使用implements关键字实现的
         
      2、五颗星的结论：
         当一个非抽象的类实现接口的话，必须将接口中所有的抽象方法全部是实现（覆盖，重写）。
*/
//特殊的抽象类，完全抽象的，叫做接口
interface MyMath{
    double PI = 3.1415926;
    int sum(int a, int b);
    int sub(int a, int b);
}
//修正（类与接口）
class MyMathImpl implements MyMath{
    //重写/覆盖/实现 接口中的方法（通常叫做实现）
    public int sum(int a, int b){
        //修饰列表不能比父接口更低，必须加public
        return a + b;
    }
    public int sum(int a,int b){
        return a - b;
    }
}

public class Test02{
    public static void main(String[] args){
        //能使用多态吗？可以
        //Animal a = new Cat();
        //父类型的引用指向子类型的对象
        MyMath mm = new MyMathImpl();//编译找的式MYMath里卖弄的，运行时（堆里）找的式MyMathImp1()里面的。
        //调用接口里面的方法，（面向接口编程。）
        int result1 = mm.sum(19,20);
    }
}
```

```java
/*
   接口和接口之间支持多继承，那么一个类可以同时实现多个接口吗？
   重点（五颗星）:一个类可以同时实现多个接口。
   这种机制弥补了java中的那块缺陷？
     java中类与类只支持单继承，实际上单继承是为了简单而出现的，现实世界中存在多继承，java中的接口弥补了单继承带来的缺陷。

*/
public class Test03{
    public static void mian(String[] args){
        //多态怎么用？
        A a = new D();
        B b = new D();
        C c = new D();
        //向上转型
        B b2 = (B)a;
        //经过测试：接口和接口之间再进行强制类型转换的时候，没有继承关系，也可以强转。
        //但是一定注意，运行时可能ClassCastException异常。
        M m = new E();
        K k = (K)m;
        //经过测试：接口和接口之间再进行强制类型转换的时候，没有继承关系，也可以强转。
        //但是一定要注意，运行时可能会出现ClassCastException异常
        //编译没问题，运行有问题。
        b2.me();
        
        //要想没问题
        if(m instanceof K){
            K k = (K)m;
        }
    }
}

interface K{
    
}
interface M{
    
}
class E implements M{
    
}
//--------------------------------------------

interface A{
    void m1();
}
interface B{
    void m2();
}
interface c{
    void m3();
}
//实现多个接口，其实就类似于多继承
class D implements A, B, C{
    //以下三个语句必须有（三个接口必须全部实现）
    //实现A接口中的m1()
    public void m1(){
    }
    //实现B接口中的m2()
    public void m2(){
        
    }
    
    //实现接口c中的m3()
    public void m3(){
        
    }
}
```

### 2、extends 和implements同时出现（继承和实现）

```java
/*
  继承和实现都存在的话，代码应该怎么写？
    extends 关键字在前
    implements 关键字在后。
*/
public class Test04{
    public static void main(String[] args){
        //创建对象（表面看Animal类没有起作用！）
        Flyable f = new Cat(); //多态
        f.fly();
        
        //同一个接口
        Flyable f2 = new Pig();
        //调用同一个fly()方法，最后执行的效果不同
        f2.fly();
        Flyable f3 = new Fish();
        f3.fly();
    }
}
//动物类：父类
class Animal{
    
}
//可飞翔的接口（是一对翅膀）
//能插拔的就是接口（没有接口你怎么插拔）
//内存条查到主板上，他么之间有接口，内存条可以更换
//接口通常提取的是行为动作。
interface Flyable{
    void fly();
}
//动物类子类：猫类
//Flyable是一个接口，是一对翅膀的接口，通过接口插到猫身上，让猫可以飞翔。
class Cat extends Animal implements Flyable{
    public void fly(){
        System.out.println("飞猫起飞，翱翔太空的一只猫，很神奇，我想做");
    }
}

//蛇类，如果不想让它飞，可以不实现Flyable接口
//没实现这个接口表示你没有翅膀，没有给你翅膀，你肯定不能飞
class Snake extends Animal{
    
}
//想飞就插翅膀这个接口
class Pig extends Animal implements Flyable{
    public void fly(){
        System.out.println(“我是一个会飞的猪”);
    }
}

class Fish implements Flyable{//没写extends,也是有的，默认继承Object.
    public void fly(){
        System.out.println("我是六眼飞鱼");
    }
    
}
```

### 3、接口再开发中的作用

```java
1.3接口在开发中的作用
   注意：接口再开发中的作用，类似于多态再开发中的作用。
   多态：面向抽象编程，不要面向具体编程。降低程序的耦合度，提高程序的扩展力。
   /*
      public class Master{
         public void feed(Dog d){}
         public void feed(Cat c){}
      }
   
   
   */
    public class Master{
        public void feed(Animal a){
            //面向Animal父类编程，父类是比子类更抽象的
            //所以我们叫做面向抽象编程，不要面向具体编程
            //这样程序的扩展能力就强
        }
    }
/*
   接口在开发中的作用？
       接口是不是完全的？是
       而我们以后正好要求，面向抽象编程
       面向抽象编程这句话以后可以修改为：面向接口编程
       有了接口，就有了可插拔，可插拔表示扩展能力强，不是焊死的。
       
       主板和内存条之间有插槽，这个插槽就是接口，内存条坏了，可以重新买下来换一个，这叫做高扩展型（低耦合度）
       
       接口在现实世界中是不是到处都是呢？
          螺栓和螺母之间有接口
          灯泡和灯口之间有接口
          笔记本电脑和键盘之间有接口
          接口有什么用？扩展性好，可插拔
          接口是一个抽象的概念
      
      总结：
         接口的使用离不开多态机制（接口 + 多态才可以达到降低耦合度。）
*/
```

```java
//实例
/*
  接口：菜单，抽象的
*/
interface FoodMenu{
    //西红柿炒鸡蛋
    void shiZiChaoDan();
    //鱼香肉丝
    void yuXiangRouSi();
    
}
//顾客
class Customer{
    //顾客手里有一个菜单
    //Customeer has a FoodMenu!(顾客有一个菜单)
    //记住：以后凡是能够使用has a 来描述的，统一以属性的方式存在
    //实例变量，属性
    //面向抽象编程，面向接口编程
    private FoodMenu foodMenu;//封装的好习惯
    //food Munu = new ChinCooker();
    //foodMenu = new AmericCooker();//子类
    
    //构造方法
    public Customer(){
        
    }
    public Customer(FoodMenu foodMenu){
        this.FoodMenu = foodMenu;
    }
    //get and set
    public void setFoodMenu(FoodMenu foodMenu){
        this.foodMenu = foodMenu;
    }
    public FoodMenu getFoodMenu(){
        return foodMenu;
    }
    //提供一个点菜的方法
    public void order(){
        //先拿到菜单才能点菜
        foodMenu.shiZiChaoDan();//调用接口
        foodMenu.yuXiangRouSi();
    }
}

/*
Cat is a Animal ,单反满足is a的表示都可以设置为继承
Customer has a FoodMenu,单反满足has a的表示都以属性的形式存在。


*/
//厨师是接口的实现者
//中国厨师
//实现菜单上的菜
class ChinaCooker implements FoodMenu{
    //西红柿炒蛋
    public void shiZiChaoDan(){
         System.out.println("中餐师傅做的西红柿炒鸡蛋");
    }
    
    //鱼香肉丝
    public void yuXiangRouSi(){
        System.out.println("中餐师傅做的鱼香肉丝");
    }
}
//西餐厨师
//实现菜单上的菜
class AmericCooker implements FoodMenu{
    //西红柿炒蛋
    public void shiZiChaoDan(){
        System.out.println("西餐师傅做的西红柿炒鸡蛋");
    }
    
    //鱼香肉丝
    void yuXiangRouSi(){
        System.out.println("西餐师傅做的鱼香肉丝");
    }
}

public class Test{
    public static void main(String[] args){
        //创建厨师对象
        FoodMenu cooker1 = new ChinaCooker();
        //FoodMenu cooker1 = new AmericCooker();
        //创建顾客对象
        Customer customer = new Customer(cooker1);
        //顾客new一个厨师，然后点菜
        customer.order();
    }
}

/*
   //”自己“类
   //MySelf has a Friend;
class MySelf{
   //你这个对象，应该有一个朋友对象的电话号码
   //电话号码就是一个对象的内存地址，联系你朋友的时候，打电话
   //f是一个应用，f默认为null，是null表示，你没朋友
   
   Firend f;
   public Myself(){
   
   }
   //通过构造方法能不能给你一个朋友对象
   public Myself(Friend f){
      this.f = f;
   }
   public static void main(String[] args){
      //创建自己对象
      Friend f = new Friend();//朋友对象有了
      //目前还没有交朋友
      Myself m = new Myself(); //自己对象
      //交朋友
      m.f = f;//把朋友的地址给了你。
   }
}

class Friend{ //“朋友类”

}
*/
```

### 4、类和类之间的关系

```markdown
is a（继承）、 has a（关联）、 like a（实现）
is a:
    Cat is Animal(猫是一个动物)
    凡是能够满足is a的表示“继承关系”；
has a:
    I has a Pen(我有一只笔)
    凡是能够满足has a关系的表示“关联关系”
    关联关系通常以“属性”的形式存在。
like a:
    Cooker like a FoodMenu(厨师像一个菜单一样)
    凡是能够满足like a关系的表示“实现关系”
    实现关系通常是：类实现接口。
```

### 5、抽象类和接口的区别

```markdown
1、 
    抽象类是半抽象的。
    接口是完全抽象的。
2、
    抽象类中有构造方法
    接口中没有构造方法
3、
    接口和接口之间支持多继承
    类和类之间只支持单继承
4、
    一个类可以同时实现多个接口
    一个抽象类只能继承一个类（单继承}
    
5、 
    接口中只允许出现常量和抽象方法。
    
6、这里现透漏一个信息：
    以后接口使用的比抽象类多，一般抽象类使用的还是少
    接口一般都是对“行为”的抽象。
```

### 6、USB接口的实现

```java
package cn.kong;

import java.io.FileNotFoundException;
import java.io.FileWriter;
import java.io.IOException;
import java.util.Scanner;

public class PreserveTest {
    public static void main(String[] args) {
        FileWriter out = null;
        try{
            //创建文件字符输出流
            out = new FileWriter("file",true);//以追加的方式
            Scanner s = new Scanner(System.in);
            System.out.println("请输入你想要的姓名和地址，姓名和地址中间用f符号”-”分开");
            String str = s.next();
            while(true){
                out.write(str);
                out.write("\n");
                System.out.println("请再次输入你想要的姓名和地址，姓名和地址中间用f符号”-”分开");
                str = s.next();
                if("quit".equals(str)){
                    System.out.println("str = " + str);
                    break;
                }
            }
            if("quit".equals(str)){
                System.out.println("对不起，该程序已经结束了，不能再往文件中录入信息了");
            }
            out.flush();//刷新
        }catch(FileNotFoundException e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }finally{
            if(out != null){
                try{
                    out.close();
                }catch(IOException e){
                    e.printStackTrace();
                }
            }
        }
    }
}
```



## 解释Scanner

```java
import java.util.Scanner;
//或者这样import java.util.*;
public class Test03{
    public static void main(String[] args){
        //为什么要这样写？
        //Test03类和Scanner类不在同一包下。
        //java.util就是Scanner类的包名。
        //java.util.Scanner s = new.util.Scanner(System.in);
        Scanner s  = new Scanner(System.in);
        String str = s.next();//接受输入的内容
        System.out.println("你输入的自符串为" + str);
    }
}
/*
//数组方法：
String next()；//数组自符串型数据
boolean nextBoolean();
byte nextByte();
double nextDouble();
float nextFloat();
int nextInt();
String nextLine();//一行字符串
long nextLong();
short nextShort();
*/
```

