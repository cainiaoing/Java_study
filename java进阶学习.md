## 1、Object类

### 1、源码及API文档

```markdown
1、JDK类库的根类：Object
   1.1、这个老祖宗中的方法我们需要先研一下，因为这些方法都是所有子类通用的，
   任何一个类默认继承Object,就算没有直接继承，最终也会间接继承。
   2.2、Object类当中有那些常用的方法？
        目前为止我们只需要直到这几个方法即可：
           protected Object clone(); //负责对象克隆
           int hashCode(); //获取对象哈希值的一个方法
           boolean equals(Object obj);//判断两个对象是否相等
           String toString(); //将对象转成字符串的形式
           protected void finalize();//垃圾回收器负责调用的方法
```



### 2、toString方法(一般是要重写的)

```java
/*
   关于Object类中的toString()方法
      1、源代码长什么样子？
          public String toString(){
             return this.getClass().getName() + "@" + Integer.toHexString(hashCode());
          }
          源代码上的toString()方法的默认实现是：
             类名@对象的内存地址转换成为十六进制的形式
      2、SUN公司设计的toString()方法的默认实现是什么？
          toString()方法的作用是什么？
             toString()方法的设计目的是：通过这个方法可以将一个“java”对象“转变成为”字符串，返回该对象的字符串表示返回该对象的字符串表示
             
      3、其实SUN公式开发java语言的时候，建议所有子类都去重写toString()方法
         toString()方法应该是一个简洁的，详实的、易阅读的。
*/
public class Test01{
    public static void main(String[] args){
        MyTime t1 = new MyTime(1970,1,1,);
        String s1 = t1.toString();
        System.out.println(s1);
        
    }
}
class MyTime{
    int year;
    int month;
    int day;
    public MyTime(){
        
    }
    public MyTime(int year, int month, int day){
        this.year = year;
        this.month = month;
        this.day = day;
    }
    //重写toString()方法
    public String toString(){
        return this.year + "年" + this.month + "月" + this.day + "日";
    }
}
```

### 3、equals方法

```java
/*
   关于Object类中的equals方法
      1、equals方法的源代码
      public boolean equals(Object obj){
          return (this == obj);
      }
      以上这个方法是Object类默认实现
      
      2、SUN公司设计equals方法的目的是什么？
         以后编程的过程当中，都要通过equals方法来判断两个对象是否相等
         
      3、我们需要研究一下Object类给的这个默认的equals方法都不够用（需要重写），因为默认情况下是用”==“去判断两个对象是否相等。
      
      4、判断两个java对象是否相等，不能使用”==“，因为”==“比较的是两个对象的内存地址。
*/

public class Test02{
    public static void main(String[] args){
        int a = 100;
        int b = 100;
        //这个是判断a中保存的100和b中保存的100是否相等
        System.out.println(a == b);//true
        
        //判断java对象是否相等，我们怎么办？
        //MyTime t1 = 0x1234;
        MyTime t1 = new MyTime(2008,1,1);
        //MyTime t2 = 0x3566;
        MyTime t2 = new MyTime(2008,1,1);
        //这里”==“判断的是：t1中保存的对象内存地址和t2保存的对象的内存地址是否相等
       // System.out.println(t1 == t2);//false
        
        //重写object equals
        boolean flag = t1.equals(t2);
        //在创建一个新的日期
        MyTime t3 = new MyTime(2008,8,9);
        System.out.println(t1.equals(t3));
    }
}
class MyTime{
    int year;
    int month;
    int day;
    public MyTime(){
        
    }
    public MyTime(int year, int month, int day){
        this.year = year;
        this.month = month;
        this.day = day;
    }
    //重写Object类的equals方法
    //重写的时候，赋值粘贴，相同的返回值类型，相同的方法名，相同的形式参数列表
    
    public boolean equals(Object obj){
        //获取第一个日期的年月日
        int year1 = this.year;
        int month1 = this.month;
        int day1 = this.day;
        //获取第二个日期的年月日
        
        /* 不可以，因为obj没有此方法调用
        int year2 = obj.year;
        int month2 = obj.month;
        int day2 = obj.day;
        */
        if(obj instanceof MyTime){
            MyTime t = (MyTime)obj; //强制类型转换
            int year2 = t.year;
            int month2 = t.month;
            int day2 = t.day;
            if(year1 == year2 && month1 == month2 && day1 == day2){
                return true;
            }
        }
        return false;
    }
   
}

改良后的equals (IDEA会自动生成 alt + fn + f12) 输入equals
public boolean equals(Object obj){
    if(obj == null){
        return false;
    }
    if(!(obj instanceof MyTime)){
        return false;
    }
    if(this == obj) //同一个对象
    {
        return true;
    }
    MyTime t = (MyTime)obj; //强制类型转换
    int year2 = t.year;
    int month2 = t.month;
    int day2 = t.day;
    if(year1 == year2 && month1 == month2 && day1 == day2){
        return true;
    }
    return false;
}
```

###  4、String类重写了toString和equals

```java
/*
   java语言当中的字符串String 重写机制
      1、String 类已经重写了equals方法，比较两个字符串不能使用==,必须使用equals
      2、String类已经重写了toString方法
      
   大结论：
      java中什么类型的数据可以使用”==“判断
         java中基本数据类型比较是否相等，使用”==“
      java中什么数据类型需要使用equals判断
         java中搜友的引用数据类型统一使用equals方法来判断是否相等。
*/
public class Test03{
    public static void main(String[] args){
        //大部分情况下，采用这样的方式创建字符串对象
        String s1 = "hello";
        String s2 = "abc";
        //实际上String也是一个类，不属于基本数据类型
        //既然String是一个类，那么一定存在构造方法。
        String s3 = new String("Test1");
        String s4 = new String("Test2");
        System.out.println(s3 == s4);//false
        //利用String类已经重写equals方法
        System.out.println(s3.equals(s4));//true
        //利用String类里面的重写方法toString()方法
        String x = new String("动力节点");
        System.out.println(x);
    }
}
```

```java
public class Test04{
    public static void main(String[] args){
        Student s1 = new Student(111,"河北省");
        Student s3 = new Student(111,"山西省");
        System.out.println(s1.equals(s3));
    }
}
class Student{
    int no;
    String school;
    public Student(){}
    public Student(){
        this.no = no;
        this.school = school;
    }
    public String toString(){
        return "学号" + no + "，所在学校 " + school;
    }
    public boolean equals(Object obj){
        if(obj == null || !(obj instanceof Student)) return false;
        if(this == obj) return true;
        Student s = (Student)obj;
        if(this.no === s.no && this.school.equals(s.school)) return  true;
        return false;
    }
}
```

```java
public class Test05{
    public static void main(String[] args){
        Address addr = new Address("北京","复兴路","93939");
        User u1 = new User("zhangsan",addr);
        //或者这样写
        //User u1 = new User("zhangsan",new Address("北京","复兴路","93939"));
        User u2 = new User("zhangsan",addr);
        System.out.println(u1.equals(u2));
        //多态
        //Object o1 = new String("hello world");
        //夫类型的引用指向子类型（自动类型转换，Object完全可以接受子类）
    }
}
class User{
    //用户名
    String name;
    Address addr;
    public User(){
        
    }
    public User(String name, Address addr){
        this.name = name;
        this.addr = addr;
    }
    //重写equals方法
    //重写规则：当一个用户名和家庭住址都相同，表示同一个用户
    //这个queals判断的是User对象和User对象是否相等。
    public boolean equals(Object obj){
        if(obj === null || !(obj instanceof User)) return false;
        if(this == obj) return true;
        User u = (User)obj;
        //下面的Address方法的equals方法必须重写，否则会使用默认的equals方法，使用的是==比较的，得到的结果必然是false.
        if(this.name.equals(u.name) && this.addr.equals(u.addr)) return true;
        return false;
    }
}
class Address{
    String city;
    String street;
    String zipcode;
    public Address(){
        
    }
    public Address(String city, String street, String zipcode){
        this.city = city;
        this.street = street;
        this.zipcode = zipcode;
    }
    //注意：这里并没有重写equals方法
    //这里的equals方法判断的是：Address对象和Address对象是否相等
    public boolean equals(Object obj){
        if(obj == null || !(obj instanceof Address)) return false;
        if(this == obj) return true;
        Address a = (Address)obj;
        if(this.city.equals(a.city) && this.street.equals(a.street) && this.zipcode.equals(a.zipcode)) return true;
        return false;
    }
}
```

### 5、Object的finalize()方法

```java
/*
   关于Object类中的finalize()方法。
      1、在Object类中的源代码：
         protected void finalize() throws Throwable{}
      2、finalize()方法只有一个方法体，里面没有代码，而且这个方法是protected修饰的。
      3、这个方法不需要程序员手动调入，JVM的垃圾回收器负责调用这个方法
      4、finalize()方法实际上是SUN公司为java程序员准备的一个时机，垃圾销毁时机。
         如果希望在对象销毁时机执行一段代码的话，这段代码要写到finalize()方法中。
      5、静态代码块的作用是什么？
         static {
            
         }
         静态代码块在类加载时刻执行，并且只执行一次，
         这是一个SUN准备的类加载时机。
         finalize()方法同样也是SUN为程序员准备的一个时机
         这个时机是垃圾回收时机。

*/
public class Test06{
    public static void main(String[] args){
        //创建对象
        Person p = new Person();
        //怎么把Person对象变成垃圾？
        p = null;
        for(int i = 0; i < 1000; i++){
            Person p = new Person();
            p = null;
            //有一段代码可以建议垃圾回收器启动
            if(i % 2 == 0){
                System.gc(); //建议启动垃圾回收器
            }
        }
    }
}
//项目开发的时候，有这样的需求，所有的对象在JVM中被释放的时候，请记录一下释放的时间
//记录对象被释放的时间点，这个负责记录代码写到哪？
//写道finalzie()方法中
class Person{
    //重写finalzie()方法
    //Person类型对象被垃圾器回收的时候，垃圾回首器负责调用：p.finalize();
    protected void finalize() throws Throwable{
        System.out.println("即将被销毁");
    }
}
```

### 6、hashCode()

```java
/*
   hashCode方法中：
      在Object中的hashCode方法中是怎样的？
        public native int hashCode();
        这个方法不是抽象的，带有native关键字，底层调用c++程序
        
   hashCode()方法返回的是哈希码：
       实际上就是一个java对象的内存地址，经过哈希算法得出一个值
       所以hashCode()方法的执行结果可以等同于看作java对香象的内存地址
*/
public class Test07{
    public static void main(String[] args){
        Object o = new Object();
        int hashCodeValue = o.hashCode();
        //对象内存地址经过哈希算法装换成的一个数字，可以等同看作内存地址
        System.out.println(hashCodeValue);
        
        MyClass mc = new MyClass();
        System.out.println(hashCodeValue2);
    }
}
class Myclass{
    
}
```



## 2、匿名内部类

```java
/*
   匿名内部类：（类中不能有构造方法）
      1、什么是匿名内部类？
         内部类：在类的内部定义了一个新的类，被称为内部类。
      2、内部类的分类：
         静态内部类：类似于静态变量
         实例内部类：类似于实例变量
         局部内部类：类似于局部变量
      3、使用内部类编写的代码，可读性很差，能不用，尽量不用
      
      4、匿名内部类是局部内部类的一种。
         因为这个类没有名字而得名，叫做匿名内部类
         
      5、通常在使用抽象类得时候，没办法实现（不想用子类继承）这时就要用匿名内部类，
*/
class Test01{
    //该类在类的内部，所以称为内部类、
    //静态内部类
    static class Inner1{
        
    }
    //该类在类的内部，所以称为内部类
    //没有static叫做实例内部类
    class Inner2{
        
    }
    public void doSome(){
        //局部变量
        int i = 100;
        //局部内部类
        class Inner3{
            
        }
    }
    public void doOther(){
        //doSome()方法中局部内部类Inner3,在doOther中不能用
    }
    public static void main(String[] args){
        //调用MyMath中的mySum方法
        MyMath mm = new MyMath();
        //这样写代码，表示这个类名是有的，类名是ComputerImpl
        mm.mySum(new ComputerImpl(),100,200);
        //使用匿名内部类，表示这个ComputerImpl这个类没有名字了
        //这里表面看好像是接口可以直接new了，但是实际上并不是接口可以newl.
        //后面的{}代表了对接口的实现
        //不建议使用匿名内部类，为什么？
        //因为一个类没有名字，没有办法重复使用，另外代码太乱，可读性太差
        mm.mySum(new Computer(){
            public int sum(int a,int b){
                return a + b;
            }
        },200, 300);
    }
}
//负责计算的接口
interface Computer{
    //抽象方法
    int sum(int a, int b);
}
//自动编写一个Computer接口的实现类
class ComputerImpl implements Computer{
    //对方法的实现
    public int sum(int a, int b){
        return a + b;
    }
}
//数学类
class MyMath{
    //数学求和方法
    public void mySum(Computer c, int x, int y){
        int reValue = c.sum(x, y);
        System.out.println(x + " + " + y + " = " + reValue);
    }
}
```



## 3、数组

### 1、一维数组

![image-20210430151003799](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210430151003799.png)

```java
/*
Array
    1、Java语言中的数组是一种引用数据类型，不属于基本数类型，数组的父类是Object.
    2、数组当中可以存储“基本数据类型”，也可以存放“引用数据类型”的数据
    3、数组因为是引用数据类型，所以数组是存储再堆内存当中的。
    4、数组当中如果存储的是“java对象”的话，实际上存储的对象是“引用（内存地址）”，数组不可以直接存储java对象。
    5、数组一旦创建，再java中规定，长度不可变（数组长度不可变）
    6、所有的数组对象都有length属性（java自带的），用来获取数组元素中的个数。
    7、数组再内存方面存储的时候，数组中的元素内存地址都是连续的，内存地址连续。
    这是数组存储元素的特点。
    8、数组中首元素的内存地址作为整个数组对象的内存地址。
    9、数组这种数据结构的优点和缺点是什么？
       优点：查询/查找/检索某个下标上1的元素时效率极高，可以说是查询效率最高的一个数据结构。
            为什么检索效率高？
              第一：每个元素的内存地址再空间存储上是连续的
              第二：每个元素类型形同，所以占用空间大小一样
              第三：直到第一个元素内存地址，知道每一个元素占用空间的大小，又知道小标，所以通过一个数学表达式就可以计算出某个下标上元素的内存地址。直接通过内存地址定位元素，所以数组的检索效率是最高的。
       缺点：
           第一：由于为了保证数组中每个元素的内存地址连续，所以再数组上随机删除或增加元素的时候，效率较低，因为随机增删元素会涉及到后面元素统一向前或向后移位的操做
           第二：数组不能存储大数据量，因为很难再内u才能空间上找到一块特别大的连续的内存空间。
       注意：对于数组中最后一个元素的增删，是没有效率影响的。
    10、怎么声明/定义一个一维数组？
        语法格式：
          int[] array1;
          double[] array2;
          boolean[] array3;
          String[] array4;
          Object[] array5;
    11、怎么初始化一个一维数组呢？
        包括两种方式：静态初始化一维数组，动态初始话一维数组
          静态初始化一维数组格式：
            int[] array = {100,2,3,4,5};
          动态初始化一维数组语法格式：
             int[] array = new int[5];//这里的5表示5个长度的int类型数组，每个元素默认值为0
             String[] names = new String[6];//初始化6个长度的String类型数组，每个元素默认值为null.
             
    12、什么时候采用静态初始化方式，什么时候采用动态初始化方式呢？
       当你创建数组的时候，确定数组中存储那些数据，你可以用动态初始化方式
       当你创建数组的时候，不确定将来数组中储存那些数据，你可以采用动态初始化方式，预先分配内存空间
*/
//静态初始化
public class ArrayTest01{
    public static void main(String[] args){
        int[] a1 = {100,3,5,56};
        //所有的数组对象都有length属性
        System.out.println("数组长度为 " + a1.length);
        for(int i = 0; i < a1.length;i++){
            System.out.println(a1[i]);
        }
    }
}
//动态初始化
public class ArrayTest02{
    public static void main(String[] args){
        int[] a = new int[4];
        for(int i = 0; i < a1.length;i++){
            System.out.println(a[i]);
        }
        Object[] b= new Object[6];
        for(int i = 0; i < b.length; i++){
            System.out.println(b[i]);
        }
    }
}
//调用方法传数组(当一个方法数组上是数组的时候，因该怎么传参)
public class ArrayTest03{
    public static void mian(String[] args){
        int[] x = {19,32,3,45};
        printArray(x);
        String[] str = new String[10];
        printArray(str); //10个null
        
        //另一种方式
        printArray(new int[3]);
        printArray(new String[4]);
    }
    
    public static void printArray(int[] array){
        for(int i = 0; i < array.length; i++){
            System.out.println(array[i]);
        }
    }
    public static void printArray(String[] args){
        for(int i = 0; i < args.length; i++){
            System.out.println(args[i]);
        }
    }
}
//当一个方法的参数是一个数组的时候，我们还可以采用这种方式传
public class ArrayTest04{
    public static void main(String[] args){
        int[] a = {1,2,3};
        printArray(a);
        System.out.println("----------");
        //直接传入静态数组的语法必须这样写
        printArray(new int[]{1,2,34,5,6});
        //动态初始化一维数组
        int[] a2 = new int[4];
        printArray(a2);
        System.out.println("-------------");
        printArray(new int[3]);
    }
    public static void printArray(int[] x){
        for(int i = 0; i < x.lenght; i++){
            System.out.println(x[i]);
        }
    }
}

```

### 2、main方法的String数组

```java
/*
1、main方法上面的“String[] args”有什么用？
   分析以下：谁负责调用main方法（JVM)
   JVM调用main方法时候，会自动传一个String数组过来。
   且等价于String[] args = {};
*/
public class ArrayTest05{
    public static void mian(String[] args){
        System.out.println("JVM给传递过来的String数组这个数组长度是？" + args.length);
    }
}
/*
   模拟一个系统，假设这个系统要使用，必须输入用户名和密码
*/
public class ArrayTest05{
    //用户名和密码输入到String[] args数组当中
    //String[] args是用来接受用户的参数的
    public static void mian(String[] args){
        if(args.length != 2){
            System.out.println("使用该系统时，请输入程序参数，参数中包括用户名和密码信息，例如：zhangsan 123");
            return;
        }
        //程序执行到此处，说明用户提供了用户名和密码
        //接下来应该判断用户名和密码是否正确
        //取出用户名
        String username = args[0];
        //取出密码
        String password = args[1];
        //假设用户名是zhangsan 密码是123
        //判断两个字符是否相等，需要使用equals方法
        //if(username.equals("zhangsan") && password.equals("123")){//这样容易产生空指针异常
        //以下的编程方式不会产生空指针异常，因为“zhangsan”和“123”不会为null,但是以上的username和possword容易产生空指针异常
        if(“zhangsan”.equals(username) && "123".equals(password)){
            System.out.println("登录成功，欢迎");
            System.out.println("您可以继续使用该系统");
        }else{
            System.out.println("验证失败，该用户不存在或者密码错误");
        }
    }
}
/*
  数组中引用数据类型
  对于数组来说，实际上只能存储java对象的“内存地址”，数组中存储每个元素是”引用“。
*/
public class ArrayTest06{
    public static void mian(String[] args){
        //创建一个Animal类型的数组
        Animal a1 = new Animal();
        Animal a2 = new Animal();
        Animal[] animals = {a1,a2};
        //对Animal数组进行遍历
        for(int i = 0; i < animals.length;i++){
            /*Animal a = animals[i];
            a.move();           
            */
            //代码合并
            animals[i].move();//animals是数组，通过animals【i】变成了对象，再取出对象的方法
        }
        //动态初始化一个长度为2的Animal类型的数组
        Animal[] ans = new Animal[2];
        ans[0] = new Animal();
        ans[1] = new Cat();//Cat是Animals的子类
        for(int i = 0; i < ans.length; i++){
            ans[i].move();
        }
        
        //创建一个Animal类型的数组，数组中存储Cat和Bird
        Cat c = new Cat();
        Bird b = new Bird();
        Animal[] ansi = {c,b};
        //Animal[] ansi = {new Cat(),new Bird()};
        for(int i = 0; i < ansi.lenght;i++){
            //这个取出来的可能是Cat,可以能是Bird,不过肯定是一个Animal
            //ansi[i].move();
            //如果调用方法时父类中存在的方法，不需要向下转型，直接使用夫类型引用调用即可。
            
            //Animal an = ansi[i];
            //an.move();
            //调用子对象中特有方法的话，需要向下转型
            if(ansi[i] instanceof Cat){
                Cat cat = (Cat)ansi[i];
                cat.catchMouse();
            }else if(ansi[i] instanceof Bird){
                Bird bird = (Bird)ansi[i];
                bird.sing();
            }
        }
    }
}

class Animal{
    public void move(){
        System.out.printn("Animal move……");
        
    }
}
class Product{
    
}
class Cat extends Animal{
    public void move(){
        System.out.println("猫在有猫步");
    }
    //特有的方法
    public void catchMouse(){
        System.out.println("猫抓老鼠");
    }
}
class Bird extends Animal{
    public void move(){
        System.out.println("Bird Fly!!!");
    }
    //特有方法
    public void sing(){
        System.out.println("鸟儿在歌唱");
    }
}
```

### 3、数组扩容

```java
/*
  关于一维数组的扩容
  再java开发中，数组长度一旦确定不可变，那么数组满了怎么办？
    数组满了，需要扩容。
    java中对数组的扩容是：
       先新建一个大容量的数组，然后对小容量的数据一个一个拷贝到大数组当中
       
  结论：数组扩容效率较低，因为涉及到拷贝的问题，所以再以后的开发中请注意：尽可能少的进行数组拷贝。
       可以再创建数组对象中时候，预估计以下多长合适，这样可以减少扩容次数，提高效率
       
       涉及到arraycopy方法的使用
       第一个参数，表示拷贝源数组名
       第二个参数，表示拷贝源要拷贝的第一个位置下标
       第三个参数，表示拷贝目标数组名
       第四个参数，表示拷贝目标要备考被的目标起始位值
       第五个参数：表示从拷贝源起始位置，拷贝到目标起始位置，所要拷贝数组的长度
*/
public class ArrayTest08{
    public static void main(String[] args){
        //拷贝源
        int[] src = {1,11,22,3,5};
        //拷贝目标
        int[] dest = new int[20];//动态初始化一个长度位20的数组，每一个元素默认为0
        //掉用JDK System的arraycopy方法来完成数组拷贝
        System.out.println(src,1,dext,4,src.length);
        //遍历目标数组
        for(int i = 0; i < dest.length; i++){
            System.out.println(dest[i]);
        }
        
        //数组中如果存储的元素是引用，可以拷贝
        String[] strs = {"hello","world","study","java"};
        String[] str = new String[10];
        System.arrycopy(strs,0,str,0,strs.length);
        for(int i = 0; i < str.length; i++){
            System.out.println(str[i]);
        }
        Object objs = {new Object(),new Object(),new Object()};
        Object newObjs = new Object[10];
        System.arraycopy(objs,0,newObjs,0,objs.length);
        for(int i = 0; i < newObjs.length;i++){
            System.out.println(newObjs[i]);
        }
    }
}
```

![image-20210502220410854](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210502220410854.png)

### 4、二维数组

```java
/*
  关于二维数组：
    1、二维数组的静态初始化
       int[][] array = {{11,2,34,4},{13,13,3,5}};
       int[][]arr=newint[][2];这样是错误的
       int[][]arr=newint[2][];是正确的
    2、动态初始化二维数组
       
*/

public class ArrayTest09{
    public static void main(String[] args){
        int[][] array = {{11,2,34,4},{13,13,3,5}};
        for(int i = 0; i < array.length; i++){
            for(int j = 0; j < array[i].length;j++){
                System.out.print(array[i][j] + " ");
            }
            System.out.print('\n');
        }
        
        int[][] a = new int[3][4];
        for(int i = 0; i < a.length; i++){
            for(int j = 0; j < a[i].length;j++){
                System.out.print(a[i][j] + " ");
            }
            System.out.print('\n');
        }
        
        //调用方法
        int[][] y = {{11,2,34,4},{13,13,3,5}};
        printArray(y);
        //开可以这样写
        printArray(new int[][]{{11,2,34,4},{13,13,3,5}});
    }
    public static void printArray(int[][] x){
        for(int i = 0; i < x.length; i++){
            for(int j = 0; j < x[i].length;j++){
                System.out.print(x[i][j] + " ");
            }
            System.out.print('\n');
        }
    }
}
```

### 5、Arrays工具类

```java
/*
  java问什么好用，因为提供了一套类库，我们直接调用就好
  
  要排序，直接调用方法就好，再java中提供了一个工具类
      java.util.Arrays
      
  

*/
public class ArraysTest01{
    public static void main(String[] args){
        int[] arr = {111,2,3,45,5};
        //工具类当中的方法大部分都是静态的，直接类名.方法名
        Arrays.sort(arr);
        //遍历输出
        for(int i = 0; i < arr.length;i++){
            System.out.println(arr[i]);
        }
        //二分查找，建立再排序基础之上
        int index = Arrays.binarySearch(arr,32);
        System.out.println(index == -1? "该元素不存在":"该元素的下标是 " + index);
    }
}
```

### 6、随机点名器

```java
import java.util.Random;
import java.util.Scanner;

public class CallName {
    //存姓名
    public static void addStudentName(String[] students){
        Scanner s = new Scanner(System.in);
        for(int i = 0; i < students.length; i++){
            System.out.println("存储第"+ (i + 1) + "个姓名");
            students[i] = s.next();
        }
    }
    //总览全班姓名
    public static void printStudentName(String[] students){
        for(int i = 0; i < students.length;i++){
            String name = students[i];
            System.out.println("第"+ (i + 1) + "个姓名是 " + name);
        }
    }
    public static String randomStudentName(String[] students){
        int index = new Random().nextInt(students.length);
        String name = students[index];
        return name;
    }
    public static void main(String[] args) {
        System.out.println("----随机点名器-----");
        String[] students = new String[3];
        addStudentName(students);
        printStudentName(students);
        String name = randomStudentName(students);
        System.out.println("随机点名的人为--->"+ name);
    }
}

```







## 4、常用类

### 1、String类

#### 1、基本语法

```java
/*
 关于java JDK中内置一个类：java.lang.string;
   1、String表示字符串类型，属于引用数据类型，不属于基本数据类型。
   2、再java中随便使用双引号括起来的都是String对象。例如“abc","def"，这是2个String对象
   3、再java中规定，双引号括起来的字符串，都是直接存放再”方法区“的”自负串常量池“当中的。
*/
public class StringTest01{
    public static void main(String[] args){
        //这两行代码表示底层创建了3个字符串对象，都在字符串常量池当中
        String s1 = "abcdef";
        String s3 = "abede" + "xy";
        //分析：这是使用new的方式创建的字符串对象，这个代码中的”xy“从哪里来？
        //凡是双引号括起来的都在字符串常量池中有一份
        //new对象的时候，一定在堆内存当中开辟空间
        String s3 = new String("xy");
    }
}
```

![image-20210503162616499](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210503162616499.png)

```java
public class StringTest02{
    public static void main(String[] args){
        String s1 = "hello";
        String s2 = "hello";
        //"hello"式存储在方法区的字符串常量池当中
        //所以这个”hello"不会新建（因为这个对象已经新建了）
        
        //分析结果式true还是false?
        //==双等号比较的是变量中保存的内存地址
        System.out.println(s1 == s2);//true
        
        String x = new String("xyz");
        String y = new String("xyz");
        System.out.println(x == y);//false
        //通过这个案例的学习，我们知道了字符串对象之间的比较不能使用“==”，
        //"=="不保险，因该调用String类的equals方法
        //String类中的equals方法已经重写了
        System.out.println(x.equals(y)); // true
        System.out.println("text".equals(x));
        System.out.println(x.equals(text));//存在空指针异常的风险
        
    }
}
```

![image-20210503164325522](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210503164325522.png)

```java
/*
  分析以下程序，一共创建了几个对象
*/
public calss StringTest03{
    public static void main(String[] args){
        /*
        一共new了三个对象：
           方法区字符串常量池中有一个“hello”
           堆内存当中有两个String对象
           一共有三个        
        */
        String s1 = new String("hello");
        String s2 = new String("hello");
    }
}
```

#### 2、String中常用的构造方法

```java
/*
  关于String类中的构造方法
    1、String s = new String("");
    2、String s = "";
    3、String s = new String(char数组);
    4、String s = new String(char数组，起始下标，长度);
    5、String s = new String(byte数组);
    6、String s = new String(byte数组，起始下标，长度);
*/
public calss StringTest04{
    public static void main(String[] args){
        //创建了字符串对象最常用的一种方式
        //--------构造方法一
        String s1 = "hello world";
        //s1这个变量中保存的是一个内存地址
        //按说以下应该输出的是一个地址
        //但是输出一个字符串，说明String类已经重写了toString（）方法
        //这里只是掌握最常用的构造方法
        byte[] bytes = {97,98,99}; //a，b,c
        String s2 = new String(bytes);
        //前面说过：输出一个引用的时候，会自动调用toString（）方法，默认Object的话，会自动输出对象的内存地址
        //通过输出结果，我们得出一个结论：String类已经重写了toString方法
        //输出字符串对象的话，输出的不是对象的内存地址，而是字符串本身
        System.out.println(s2);//等价于下面语句
        System.out.println(s2.toStirng());
        
        //String(字节数组，数组元素下标的起始位置，长度)
        //将bytes数组一部分转换成字符串
        //----------构造方法二
        String s3 = new String(bytes, 1,2);
        System.out.println(s3);
        
        //---------构造方法三
        char[]  s4 = {97,98,99,100};
        String s5 = new String(s4);
        System.out.println(s5);
        String s6 = new Strig(s4,1,3);
        System.out.println(s6);
    }
}
```

#### 3、String类中常用的方法

```java
//1、 char charAt(int index)//返回字符串下标位index的字符
public calss StringTest05{
    public static void main(String[] args){
        //String类当中常用的方法
        //1、.char charAt(int index)
        char c = "中国人".charAt(1);
        System.out.prinln(c);
        
        //2、.int compareTo(String anotherString)
        int result = "abc".compareTo("abc");
        System.out.println(result);//0相等，正数前者大于后者，负数后者大于前者
        
        //3、.boolean contains(CharSequence s)
        //判断前面的字符串中是否包含后面的子字符串
        System.out.println("helloWorld.java".contains("java"));//true
        
       //4、.boolean endsWith(String suffix)
       //判断当前字符串是否以某个字符串结尾
        System.out.println("tset.txt".endsWith(".java"));//false
        System.out.prinln("test.txt".endsWith(".txt"));//true
        
        //5、.boolean equals(Object anObject)
        //比较两个字符串必须使用equals方法，不能使用”==“
        //equals方法没有调用compareTo方法
        //equals只能判断两个字符串是否相等
        //compareTo能判断两个字符串是否相等，还能判断谁打谁小1
        System.out.println("abc".equals("abc"));
        
        //6.boolean equalsIgnoreCase(String anotherString)
        //判断两个字符串是否相等，并同时忽略大小写
        System.out.println("ABc".equalsIgnoreCase("abc"));
        
        //7、.byte[] getBytes()
        //将字符串对象转换成字节数组
        byte[] bytes = "abcdef".getBytes();
        for(int i = 0; i < bytes.length;i++){
            System.out.println(bytes[i]);
        }
        
        //8、.int indexOf(String str)
        //判断某个字符串再当前字符串中第一次出现出的索引（下标）
        System.out.println("javac++.c++.java.python.python".indexOf("c++"));
        
        //9、.boolean isEmpty()
        //判断某个字符串是否为空
        String s = "";
        System.out.println(s.isEmpty());
        String s = "123";
        System.out.println(s.isEmpty());
        
        //10、.int length()
        //判断数组长度是length属性，判断字符串长度是length()方法
        System.out.println("abc".length());//3
        
        //11.int lastIndexOf(String str)
        //判断某个字符串再当前字符串中对后一次出现的索引（下标）
        System.out.println("oraclejavac++javac".lastIndexOf("jacac"));
        
        //12、.String replace（CharSequence target,CharSequence replacement)
        //String 的父接口就是CharSequence
        String newString = "www.baiud.com".replace("www","https://www");
        System.out.println(newString);
         String newString = "https://www=baiud=com".replace("=",":");
        System.out.println(newString);
        
        //13、.String[] split(String regex)
        //拆分字符串
        String[] ymd = "1999-04-22".split("-");//将字符串以字符”-“进行拆分,拆好的的放在字符串数组当中去
        for(int i = 0; i < ymd.length;i++){
            System.out.println(ymd[i]);
        }
        
        //14、.boolean startsWith(String prefix)
        //判断某个字符串是否以某个子字符串开始
         System.out.println("test.txt".startsWith("test"));//true
        System.out.prinln("test.txt".startWith("txt"));//false
        
        //15、.String substring(int beginIndex)
        //截取字符串
        System.out.println("http://www.baidu.com".substring(7));
        
        //16、.String substring(int beginIndex, int endIndex);截取某字符串开始到截止位置的字符串
        System.out.println("http://www.baidu.com".substring(7,10)); //左闭右开
        
        //17、.char[] toCharArray()
        //将字符串转换成char数组
        char[] chars = "我是中国人".toCharArray();
        for(int i = 0; i < chars.lenght; i++){
            System.out.println(chars[i]);
        }
        
        //18、.String toLowerCase()
        //转换成小写
        System.out.println("ABCDefk".toLowerCase());
        
        //19、.String toUpperCase()
        //转成大小
        System.out.println("ABCDefk".toUpperCase());
    }
    
    //20、String trim();
    //去除字符串前后的空白
    System.out.println("   hello     world  ".trim());
    
    //21、String中只有一个是静态的，不需要new对象
    //这个方法叫做valueOf
    //作用：将”非字符串“转成”字符串“
    String s1 = String.valueOf(1983920);
    System.out.println(s1);
    
    //这个静态的valueOf()方法，参数是一个对象的时候，会自动调用对象的toString()方法
    //如果菜类中没有重写toString()方法，输出的是内存地址
    //重写toString()方法，会输出字符串
    String s2 = String.valueOf(new Customer());
    System.out.println(s2);
    
    //研究以下println()方法
    Object obj = new Object();
    //本质上System.out.println()这个方法再输出任何数据的时候，都是现转成字符串，再输出
    System.out.println(obj);
    
}
class Customer{
    //重写toString()方法
    public String toString(){
        return "我是一个VIP客户!!!";
    }
}
```

#### 4、StringBuffer

```java
/*
  思考：我们在实际开发中，如果需要进行字符串的频繁的拼接，会有什么问题？
       因为java中的字符串是不可变的，每一次的拼接都会产生新的字符串
       这样会占用大量的方法区内存，造成内存空间的浪费。
       String s = "abc";
       s += "hello";
       以上两行代码，就导致方法区字符串常量池当中创建了3个对象
       ”abc“
       "hello"
       "abchello"
       
       
    如果以后需要进行大量字符串的拼接操作，建议使用JDK中自带的：
      java.lang.StringBuffer
      java.lang.StringBuilder
      
    如何优化StringBuffer的性能？
      在创建StringBuffer的时候，尽可能给定一个初始化容量
      最好减少底层数组的扩容次数，预估计一个，给一个合适的初始化容量，可以提高程序的执行效率
*/

public class StringBufferTest01{
    public static void main(String[] args){
        String s = "";
        //这样做会给java的方法区字符串常量池带来很大的压力。
        for(int i = 0; i < 100; i++){
            s = s + i;
            System.out.println(s);
        }
    }
}

public class StringBufferTest02{
    public static void main(String[] args){
        //创建一个初始化容量为16个byte[]数组（字符串缓冲区对象）
        StringBuffer stringBuffer = new StringBuffer();
        //拼接字符串，以后拼接字符串统一调用append()方法
        //append是追加的意思
        stringBuffer.append("a");
        stringBuffer.append("b");
        stringBuffer.append(19939);
        stringBuffer.append(true);
        stringBuffer.append(3.1415926);
        //append方法底层在进行追加的时候，如果byte数组满了，会自动扩容
        System.out.println(stringBuffer);
        //等价于下面的
        System.out.println(stringBuffer.toString());
        
        
        //指定初始化容量的StringBuffer对象（字符串缓冲区）
        StringBuffer sb = new StringBuffer(100);
        sb.append("hello");
        sb.append("world");
        sb.append("kitty");
        sb.append(19399202);
        System.out.println(sb);
    }
}
/*
StringBuffer和StringBuilder的区别？
   StringBuffer中方法都有：synchronized关键字修饰，表示StringBuffer在多线程环境下运行时是安全的
   
   StringBuilder中方法没有：synchronized关键字修饰，表示StringBuilder在多线程环境下运行时是不安全的

*/

public class StringBuilder01{
    public static void main(String[] args){
        StringBuilder sb = new StringBuilder(100);
        sb.append("hello");
        sb.append("world");
        sb.append("kitty");
        sb.append(19399202);
        System.out.println(sb);
    }
}

```

```java
/*
i、面试题: String为什么是不可变的?
   我看过源代码，String类中有一个byte[ ]数组，这个byte[ ]数组采用了final修饰，因为数组一旦创建长度不可变。并且被final修饰的引用一旦指向某个对象之后，不可再指向其它对象，所以String是不可变的!
   "abc”无法变成"abcd"
2、StringBuilder/StringBuffer为什么是可变的呢?
   我看过源代码，StringBuffer/StringBuilder内部实际上是一个byte[ ]数组，这个byte[ ]数组没有被final修饰，StringBuffer/StringBuilder的初始化容量我记得应该是16，当存满之后会进行扩容，底层调用了数组拷贝的方法System.arraycopy()...是这样扩容的。所以stringBuilder/StringBuffer适合于使用字符串的频繁拼接操作。

*/
```



### 2、8种基本数据类型的包装类

#### 1、引入

```java
/*
  1、java中8种基本数据类型对应8种包装类型，8种包装类属于引用数据类型，父类是Object
  2、为什么要再提供8种包装类呢？
     8种基本数据类型不够用，所以提供这8种，都是引用数据类型
  
*/
public class IntegerTest01{
    //入口
    public static void main(String[] args){
        //这样一种需求：调用doSome()方法时候需要传进入一个数字
        //但是数字属于基本数据类型，而doSome()方法参数类型是Object
        //可见doSome()方法无法接受基本数据类型，
        
        //把100这个数字包装成功对象
        MyInt myInt = new MyInt(100);
        //doSome()方法虽然不能直接传入100，但是可以传入一个100对应的包装类型
        doSome(myInt);
    }
    
    public static void doSome(Object obj){
        System.out.println(obj.toString());
    }
}
//这种包装类，SUN公司写好了，我们直接用就好，这个是自己直接写的
class MyInt{
    int value;
    public MyInt(){
        
    }
    public MyInt(int value){
        this.value = value;
    }
    
    //重写
    public String toString(){
        return String.valueOf(value);
    }
}
```

#### 2、拆箱和装箱的概念

```java
/*
  1、8种基本数据类型对应的包装类型名是什么？
   基本数据类型               包装类型
   ----------------------------------------------
   byte              java.lang.Byte(父类Number)
   short             java.lang.Short(父类Number)
   int               java.lang.Integer(父类Number)
   long              java.lang.Long(父类Number)
   float             java.lang.Float(父类Number)
   double            java.lang.Double(父类Number)
   boolean           java.lang.Boolean(父类Object)
   char              java.lang..Character(父类Object)
 2、以上8种包装类只以Integer为例，其它的都一样
 3、八种包装类其中6个都是数字对应的包装类，他们的父类都是Number,可以先研究Number中公共方法：
    Number是一个抽象类，无法实例化对象。
    Number中有这样的方法：
        byte byteValue() 以byte形式返回指定的数值
        abstract float floatValue()以float形式返回指定的数值
        abstract double doubleValue()以double形式返回指定数值
        abstract int intValue()以int形式返回指定数值
        abstract long longValue()以long形式返回指定类型数值
        short shortValue() 以short形式返回指定的数值
        这些方法都是所有的数字包装类的子类都有，这些方法是负责拆箱的
*/
public class IntegerTest02{
    public static void main(String[] args){
        //123这个基本数据类型，进行构造方法的包装达到了：基本数据类型向引用数据类型的转换
        //基本数据类型-（转换）-> 引用数据类型（装箱）
        Integer i = new Integer(100);
        
        //将引用数据类型 -(转换)-> 基本数据类型（拆箱）
        float f = i.floatValue();
        System.out.println(f);
        
        int retValue = i.intValue();
        System.out.println(reValue);
    }
}

/*
  关于Integer类的构造方法，有两个
     Integer(int)
     Integer(String)
*/
public class IntegerTest03{
    public static void main(String[] args){
        Integer x = new Integer(100);
        System.out.println(x);
        
        Integer y = new Integer("123");
        System.out.println(y);
        
        Double e = new Double(3.14);
        System.out.println(e);
        Double f = new Double("4.423");
        System.out.println(f);
        
    }
}
```

#### 3、通过常量获取最大值和最小值

```java
/*
  API帮助文档中在   字段摘要   里，都是常量，直接调用就好

*/
public class IntegerTest04{
    public static void main(String[] args){
        //通过访问包装类的常量，来获取最大值和最小值
        System.out.println("int 最大值 " + Integer.MAX_VALUE);
        System.out.println("long 最大值 " + Long.MAX_VALUE);
        System.out.println("Short 最大值 " + Short.MAX_VALUE);
        System.out.println("int 最小值 " + Integer.MIN_VALUE);
        System.out.println("long 最小值 " + Long.MIN_VALUE);
        System.out.println("Short 最小值 " + Short.MIN_VALUE);
    }
}
```

#### 4、自动装箱和拆箱

```java
/*
  在JDK1.5之后，支持自动装箱和拆箱
  Number类中方法就用不到了
     自动装箱：基本数据类型自动转换成包装类。
     自动拆箱：包装类自动转换成基本数据类型
*/
public class IntegerTest05{
    public static void main(String[] args){
        //自动装箱
        Integer x = 100;
        System.out.println(x);
        //自动拆箱
        int y = x;
        System.out.println(y);
        
        //z是一个引用，z是一个变量，z还是保存了一个对象的内存地址
        Integer z = 1000; //等同于Integer z = new Integer(1000);
        //+两边要求是基本数据类型，z是包装类，不属于基本数据类型，这个会自动拆箱，将z装换成基本数据类型
        System.out.println(z + 1);
        
        Integer a = 1000;
        Integer b = 1000;
        //==这个运算符不会触发自动拆箱装箱机制（只有+ - * /灯光运算符才会）
        System.out.println(a == b); //false,比较的是内存地址
    }
}
```

```java
/*
这个题目再面试的时候，很重要
*/
public class IntegerTest06{
    public static void main(String[] args){
        Integer a = 128;
        Integer b = 128;
        System.out.println(a == b);//false
        
        /*
          java中为了提高程序执行效率，将[-128 - 127]之间所有的包装对象提前创建好，放到一个方法区的”整数型常量池“当中了，目的是只要用了这个区间·的数据，不需要再new了，直接从整数型常量池当中取出来
          以下代码的原理：x变量中保存的对象的内存地址和y变量保存的内存地址是一样的
        */
        
        Integer x = 127;
        Integer y = 127;
        System.out.println(x == y); //true
    }
}
```

![image-20210503220037656](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210503220037656.png)

```java
/*
总结一下之前所学过的经典异常
   空指针异常：NullPointerException
   类型转换异常：ClassCastException
   数字下标越界异常：ArrayIndexOutOfBoundsException
   数字格式化异常：NumberFormatException

 重点方法
 //static int parseInt(String s);
 //静态方法传参String,返回int
 还有static double parseDouble(String s);
 static float parseFloat(String s);
*/
public class IntegerTest05{
    public static void main(String[] args){
        //手动装箱
        Integer x = new Integer(1000);
        Integer y = new Integer("1000");//字符串的话，这个字符串最起码是个数字字符串
        
        //手动拆箱
        int y = x.intValue();
        //int retValue = Integer.parseInt("中文");//汉字转不了数字，从而出现了NumberFormatException
        System.out.println(y);
        
        //valueOf方法
        //static Integer valueOf(int i)
        //静态的-> Integer
        Integer i1 = Integer.valueOf(100);
        System.out.println(i1);
        
        //static Integer valueOf(String s)
        //String -> Integer
        Integer i2 = Integer.valueOf("100");
        System.out.println(i2);
    }
}
```

#### 5、String int Integer互相转换

```java
public class IntegerTest01{
    public static void main(String[] args){
        //String -> int
        String s1 = "100";
        int i1 = Integer.parseInt(s1);
        System.out.println(i1 + 1);//101
        
        //int -> String
        String s2 = i1 + "";//字符串100
        System.out.println(s2 + 1);//1001
        
        //int -> Integer
        //自动装箱
        Integer x = 1000;
        
        //Integer -> int
        //自动拆箱
        int y = x;
        
        //String -> Integer
        Integer k = Integer.valueOf("123");
        
        //Integer -> String
        String e = String.valueOf(k);
    }
}
```

![image-20210505091603647](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210505091603647.png)



### 3、java对日期的处理

#### 1、DATA类

```java
/*
Date类中的方法大多都不用了，可以创建对象，也可以获取时间，不过这个时间不是日常格式，不太容易理解。
所以想要改变一下格式输出， 想找和这个类有关的，看“另请参见”有个DateFormat,这个类是个抽象的，有些非静态的操作可能不太方便，所以查看DateFormat类中“直接已知子类”：SImpleDateFormat （若年月日都要，用这个方便）
   1、public SimpleDateFormat(String pattern)
      pattern–描述日期和时间格式的模式，这个模式写法看“日期和时间模式”

   2、public final String format(Date date)：这个方法是抽象类DateFormat中的方法，这是个final方法，DateFormat的子类不可以重写，但可以使用，所以在SimpleDateFormat 类中并没有呈现这个方法，但是也可以使用。

   3、若要单独获得年或者月或者日，或者其他日期时间，并对其进行操作，
   用Calendar类中的方法
      1.public int get(int field)：获得指定字段的时间，例如星期几
        在Calendar中的字段是大写英文的，不太容易查看，
        所以看Date类中的“已过时”方法，这个比较方便。

      2、public final void set(int year, int month, int date):设置时间
      
      3、public abstract void add(int field, int amount)：对指定字段加减操作

*/
import java.util.*;
import java.text.*;
public class DateDemo {

    public static void main(String[] args) {
        // TODO Auto-generated method stub

        Date d=new Date();
        System.out.println(d);//Thu Jul 20 13:22:33 CST 2017打印的时间看不懂

        //将模式封装到SimpleDateFormat对象中
        SimpleDateFormat sdf=new SimpleDateFormat("yyyy年MM月dd日 hh:ss:mm");
        //调用format方法让模式格式化指定的Date对象
        String s=sdf.format(d);
        System.out.println(s);

        //获取月份，可以用sdf实现，但是若对年操作如加减，还需要类型转换，若含非十进制的字符，还转换不了，麻烦
        SimpleDateFormat sdf1=new SimpleDateFormat("MM");
        String s1=sdf1.format(d);

        int month=Integer.parseInt(s1);
        System.out.println(s1); 
        //Calendar
        Calendar cal=Calendar.getInstance();//返回的是GregorianCalendar，很好理解，Calendar抽象，返回此抽象类的子类   
        //System.out.println(cal);
        System.out.println(cal.get(Calendar.YEAR)+"年");
        System.out.println((cal.get(Calendar.MONTH)+1)+"月");
        System.out.println(cal.get(Calendar.DAY_OF_MONTH)+"日");
        System.out.println("星期"+cal.get(Calendar.DAY_OF_WEEK));

        System.out.println("-----------------------");

        //查表法：大写的月份数字
        //美国月份0-11，星期是星期日为第一天，1-7
        String[] s2= {"一月","二月","三月","四月","五月","六月","七月","八月","九月","十月","十一月","十二月"};
        String[] weeks= {"","星期日","星期一","星期二","星期三","星期四","星期五","星期六"};//0号没元素，所以用空表示，否则还得加减

        System.out.println(cal.get(Calendar.YEAR)+"年");
        String mon=s2[cal.get(Calendar.MONTH)];
        System.out.println(mon);
        String day=weeks[cal.get(Calendar.DAY_OF_WEEK)];
        System.out.println(cal.get(Calendar.DAY_OF_MONTH)+"日");
        System.out.println(day);

        System.out.println("-----------------------");

        //设置时间
        cal.set(2015, 4, 1);
        System.out.println(cal.get(Calendar.YEAR)+"年");
        String mon1=s2[cal.get(Calendar.MONTH)];
        System.out.println(mon1);
        String day1=weeks[cal.get(Calendar.DAY_OF_WEEK)];
        System.out.println(cal.get(Calendar.DAY_OF_MONTH)+"日");
        System.out.println(day1);

        System.out.println("-----------------------");

        //指定字段加减
        cal.add(Calendar.YEAR, +2);//向后加2年
        System.out.println(cal.get(Calendar.YEAR)+"年");

        cal.add(Calendar.DAY_OF_WEEK, -1);
        String day11=weeks[cal.get(Calendar.DAY_OF_WEEK)];
        System.out.println(day11);


    }

}

//联系求任意一年的二月有多少天
//获取任意年的2月几天
    /*
     * 思路：先根据Calendar获得当前时间，
     *       然后根据set(year,2,1)//某一年的3月1日
     *       然后用add减去1天，再获得日期即可。
     */
    public static  int getFeb(int year) {
        Calendar  cal=Calendar.getInstance();

        cal.set(year,2,1);
        cal.add(Calendar.DAY_OF_MONTH, -1);
        return cal.get(Calendar.DAY_OF_MONTH);


    }

```



```java
/*
java中对日期的处理
   这个案例最主要掌握：
       知识点1：怎么获取系统当前时间
       知识点2：String -> Data
       知识点3：Date -> String
*/

import java.util.*;//(Date类中)
import java.text.SimpleDateFormat;
public class DateTest01{
    public static void main(String[] args){
        //获取系统当前时间（精确到毫秒系统当前时间）
        //直接调用无参数构造方法就行
        Date nowTime = new Date();
        /*
           java.util.Date类的toString()方法已经被重写了。
           SimpleDateFormat是java.txt包下的，专门负责日期格式化的。
           yyyy 年（4位）
           MM 月（2位）
           dd 日（2位）
           HH 时（2位）
           mm 分（2位）
           ss 秒（2位）
           SSS 毫秒（3位，最高999，当1000代表1秒）
        
        */
        System.out.println(nowTime);
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy - MM - dd HH: mm : ss SSS");
        String nowTimeStr = sdf.format(nowTime);
        System.out.println(nowTimeStr);
        
        //假设现在有一个日期字符串String,怎么转换成Date类型？
        String time = "2008-08-08 08:08:08 888";
        SimpleDateFormat sdf2 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
        //("格式不能随便乱写，要和日期字符串格式相同");
        Date dateTime = sdf2.parse(time);
        System.out.println(dateTime);
    }
}

```

```java
/*
  获取自1970年1月1日 00：00：00 000 到当前系统时间的总毫秒数。
1秒 = 1000毫秒
  简单总结一下，java.lang包下的System类的相关属性
     System.out[out是System类的静态变量]
     System.out.println() 【println()方法不是System类的，是PrintStream类的方法】
     System.gc()建议启动垃圾回收器
     System.currentTimeMillis()//获取自1970年1月1日到系统当前时间的总毫秒数
     System.exit(0) 退出JVM。

*/
public class DateTest02{
    public class void main(String[] args){
        //获取自1970年1月1日00:00:00 000到当前系统时间的总毫秒数
        long nowTimeMillis = System.currentTimeMillis();//(过1s就加1000)
        System.out.println(nowTimeMills);
        
        //统计一个方法耗时
        //在调用目标之前记录一个毫秒数
        long begin = System.currentTimeMillis();
        print();
        //在执行完目标方法后记录一个毫秒数
        long end = System.currentTimeMillis();
        System.out.println(”耗费时长 “ + (end - begin) + "毫秒");
    }
    
    public static void print(){
        for(int i = 0; i < 1000;i++){
            System.out.println("i = " + i);
        }
    }
}
```

```java
/*
通过毫秒构建Date对象

*/
public class DateTest03{
    public static void main(String[] args){
        //这个时间是什么时间？
        //1970-01-01 00:00:00 001
        Date time = new Date(1); //注意参数是一个毫秒
        SimpleTimeFormat sdf = new SimpleTimeFormat("yyyy-MM-dd HH:mm:ss SSS");
        String strTime = sdf.format(time);//1970-01-01 00:00:00 001
        System.out.println(strTime);
        
        //获取昨天的此时的时间(当前时间 - 一天的时间，包括毫秒数)
        Date time2 = new Date(System.currentTimeMills() - 1000 * 60 * 60 * 24);
        String strTime2 = sdf.format(time2);
        System.out.println(strTime2);
    }
}
```



### 4、number

#### 1、数字格式化

```java
/*
数字格式化有哪些？
   # 代表任意数字
   , 代表千分位
   . 代表小数点
   0 表示不够时补0
   
   ###,###.##
     表示：加入千分位，保留2个小数

*/
import java.text.DecimalFormat;
public class DecimalTest01{
    public static void main(String[] args){
        DecimalFormat df = new DecimalFormat("###,###.##");
        String s = df.format(1234,24131);//1,234,12
        System.out.println(s);
        
        DecimalFromat df2 = new DecimalFormat("###,###,0000");
        String s2 = df2.format(1234,56);//1,234,5600
        System.out.println()
    }
}
```

#### 2、高精度

```java
/*
 1、BigDecimal 属于大数据，精度极高，不属于基本数据类型，属于java对象（引用数据类型）
 2、财务软件中double是不过的，
    当别人问你处理过财务数据吗？用的那种类型？
     千万别说double ,说java.math.BigDecimal
*/
import java.math.BigDecimal;
public class BigDecimalTest01{
    public static void main(String[] args){
        //这个100不是普通的100,是精度极高的100
        BigDecimal v1 = new BigDecimal(100);
        //这个是精度极高的200
        BIgDecimal v2 = new BigDecimal(200);
        //求和（调用此类的加减乘除的方法）
        BigDecimal v3 = v1.add(v2);
        System.out.println(v3);
        
        BigDecimal v4 = v2.divide(v1);
        System.out.println(v4);
    }
}
```



### 5、产生随机数

```java
/*

*/
import java.util.Random;
public class RandomTest01{
    //创建随机数
    Random random = new Random();
    //随机产生一个int类型取值范围内的数字
    int num1 = random.nextInt();
    System.out.println(num1);
    //产生【0~100】之间的随机数，不能产生101
    //nextInt翻译为：下一个int类型的数据是101，表示只能取到100
    //例如以下
    int bum2 = random.nextInt(101);
    System.out.println(num2);
}
```

```java
/*
  编写程序：生成5个不重复的随机数，重复的话重新生成
  最终生成5个随机数放到数组中，要求数组中5个随机数不重复

*/
public class RandomTest02{
    public static void main(String[] args){
        //创建5个对象
        Random random = new Random();
        //准备一个长度为5的一维数组
        int[] arr = new int[5];//默认都是0
        for(int i = 0; i < arr.length; i++){
            arr[i] = -1;
        }
        
        //循环生成随机数
        int index = 0;
        while(index < arr.length){
            int num = random.nextInt(101);
            //判断arr数组中有没有出现这个num
            //如果没有这个num,就放进去
            if(!contains(arr,num)){
                arr[index++] = num;
            }
        }
        
        //遍历以上数组
        for(int i = 0; i < arr.length;i++){
            System.out.println(arr[i]);
        }
    }
    //单独编写一个方法，专门判断数组中是否包含了某个元素
    public static boolean contains(int arr[], int key){
        for(int i = 0; i < arr.length; i++){
            if(arr[i] == key){
                return false;
            }
        }
        return true;
    }
}
```

### 6、枚举

```java
/*
总结：
    1、枚举是一种引用数据类型
    2、枚举类型怎么定义，语法是
       enum 枚举类型名{
          枚举值1，枚举值2……;
       }
    3、结果只有两种情况的，建议使用布尔类型
       结果超过两种，并且还是可以一枚一枚列举出来的，建议使用枚举类型
       例如：颜色，四季，星期等
*/
public class EnumTest01{
    public static void main(String[] args){
        Result r = divide(10,2);
        System.out.println(r == Result.SUCCESS?"计算成功":"计算失败");
    }
    //两种情况建议使用枚举，两种以上的情况建议使用enum
    //不建议商用int,因为并不是只能表示两种状态
    public static boolean divide(int a, int b){
        try{
            int c = a/ b;
            return Result.SUCCESS;
        }catch (Exception e){
            return Result.FAIL;
        }
    }
}
enum Result{
    //SUCCESS 是枚举类型中的一个值
    //FAIL是枚举Result类型中的一个值
    //枚举中的每个值，可以看作是”常量“
    SUCCESS,FAIL;
}
```

### 7、System类

```markdown
一、System类（final）
   1、包含一些有用的类字段和方法，它不能被实例化。
       它不能实例化的原因是：没有构造函数。
   2、System类中的方法和属性都是静态的
      out：标准输出，默认是控制台
      in：标准输入，默认是键盘
   3、获取系统属性信息：
      public static Properties getProperties()（所有属性）
      public static String getProperty(String key)（获取指定键的值）
      若没有该键，则返回null
   4、设置系统键值对（可以添加新的，也可以重置旧值）（获取系统所有的属性和属性值）
      public static String setProperty(String key, String value)

```

### 8、Runtime类

```java
/*
单例设计模式

没有构造函数，说明不能new建立对象，

可以直接想到该类中的方法都是静态的，但是此类的方法中含有非静态的（说明：这些方法必须得该类对象调用），说明这个类对象要通过方法获取，并且该方法的返回值为Runtime类型，并且该方法被静态所修饰。

public static Runtime getRuntime()：返回与当前Java应用程序相关的运行时对象，说明Java应用程序启动，JVM就自动创建了对象，只要获取就可以了，没必要手动新建，也新建不了。
这也是单例设计模式的应用，保证了一个该类只有一个对象。
*/
public static void main(String[] args)throws Exception {
    Runtime rt=Runtime.getRuntime();
    Process p=rt.exec("notepad.exe");//打开记事本工具
    Thread.sleep(4000);//4秒后
    p.destroy();//杀死这个进程；
}


```

### 9、Math类

```java
/*
  1、public static double ceil(double a)：返回大于等于a的最小值。
     a=16.52 返回值为：17.0
     a=-15.21 返回值为：-15.0
     a=16 返回值为：16.0
  2、public static double floor(double a)：返回小于等于a的最大数
     a=16.52 返回值为：16.0
     a=-15.21 返回值为：-13.0
     a=16 返回值为：16.0
  
  3、public static long round(double a)：返回最接近a的整数（四舍五入）
     a=16.52 返回值为：17
     a=16.12 返回值为：16
     a=16 返回值为：16

   4、public static double pow(double a, double b)
      a—底数 b—指数 返回a^b：a的b次幂
 
   5、public static double random()
      返回：大于等于0.0且小于1.0的伪随机double值（近似均匀分布）
      <随机数类Random>

*/
//输出1-6的整数(骰子)
        for(int i=0;i<10;i++) {
            int  m=(int)((Math.random()*6)+1);
            System.out.println(m);
        }
```

```java
/*
常用静态方法
  1、public static int abs(int a) 返回参数的绝对值
  2、public static double ceil(double a)返回大于参数的最小整数
  3、public static double floor(double a)返回小于参数的最大整数
  4、public static long round(double a) 四舍五入
  6、public static float max(float a, float b)饭hi两个数的较大值
  7、public static double min(double a, double b) 返回两个数的较小值
  8、public static double random() 返回一个大于等于0.0小于1.0的随机小数
*/
public class MathTest{
    public static void main(String[] args){
        System.out.println("计算绝对值后的结果"+Math.abs(-1));
        System.out.println("大于参数的最小整数"+Math.ceil(5.6);
        System.out.println("小于参数的最大整数"+Math.floor(5.6);
        System.out.println("小数四舍五入后的结果"+Math.round(5.6); 
        System.out.println("求两个数的较大值"+Math.max(2.1,4.5));
        System.out.println("求两个数的较小值"+Math.min(2.1,5.6));
        System.out.println("生成一个大于等于0.0小于等于1.0的随机数"+Math.random());
    }
}
```







## 5、异常

```java
1、Error异常和Exception异常都继承于throwable异常类。
   
    throwable异常类下面分为两个子类：error异常（又名系统异常）和Exception异常（编码，环境，操作异常）

    
2、Error异常
    是系统异常(也叫做非检查异常，源码注释：That is, {@code Error} and its subclasses are regarded as unchecked exceptions for the purposes of compile-time checking of exceptions.)，主要包括虚拟机错误（virtualmachineError）、线程死锁（threaddeth）。一旦出现Error异常就代表着程序崩溃了，可将其看作程序的终结者。

3、Exception异常
    包括两个大类：运行时检查异常（RuntimeException）和编译时异常；RuntimeException异常包含以下四种常见异常：空指针异常，数组下标越界异常、类型转换异常、算术异常，由java虚拟机自动抛出和自动捕获；检查异常：主要是一些文件异常，日志异常，sql异常，和一些需要我们人为干预的异常。检查异常，需要手动添加异常的捕获和处理
    
4、所以：throwable的直接父类是Object
```









### 1、基本语法

```java
/*
1、什么是异常，java异常处理机制的作用
   以下程序执行过程中发生了不正常的情况，而这种不正常的情况叫做:异常
   java语言是很完善的语言，提供了异常的处理方式，以下程序执行过程中出现了不正常情况﹐java把该异常信息打印输出到控制台，供程序员参考。程序员看到异常信息之后，可以对程序进行修改，让程序更加的健壮。
   什么是异常：程序执行过程中的不正常情况
   异常的作用：增强了程序的健壮性。
   
2、以下程序执行控制台出现了:
Exception in thread "main" java.Lang.ArithmeticException: / by zero
at com.bjpowernode.javase.exception.ExceptionTest01.main(ExceptionTest01.java:14)这个信息被我们称为:异常信息。这个信息是JVM打印的。

*/
public class ExceptionTest01{
    public static void mian(String[] args){
        int a = 10;
        int b = 0;
        //实际上JVM在执行到此处的时候，会new异常对象：new ArithmeticException("/ by zero");
        //并且JVM将new异常对象抛出，打印输出信息到控制台了
        int c = a / b;
        System.out.printnl(a + " / " + b " = " + c);
        //我们观察过异常信息后，对程序进行修改，更加健壮
        /*
        int a = 10;
        int b = 0;
        if(b == 0) {
           System.out.println("0");
           return;
         }else{
           int c = a / b;
           System.out.printnl(a + " / " + b " = " + c);
         }
        
        */
    }
}
```

```java
/*
java语言中异常是以什么形式存在的呢？
    1、异常在java语言中以类的形式存在的，每一个异常类都可以创建一个异常对象
java语言中异常是以什么形式存在的呢?
    2、异常在java中以类的形式存在，每一个异常类都可以创建异常对象。
    3、异常对应的现实生活中是怎样的?
       火灾(异常类):
          2008年8月8日,小明家着火了（异常对象)
          2008年8月9日,小刚家着火了（异常对象)
          2008年9月8日,小红家着火了(异常对象)
       类是:模板。
       对象是:实际存在的个体。
       
       钱包丢了（异常类) :
          2008年1月8日，小明的钱包丢了(异常对象)
          2008年1月9日，小芳的钱包丢了(异常对象)
          ....
*/
public class ExceptionTest02{
    public static void main(String[] args){
        //通过”异常类“实例化”异常对象“
        NumberFormatException nfe = new NumberFormatException("数字格式化异常");
        System.out.println(nfe);
        
        //通过”异常类“创建”异常对象“
        NullPointerException npe = new NullPointerException("空指针异常");
        System.out.println(npe);
    }
}
```

```java
/*
1、 java的异常处理机制
    1.1、异常在java中以类和对象的形式存在
    1.2、编译时异常和运行时异常，都是发生在运行阶段。编译阶段异常是不会发生的。编译时异常因为什么而得名?
         因为编译时异常必须在编译(编写)阶段预先处理，如果不处理编译器报错，因此得名。
         所有异常都是在运行阶段发生的。因为只有程序运行阶段才可以new对象。
         因为异常的发生就是new异常对象。
         
   1.3、编译时异常和运行时异常的区别?
      编译时异常一般发生的概率比较高。
        举个例子:
        你看到外面下雨了，倾盆大雨的。
        你出门之前会预料到:如果不打伞，我可能会生病（生病是一种并常）。而且这个异常发生的概率很高，所以我们出门之前要拿一把伞。
        " 拿一把伞"就是对w生病异常"发生之前的一种处理方式。
        对于一些发生概率较高的异常，需要在运行之前对其进行预处理。
        
     运行时异常一般发生的概率比较低。
       举个例子:
       小明走在大街上，可能会被天上的飞机轮子砸到。被飞机轮子砸到他算一种异常。
       但是这种异常发生概率较低。
       在出门之前你没必要提前对这种发生概率较低的异常进行预处理。如果你预处理这种异常，你将活的很累。
  1.4、编译时异常还有其它名字：
     受检异常：checkedException
     受控异常
     
  1.5、运行时异常还有其它名字：
     未受检异常：UnCheckedException
     未受控异常
     
  1.6、再次强调：所有的异常都是发生在运行阶段的。
*/

```

```java
/*
1.7、 java语言中对异常处理包括两种方式：
      第一种方式：在方法声明的位置上，使用throws关键字，抛给上一级
      第二种方式：使用try……catch语句进行异常的捕捉
      
      举个例子:
        我是某集团的一个销售员，因为我的失误，导致公司损失了1000元,
        "损失1000元"这可以看做是一个异常发生了。我有两种处理方式，
        第一种方式:我把这件事告诉我的领导【异常上抛】
        第二种方式:我自己掏腰包把这个钱补上。【异常的捕捉】
            张三-->李四--->王五-->CEO
     思考:
        异常发生之后，如果我选择了上抛，抛给了我的调用者，调用者需要对这个异常继续处理，那么调用者处理这个异常同样有两种处理方式.
        
1.8、注意:Java中异常发生之后如果一直上抛，最终抛给了main方法，main方法继续向上抛，抛给了调用者JVM,JVM知道了这个异常，只有一个结果，终止java程序的执行。

*/
public class ExceptionTest03{
    public static void main(String[] args){
        /*
        程序执行到此处发生了AritAmeticException异常，底层new了一个ArithmeticException异常
        对象，然后抛出了，由于是main方法调用了100 / 0 ,
        所以这个异常ArithmeticException抛给了main方法，main方法没有处理，
        将这个异常自动抛给了JVM。
        JVM最终终止程序的执行。
        ArithmeticException继承RuntimeException，属于运行时异常。
        在编写程序阶段不想要对这种异常进行预先的处理。
        
        */
        System.out.println(100/0);
        //这里的helloWorld没有输出，没有执行
        System.out.println("Hello World!");
    }
}
```

```java
public class ExceptionTest04{
    public static void main(String[] args){
        //main方法中调用doSome()方法
        //因为doSome()方法声明位置上有：throws ClassNotFoundException
        //我们在调用doSome()方法的时候必须对这种异常进行预先的处理。
        //如果我们不处理，编译器就会报错
        doSome();
    }
    /*
    doSome()方法在方法声明位置上使用了：throws ClassNotFoundException
    这个代码表示doSome()方法在执行的时候，有可能会出现ClassNotFoundException异常
    叫做类没找到异常，这个异常直接父类是：Exception,所以ClassNotFoundException属于编译时异常
    
    */
    public void doSome() throws ClassNotFoundException{
        System.out.println("doSome!!!");
    }
}
```

```java
public class ExceptionTest05{
    //第一种处理方式：在方法声明的位置上继续使用：throws来完成异常的继续上抛，抛给调用者
    //上抛类似于推卸责任（继续包异常传递给调用者）
    /*
    public static void main(String[] args) throws ClassNotFoundException{
        doSome();
    }*/
    
    //第二种处理方式：try……catch进行捕捉
    //捕捉等于把异常拦下来了，异常真正的解决了（调用者时不知道的）
    public static void main(String[] args){
        try{
            doSome();
        } catch(ClassNotFoundException){
            e.printStackTrace();
        }
    }
    public void doSome() throws ClassNotFoundException{
        System.out.println("doSome!!!");
    }
}
```

```java
/*
处理异常的第一种方式：在方法声名的位置上使用throws关键字抛出，谁调用我的这个方法，我就跑给谁，抛给调用者来处理
   运行时异常的态度：在编译时，可以抛出异常，或这捕捉异常，但是编译器不会对次进行任何处理
   而编译时异常，之要发生，就必须对其进行处理，否则报错
   
注意：   
    只要异常没有捕捉，采用上报的方式，此方法的后续代码不会执行。
    另外需要注意的是，try语句块中某一行出现异常，改行后面的代码不会执行
    try..catch捕捉异常之后，后续的代码可以执行。
*/
import java.io.FileInputStream;
public class ExceptionTest06 {
    //一般不建议在main方法上使用throws，因为这个异常如果真正的发生了，一定会抛给JVM，JVM只有终止.
    //异常处理机制的作用就是增强程序的健壮性，怎么能做到，异常发生时也不影响程序的执行，所以
    //一般main方法中的异常建议使用try……catch进行捕捉，main就不要继续往上抛了。
    //public static void main(String[] args) throws Exception{
    public static void main(String[] args) {
        System.out.println("main begin");
        try{
            //try尝试
            m1();
            //以上代码出现异常直接进入catch语句块中执行
            System.out.println("hello world!");
        }catch (FileNotFoundException e){
            //catch是捕捉异常以后走的分支
            //这个分支中可以使用e引用，e引用保存的内存地址是哪个new出来的异常对象的内存地址。
            //catch在分支中是处理异常的
            System.out.println("文件不存在，可能路径错误，也可能该文件被删除了！");
        }
        //try……catch把异常抓住之后，这里的代码会继续执行。
        System.out.println("main over");
    }
    //Exception时所有异常的父类
    private static void m1() throws Exception{
        System.out.println("m1 begin");
        m2();
        System.out.println("m1 over");
    }
    
    //只能抛FileNotFoundException的父对象，像->IOExcption或者该FileNotFoundException本身
    //抛出也可以抛出多个异常，且异常与异常之间用逗号隔开
    private static void m2() throws IOException{
        System.out.println("m2 begin");
        //对m3要么进行捕捉，终止上抛，要么不断往上抛
        m3();
        //以上代码出现异常，这里是无法执行的。
        System.out.println("m2 over");
    }
    
    private static void m3() throws FileNotFoundException{
        //调用SUN jdk种某个类的构造方法
        //这个类还没有接触过后期IO流就知道了
        //我们只是借助这个类学习一下，该流指向一个文件
        //我们采用第一种方式，在方法声明位置上使用throws继续上抛
        //一个方法体当中的代码出现异常之后，如果上报的话，此方法结束。
        new FileInputStream("C:\\Users\\28929\\Desktop\\ACM作业");
        
    }
    
}
```

```java
/*
深入try..catch
   1、catch后面的小括号中的类型可以是具体异常类型，也可以是异常类型的父类型
   2、catch可以写多个，建议catch的时候，精确的一个一个处理，这样有利于程序的调试
   3、catch写多个的时候，从上到下，必须遵守从小到大，因为从大到小的话，像父类一定会有子类，所以后面小的根本执行不到，所以会报错
*/
public class ExceptionTest07{
    public static void main(String[] args){
        try{
            FileInputStream fis = new FileInputStream("C:\\Users\\28929\\Desktop\\ACM作业");
        } catch (FileNotFoundException e){
            System.out.println("文件不存在");
        } catch(IOException e){
            System.out.println("读文件报错了");
        }
        System.out.println("hello world");
    }
    /*
    从大到小，编译报错
    try{
            FileInputStream fis = new FileInputStream("C:\\Users\\28929\\Desktop\\ACM作业");
        } catch (IOException e){
            System.out.println("文件不存在");
        } catch(FileNotFoundException e){
            System.out.println("读文件报错了");
        }
        System.out.println("hello world");
    }
    
    */
}
```

```java
/*
以后的开发中，处理编译时异常，应该采用上报还是捕捉呢，怎么选则？
   如果希望调用者来处理，选则throws上报，只有这一个标杆。
   其它使用捕捉的方式

运行时异常，既不需要上报，也不需要捕捉
*/
public class ExceptionTest07{
    public static void main(String[] args){
        //JDK8的新特性，允许或的符号来判断多个异常
        try{
            FileInputStream fis = new FileInputStream("C:\\Users\\28929\\Desktop\\ACM作业");
        } catch (FileNotFoundException | ArithmeticException | NullPointerException e){
            System.out.println("文件不存在?数字异常？空指针异常?都有可能！");
        } 
        System.out.println("hello world");
    }
    
}
```

### 2、异常对象的常用方法

```java
/*
  异常对象有两个常用的非常重要的方法
     获取异常简单的描述信息
     String msg = exception.getMessage();
     
     打印异常追踪的堆栈信息：
       exception.printStackTrace();

*/
public class ExceptionTest08{
    public static void main(String[] args){
        NullPointerException e = new NullPointerException("空指针异常");
        String msg = e.getMessage();//空指针异常
        System.out.println(msg);
        
        //打印1异常堆栈信息
        //java后台异常堆栈追踪信息的时候，采用异步线程的方式打印的
        e.printStackTrace();
        System.out.println("hello World");
    }
}
/*
异常对象的追踪喜喜，我们因该怎么看，可以快速调式程序？
   异常信息追踪信息，从上往下一行一行的看
   但是注意的是：SUM写的代码就不用看了（看包名就知道是自己写的还是SUN的）
   主要问题是出现在自己编写的代码上，第一场给出出错的行号，在这行找出问题就好。。


*/
```

### 3、finally关键字

```java
/*
关于try..catch中的finally子句
   1、在finally子句中的代码是最后执行的，并且一定会执行的，即使try语句块中代码出现了异常
      finally子句必须和try一起出现，不能单独编写
      
   2、finally语句通常使用在哪些情况下？
     通常在finally语句块中完成资源的释放/关闭
     因为finally中的代码比较有保证
     即使try语句中的代码出现异常，finally中代码也会正常执行。
*/
public class ExceptionTest09{
    public static void main(Stirng[] args){
        FileInputStream fis = null;//声明位置放到try外面，这样在finally中才能使用。
        try{
            fis = new FileInputStream("C:\\Users\\28929\\Desktop\\ACM作业");
            String s = null;
            //这里一定会出现空指针异常
            s.toString();
            System.out.println("hello");
            //流使用完需要关闭，因为流是占用资源的
            //即使异常程序出现异常，流也必须关闭
            //放在这里有可能关闭不了
            //fis.close();
        } catch (FileNotFoundException e){
            e.printStackTrace();
        } catch(IOException e){
            e.printStackTrace();
        } catch(NullPointerException e){
            e.printStackTrace();
        } finally {
            //流的关闭放在这里比较保险
            //finally中的代码一定会执行的
            //即使try中出现了异常！
            if(fis != null){
                try{
                    //close方法有异常，采用捕捉的方式
                    fis.close();
                } catch {
                    e.printStackTrace();
                }
            }
        }
        System.out.println("hello kitty");
    }
}
```

```java
/*
finally语句。
*/
public class ExceptionTest11{
    public static void main(String[] args){
        /*
        try和finally，没有catch可以
          try不能单独使用
          try finally可以联合使用
        以下代码执行顺序
          先执行try……
          在执行finally……
          最后执行return(return语句只要执行方必然结束)
        */
        try{
            System.out.println("try……");
            return;
        }finally {
            System.out.println("finally...");
        }
        //这里不能写语句，因为这里是执行不到的
    }
}
```

```java
/*
finally中的语句什么时候不能用？
   退出JVM之后，finally语句中的代码就不执行了！
*/
public class ExceptionTest12{
    public static void main(String[] args){
        try{
            System.out.println("try……");
            //退出JVM
            System.exit(0);//退出JVM之后，finally语句中的代码就不执行了！
        }finally {
            System.out.println("finally...");
        }
    }
}
```

```java
/*
finally面试题
*/
public class ExceptionTest13{
    public static void main(String[] args){
        int result = m();
        System.out.println(result);//100
    }
    /*
    java语法规则（有一些规则是不能被破坏的，一旦这么说了就必须这么做）
      java中有这样一条规则：
         方法体中的代码必须遵循自上而下的顺序依次逐行执行（亘古不变的语法）
      java中还有这样一条语法规则：
         return 语句一旦执行，整个方法必须结束
    
    */
    public static int m(){
        int i = 100;
        try{
            //这行代码出现在int i = 100;的下面，所以最终结果必须返回的是100，尽管是i++先执行，但是程序确实依次向下编译的
            //reetun语句还必须保证最后执行的，一旦执行，整个方法结束。
            return i;
        } finally {
            i++;
        }
    }
}
/*
反编译之后的效果(保证了那两条更古不变的规则)
  public static int m(){
     int i = 100;
     int j = i;
     i++;
     return j;
  }
*/
```

### 4、final、finally、finalize区别

```java
/*
final关键字
   final修饰的类无法继承final修饰的方法无法覆盖
   final修饰的变量不能重新赋值。
finally关键字
   和try一起联合使用。
   finally语句块中的代码是必须执行的。
finalize标识符
   是一个object类中的方法名。
   这个方法是由垃圾回收器Gc负责调用的。

*/

public class ExceptionTest14{
    public static void main(String[] args){
        //final是一个关键字，表示最终的，不变的
        final int i = 100;
        
        //finally也是一个关键字，和try联合使用，使用在异常处理机制中
        //在finally语句块中的代码时一定会执行的
        try{
            
        } finally {
            System.out.println("finally....");
        }
        
        //finalize()是Object类中的一个方法，作为方法名出现
        //所以finalize是标识符
        
    }
}
```

### 5、自定义异常类

```java
/*
1、如何自定义异常
   两步：
      第一步：编写一个类继承Exception或者RuntimeException
      第二步：提供两个构造方法，一个无参的，一个带有String参数的
2、手动抛出异常
*/
public class MyException extends Exception{//编译异常
    public MyException(){
        
    }
    public MyException(String s){
        super(s);
    }
    
}
public class ExceptionTest15{
    public static void main(String[] args){
        //创建异常对象
        MyException e = new MyException("用户名不能为空");
        
        //打印异常堆栈信息
        e.printStackTrace();
        
        //获取异常简单描述信息
        String　msg = e.getMessage();
        System.out.println(msg);
    }
}
/*
如何使用异常：
   手动抛出
   public void pop() throws MyException(){
      if(index < 0){
         throw new MyException("弹栈失败，栈已经空");//手动抛出异常
      }
      //执行到这里说明栈没空
      System.out.println("弹栈" );
   }

*/
```

### 6、异常与方法覆盖

```java
//
/*
之前在讲解覆盖方法的时候，当时遗留了一个问题？
   重写之后的方法不能比重写之前的方法抛出更多(更宽泛)的异常，可以更少
   就是父类，有抛出，子类可抛，可不抛，可以抛出更小的异常
   父类不抛，子类就不能抛出（也可以抛运行异常）

*/
class Animal{
    public void doSome(){
        
    }
    public void doOther() throws Exception{
        
    }
}
class Cat extends Animal{
    //编译报错
    /*
    public void doSome() throws Exception{
     
    }
    */
    //编译正常
    /*
    public void doSome(){
    
    }
    public void doSome() throws Exception{
     
    }
    public void doSome() throws NullPointerException{
     
    }
    */
}
/*
总结异常中的关键字
  try
  catch
  finally

  throws //在方法声明的位置上使用，表示上报异常信息给调用者
  
  throw 手动抛出异常
*/
```



## 6、集合



### 1、集合语法

```java
/*
1、集合概述
   1.1、什么是集合?有什么用?
          数组其实就是一个集合。集合实际上就是一个容器。可以来容纳其它类型的数据。
        集合为什么说在开发中使用较多?
          集合是一个容器，是一个载体，可以一次容纳多个对象。在实际开发中，假设连接数据库，
          数据库当中有10条记录，那么假设把这10条记录查询出来，在java程序中会将10条数据封装
          成10个java对象，然后将10个java对象放到某一个集合当中，将集合传到前端，然后遍历
          集合，将一个数据一个数据展现出来。
   1.2、集合不能直接存储基本数据类型，另外集合也不能直接存储java对象，集合当中存储的都是java对象的内存地址。(或者说集合中存储的是引用。)
   
   注意:
        集合在java中本身是一个容器，是一个对象。集合中任何时候存储的都是"引用"。
  
   1.3、在java中每一不同的集合，底层会对应不同的数据结构，往往不同的集合中存储的元素，等于将数据放到了不同的数据结构当中。
       
   1.4、集合在java JDK中哪个包下？
        java.util.*
           所有的集合类和集合接口都在java.util包下
*/
```

### 2、集合继承结构图

![image-20210505214851269](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210505214851269.png)



### 3、Collection集合

#### 1、接口中常用的方法

```java
/*
关于java.util.Collection接口中常用的方法。
   1、Collection中能存放什么元素？
      没使用”泛型“之前，Collection中可以存储Object的所有子类型
      使用了”泛类型“之后，Collection中只能存储某个具体的类型
      集合后期我们会学习“泛型”，目前先知道Collection中什么都能存，
      只要是Object的子类型就行(集合中不能直接存基本数据类型，也不能存java对象，只是存储对象的内u内存地址）
      
   2、Collection中常用方法(下面每个孩子都可以用)
      boolean add(Object e) 向集合中添加元素
      int size() 获取集合中元素的个数
      void clear() 清空集合
      boolean contains(Object 0) 判断荡当前集合是否包含元素0
      
      boolean remove(Object 0) 删除集合中某个元素
      boolean isEmpty() 判断该集合中元素的个数是否为0
      object[] toArray() 调用这个方法可以把集合转换为数组
   3、子接口有List,Set
*/
public class CollectionTest01{
    public static void mian(String[] args){
        //创建一个集合对象
        //Collection c = new Collection();接口时抽象的，无法实例化
        //多态
        Collection c = new ArrayList();
        //测试Collection接口中常用的方法
        c.add(1200);//自动装箱，实际上是放进去了一个对象的内存地址，Integer x = new Integer(1200);
        c.add(3.14);//自动装箱
        c.add(new Object());
        c.add(new Student());
        
        //获取集合中元素的个数
        System.out.println("元素个数为：" + c.size());
        //清空集合
        c.clear();
        System.out.println("元素个数为：" + c.size());
        
        //在向集合添加元素
        c.add(1200);
        c.add(3.14);
        c.add("hello");//hello对象的内存地址放到了集合中
        c.add("绿巨人");
        
        //判断集合中是否包含了“绿巨人”
        boolean flag = c.contains("绿巨人");
        System.out.println(flag);
        
        //删除集合中的某个元素
        c.remove(1200);
        System.out.println("元素个数为：" + c.size());
        
        //判断集合中是否为空
        System.out.println(c.isEmpty());//false
        c.clear();
        System.out.println(c.isEmpty());//true
        
        c.add("abc");
        c.add("edf");
        c.add(1000);
        c.add(3.14);
        
        c.add(new Student()); //没有重写toString方法，所以输出的是内存地址
        Object[] obj = c.toArray();
        for(int i = 0; i < obj.length;i++){
            Object o = obj[i];
            System.out.println(o);
        }
    }
}
class Student{
    
}
```

#### 2、Collection集合迭代

```java
/*
关于集合遍历/迭代专题
    注意：以下的遍历方式/迭代方式，是所有Collection通用的一种方式，在Map集合中不能用，在所有的Collection以及子类中使用。
*/
public class CollectionTest02{
    public static void main(String[] args) {
        //创建集合对象
        Collection c = new ArrayList();//后面的集合无所谓，主要是看前面的Collection接口，怎么遍历/迭代
        //添加元素
        c.add("abc");
        c.add("def");
        c.add(100);
        c.add(new Object());
        //对集合Collection进行遍历
        //第一步：或取集合对象的迭代器对象Iterator
        Iterator it = c.iterator();
        //第二步：通过以上获取的迭代器对象开始迭代/集合遍历
        /*
           以下两个方法是迭代器对象Iterator中的方法：
             boolean hasNext() 如果仍可以迭代，则返回true
             Object next() 返回迭代的下一个元素
        
        */
        while(it.hasNext()){
            Object obj = it.next();
            System.out.println(obj);
        }
        
    }
}
```

![image-20210506111354269](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210506111354269.png)



![image-20210506112314198](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210506112314198.png)



```java
public class CollectionTest03{
    public static void main(String[] args) {
        //创建集合对象
        Collection c = new ArrayList();//ArrayList集合有序可重复
        //添加元素
        c.add(1);
        c.add(2);
        c.add(3);
        c.add(4);
        //对集合Collection进行遍历
        //第一步：或取集合对象的迭代器对象Iterator
        Iterator it = c.iterator();
        while(it.hasNext()){
           //存进去是什么类型，取出来还是什么类型
            Object obj = it.next();
            /*
            if(obj instanceof Integer){
                System.out.println("Integer类型");
            }
            */
            //只不过在输出的时候，会转成字符串
            System.out.println(obj);
        }
        
        Collection c1 = new HashSet();//HashSet集合无序不可重复
        //无序：存进去和取出的顺序不可重复
        c1.add(100);
        c1.add(200);
        c1.add(300);
        c1.add(200);
        Iterator it = c1.iterator();
        while(it.hasNext()){
            Object obj = it.next();
            System.out.println(obj);
            //System.out.println(it.next());
        }
    }
}
```

#### 3、深入contains方法

```java
/*
深入Collection集合contains方法：
   boolean contains(Object o)
      判断集合中是否包含某个对象0
      如果包含返回true,否则返回false     
   contains方法是用来判断集合中是否包含某个元素的方法，
   那么它在底层是怎样判断集合中是否包含某个元素的呢？
      调用了equals方法进行比对
      equals方法返回true,就表示包含这个元素。
*/
public class CollectionTest04{
    public static void main(String[] args){
        //创建集合对象
        Collection c = new ArrayList();
        //向集合中存储元素
        String s1 = new String("abc");
        c.add(s1);
        String s2 = new String("def");
        c.add(s2);
        System.out.println("元素个数为：" + c.size());
        
        //新建的对象String
        String x = new String("abc");
        System.out.pritln(c.contains(x));//包含
    }
}
```

![image-20210506115002998](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210506115002998.png)

```java
/*
结论：
    存放在一个集合中的类型，一定要重写equals方法。
*/
public class CollectionTest05{
    public static void main(String[] args){
        //创建集合对象
        Collection c = new ArrayList();
        //创建用户
        User u1 = new User("jack");
        c.add(u1);
        User u2 = new USer("jack");
        //判断集合中是否包含u2
        
        //没重写equals之前，这个结果是false,因为调用的是Object类中的equals,而Object类中的equals是用“==”比较的内存地址
        //System.out.println(c.contains(u2));//false
        
        //重写之后，一定为true
        System.out.println(c.contains(u2));
    }
}
class User{
    private String name;
    public User(){}
    public User(String name){
        this.name = name;
    }
    //重写equals方法
    public boolean equals(Object o){
        if(0 == null || !(o instanceof User)) return false;
        if(o == this) return true;
        User u = (User) o;
        return u.name.equals(this.name);
    }
}
```

#### 4、深入remove方法

```java
//跟contains原理一致，都是在底层调用equals方法
public class CollectionTest06{
    public static void main(String[] args){
        //创建集合对象
        Collection cc = new ArrayList();
        //创建用户
        User u1 = new User("jack");
        c.add(u1);
        User u2 = new USer("jack");
        //没重写之前删除不了u1,长度为1
        //重写之后，可以删除u1了
        System.out.println(c.remove(u2));//长度为0
        System.out.println(c.size());
    }
}
class User{
    private String name;
    public User(){}
    public User(String name){
        this.name = name;
    }
    //重写equals方法
    public boolean equals(Object o){
        if(0 == null || !(o instanceof User)) return false;
        if(o == this) return true;
        User u = (User) o;
        return u.name.equals(this.name);
    }
}
```

#### 5、关于集合元素中的删除

```java
/*
关于集合元素remove
    重点：当集合的结构发生改变时，迭代器必须重新获取，如果还是用以前的老迭代器，会出现异常
    java.util.ConcurrentModificationException
    
    重点：在迭代元素的过程当中，一定要使用迭代器Iterator的remove方法，删除元素
         不要使用集合自带的remove方法删除元素
*/
public class CollectionTest06{
    public static void main(String[] args){
        //创建集合
        Collection c = new ArrayList();
        //注意:此时获取的迭代器，指向的是那是集合中没有元素状态下的迭代器。
        //一定要注意:集合结构只要发生改变，迭代器必须重新获取。
        /*当集合结构发生了改变，迭代器没有重新获取时，
          调用next()方法时 : java.util.ConcurrentNodificationException*/
        Iterator it = c.iterator();
        //添加元素（之后必须重新获取迭代器）
        c.add(1);//Integer
        c.add(2);
        c.add(3);
        c.add(4);
        //
        Iterator it = c.iterator();
        while(it.hasNext()){
            Object obj = it.next();
            System.out.println(obj);
        }
        
        Collection c2 = new ArrayList();
        c2.add("abc");
        c2.add("def");
        c2.add("xyz");
        Iterator it2 = c2.iterator();
        while(it2.hasNext()){
            Object o = it2.next();
            //删除元素
            //删除元素之后，集合的结构发生改变应该重新获取迭代器
            //但是循环下一次的时候，并没有重新获取迭代器，所以会出现异常
            //出现异常的根本原因是：集合中的删除元素，没有通知迭代器。
            //c2.remove(0);//直接通知集合去删除元素，没有通知迭代器（导致迭代器的快照和原集合的状态不同）
            //使用迭代器来删除
            //使用迭代器去删除时，会自动更新迭代器，并且更新集合（删除集合中的元素）
            it2.remove(o);
            System.out.println(o);
        }
        System.out.println(c2.size());//0
    }
}
```

### 4、List接口特有方法

```java
/*
测试List接口中常用的方法
    1、List集合存储元素的特点：有序可重复
       有序：List集合中国的元素有下标
       可重复：存储一个1，还可以在存储一个1
    2、List既然时Collection接口的子接口，肯定有自己特有的方法
      一下只列出List接口特有的常用的方法
         void add(int index, Object element);
         Object get(int index)
         int indexOf(Object o)
         int lastIndexOf(Object o)
         Object remove(int index)
         Object set(int index, Object element)
    3、子类为：ArrayList,LinkedList,Vevtor
*/
public class ListTest01{
    public static void main(String[] args){
        List myList = new ArrayList();
        //添加元素
        myList.add("A");//默认都是向集合末尾添加元素
        myList.add("B");
        
        //在列表的指定位置插入指定元素
        myList.add(1,"King");
        
        //迭代
        Iterator it = myList.iterator();
        while(it.hasNext()){
            Object o = it.next();
            System.out.println(o);
        }
        
        //根据下标获取元素
        Object firstObj = myList.get(0);
        System.out.println(firstObj);
        
        //因为有下标,所以List集合有字符比较特殊遍历方式
        //通过下标遍历【List集合特有的方式，Set没有】
        for(int i = 0; i < myList.size();i++){
            Object obj = myList.get(i);
            System.out.println(obj);
        }
        
        //获取指定对象第一次出现处的索引->下标
        System.out.println(myList.indexOf("KING"));
        
        //获取指定对象最后一次出现处的索引->下标
        System.out.println(myList.lastIndexOf("D"));
        
        //删除指定下标位置的元素
        myList.remove(0);
        System.out.println(myList.size());
        
        //修改执行位置的元素
        myList.set(2,"SOFT");
        //遍历集合
        for(int i = 0 ;i < myList.size();i++){
            Object obj = myListt.get(i);
            System.out.println(obj);
        }
        
    }
}
```

### 5、ArrayList集合

```java
/*
ArrayList集合：(数组)非线程安全的
   1、默认初始化容量为10(底层先创建了一个长度为10的数组，当添加第一个元素的时候，初始化容量为10)
   2、集合底层是一个Object[]数组
   3、构造方法：
      new ArrayList();
      new ArrayList(20);
   4、扩容是原容量的1.5倍。
      AraayList集合底层是数组，怎么优化?
         尽可能少的扩容，因为数组扩容效率比较低，建议在使用ArrayList集合的时候，预估计元素的个数，给定一个初始化容量。
         
    5、数组优点：
       检索效率比较高
       无法存储大数据量
    6、数组缺点：
       随机增删元素比较低
       
    7、面试官经常问这么多集合，你用哪个集合最多？
       ArrayList集合
       因为往数组末尾添加元素，效率不受影响
       另外，我们检索/查找某个元素的操作比较多
*/
```

### 6、ArrayList另一种构造方法

```java
/*
集合ArrayList构造方法
*/
public class ArrayTest01{
    public static void main(String[] args){
        //默认容量为10
        List myList1 = new ArrayList();
        
        //指定初始化容量为100
        List myList2 = new ArrayList(100);
        
        //创建一个HashSet集合
        Collection c = new HashSet();
        //添加容量到set集合
        c.add(100);
        c.add(200);
        c.add(900);
        c.add(50);
        //通过这个构造方法，就可以把HashSet()集合转为List集合
        List myList3 = new ArrayList(c);
        for(int i = 0; i< myList3.size();i++){
            System.out.println(myList3.get(i));
        }
    }
}
```

### 7、单向链表数据结构

```java
/*
每个结点都有两个属性：
    一个属性：是存储的数据
    一个属性：是下一个结点的内存地址
*/
public class Node{
    //存储的数据
    Object element;
    //下一个结点的内存地址
    Node next;
    public Node(){
        
    }
    public Node(Object element, Node next){
        this.element = element;
        this.next = next;
    }
}
public class Link {
    //头节点
    Node header = null;
    //向链表中添加元素的方法
    public void add(Object data){
        if(header == null){
            
            header = new Node(data,null);
        } else {
            //添加到末尾
            Node currentLastNode = findLast(header);
            currentLastNode.next = new Node(data,null);
        }
    }
    
    //专门查找末尾结点放方法
    private Node findLast(Node node){
        if(node.next == null){
            return node;
        }
        return findLast(node.next);
    }
}
/*
链表优点：随机增删元素效率较高（不涉及大量元素的位移）
链表缺点：查询效率较低，每一次查找某个元素的时候，都需要从头节点开始往下遍历

*/
```

### 8、LinkedList(双向链表)

```java
//链表（线程安全的）
import java.util.LinkedList;
import java.util.List;
public class LinkListTest01{
    public static void main(String[] args){
        //LinkedList集合底层也是有下标的
        //注意ArrayLIst之所以检索效率高不是因为单纯的下标的原本，是因为底层数组发挥作用
        //LinkedList集合照样有下标，但是检索/查找某个元素的时候效率比较低，只能从头节点开始一个一个遍历
        List list = new LinkedList();
        list.add("a");
        list.add("b");
        list.add("c");
        for(int i = 0; i < list.size(); i++){
            Object obj = list.get(i);
            System.out.println(obj);
        }
        //LinkedList集合没有初始化容量
        //最初这个链表没有任何元素，first合last引用都是null
        //不管LinkedList还是ArrayList,以后写代码时不需要关心具体是哪个集合
        //因为我们要面向接口编程，调用的都是接口中的方法
        //List list2 = new ArrayList(); //表示底层调用了数组
        List list2= new LinkedList();//表示底层调用了双向链表
        
        //这些方法都是面向接口编程
        list2.add("123");
        list2.add("4556");
        list2.add("879");
        for(int i = 0; i < list2.size(); i++){
            Object obj = list2.get(i);
            System.out.println(obj);
            //System.out.println(list2.get(i));
        }
    }
}
//ArrayList :把检索发挥到极致
//ListList:  把随机增删发挥到极致
```

### 9、Vector集合分析

```java
/*
Vector:
   1、底层也是一个数组
   2、初始化容量为：10
   3、怎么扩容？
      扩容之后，是原容量的2倍
      10 -> 20 -> 40
   4、Vector中所有方法都是线程同步的，都带有synchronized关键字，是线程安全的，效率比较低，使用比较少了
   
   5、怎么将一个线程不安全的ArrayList集合转换成线程安全的呢？
      使用集合工具类：
      java.util.Collections;
      java.util.Collection 是集合接口
      java.util.Collections 是集合工具类
      
*/
public class VectorTest{
    public static void main(String[] args){
        //创建一个Vector集合
        Vector vector = new Vector();
        
        //添加元素
        //默认容量为10个
        vector.add(1);
        vector.add(2);
        vector.add(3);
        vector.add(4);
        vector.add(11);
        vector.add(12);
        vector.add(13);
        vector.add(16);
        vector.add(163);
        vector.add(1631);
        
        //满了以后扩容
        vector.add(19);
        Iterator it = vector.iterator();
        while(it.hasNext()){
            Object obj = it.next();
            System.out.println(obj);
        }
        
        //这个可能以后要使用！！！
        List myList = new ArrayList();//非线程安全的
        //变成线程安全的
        Collections.synchronizedList(myList);
        myList.add("111");
        myList.add("222");
        myList.add("333");
    }
}
```

### 10、泛型

#### 1、基本语法

```java
/*
Generic:泛型

1、 泛型这种语法机制：只在程序编译阶段起作用，只是给编译器参考的
2、 使用泛型好处是
    第一：集合中存储的元素统一了
    第二：从集合中取出的元素是泛型指定的类型，不需要进行大量的“向下转型”

3、泛型缺点？
   导致集合中存储的元素却反多样性！
   大多数业务后，集合中的元素类型都是统一了
*/
public class CenericTest01{
    public static void main(String[] args){
        /*
        //不适用泛型机制，分析程序存在缺点
        List myList = new ArrayList();
        //准备对象
        Cat c = new Cat();
        Bird b = new Bird();
        
        //将对象添加到集合当中
        myList.add(c);
        myList.add(b);
        //遍历集合，取出Cat，和BIrd
        Iterator it = myList.iterator();
        while(it.hasNext()){
            Object obj = it.next();
            //通过迭代器只能取出的是Object,
            //Animal a = it.next();//不行，没这个语法
            //obj中没有move方法，无法调用，需要向下转型
            if(obj instanceof Animal){
                Animal a = (Animal)obj;
                a.move();
            }
            System.out.println(obj);
        }
        */
        //使用泛型之后List<Animal>之后，表示List集合中只允许存储Animal类型的数据
        //用泛型白指定集合中存储的数据类型
        List<Animal>myList = new ArrayList<Animal>();
        //指定List集合中只能存储Animal,那么存储String就编译报错了
        //这样用了泛型后，集合中元素类型就更加统一了
        Cat c = new Cat();
        Bird b = new Bird();
        myList.add(c);
        myList.add(b);
        //获取迭代器
        //迭代器迭代的是Animal类型
        Iterator<Animal> it = myList.iterator();
        while(it.hasNext()){
            //使用泛型之后，每一次迭代返回都是Animal类型
            //Animal a = it.next();
            //这里不要强制类型转换了
            //a.move();
            //调用子类型特有的方法还是需要向下转型的
            Animal a = it.next();
            if(a instanceof Cat){
                Cat x = (Cat)a;
                x.catchMouse();
            }
            if(a instanceof Bird) {
                Bird b = (Bird)a;
                b.fly();
            }
        }
    }
}
class Animal{
    public void move(){
        System.out.println("动物在移动");
    }
}
class Cat extends Animal{
    public void catchMouse(){
        System.out.println("猫抓老鼠");
    }
}
class Bird extends Animal{
    public void fly(){
        System.out.println("鸟儿在飞翔");
    }
}
```

```java
/*
JDK之后引入了：自动类型判断（又称钻石表达式）JDK8之后才允许的
*/
public class GenericTest02{
    public static void main(String[] args){
        //ArrayList<这里的类型会自动判断>()
        //自动类型判断，钻石表达式
        List<Animal>myList = new ArrayList<>();
        myList.add(new Animal());
        myList.add(new Cat());
        myList.add(new Bird());
        //遍历
        Iterator<Animal> it = MyList.iterator();
        while(it.hasNext()){
            Animal a = it.next();
            a.move();
        }
        
        List<String> strList = new ArrayList<>();
        strList.add("abd");
        strList.add("edf");
        System.out.println(strList.size());
        Iterator<String> it2 = MyList.iterator();
        while(it2.hasNext()){
            //直接通过迭代器获取String类型数据
            String s = it2.next();
            //直接调用String类的subString方法截取字符串
            String newString = s.substring(7);
            System.out.println(newString);
        }
    }
}
```

#### 2、自定义泛型

```java
/*
<自定义标识符,随便写>
   java源代码中经常出现的是E,T
   E是element单词首字母
   T是Type单词首字母
*/

public class GenericTest03<abc>{
    public void doSome(abd o){
        System.out.println(o);
    }
    
    public static void main(String[] args){
        GenericTest03<String> gt = new GenericTest03<>();
        gt.doSome("abc");
        
        GenericTest03<Integer> gt2 = new GenericTest03<>();
        gt2.doSome(100);
        
        MyIterator<String> mi = new MyIterator<>();
        String s1 = mi.get();
    }
}
class MyIterator<T> {
    public T get(){
        return null;
    }
}
```

### 11、foreach

```java
/*
JDK5.0之后退出了一个新特性：叫做增强for循环，或者叫foreach
*/
public class ForEachTest01{
    public static void main(String[] args){
        int[] arr = {431,31,55,14,46};
        //遍历数组(普通for循环)
        for(int i = 0; i < arr.length;i++){
            System.out.println(arr[i]);
        }
        //增强for循环(foreach)
        /*
        以下是语法
        for(元素类型 变量名 : 数组或集合){
            System.out.println(变量名)
        }
        */
        //foreach有个缺点
        //没有下标，当使用下标的时候，不建议使用
        for(int data : arr){
            //data就是数组中的元素
            //data代表的是每个元素中的元素
            System.out.println(data);
        }
    }
}
```

```java
//集合使用foreach
public class ForEachTest02{
    public static void main(String[] args){
        //创建List集合
        List<String>strList = new ArrayList<>();
        //添加元素
        strList.add("hello");
        strList.add("world");
        strList.add("kitty");
        //遍历，使用迭代器
        Iterator<String>it = strList.iterator();
        while(it.hasNext()){
            String s = it.next();
            System.out.println(s);
        }
        //使用下标的方式
        for(int i = 0; i < strList.size();i++){
            System.out.println(strList.get());
        }
        
        //使用foreach
        for(String i : strList){
            System.out.println(i);
        }
    }
}
```

### 12、set

#### 1、HashSet()

```java
/*
这里只是简单的讲一下
HashSet集合：
  无序不可重复。
*/
public class HashSetTest01{
    public static void main(String[] args){
        //演示一下HashSet集合特点
        Set<String> strs = new HashSet<>();
        strs.add("bai");
        strs.add("bdie");
        strs.add("bai");
        strs.add("biiad");
        //遍历
        for(String s : strs){
            System.out.println(s);
        }
    }
}
```

```java
/*
TreeSetTest集合元素特点
   1、无需不可重复，但是存储大的元素可以自动按照大小顺序排序
   称为：可排序集合
   
   2、无序：这里的无序指的是存进去的顺序和取出来的顺序不同，并且没有下标
      无序跟排序是两种不同的对象。
*/
public class TreeSetTest01{
    public static void main(String[] args){
        //创建集合对下个
        Set<String> strs = new TreeSet<>();
        //添加元素
        strs.add("A");
        strs.add("B");
        strs.add("C");
        strs.add("Z");
        strs.add("T");
        for(String s : strs){
            System.out.println(s);
        }
    }
}
```

### 13、Map接口

#### 1、Map常用方法

```java
/*
双列集合Map中子接口为：HashTable,HashMap,TreeMap
java.util.Map接口中常用的方法
   1、Map和Collection没有继承关系。
   2、Map集合以key和Value的方式储存数据：键值对
      key和value都是引用数据类型。
      key和value都是存储对象的内存地址
      key起到主导的地位，Value是key的一个附属品
   3、Map接口中常用方法
      V put(K key, V value) 向Map集合中添加键值对
      
      V get(Object key) 通过key获取value
      
      void clear()  清空Map集合
      
      boolean containsKey(Object key) 判断Map中是否包含某个key
      
      boolean containsValue(Object value) 判断Map中是否包含某个value
      
      boolean isEmpty() 判断Map集合中元素个数是否为0
      
      Set<K> keySet() 获取Map集合中所有的key(所有的键是一个set集合)
      
      V remove(Object key) 通过key键删除键值对
      
      int size() 获取Map集合中键值对的个数
      
      Collection<V> values() 获取Map集合中所有的value,返回一个Collection
      
      Set<Map.Entry<K,V>> entrySet() 将Map集合转换成Set集合
         将Map集合转换成Set集合
         假设现在有一个Map集合，如下所示：
            map1集合对象
            key           value
            ---------------------
            1             zhangsan
            2             lisi
            3              wangwu
            4             zhaoliu
            
            Set set = map1.entrySet();
            Set集合对象
            1=zhangsan 【注意：Map集合通过entrySet()方法转换成Set集合，Set集合中元素类型是Map.Entry<K,V>>】
            
            2=lisi 【Map.Entry和String一样，都是一种类型名字，只不过Map.Entry是静态内部类，是Map中静态内部类】
            3=wangwu
            4=zhaoliu  --> 这个东西是什么？Map.Entry
*/
public class MapTest01{
    public static void main(String[] args){
        //创建Map集合对象
        Map<Integer,String> map = new HasMap<>();
        //向Map集合中添加键值对
        map.put(1,"zhangsan");//自动装箱
        map.put(2,"lisi");
        map.put(3,"wangwu");
        map.put(4,"zhaoliu");
        //通过key获取value
        String value = map.get(2);
        System.out.println(value);
        //获取键值对的数量
        System.out.println(value);
        //获取键值对的数量
        System.out.println("键值对数量为 " + map.size());
        //通过key删除key--value
        map.remove(2);
        System.out.println("键值对数量为 " + map.size());
        //判断是否包含某个key
        //contains方法底层调用的都是equals进行比对的，所以自定义的类型需要重写equals方法
        System.out.println(containsKey(4));//true
        //判断是否包含某个value
        System.out.println(containsValue("王五"));//true
        //获取所有的value
        Collection<String> values = map.values();
        for(String s : values){
            System.out.println(s);
        }
        
        //清空map集合
        map.clear();
        System.out.println("键值对数量为 " + map.size());
        //判断是否为空
        System.out.println(map.isEmpty());//true
        
    }
}
```

```java
/*
Map集合的遍历


*/
public class MatTest02{
    public static void main(String[] args){
        //第一种方式：获取所有的key，通过遍历key,来遍历value
         Map<Integer,String> map = new HasMap<>();
        //向Map集合中添加键值对
        map.put(1,"zhangsan");//自动装箱
        map.put(2,"lisi");
        map.put(3,"wangwu");
        map.put(4,"zhaoliu");
        //遍历Map集合(键值去调用value)
        //获取所有的key,所有的key是一个Set集合
        Set<Integer> keys = map.keySet();
        //迭代器方式
        Iterator<Integer>it = keys.iterator();
        while(it.hasNext()){
            Integer key = it.next();
            String value = map.get(key);
            System.out.println(key + " = " + value);
        }
        //foreach
        for(Integer key : keys){
            System.out.println(key + " = " + map.get(key));
        }
        
        //第二种方式：Set<Map.Entry<K,V>> entrySet()
        //以上这种方法是把Map集合直接全部转换成Set集合
        //Set集合中元素的类型是Map.Entry
        //这种遍历效率很高
        Set<Map.Entry<Integer,String>>set = map.entrySet();
        //遍历Set集合，每一次取出一个Node
        //迭代器
        Iterator<Map.Entry<Integer,String>>it = set.iterator();
        while(it.hasNext()){
            Map.Entry<Integer,String> node = it.next();
            Integer a = node.getKey();
            String b = node.getValue();
            System.out.println(a + " = " + b);
        }
        
        //foreach
        for(Map.Entry<Integer,String> node : set){
            System.out.println(node.getKey() + " ->" node.getValue());
        }
    }
}
```

![image-20210508145939466](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210508145939466.png)

#### 2、HashMap集合

```java
/*
HahsMap集合：
   1、HahsMap集合底层是哈希表/散列表数据结构
   2、哈希表是一个数组和单向链表的数据结构
    
   3、最主要掌握的是：
      map.put(k,v);
      v = map.get(k);
   4、HashMap集合的key部分特点：
      无序，不可重复
      为什么无序？因为不一定挂到哪个单链表上。
      不可重复怎么保证？ equals方法来保证HashMap的key不可重复，key重复了，value会覆盖
      
      放在HashMap集合key部分的元素就是放到了HashSet集合中了
      所以HashSet集合中的元素也需要同时重写hashCode() + equals()方法
      
   5、哈希表HashMap使用不当时无法发挥性能!
      假设将所有的hashCode()方法返回值固定为某个值，那么会导致底层哈希表变成了纯单向链表。这种情况我们成为:散列分布不均匀。
      什么是散列分布均匀?
          假设有100个元素，10个单向链表，那么每个单向链表上有10个节点，这是最好的，是散列分布均匀的。
          假设将所有的hashcode()方法返回值都设定为不一样的值，可以吗，有什么问题?
不行，因为这样的话导致底层哈希表就成为一维数组了，没有链表的概念了。也是散列分布不均匀。
散列分布均匀需要你重写hashCode()方法时有一定的技巧。
   6、重点：放在HashMap集合key部分元素，以及放在HashSet集合中的元素，需要同时重写hashCode和equals方法。
   7、HashMap集合默认初始化容量是16，默认加载因子是0.75
   这个默认因子是当HashMap集合底层数组容量达到75%时候，数组开始扩容
     重点：HahsMpa集合初始化容量必须是2的倍数，这是因为达到散列均匀，为了提高HashMap集合存储效率所必须的

*/
public class HashMapTest01{
    public static void main(String[] args){
        //测试HashMap集合key部分元素特点
        //Integer是key,它的hashCode和equals方法都重写了
        Map<Integer,String>map= new HashMap<>();
        map.put(111,"zhangsan");
        map.put(666,"lisi");
        map.put(555,"zhaowu");
        map.put(3333,"wangliu");
        map.put(3333,"king");//key重复是value会自动覆盖
        System.out.println(map.size());
        //遍历Map集合
        Set<Map.Entry<Integer,String>>set = map.entrySet();
        for((Map.Entry<Integer,String> node :set)){
            System.out.println(node.getKey() + "= " node.getValue());
        }
    }
}
```

![image-20210508154223556](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210508154223556.png)

```java
/*
1、向Map集合中存，以及从Map集合中取，都是先调用key的hashCode方法，然后再调用equals方法!equals方法有可能调用，也有可能不调用。
    拿put( k , v)举例，什么时候equals不会调用?
       k .hashCode()方法返回哈希值，
       哈希值经过哈希算法转换成数组下标。
       数组下标粒置上如果是null , equals不需要执行。
    拿get(k)举例，什么时候equals不会调用?
       k .hashCode()方法返回哈希值，
       哈希值经过哈希算法转换成数组下标。
       数组下标位置上如果是null , equals不需要执行。
2、注意:如果一个类的equals方法重写了，那么hashCode()方法必须重写。
        并且equals方法返回如果是true , hashCode()方法返回的值必须一样。
        equals方法返回true表示两个对象相同，在同一个单向链表上比较。
        那么对于同一个单向链表上的节点来说，他们的哈希值都是相同的。
        所以hashcode()方法的返回值也应该相同。
        
3、equals和hashCode（）方法通过IDEA工具一键生成
*/
public class HashMapTest02{
    public static void main(String[] args){
        Student s = new Student("zhangsan");
        Student s2 = new Student("zhangsan");
        System.out.println(s.equals(s2));//没重写之前是fasle,重写之后是true
        System.out.println("s的hashCode=" + s.hashCode());
        System.out.println("s2的hashCode=" + s2.hashCode());
        //s.equals(s2)结果已经是true了，表示s和s2是一样的，相同的那么往HashSet集合中放的话，
        //按说只能放一个，（HashSet特点，无序不可重复
        Set<Student>students = new HashSet<>();
        students.add(s);
        students.add(s2);
        System.out.println(students.size());
    }
}
public class Student{
    private String name;
    public Student(){
        
    }
    public Student(String name){
        this.name = name;
    }
    public String getName(){
        return name;
    }
    public void setName(String name){
        this.name = name;
    }
    //重写hashCode
    public int hashCode(){
        return Objects.hash(name);
    }
    //重写equals
    public boolean equals(Object obj){
        if(obj == null || !(obj instanceof Student)) return false;
        if(obj == this) return true;
        Student s = (Student) obj;
        if(this.name.equals(s.name)) return true;
        return false;
    }
}
```

#### 3、HashMap和HashTable()区别

```java
/*
HashMap集合key和value允许null,但是开发时用不着
HashTable集合的key和value不允许为空

Hahstable方法都带有synchronized:线程安全的
线程安全有其它的方案，这个Hashtable对线程的处理导致效率较低，使用较少了

Hashtable和HashMap一样，底层都是哈希表数据机构
Hashtable的初始化容量为11，默认加载因子时：0.75f
Hashtable的扩容是：原容量 * 2 + 1
*/
public class HashtableTest01{
    public static void main(String[] args){
        Map map = new Hashtable();
        //map.put(null,"123");
        map.put(100,null);
    }
}
```

#### 4、Properties

```java
/*
Properties是一个Map集合，继承Hashtable,Propreties的key和value都是String类型的
Properties被称为属性类对象
Properties是线程安全的
*/
public class PropertiesTest01{
    public static void main(String[] args){
        //船舰一个Properties对象
        Properties pro = new Properties();
        //掌握Properties的两个方法，一个存，一个取
        pro.setProperty("a","oooooo");
        pro.setProperty("b","999999");
        pro.setProperty("c","555555");
        pro.setProperty("d","111111");
        
        //通过key获取value
        String a = pro.getProperty("a");
        String b = pro.getProperty("c");
        String c = pro.getProperty("c");
        String d = pro.getProperty("d");
        
        System.out.println(a);
        System.out.println(b);
        System.out.println(c);
        System.out.println(d);
    }
}
```

#### 5、TreeSet

```java
/*
1、TreeSet集合底层实际上是一个TreeMap
2、TreeMap集合底层是一个二叉树
3、放到TreeSet集合中的元素，等同于放到TreeMap集合key部分
4、TreeSet集合中的元素：无序不可重复，但是可以按照元素大小顺序自动排序，称为：可排序集合

*/
public class TreeSetTest02{
    public static void main(String[] args){
        //创建一个TreeSet集合
        TreeSet<String>ts = new TreeSet<>();
        ts.add("zhangsan");
        ts.add("lisi");
        ts.add("wangwu");
        ts.add("wangliu");
        //遍历
        for(String i : ts){
            System.out.println(i);
        }
        TreeSet<Integer>ts1 = new TreeSet<>();
        ts.add(100);
        ts.add(56);
        ts.add(89);
        ts.add(56);
        for(Integer i : ts1){
            System.out.println(i);
        }
        
    }
}
```

```java
/*
对于自定义类型来说：TreeSet可以排序吗？不行
   因为没有在类中规定谁打谁小，需要重写Compareable接口
*/
public class TreeSetTest03{
    public static void main(String[] args){
       Person p1 = new Person(32);
       Person p2 = new Person(20);
       Person p3 = new Person(45);
       //创建TreeSet集合
        TreeSet<Person> persons = new TreeSet<>();
        persons.add(p1);
        persons.add(p2);
        persons.add(p3);
        persons.add(p4);
        for(Person p : persons){
            System.out.println(p);
        }
    }
}
/*
class Preson{
    int age;
    public Person(int age){
        this.age = age;
    }
    //重写toString方法
    public String toString(){
        return "Person[age =" + age + "]";
    }
}

*/
//放在TreeSet集合中的元素需要实现java.lang.Comparable接口
class Person implements Comparable<Person>{
    int age;
    public Person(int age){
        this.age = age;
    }
    //需要在这个方法中编写比较逻辑，
    //k.compareTo(t.key)
    //拿着参数k和集合中每一个k进行比较，返回值> 0,<0,=0
    public int compareTo(Person c){//c1.compareTo(c2)
        //this是c1
        //c.age = c2;
        int age2 = c.age;
        int age1  = this.age;
        //升序
        if(age1 == age2){
            return 0;
        }else if(age1 > age2){
            return 1;
        }else if(age1 < age2){
            return -1;
        }
    }
    
    //重写toString方法
    public String toString(){
        return "Person[age =" + age + "]";
    }
}

```

```java
/*
先按照年龄升序，再按照姓名升序

*/
public class TreeSetTest03{
    public  static void main(String[] args){
        TreeSet<Vip>vips = new TreeSet<>();
        vips.add(new Vip("zhangsan",35));
        vips.add(new Vip("lisi",83));
        vips.add(new Vip("wangwu",14));
        for(Vip v : vips){
            System.out.println(v);
        }
    }
}
class Vip implements Comparable<Vip>{
    String name ;
    int age ;
    public Vip(String name, int age){
        this.name = name;
        this.age = age;
    }
    public String toString(){
        return "Vip{"+"name=" + name + '\'' + ", age = " + age + "}";
    }
    public int compareTo(Vip v){
        if(this.age == v.age){
            //年龄相同按照名字排序
            //姓名是String类型，可以直接比，直接调用compaerTo比就好
            return this.name.compaerTo(v.name);
        }else{
            //年龄不一样
            return this.age - v.age;
        }
    }
}
```

#### 6、（二叉查找树）

```java
/*
TreeSet/TreeMap是自平衡二叉树（二叉查找树），遵循左小右大原则
2、TreeSet集合和TreeMap集合采用的是：中序遍历方式
   Iterator迭代器采用的是中序遍历方式  左根右
   
3、compareTo比较规则就是调用的二叉查找树的比较原理
   所以才会有>0 , <0 , =0; 
*/
```

#### 7、实现比较器的方式

```java
/*
TreeSet集合中元素可排序的第二种方式 :使用比较器的方式
    放到TreeSet或者TreeMap集合key部分的元素要想做到排序，包括两种方式
    第一种：放在集合中元素时间java.lang.Comparable接口
    第二种：在构造TreeSet或者TreeMap集合的时候，给传一个比较器对象
    
2、Comparable和Comparator怎么选择呢?
      当比较规则不会发生改变的时候，或者说当比较规则只有1个的时候，建议实现comparable接口。
      如果比较规则有多个，并且需要多个比较规则之间频繁切换，建议使用Comparator接口。
*/
public class TreeSetTest06{
    public static void main(String[] args){
       //TreeSet<WuGui> wuGuis = new TreeSet<>();这样不行，没有传递一个比较器进去
        //TreeSet<WuGui> wuGuis = new TreeSet<>(new WuGuiComparator());
        //可以是使用匿名内部类,这个类没有名字，只有接口
        TreeSet<WuGui> WuGuis = new TreeSet<>(new Comparator<WuGUi>(){
            public int compare(Wugui o1,WuGui o2){
                //指定比较规则
                //按照年龄排序
                return o1.age - o2.age;
           }
        });
        WuGuis.add(new WuGui(1000));
        WuGuis.add(new WuGui(800));
        WuGuis.add(new WuGui(810));
        for(WuGui wugui: WuGUis){
            System.out.println(wugui);
        }
    }
}
class WuGui{
    int age;
    public WuGui(int age){
        this.age =age;
    }
    public String toString(){
        return "小乌龟[" + "age=" + age + "]";
    }
}
//单独写一个比较器
//比较器实现java.util.Comparable接口（Comparable是java.lang包下的，Comparator是java.util包下的
class WuGuiComparator implements Comparator<WuGui> {
    public int compare(Wugui o1,WuGui o2){
        //指定比较规则
        //按照年龄排序
        return o1.age - o2.age;
    }
}
```

#### 8、Collections集合工具类

```java
/*

*/
import java.util.Collections;
public class CollectionsTest{
    public static void main(String[] args){
        //ArrayList集合不是线程安全的
        List<String>list = new ArrayList<>();
        //变成线程安全的
        Collections.synchronizedList(list);
        //排序,排序的前提是，自定义类必须实现Comparator接口，否则排不了
        list.add("abdd");
        list.add("eek");
        list.add("99els");
        list.add("ab3");
        Collections.sort(list);
        for(String i : list){
            System.out.println(i);
        }
        //这种方式也可以排
        //Collections.sort(list集合，比较器对象);
        
        //对Set集合怎么排
        Set<String>set = new HashSet<>();
        set.add("king");
        set.add("kingsoft");
        set.add("bai");
        set.add("kong");
        //将Set集合转换成List集合
        List<String>myList = new ArrayList<>(set);
        Collections.sort(myList);
        for(String s : myList){
            System.out.println(s);
        }
    }
}
```

## 7、IO流

### 1、定义

```java
/*
1、IO流：什么是IO?
    I:Input
    O:Output
    通过IO可以完成硬盘的读和写
    
2、IO流的分类？
   有多种分类方式：
   一种方式按照流的方向进行分类：
      往内存中去，叫做输入(Input).或者叫做读(read)
      从内存中出来，叫做输出(Output),或者叫做写(write)
      
   另一种方式是按照读取数据的方式不同进行分类的
       有的流是按照字节的方式读取数据，一次读取1个字节byte,等同于一次读取8个二进制位
       这种流是万能的，什么类型的文件都可以读取，包括：文本文件，图片，声音文件，视频文件等
       假设文件file1.txt,采用字节流话，是这样读的：
       a中国bc
       第一次读：‘a’字符(在windowns系统中占用1个字节)
       第二次读：‘中’字符一半（(在windowns系统中占用2个字节)）
       第三次读：‘中’字符另一半
       ...
       
       
       有的流是按照字符的方式读取数据的，一次读取一个字符，这种流是为了方便读取普通文件而存在的，这种流不能读取：图片、声音、视频、等文件。只能读取纯文本文件（.txt文件）和普通文件（能用记事本编辑和打开的都是普通文件），连word文件都无法读取。
       假设文件file1.txt,采用字符流话，是这样读的：
       a中国bc
       第一次读：‘a’字符(在windowns系统中占用1个字节)
       第二次读：‘中’字符（(在windowns系统中占用2个字节)）
       ...
       
       
   综上所述：流的分类
     输入流、输出流（按流的方向分）
     字节流、字符流（按输入、输出的方式分）
     

3、Java的IO流到写好了，程序员不需要关心，需要提供了那些流，每个流的特点，每个流对象上的常用方法有那些？
   java中所有的流都是在：java.io.*;下
   
   java中主要研究：
     怎么new流对象
     调用流对象的哪些方法是读，哪些方式是写。
     
4、java IO流的四大家族首领（都是抽象类 abstract class）
     java.io.InputStream (字节输出流)
     java.io.OUtputStream （字节输出流）
     java.io.Reader  (字符输入流)
     java.io.Writer  (子符输出流)
   
   注意：在java中只要是以”类名“以Stream结尾的都是字节流，以”Reader/Writer“结尾的都是字符流
   
   所有的流都实现了：
     java.io.Closeable接口，都是可以关闭的，都有close()方法
     流毕竟是一个管道，这个是内存和硬盘之间的通道，用完之后一定要关闭
     不然会耗费（占用内存资源），养成好习惯，用完流一定要关闭
     
   所有的输出流都实现了：
     java.io.Flushable接口，都是可刷新的，都有flush()方法，养成一个好习惯，输出流在最终输出之后，一定要flush()方法。刷新一下，这个刷新表示将通道/管道当中剩余的数据强行输出完（清空管道）刷新的作用就是清空管道
     
6、java.io包下需要掌握的流有16个：
    文件专属
     java.io.FileInputStream
     java.io.FileOutputStream
     java.io.FileReader
     java.io.FileWriter
     
    转换流（将字节流转换成字符流）
     java.io.InputStreamReader
     java.io.OutputStreamWriter
     
    缓冲流专属：
     java.io.BufferedReader
     java.io.BufferedWriter
     java.io.BufferedInputStream
     java.io.BufferedOutputStream
     
    数据流专属：
     java.io.DateInputStream
     java.io.DateOutputStream
     
    标准输出流 
     java.io.PrintWriter
     java.io.PrintStream
    对象专属流
     java.io.ObjectInputStream
     java.io.ObjectOutputStream
     
*/

```

### 2、FileInputStream

```java
/*
java.io.FileInputSteam
   1、文件字节输入流，万能的，任何类型的文件都可以采用这个流来读
   2、字节的方式，完成输入操作，完成读的操作（硬盘-->内存）
   3、read()方法学习，但是一个一个读，交互的太频繁，效率太低
*/
public class FileInputTest01{
    public static void main(String[] args){
        FileInputStream fis = null;
        try{
            //创建文件字节输入流对象
            //文件路径E:\\各种软件文档\\网课须知(IDEA会自动把\变成\\，因为在java中\表示转义)
            fis = new FileInputStream("E:\\各种软件文档\\网课须知\\ios");
            //开始读
            while(true){
                int readData = fis.read();
                if(readData == -1){
                    break;
                }
                System.out.println((char)readData);
            }
            
            //改造while循环
            int readData = 0;
            while((readData = fis.read()) != -1){
                System.out.println((char)readData);
            }
        }catch(FileNotFoundException e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }finally{
            //在finally语句块当中确保流一定关闭
            if(fis!=null){//避免空指针异常！
                //关闭流的前提是：流不是空，流是null的时候，没必要关闭
                try{
                    fis.close();
                } catch(IOException e){
                    e.printStackTrace();
                }
            }
        }
    }
}
```

```java
/*
1、IDEA下的当前路径的建立（相对路径）
   与Mouble并排(谁也不包括谁)以工程作为根
     如果不并排，找某个文件的话，需要从Mouble的名称开始找起，知道找到该文件
   关于eclipse是与project并排的位置创建当前路径
   
   
2、read(byte[] b) 方法的学习
   一次最多读取b.length个字节。
   减少硬盘和内存的交互，提高程序的执行效率
*/

public class FileInputTest02{
    public static void main(String[] args){
        FileInputStream fis = null;
        try{
           
            
            fis = new FileInputStream("E:\\各种软件文档\\网课须知\\ios");
            //开始读，采用byte数组，一次读取多个字节，最多读取”数组.length"字节。
            //如果文件内容是abcdef的话
            byte[] byte = new byte[4];//准备一个长度为4的byte数组，一次最多读取4个字节。
            //这个方法的返回值是：读取到的字节数量，（并不是字节本身）
            int readCount = fis.read(bytes);//第一次读到了4个字节数,该数组内容为abcd
            System.out.println(readCount);//4
            //System.out.println(new String(bytes));//abcd
            //不应该是全部都转换，应该是读取的多少个，转换多少个
            System.out.println(new String(bytes,0,readCount));
            
            
            readCount = fis.read(bytes);//只能读取两个字节且内容为efcd
            System.out.println(readCount);//2
            //System.out.println(new String(bytes));//efcd
            System.out.println(new String(bytes,0,readCount));
            
            
            readCount = fis.read(bytes);//没有内容可读，且还为原内容efcd,并且字节数为-1
            System.out.println(readCount);
            //System.out.println(new String(bytes));//efcd
            System.out.println(new String(bytes,0,readCount));
            
            
        }catch(FileNotFoundException e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }finally{
            //在finally语句块当中确保流一定关闭
            if(fis!=null){//避免空指针异常！
                //关闭流的前提是：流不是空，流是null的时候，没必要关闭
                try{
                    fis.close();
                } catch(IOException e){
                    e.printStackTrace();
                }
            }
        }
    }
}
```

```java
/*
FileInputStream最终版，都需要掌握
*/
public class FileInputStreamTest04{
    public static void main(String[] args){
        FileInputStream fis = null;
        try{
            fis = new FileInputStream("tempfile");//需要在IDEA的Project根目录下创建一个这样的文件，并输入内容
            byte[] bytes = new byte[4];
            int readCount = 0;
            while((readCount = fis.read(bytes)) != -1){
                //把byte数组转换成字符串，读取到多少个转换成多少个
                System.out.println(new String(bytes,0,readCount));
            }
        }catch (FileNotFoundException e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }finally{
            if(fis != null){
                try{
                    fis.close();
                } catch(IOException e){
                    e.printStackTrace();
                }
            }
        }
    }
}
```

```java
/*
FileInputStream类的其它常用方法：
   int available()返回流当中剩余没有督导的字节数量
   long skip(long n)跳过集合字节不读

*/
public class FileInputStreamTest05{
    public static void main(String[] args){
        FileInputStream fis = null;
        try{
            fis = new FileInputStream("tempfile");
            System.out.println("总节数为：" + fis.available());
           //读1个字节
            //int readByte = fis.read();
            //还剩下可读字节数量为5
            //System.out.println("剩下可读字节数为：" + fis.available());
            //这个方法的作用是，不需要循环了，只需要读一次就可以了
            byte[] bytes = new byte[fis.available()];//这种方式不太适合大文件，因为byte数组不能太大
            int readCount = fis,read(bytes);//6
            System.out.println(new String(bytes));
            
            //skip跳过几个字节不读取，这个方法可能以后会用
            fis.skip(3);//跳过3个字节不读取(读取之后的一个字节)
            System.out.println((char)fis.read());
            
        }catch (FileNotFoundException e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }finally{
            if(fis != null){
                try{
                    fis.close();
                } catch(IOException e){
                    e.printStackTrace();
                }
            }
        }
    }
}


```

### 3、FileOutputStream

```java
/*
文件字节输出流，负责写
   从内存到硬盘
*/
public class FileOutputStreamTest01{
    public static void main(String[] args){
        FileOuntputStream fos = null;
        try{
            //这种方式谨慎使用，因为会将原文件清空，在重写写入
            //fos = new FileOutputStream("myfile");//该文件需要自己手动建立,如果不存在，系统会新建一个文件
            //以追加的方式在文件末尾写入，不会清空原文件内容
            fos = new FileOutputStream("myfile",true);//true,false，是否已追加的方式写入
            //开始写
            byte[] bytes = {97,98,99,100,101};
            //将bytes数组全部写出
            fos.write(bytes);//abcde
            
            //将bytes数组一部分写出（在原先重写的基础上）
            fos.write(bytes,0,2);//abcdeab
            //写完之后，最后一定记得刷新
            
            String s = "我是一个中国人，我骄傲";
            //将字符串转换成byte数组
            byte[] bs = s.getBytes();
            //写
            fos.write(bs);
            
            fos.flush();
        }catch(FileNotFoundException e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }finally{
            if(fos != null){
                try{
                    fos.close();
                }catch(IOException e){
                    e.printStackTrace();
                }
            }
        }
    }
}
```

### 4、文件复制

```java
/*
使用FileInputStream + FileOutputStream 完成文件的拷贝
拷贝的过程应该是一边读，一边写。
使用以上的字节流拷贝文件的时候，文件的类型随意，万能的，什么样的文件都能拷贝。

*/
public class Copy01{
    public static void main(String[] args){
        FileInputStream fis = null;
        FileOutputStream fos = null;
        try{
            //创建一个输入流对象
            fis = new FileInputStream("C:\\Users\\28929\\Videos\\MV\\剩下的盛夏.mkv");
            
            //最核心的一边读，一边写
            byte[] bytes = new byte[1024*1024];//1MB(一次最多拷贝1MB)
            int readCount = 0;
            while((readCount = fis.read(bytes)) != -1){
                fos.write(bytes,0,readCount);
            }
            
            //创建一个输出流对象
            fos = new FileOutputStream("E:\\剩下的盛夏.mkv");
            
            //刷新
            fos.flush();
        }catch(FileNotFoundExceptin e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }finally{
            //分开try,不要一起try
            //一起try的时候，其中一个出现异常，可能会影响到另一个流的关闭
            if(fos != null){
                try{
                    fos.close();
                }catch(IOException e){
                    e.printStackTrace();
                }
            }
            if(fis != null){
                try{
                    fis.close();
                }catch(IOExcption e){
                    e.printStackTrace();
                }
            }
        }
    }
}
```

![image-20210509161931626](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210509161931626.png)

### 5、FileReader

```java
/*
FileReader:
  文件字符输入流，是能读取普通文本。
  读取文本内容时，比较方便，快捷
*/
public class FileReaderTest{
    public static void main(String[] args){
        FileReader reader = null;
        try{
           //创建文件字符输入流
            reader = new FileReader("tempfile");
            //开始读
            char[] chars = new char[4];//一次读取4个字符
            int readCount = 0;
            while((readCount = reader.read(chars)) != -1){
                for(char c : chars){
                    System.out.println(c);
                }
                System.out.println(new String(chars,0,readCount));
            }
        }catch(FileNotFoundException e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }finally{
            if(reader != null){
                try{
                    reader.close();
                }catch(IOException e){
                    e.printStackTrace();
                }
            }
        }
    }
}
```

### 6、FileWriter

```java
/*
FileWriter:
   文件字符输出流

*/
public class FileWriterTest{
    public static void main(String[] args){
        FileWriter out = null;
        try{
           //创建文件字符输出流
            out = new FileWriter("file",false);//不是以追加的方式写入的
            //开始写
            char[] chars ={'我','是','中','国','人'};//一次读取4个字符
            out.write(chars);
            out.write(chars,2,3);
            
            out.write("我是一名java软件工程师");
            out.write("\n");
            out.write("helloWorld");
            
            out.flush();
        }catch(FileNotFoundException e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }finally{
            if(reader != null){
                try{
                    reader.close();
                }catch(IOException e){
                    e.printStackTrace();
                }
            }
        }
    }
}
```

### 7、普通文件的拷贝

```java
/*
使用FileReader FileWriter进行拷贝的话，只能拷贝“普通文本”文件

*/
public class Copy02{
    public static void main(String[] args){
        FileReader in = null;
        FileWriter out = null;
        try{
            //读
            in = new FileReader("E:\\c语言习题\\字符串习题\\字符串应用实例.txt");
            //写
            out = new FileWriter("E:\\字符串应用实例.txt");
            
            //一边读，一边写
            char[] chars = new char[1024*1024];//1MB
            int readCount = 0;
            while((readCount = in.read(chars)) != -1){
                out.write(new String(chars, 0,readCount));
            }
             //刷新
            out.flush();
        }catch(FileNotFoundExceptin e){
            e.printStackTrace();
        }catch(IOException e){
            e.printStackTrace();
        }finally{
            if(in != null){
                try{
                    in.close();
                }catch(IOException e){
                    e.printStackTrace();
                }
            }
            if(out != null){
                try{
                    out.close();
                }catch(IOExcption e){
                    e.printStackTrace();
                }
            }
        }
    }
}
```

### 8、带有缓冲区的字符流

```java
/*
BufferedReader:
   带有缓冲区的字符输入流
   使用这个流的时候，不需要自定义char数组，或者说不需要自定义byte数组，自带缓冲区

*/
public calss BufferedReaderTest01{
    public static void main(String[] args) throws Exception{
        FileReader reader = new FileReader("Copy02.java");
        //当一个流的构造方法中需要一个流的时候这个被传进来的流叫做：节点流
        //外部负责包装的这个流叫做：包装流，还有一个名字叫做：处理流
        //像当前的这个程序来说：FileReader就是一个节点流，BufferedReader就是包装流/处理流
        BufferedReader br = new BufferedReader(reader);
        
        //读一行,但是读不到最后的换行符
        /*String firstLine = br.readLine();
        System.out.println(firstLine);*/
        String s = null;
        while((S = br.readLine()) != null){
            System.out.println(s);
        }
        
        //关闭流
        //对于包装流来说，只需要关闭最外层流就行，里面的节点流会自动关闭
        br.close();
    }
}
```

```java
public calss BufferedReaderTest02{
    public static void main(String[] args) throws Exception{
        /*FileInputStream in = new FileInputStream("Copy02.java");
        //通过转换流转换
        InputStreamReader reader = new InputStreamReader(in);
        //in是节点流，reader是包装流
        
        //这个构造方法只能传入一个字符流，不能传字节流
        
        BufferedReader br = new BufferedReader(reader);*/
        
        //将以上代码合并
        BufferedReader br = new BufferedReader(new InputStreamReader(new FileInputStream("Copy02.java")));
        String line = null;
       while((line = br.readLine()) != null){
           System.out.println(line);
       }
        br.close();
    }
}
```

```java
/*
BufferedWriter:带有缓冲的字符输出流
*/
public calss BufferedReaderTest02{
    public static void main(String[] args) throws Exception{
        //BufferedWriter bw = new BufferedWriter(new FileWriter("copy"));
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(new FileOutputStream("copy",ture)));
        //开始写
        bw.write("helloWorld");
        bw.write("\nzhangsan");
        //刷新
        out.flush();
        //关闭
        bw.close();
    }
}
```

### 9、数据流

```java
/*
java.io.DataOutputStream:数据专属流。
这个流可以将数据联同数据的类型一并写入文件
注意：这个文件不是普通文本文件，（这个文件用记事本打不开）
*/
public class DateOutputStreamTest{
    public static void main(String[] args) throws Excetion{
        //创建数据专属的字节输出流
        DataOutputStream dos = new DataOutputStream(new FileOutputStream("data"));
        //写数据
        byte b = 100;
        short s = 20;
        int i = 300;
        long l = 400L;
        float f = 3.0f;
        double d = 3.15;
        boolean set = false;
        char c = 'a';
        //写
        dos.writeShort(s);
        dos.writeInt(i);
        dos.writeByte(b);
        dos.writeLong(l);
        dos.writeFloat(f);
        dos.writeDouble(d);
        dos.writeBoolean(set);
        dos.writeChar(c);
        
        //刷新
        dos.flush();
        //关闭最外层
        dos.close();
    }
}
```

```java
/*
DataInputStream：数据字节输入流
DataOutputStream:写的文件，只能使用DataInputStream去读，并且读的时候你需要提前知道写入的顺序
读的顺序和写的顺序一致，才可以正常取出数据
    每次读取多个字节的数据，传入的参数为一个byte型数组，读取的数据会填充到该数组中区，最终返回实际读取的字节数，不是-1，也不是null

*/
public class DateInputStreamTest{
    public static void main(String[] args) throws Excetion{
        //创建数据专属的字节输出流
        DataInputStream dos = new DataInputStream(new FileInputStream("data"));
        //开始读
        short s = dos.readShort();
        int i = dos.readInt();
        byte b = dos.readByte();
        long l = dos.readLong();
        float f = dos.readFloat();
        double d = dos.readDouble(d);
        boolean sex = dos.readBoolean();
        char c = dos.readChar();
        
        System.out.println(s);
        System.out.println(i);
        System.out.println(b);
        System.out.println(l);
        System.out.println(f);
        System.out.println(d);
        System.out.println(sex);
        System.out.println(c);
        //刷新
        dos.flush();
        //关闭最外层
        dos.close();
    }
}
```

### 10、标准输出流

```java
/*
java.io.PrintStream：标准的字节输出流，默认输出到控制台。
*/
public class PrintStreamTest{
    public static void main(String[] args) throws Exception{
        //联合起来写
        System.out.println("hello world");
        //分开写
        PrintStrem ps = System.out;
        ps.println("hello zhangsan");
        ps.println("hello lisi");
        ps.println("hello wangwu");
        //标砖输出流不需要手动close()关闭
        //改变标准输出流的输出方向是可以的
        
        //标准输出流不在指向控制台，指向“log”文件
        PrintStream printStream = new PrintStrem(new FileOutputStream("log"));
        //修改输出方向
        System.setOut(printStream);
        //在输出
        System.out.println("heool");
        System.out.println("你好");
        System.out.println("zhangsan");
        System.out.println("lisi");
    }
}
```

```java
/*
日志工具
*/
class Logger{
    public static void log(String msg){
        try{
            //指向一个日志文件
            PrintStream out = new PrintStream(new FileOutputStream("log.txt",true));
            //输出改变方向
            System.setOut(out);
            //日期当前时间
            Date nowTime = new Date();
            SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
            String strTime = sdf.format(nowTime);
            System.out.println(strTime + ":" + msg);
        }catch(FileNotFoundException e){
            e.printStackTrace();
        }
    }
}
public class LoggerTest{
    public static void main(String[] args){
        Logger.log("你好李焕英");
        logger.log("baidu1");
        logger.log("特利迦奥特曼");
        logger.log("lijing");
    }
}
```

### 11、File类

```java
/*
1、File类和四大家族没有关系，所以File类不能完成文件的读和写
2、File对象代表着：
   文件和目录路径名的抽象表示形式
   C:\Drivers 这是一个File对象
   c:\Diivers\lan\Readletk\Radme.txt 也是File对象
   一个File对象可能对对应的是目录，也可能是文件
   File只是一个路径名的抽象表示形式。
   
3、需要掌握File类的常用方法

*/
public class FileTest01{
    public static void main(String[] args)throws Exception{
        File f1 = new File("D:\\file");
        System.out.println(f1.exist());//判断是否存在
        //如果该文件不存在,则以文件形式船舰出来
        if(!f1.exist()){
            //以文件的形式新建
            f1.createNewFile();
        }
        
        
        //如果该文件不存在,则以目录形式船舰出来
        if(!f1.exist()){
            //以文件的形式新建
            f1.mkdir();
        }
        
        //创建多重目录
        File f2 = new File("D:/a/b/c/d");
        if(!f2.exist()){
            //多重目录形式新建
            f2.mkdirs();
        }
        
        File f3 = new File("E:\\c++\\code\\practice\\text.cpp");
        //获取文件的父路径
        String parentPath = f3.getParent();
        System.out.println(parentPath);
        
        File parentFile = f3.getParentFile();
        System.out.println("获取绝对路径" + parentFile.getAbsoultePate());
        
        File f4 = new File("copy");
        System.out.println("绝对路径" + f4.getAbsolutePath());
    }
}
```

```java
/*


*/
public class FileTest02{
    public static void main(String[] args){
        File f1 = new File("E:\\c++\\code\\practice\\text.cpp");
        //获取文件名
        System.out.println("文件名：" + f1.getName());
        
        //判断是否是一个目录
        System.out.println(f1.isDirectory());
        
        //判断是否是一个文件
        System.out.println(f1.isFile());
        
        //获取文件最后一次修改时间
        long haoMiao = f1.lastModified()
    };//这个毫秒是从1970年到现在的总毫秒数
    //将总毫秒数改成日期
    Date time = new Date(haoMiao);
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS");
    String strTime = sdf.format(time);
    System.out.println(StrTime);
    
    //获取文件大小
    System.out.println(f1.length());
    
    
}
```

```java
/*
File中listFiles方法

*/
public class FileTest03{
    public static void main(String[] args){
        //获取当前目录下所有的子文件
        //File[] listFiles()
        File f = new File("E:\\c++\\code\\practice");
        File[] files = f.listFiles();
        for(File file : files){
            System.out.println(file.getName());
            System.out.println(file.getAbsolutePath());
        }
    }
}
```

### 12、目录拷贝

```java
public class CopyAll{
    public static void main(String[] args){
        //拷贝源
        File srcFile = new File("E:\\c++\\code\\practice");
        //拷贝目标
        File destFile = new File("D:\\");
        //调用方法拷贝
        copyDir(srcFile,destFile);
    }
    private static void copyDir(File srcFile,File destFile){
        if(srcFile.isFile()){
            //srcFile如果是一个文件，递归结束
            //是文件的时候，需要拷贝，
            //一边读，一边写
            FileInputStream in = null;
            FileOutputStream out = null;
            try{
                //读这个文件
                in = new FileInputStream(srcFile);
                String path = (destFile.getAbsolutePath().endsWith("\\")?destFile.getAbsolutePath():destFile.getAbsolutePath() + "\\") + srcFile.getAbsolutePath().substring(3);
                //写到这个文件中
                out = new FileOutputStream(path);
                byte[] bytes = new byte[1024*1024];
                int readCount = 0;
                while((readCount = in.read(bytes)) != -1){
                    out.write(bytes.0,readCount);
                }
                out.flush();
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
                if(in != null){
                    try{
                        in.close();
                    }catch(IOException e){
                        e.printStackTrace();
                    }
                }
            }
            return;
        }
        //获取源下面的子目录
        File[] files = srcFile.listFiles();
        for(File file : files){
            //获取所有文件，（包括目录何为文件）绝对路径
            if(file.isDirectory()){
                //新建对应目录
                //E:\\c++\\code\\practice源路径
                //D:\\c++\\code\\practice目标路径
                String srcDir = file.getAbsulutePath();
                String destDir = (dextFie.getAbsolutePath().endsWith("\\")? destFile.getAbsolutePath(): + srcDir.substring(3));
                System.out.println(destDir);
            }
            
            //递归调用
            copyDir(file,destFile);
        }
    }
}

```

### 13、对象流



![image-20210509192710755](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210509192710755.png)

#### 1、序列化

```java
/*
   1、java.io.NotSerializableException:
      student对象不支持序列化
   
   2、参与序列化和反序列化对象，必须实现Serializable接口
   
   3、注意：通过源代码发现Serizlizable接口只是一个标志接口：
    public interface Serializable{
    
    }
    这个接口当中什么也没有。
    他起到标识作用，标志的作用，java虚拟机看到这个类实现了这个接口，可能会对这个类进行特殊待遇。


   4、反序列化版本号的作用是什么？
      
      java语言中采用的是什么机制区分类的？
         第一：首先通过类名进行比对，类名一样，，肯定不是同一个类
         第二：如果类名一样，在通过序列化版本号进行区分
         
         最终结论：
            凡是一个类的实现了Serializable接口，建议给该类提供一个固定不变的序列版本号
            这样，以后这个类即使代码修改了，但是版本号不变，java虚拟机会认为是同一个类。
         
*/
public class ObjectOutputStreamTest04{
    public static void main(String[] args)throws Exception{
        //创建java对象
        Student s = new Student(111,"zhangsan");
        //序列化
        ObjectOutputStream = oos = new ObjectOutputStream(new FileOutputStream("students"));
        
        //序列化对象
        oos.writeObject(s);
        
        //刷新
        oos.flush();
        //关闭
        oos.close();
    }
}
class Student implements Serializable{ //实现可序列化接口
    
    //java虚拟机看到Serializable接口后，会自动生成一个序列化版本号
    //这里没有手动写出来，java虚拟机会提供这个序列化版本号
    //建议将序列化版本号手动写成，不建议自动生成
    //这里没有手动写出来，Java虚拟机会默认提供这个序列化版本号。
    private static final long serialVersionUID = 1L;//java虚拟机识别一个类的时候，先通过类名，如果类名一致，在去识别序列化版本号。
    private int no;
    private String name;
    public Student(){
        
    }
    public Student(int no, String name){
        this.no = no;
        this.name = name;
    }
    public int getNo(){
        return no;
    }
    public void setNo(int no){
        this.no = no;
    }
    public String getName(){
        return name;
    }
    public void setName(String name){
        this.name = name;
    }
    public String toString(){
        return "Student{" + "no=" + no + ",name=" + name + "}";
    }
}
```

#### 2、反序列化

```java
/*
反序列化
*/
public class ObjectInputStreamTest01{
    public static void main(String[] args) throws Exception{
        ObjectInputStream ois = new ObjectInputStream(new FileInputStream("students"));
        //开始反序列化，读
        Object obj = ois.readObject();
        //反序列化回来是一个学生对象，所以会调用学生对象toString()方法
        System.out.println(obj);
        ois.close();
    }
}
```

#### 3、序列化多个对象

```java
/*
一次序列化多个对象呢？
   可以，可以将对象放到集合中，序列化集合

如果不使用集合，直接将多个对象放到反序列化中，会直接报错
*/
public class ObjectOutputStreamTest02{
    public static void main(String[] args)throws Exception{
        List<User>userList = new ArrayList<>();
        userList.add(new User(1,"zhangsan"));
        userList.add(new User(2,"lisi"));
        userList.add(new User(3,"wangwu"));
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("users"));
        
        //序列化一个集合，这个集合中放了很多其它对象
        oos.writeObject(userList);
        
        oos.flush();
        oos.close();
    }
}
class User implements Serializable{ //实现可序列化接口
    
    
    private int no;
    private String name;
    public Student(){
        
    }
    public Student(int no, String name){
        this.no = no;
        this.name = name;
    }
    public int getNo(){
        return no;
    }
    public void setNo(int no){
        this.no = no;
    }
    public String getName(){
        return name;
    }
    public void setName(String name){
        this.name = name;
    }
    public String toString(){
        return "User{" + "no=" + no + ",name=" + name + "}";
    }
}
```

```java
/*
反序列化集合
*/
public class ObjectInputStreamTest02{
    public static void main(String[] args)throws Exception{
        ObjectInputStream ois = new ObjectInputStrem(new FileInputStream("users"));
        List<User>userList = (List<User>)ois.readObject();
        for(User user : userList){
            System.out.println(user);
        }
        ois.close();
    }
}
```

#### 4、transient关键字

```java
/*
当不想要序列化某个对象中的变量时，可以给其加上关键字
transient,表示不可序列化(表示游离的，不参与关键字)

*/
public class ObjectOutputStreamTest02{
    public static void main(String[] args)throws Exception{
        List<User>userList = new ArrayList<>();
        userList.add(new User(1,"zhangsan"));
        userList.add(new User(2,"lisi"));
        userList.add(new User(3,"wangwu"));
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("users"));
        
        //序列化一个集合，这个集合中放了很多其它对象
        oos.writeObject(userList);
        
        oos.flush();
        oos.close();
    }
}
class User implements Serializable{ //实现可序列化接口
    
    
    private int no;
    //name不参与序列化操作，在反序列化输出后，会给name赋予null
    private transient String name;
    public Student(){
        
    }
    public Student(int no, String name){
        this.no = no;
        this.name = name;
    }
    public int getNo(){
        return no;
    }
    public void setNo(int no){
        this.no = no;
    }
    public String getName(){
        return name;
    }
    public void setName(String name){
        this.name = name;
    }
    public String toString(){
        return "User{" + "no=" + no + ",name=" + name + "}";
    }
}
```

#### 5、IO和Properties联合使用

```java
/*
IO + Properties的联合使用

  非常好的设计理念：
     以后经常改变的数据，可以单独写到一个文件中，使用程序动态读取。
     将来只需要修改这个文件的内容，java代码不需要改动，不需要重新编译，服务器也不需要重启，就可以拿到动态信息。
     
     类似于以上机制的这种文件被称为配置文件。
     并且当配置文件中内容格式是：
        key1 = value;
        key2 = value;
     的时候，我们把这种配置文件叫做属性配置文件。
     
     java规范中有要求：属性配置文件建议以.properties结尾，但这不是必须的。
     这种以.properties结尾的文件在java中被称为：属性配置文件。
     其中Properties是专门存放配制文件的一个类。
     
     在属性配置文件中#代表注释
     
     当某个key或者value重复的话，会发生覆盖现象。
     
     key=value
     中间用等号隔开，也可以用冒号隔开
     且中间最好不加空格。
*/
public class IoPropertiesTest01{
    public static void main(String[] args) throws Exception{
        /*
        Properties是一个Map集合，key和Value都是String类型
        想要将userinfo文件中的数据加载到Properties对象当中
        userinfo中的文件内容是
        zhangsan = lisi
        wangwu = zhaoliu
        */
        FileReader reader = new Filereader("userinfo");
        //新建一个map集合
        Properties pro = new Properties();
        //调用Properties对象的load文件中的数据加载到Mpa集合中
        pro.load(reader);//文件的数据顺着管道加载到Map集合当中，其中等号左边做key，右边做value
        //通过key来获取value
        String username = pro.getProperty("zhangsan");//字符串为等号左边的key值
        System.out.println(username);
    }
}
```



## 8、多线程



```java
/*
1、概念：进程是一个应用程序(1个进程是一个软件)。
        线程是一个进程中的执行场景/执行单元。
        
        一个进程可以启动多个线程。
2、对于java程序来说,当在DoS命令窗口中输入:
   java He1loworld回车之后。
   会先启动JVM，而JVM就是一个进程。
   JVM再启动一个主线程调用main方法。
   同时再启动一个垃圾回收线程负责看护,回收垃圾。最起码,现在的java程序中至少有两个线程并发，
   一个是垃圾回收线程,一个是执行main方法的主线程。
   
3、进程和线程是什么关系?举个例子
     阿呵里巴巴:进程
     马云:阿里巴巴的一个线程
     童文红:阿里巴巴的一个线程
     
     京东:进程
     强东:京东的一个线程
     妹妹:京东的一个线程
     
  进程可以看做是现实生活当中的公司。线程可以看做是公司当中的某个员工。
  
  注意:
    进程A和进程B的内存独立不共享。（阿里巴巴和京东资源不会共享的!)
      魔兽游戏是一个进程
      酷狗音乐是一个进程
      这两个进程是独立的,不共享资源。

   线程A和线程B呢?
   在java语言中:
   线程A和线程B，堆内存和方法区内存共享。但是栈内存独立，一个线程一个栈。   
   
   假设启动10个线程,会有10个栈空间，每个栈和每个栈之间，宜不干扰,各自执行各自的,这就是多线程并发。
   
    火车站,可以看做是一个进程。
    火车站中的每一个售票窗口可以看做是一个线程。
    我在窗口1购票，你可以在窗口2购票，你不需要等我，我也不需要等你。
    所以多线程并发可以提高效率。

    java中之所以有多线程机制，目的就是为了提高程序的处理效率。

4、思考一个问题:
   使用了多线程机制之后，main方法结束，是不是有可能程序也不会结束。main方法结束只是主线程结束了，主栈空了，其它的栈(线程)可能还在压栈弹栈。
   
   
5、分析一个问题:对于单核的CPu来说，真的可以做到真正的多线程并发吗?
   对于多核的CPU电脑来说,真正的多线程并发是没问题的。
      4核CPU表示同一个时间点上，可以真正的有4个进程并发执行。
      
      什么是真正的多线程并发?
        t1线程执行t1的。
        t2线程执行t2的。
        t1不会影响t2，t2也不会影响t1。这叫做真正的多线程并发。
        
   单核的cPU表示只有一个大脑:
      不能够做到真正的多线程并发，但是可以做到给人一种"多线程并发"的感觉。
      对于单核的CPu来说，在某一个时间点上实际上只能处理一件事情，
      但是由于CPu的处理速度极快，多个线程之间频繁切换执行，
      跟人来的感觉是:多个事情同时在做!!!!!

      线程A:播放音乐
      线程B:运行魔兽游戏
      线程A和线程B频繁切换执行，人类会感觉音乐一直在播放，
      
      
5、java语言中，实现线程有两种方式，那两种方式为：
   
   java语言支持多线程机制，并且java已经将多线程实现，我们只需要继承就可以了
   
   第一种方式：编写一个类，直接继承java.lang.Thread,重写run方法
   
   使用第二种方式实现接口比较常用，因为一个类实现接口，它后期可以去继承其他类，更灵活
   
*/

```

![image-20210511073900564](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210511073900564.png)

### 1、实现线程的第一种方式

```java
/*
实现线程的第一种方式：
    编写一个类，直接继承java.lang.Thread，重写run方法
    
    怎么创建线程对象？ new就行了
    怎么启动线程呢？   调用线程对象的start()方法。
    
更古不变的道理：
   方法体中永远都是自上而下一次顺序执行的，当某个语句结束完，才会去执行下一条语句。
*/
public class ThreadTest02{
    public static void main(String[] args){
        //这里是main方法，这里的代码属于主线程，在主栈中运行
        //新建一个分支线程对象
        MyThread myThread = new MyThread();
        //启动线程
        
        //myThread.run();不会启动线程，不会分配新的分支栈（这种方式是单线程）
        //start()方法的作用是：启动一个分支线程，在JVM中开辟一个新的栈空间，这段代码完成之后，瞬间就结束了
        //这段代码的任务只是为了开启一个新的栈空间，只要新的栈开出来，start()方法就结束了，线程就启动成功了。
        //启动成功的线程会自动条用run方法，并且run方法在分支栈的栈底部（压栈）
        //run方法在发分支栈的栈底部，main方法在主栈的栈底部，run和main方法是平级的。
        myThread.start();
        for(int i = 0; i < 1000; i++){
            System.out.println("主线程-->" + i);
        }
    }
}
class MyThread extends Thread{
    public void run(){
        //编写程序，这段程序运行在分支线程中（分支栈）
        for(int i = 0; i < 1000; i++){
            System.out.println("分支线程-->" + i);
        }
    }
}
```

### 2、实现线程的第二种方式

```java
/*
第二种方式：编写一个类实现java.lang.Runnable接口
*/
public class ThreadTest03{
    public static void main(String[] args){
        //创建一个可运行的对象
        MyRunnable r = new MyRunnable();
        //将可运行的对象封装成一个线程对象
        Thread t = new Thread(r);
        //启动线程
        t.start();
        
        //合并代码的实现
        //Thread t = new Thread(new MyRunnable());
        for(int i = 0; i < 1000; i++){
            System.out.println("主线程-->" + i);
        }
    }
}
class MyRunnable implements Runnable{
    public void run(){
         for(int i = 0; i < 1000; i++){
            System.out.println("分支线程-->" + i);
        }
    }
}
```

### 3、采用匿名内部类方式

```java
public class ThreadTest04{
    public static void main(String[] args){
        Thread t = new Thread(new Runnable(){
           public void run(){
               for(int i = 0; i < 1000; i++){
                   System.out.println("分支线程->" + i);
               }
           } 
        });
        t.start();
        for(int i = 0; i < 100; i++){
            System.out.println("主线程->"+i);
        }
    }
}
```

### 4、线程的生命周期

![image-20210511084307873](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210511084307873.png)

> 新建状态，运行状态、阻塞转态、死亡状态

### 5、线程对象的获取

```java
/*
1、怎么获取当前线程对象？

2、获取线程对象的名字
   String name = 线程对象.getName();
3、修改线程对象的名字
   线程对象.setName("线程名字");
   
4、当线程没有设置名字的时候，默认的名字有什么规律
   Thread-0
   Thread-1
   Thread-2
   ....

*/

public class ThreadTest05{
    public static void main(String[] args){
        //curreatThread就是当前线程对象
        Thread currentThread = Thread.currentThread();
        System.out.println(currentThread.getName());//main
        
        //创建线程对象
        MyThread2 t = new MyThread();
        //设置线程的名字
        t.setName("tttt");
        //获取线程的名字
        String tName = t.getName();
        System.out.println(tName);
        //启动线程
        t.start();
        
        MyThread2 t2 = new MyThread();
        System.out.println(t2.getName());
        t2.start();
    }
}

class MyThread2 extends Thread{
    public void run(){
       for(int i = 0; i < 100; i++){
           //currentThread就是当前线程对象，当前线程是谁呢？
           //当t1线程执行run方法，那么这个当前线程就是t1
           //当t2线程执行run方法，那么这个当前线程就是t2
           Thread currentThread = Thread.currentThread();
            System.out.println(currentThread.getName() + "-->" + i);
       }
    }
}
```

### 6、阻塞状态

```java
/*
关于线程的sleep方法：
   static void sleep(long millis)
   1、静态方法：Thread.sleep(1000);
   2、单位是毫秒
   3、作用：让当前线程进入休眠状态，进入“阻塞状态”，放弃占有CPU时间片，让给其它线程使用
      这行代码出现在A线程中，A线程就会进入休眠
      这行代码出现B线程，B线程就会进入休眠
   4、Thread.sleep()方法，可以做到这种效果：
      间隔特定的时间，去执行一段特定的代码，每隔多久执行一次。

*/
public class ThreadTest06{
    public static void main(String[] args){
        //让当前线程进入休眠，睡眠5秒
        //当前线程是为主线程
        try{
            Thread.sleep(1000*5);
        }catch(InterruptedException e){
            e.printStackTrace();
        }
        //5秒之后才会执行这里的代码
        System.out.println("hello World");
        
        for(int i = 0; i < 10; i++){
            System.out.println(Thread.currentThread().getName()+"-->" + i);
            //休眠1秒
            try{
                Thread.sleep(1000);
            }catch(InterruptedException e){
                e.printStackTrace();
            }
        }
}
```

```java
/*
关于Thread.sleep()方法的一个面试题：
*/
public class ThreadTest07{
    public static void main(String[] args){
        //创建线程对象
        Thread t = new MyThread3();
        t.setName("t");
        t.start();
        
        //调用sleep方法
        try{
            //问题：这行代码会让线程t进入休眠状态吗?
            //不会
            //以下在执行的时候会转成：Thread.sleep(1000*5);
            //下面一行代码的作用是：让当前线程进入休眠，也就是main线程进入休眠
            //这样的代码出现在main方法中，main线程休眠
            t.sleep(1000*5);
        }catch(InterruptedException e){
            e.printStackTrace();
        }
        System.out.println("hello world");
    }
}
class MyThread3 extends Thread{
    public void run(){
        for(int i = 0; i < 10000; i++){
            System.out.println(Thread.currentThread().getName() + "--->" + i);
            
        }
    }
}
```

```java
/*
终止线程的睡眠

*/
public class ThreadTest08{
    public static void main(String[] args){
        Thread t = new Thread(new MyRunnable2());
        t.setName("t");
        t.start();
        try{
            Thread.sleep(1000*5);
        }catch(InterruptedException e){
            e.printStackTrace();
        }
        //终端t线程的睡眠（这种睡眠的方式倚靠了java的异常处理机制）
        t.interrupt();//干扰
    }
}

class MyRunnable2 implements Runnable{
    public void run(){
        System.out.println(Thread.currentThread().getName() + "-->begin()");
        //睡眠一年
        try{
            Thread.sleep(1000*60*60*24*365);
        }catch(InterruptedException e){
            e.printStackTrace();//不愿让异常信息打印出来，注释掉就好
        }
        //重点：run()当中异常不能throws，只能try catch
        //重写的方法不能抛出比父类更多的异常
        System.out.println(Thread.currentThread().getName() + "-->end()")
    }
}
```

### 7、强行终止线程

```java
/*
java中强行终止线程
  线程对象.stop();不建议这样做，存在很大缺陷：这种方式是直接将线程杀死了，
  线程没有保存的数据将会丢失，不建议使用
*/
public class ThreadTest09{
    public static void main(String[] args){
        Thread t = new Thread(new MyRunnable3());
        t.setName("t");
        t.start();
        try{
            Thread.sleep(1000*5);
        }catch(InterruptedException e){
            e.printStackTrace();
        }
        //5秒之后强行终止线程
        t.stop();//已过时，不建议使用
    }
}

class MyRunnable3 implements Runnable{
    public void run(){
        for(int i = 0; i < 10; i++){
            System.out.println(Thread.currentThread().getName() + "-->" + i);
            try{
                
                Thread.sleep(1000);
            }catch(InterruptedException e){
                e.printStackTrace();
            }
        }
    }
}
```



```java
/*
合理的终止一个线程的执行
*/
public class ThreadTest10{
    public static void main(String[] args){
        //Thread t = new Thread(new MyRunnable4());
        MyRunnable4 r = new MyRunnable4();
        Thread t = new Thread(r);
        t.setName("t");
        t.start();
        try{
            Thread.sleep(1000*5);
        }catch(InterruptedException e){
            e.printStackTrace();
        }
        //终止线程
        //你先要什么时候终止t的执行，修改run为false就好
        r.run = false;
    }
}

class MyRunnable4 implements Runnable{
    boolean run = true;
    //打一个布尔标记
    public void run(){
        for(int i = 0; i < 10; i++){
            if(run){
                System.out.println(Thread.currentThread().getName() + "-->" + i);
                try{
                    
                    Thread.sleep(1000);
                }catch(InterruptedException e){
                    e.printStackTrace();
                }
            }else{
                return;
            }
        }
    }
}
```

### 8、线程调度

```java
/*
1、(这部分内容属于了解)关于线程的调度
1.1、常见的线程调度模型有哪些?
     抢占式调度模型:
        那个线程的优先级比较高，抢到的CPU时间片的概率就高一些/多一些。
        java采用的就是抢占式调度模型。
     均分式调度模型:
        平均分配CPu时间片。每个线程占有的cPu时间片时间长度一样。平均分配,一切平等。
        有一些编程语言,线程调度模型采用的是这种方式。
1.2-java中提供了哪些方法是和线程调度有关系的呢?
     实例方法:
        void setPriority (int newPriority)设置线程的优先级int getPriority ()
        获取线程优先级
          最低优先级1
          默认优先级是5
          最高优先级10
          优先级比较高的获取CPU时间片可能会多一些。
    
    静态方法:
       static void yield(让位方法)
       暂停当前正在执行的线程对象,并执行其他线程
       yield()方法不是阻塞方法。让当前线程让位，让给其它线程使用。
       yield()方法的执行会让当前线程从"运行状态"回到"就绪状态"。
       注意：在回到准备状态的时候，还是可能会抢到时间片的
       
   实例方法void join() 合并线程
*/
```

```java
/*
了解：关于线程的优先级
*/
public class ThreadTest11{
    public static void main(String[] arga){
        System.out.println("最高优先级"+ Thread.MAX_PRIORITY);
        System.out.println("最低优先级"+Thread.MIN_PRIORITY);
        System.out.println("默认优先级"+ Thread.NORM_PRIORITY);
        //获取当前线程对象过去当前线程优先级
        Thread currentThread = Thread.currentThread();
        //main线程的默认优先级为：5
        Sysetem.out.println(currentThread.getName() + "线程的默认优先级"+ currentThread.getPriority());
        //设置主线程的优先级
        Thread.currentThread().setPriority(1);
        Thread t = new Thread(new MyRunnable5());
        t.setPriority(10);
        t.setName("t");
        t.start();
        for(int i = 0; i < 100; i++){
            Sysetem.out.println(currentThread.getName() + "-->"+ i);
        }
    }
}
class MyRunnable5 implements Runnable{
    public void run(){
        for(int i = 0; i < 100; i++){
            //大概率方向执行优先级比较高的。
            Sysetem.out.println(currentThread.getName() + "-->"+ i);
        }
    }
}
```

```java
/*
让位：当前线程暂停，回到就绪状态，让给其它线程
静态方法：Thread.yield();
*/
public class ThreadTest12{
    public static void main(String[] args){
        Thread t = new Thread(new MyRunnable6());
        t.setName("t");
        t.start();
        
        for(int i = 1; i < 100; i++){
            System.out.println(Thread.currentThread().getName() + "-->" + i);
        }
    }
}
class MyRunnable6 implements Runnable{
    public void run(){
        for(int i = 0; i < 100; i++){
            if(i % 20 == 0) {//20次让一位
                Thread.yield();
                
            }
            Sysetem.out.println(currentThread.getName() + "-->"+ i);
            
        }
    }
}
```

```java
/*
线程合并
*/
public class ThreadTest13{
    public static void main(String[] args){
        System.out.println("main begin");
        Thread t = new Thread(new MyRunnable7());
        t.setName("t");
        t.start();
        
        try{
            t.join();//t合并到当前线程中，当前线程受阻塞，t线程执行到结束
        }catch(InterruptedException e){
            e.printStackTrace();
        }
        System.out.println("main over");
    }
}
class MyRunnable7 implements Runnable{
    public void run(){
        for(int i = 0; i < 100; i++){
             Sysetem.out.println(currentThread.getName() + "-->"+ i);
            
        }
    }
}
```

### 9、线程的安全（重点）

```java
/*
关于多线程并发环境下，数据安全问题
  什么时候数据在多线程并发的环境下会存在安全问题
    三个条件：
       条件一：多线程并发
       条件二：有共享数据
       条件三：共享数据有修改的行为
  2.3、怎么解决线程安全问题呢?
       
       线程排队执行。(不能并发）。用排队执行解决线程安全问题。这种机制被称为:线程同步机制。
       专业术语叫做:线程同步，实际上就是线程不能并发了，线程必须排队执行。
     
     怎么解决线程安全问题呀?
       使用"线程同步机制”。
     线程同步就是线程排队了，线程排队了就会牺牲一部分效率，没办法，数据安全第一位，
     只有数据安全了，我们才可以谈效率。数据不安全，没有效率的事儿。
2.4、说到线程同步这块,涉及到这两个专业术语:
     异步编程模型:
        线程t1和线程t2，各自执行各自的，t1不管t2，t2不管t1，谁也不需要等谁,
        这种编程模型叫做:异步编程模型。
        其实就是:多线程并发(效率较高。)

       异步就是并发。
     同步编程模型:
        线程t1和线程t2，在线程t1执行的时候，必须等待t2线程执行结束,或者说在t2线程执行的时候,
        必须等待t1线程执行结束,两个线程之间发生了等待关系,这就是同步编程模型。
        效率较低。线程排队执行。

        同步就是排队。
*/
```

```java
/*
银行账户非同步机制缺陷
*/

public class AccoutTest01{
    public static void main(String[] args){
        //创建账户对象
        Account act = new Account("act - 001",10000);
        //创建两个线程
        Thread t1 = new AccountThread(act);
        Thread t2 = new AccountThread(act);
        //设置name
        t1.setName("t1");
        t2.setName("t2");
        //启动取款线程
        t1.start();
        t2.start();
    }
}
class Account{
    private String actno;
    private double balance;
    public String getActno{
        return actno; 
    }
    public void setActno(String actno){
        this.actno = actno;
    }
    public double SetBalance(){
        return balance;
    }
    public void setBalance(double balance){
        this.balance = balance;
    }
    
    //取款方法
    public void withdraw(double money){
        //取款之前余额
        double before = this.getBalance();
        //取款之后余额
        double after = before - money;
        //这里模拟以下网洛延迟，100%会出问题
        try{
            Thead.sleep("1000");
            
        }catch(InterruptedException e){
            e.printStackTrace();
        }
        //更新余额
        this.setBalance(after);
    }
}

class AccountThread extends Thread{
    //两个线程必须共享同一个账户对象
    private Account act;
    public AccountThread(Account act){
        this.act = act;
    }
    public void run(){
        //run方法的执行表示取款操作
        //t1,t2并发执行此方法
        //假设取款5000
        double money = 5000;
        //取款
        act.withdraw(money);
        //t1执行到这里了，但是还没有来得及执行这行代码，t2线程进来withdraw方法了，此时一定出问题

        System.out.println("账户" + act.getActno()+"取款成功，余额"+ act.getBalance());
    }
}
```

```java
/*
使用线程同步机制来解决线程安全问题
*/
public class AccoutTest01{
    public static void main(String[] args){
        //创建账户对象
        Account act = new Account("act - 001",10000);
        //创建两个线程
        Thread t1 = new AccountThread(act);
        Thread t2 = new AccountThread(act);
        //设置name
        t1.setName("t1");
        t2.setName("t2");
        //启动取款线程
        t1.start();
        t2.start();
    }
}
class Account{
    private String actno;
    private double balance;
    public String getActno{
        return actno; 
    }
    public void setActno(String actno){
        this.actno = actno;
    }
    public double SetBalance(){
        return balance;
    }
    public void setBalance(double balance){
        this.balance = balance;
    }
    
    //取款方法
    public void withdraw(double money){
        //以下的这几行代码必须是线程排队的，不能并发
        //一个线程把这里的代码全部执行结束之后，另外一个线程才能进来
        /*
        线程同步机制的语法是：
           synchronized(){
              //线程同步代码块
           }
           synchronized后面小括号中传的这个“数据”是相当关键的，这个数据必须是多线程共享的数据
           才能达到多线程排队
           
           ()中写什么？
              那就要看想让那些线程同步了
                假设t1,t2,t3,t4,t5有5个线程
                只希望t1,t2,t3排队，t4,t5不需要排队怎么办？
                你一定要在()中写一个t1,t2,t3的共享对象，而这个对于t4,t5来说不是共享的
                
             这里的共享对象是：账户对象
             账户对象是共享的，那么this就是账户对象吧！！
             //不一定是this,只要是多线程共享个对象就行
             
             在java语言中，任何一个对象都有一把锁”，其实这把锁就是标记。
             (只是把它叫做锁。)100个对象，100把锁。1个对象1把锁。
          以下代码的执行原理?
               1、假设t1和t2线程并发，开始执行以下代码的时候，肯定有一个先一个后。
               2、假设t1先执行了，遇到了synchronized，这个时候自动找后面共享对象”的对象锁,
                  找到之后，并占有这把锁，然后执行同步代码块中的程序，在程序执行过程中一亘都
                  是占有这把锁的。直到同步代码块代码结束，这把锁才会释放。
              3、假设t1已经占有这把锁，此时t2也遇到synchronized关键字，也会去占有后面共享对
                 象的这把锁，结果这把锁被t1占有，t2只能在同步代码块外面等待t1的结束，直到t1
                 把同步代码块执行结束了,t1会归还这把锁，此时t2终于等到这把锁，然后t2占有这把
                 锁之后，进入同步代码块执行程序。
                 这样就达到了线程排怼执行。
             这里需要注意的是:这个共享对象一定要选好了。这个共享对象一定是你需要排队执行的这
             些线程对象所共享的。
        */
        synchronized(this){
            double before = this.getBalance();
            double after = before - money;
            try{
                Thead.sleep("1000");
            }catch(InterruptedException e){
                e.printStackTrace();
            }
            this.setBalance(after);
        }
    }
}

class AccountThread extends Thread{
    //两个线程必须共享同一个账户对象
    private Account act;
    public AccountThread(Account act){
        this.act = act;
    }
    public void run(){
        double money = 5000;
        //取款
        act.withdraw(money);

        System.out.println("账户" + act.getActno()+"取款成功，余额"+ act.getBalance());
    }
}
```

```java

package ThreadTest;
import java.lang.InterruptedException;
public class AccountTest01 {
	public static void main(String[] args){
        //创建账户对象
        Account act = new Account("act - 001",10000);
        //创建两个线程
        Thread t1 = new AccountThread(act);
        Thread t2 = new AccountThread(act);
        //设置name
        t1.setName("t1");
        t2.setName("t2");
        //启动取款线程
        t1.start();
        t2.start();
    }
}
class Account{
    private String actno;
    private double balance;
    public Account(String actno,double balance) {
    	this.actno = actno;
    	this.balance = balance;
    }
    //对象
    Object obj = new Object();//实例变量(Account对象是多线程共享的，Account对象中的实例变量obj也是共享的)
    Object obj3 = new Object();//都是共享的
    public String getActno(){
        return actno; 
    }
    public void setActno(String actno){
        this.actno = actno;
    }
    public double getBalance(){
        return balance;
    }
    public void setBalance(double balance){
        this.balance = balance;
    }
    
    //取款方法
    public void withdraw(double money){
        //Object obj2 = new Object();
        //synchronized(this){
        //synchronized(obj){//括号只要是共享对象就行
        //synchronized("abc"){//也行，因为“abc”在字符串1常量池当中，只有一个
        //synchronized(obj2){//不行局部变量不共享，不被多次用到
            
            double before = this.getBalance();
			double after = before - money;
            try{
                Thread.sleep(1000);
            }catch(InterruptedException e){
                e.printStackTrace();
            }
            this.setBalance(after);
        }
    }
}

class AccountThread extends Thread{
    //两个线程必须共享同一个账户对象
    private Account act;
    public AccountThread(Account act){
        this.act = act;
    }
    public void run(){
        double money = 5000;
        //取款
        act.withdraw(money);

        System.out.println("账户" + act.getActno()+"取款成功，余额"+ act.getBalance());
    }
}

```

```java
/*
3、Java中有三大变量?
   实例变量:在堆中。 
   静态变量:在方法区。
   局部变量:在栈中。
 以上三大变量中:
    局部变量永远都不会存在线程安全问题。
       因为局部变量不共享。(一个线程一个栈。)
       局部变量在栈中。所以局部变量永远都不会共享。
   实例变量在堆中,堆只有1个。
   
   静态变量在方法区中,方法区只有1个。
   
   堆和方法区都是多线程共享的所以可能存在线程安全问题。
   
4、如果使用局部变量的话：
   建议使用：StringBuilder.
   因为局部变量不存在线程安全问题。选则StringBuilder
   StringBuffer效率比较低。
   
   ArrayList是非线程安全的
   Vector是线程安全的
   HahsMap HashSet是非线程安全的
   Hahstable是线程安全的。
   
5、总结：
   synchronized有两种写法：
     第一种：同步代码块
       灵活
       synchronized(线程共享对象){
       
       }
       
     第二种：在实例方法上个使用synchronized
       表示共享对象一定是this
       并且同步代码块是整个方法体
       
     第三种：在静态方法上使用synchronized
       表示找类锁
       类锁永远只有一把
       就算创建了100个对象，那类锁也只有一把
       
     对象锁：一个对象一把锁，100个对象100把锁
     类锁：100个对象也只可能是1把锁
*/
```

```java
//实例方法上加synchronized
package ThreadTest;
import java.lang.InterruptedException;
public class AccountTest01 {
	public static void main(String[] args){
        //创建账户对象
        Account act = new Account("act - 001",10000);
        //创建两个线程
        Thread t1 = new AccountThread(act);
        Thread t2 = new AccountThread(act);
        //设置name
        t1.setName("t1");
        t2.setName("t2");
        //启动取款线程
        t1.start();
        t2.start();
    }
}
class Account{
    private String actno;
    private double balance;
    public Account(String actno,double balance) {
    	this.actno = actno;
    	this.balance = balance;
    }
    //对象
    Object obj = new Object();//实例变量(Account对象是多线程共享的，Account对象中的实例变量obj也是共享的)
    Object obj3 = new Object();//都是共享的
    public String getActno(){
        return actno; 
    }
    public void setActno(String actno){
        this.actno = actno;
    }
    public double getBalance(){
        return balance;
    }
    public void setBalance(double balance){
        this.balance = balance;
    }
    
    //取款方法
    public void withdraw(double money){
            
            double before = this.getBalance();
			double after = before - money;
            try{
                Thread.sleep(1000);
            }catch(InterruptedException e){
                e.printStackTrace();
            }
            this.setBalance(after);
        
    }
}

class AccountThread extends Thread{
    //两个线程必须共享同一个账户对象
    private Account act;
    public AccountThread(Account act){
        this.act = act;
    }
    public void run(){
        double money = 5000;
        //取款
        act.withdraw(money);

        System.out.println("账户" + act.getActno()+"取款成功，余额"+ act.getBalance());
    }
}

```

```java
//面试题doOther方法执行的时候，需要等待doSome方法得结束吗？
   //不需要，因为dother方法没有被锁(synchronized)
public class Exam01{
    public static void main(String[] args){
        MyClass mc = new MyClass();
        
        Thread t1 = new MyThread(mc);
        Thread t2 = new MyThread(mc);
        
        t1.setName("t1");
        t2.setName("t2");
        
        t1.start();
        Thread.sleep(1000);//这个休眠的作用是保证t1先执行
        t2.start();
        
        
    }
}
class MyThread extends Thread{
    private MyClass mc;
    public MyThread(MyClass mc){
        this.mc = mc;
    }
    public void run(){
        if(Thread.currentThread().getName().equals("t1")){
            mc.doSome();
        }
        if(Thread.currentThread().getName().equals("t2")){
            mc.doOther();
        }
    }
}

class MyClass{
    public synchronized void doSome(){
        System.out.println("doSome begin");
        try{
            Thread.sleep(1000*10)；
        }catch(InterruptedExcetion e){
            e.printStackTrace();
        }
        System.out.println("doSome over");
    }
    
    public void doOther(){
        System.out.println("doOther begin");
        System.out.println("doOther over");
    }
}
```

```java
//面试题doOther方法执行的时候，需要等待doSome方法得结束吗？
   //需要，因为dother方法被锁(synchronized)需要那个doSOme解锁，才能用此方法（排队）
public class Exam01{
    public static void main(String[] args){
        MyClass mc = new MyClass();
        
        Thread t1 = new MyThread(mc);
        Thread t2 = new MyThread(mc);
        
        t1.setName("t1");
        t2.setName("t2");
        
        t1.start();
        Thread.sleep(1000);//这个休眠的作用是保证t1先执行
        t2.start();
        
        
    }
}
class MyThread extends Thread{
    private MyClass mc;
    public MyThread(MyClass mc){
        this.mc = mc;
    }
    public void run(){
        if(Thread.currentThread().getName().equals("t1")){
            mc.doSome();
        }
        if(Thread.currentThread().getName().equals("t2")){
            mc.doOther();
        }
    }
}

class MyClass{
    public synchronized void doSome(){
        System.out.println("doSome begin");
        try{
            Thread.sleep(1000*10)；
        }catch(InterruptedExcetion e){
            e.printStackTrace();
        }
        System.out.println("doSome over");
    }
    
    public synchronized void doOther(){
        System.out.println("doOther begin");
        System.out.println("doOther over");
    }
}
```

```java
//面试题doOther方法执行的时候，需要等待doSome方法得结束吗？
   //不需要，因为线程不共享对象（两把锁）
public class Exam01{
    public static void main(String[] args){
        MyClass mc1 = new MyClass();
        MyClass mc2 = new MyClass();
        
        Thread t1 = new MyThread(mc1);
        Thread t2 = new MyThread(mc2);
        
        t1.setName("t1");
        t2.setName("t2");
        
        t1.start();
        Thread.sleep(1000);//这个休眠的作用是保证t1先执行
        t2.start();
        
        
    }
}
class MyThread extends Thread{
    private MyClass mc;
    public MyThread(MyClass mc){
        this.mc = mc;
    }
    public void run(){
        if(Thread.currentThread().getName().equals("t1")){
            mc.doSome();
        }
        if(Thread.currentThread().getName().equals("t2")){
            mc.doOther();
        }
    }
}

class MyClass{
    public synchronized void doSome(){
        System.out.println("doSome begin");
        try{
            Thread.sleep(1000*10)；
        }catch(InterruptedExcetion e){
            e.printStackTrace();
        }
        System.out.println("doSome over");
    }
    
    public synchronized void doOther(){
        System.out.println("doOther begin");
        System.out.println("doOther over");
    }
}
```

```java
//面试题doOther方法执行的时候，需要等待doSome方法得结束吗？
   //需要，因为静态方法是类锁，不管创建了几个对象，类锁只有一把。
//以下方法是排他锁
public class Exam01{
    public static void main(String[] args){
        MyClass mc1 = new MyClass();
        MyClass mc2 = new MyClass();
        
        Thread t1 = new MyThread(mc1);
        Thread t2 = new MyThread(mc2);
        
        t1.setName("t1");
        t2.setName("t2");
        
        t1.start();
        Thread.sleep(1000);//这个休眠的作用是保证t1先执行
        t2.start();
        
        
    }
}
class MyThread extends Thread{
    private MyClass mc;
    public MyThread(MyClass mc){
        this.mc = mc;
    }
    public void run(){
        if(Thread.currentThread().getName().equals("t1")){
            mc.doSome();
        }
        if(Thread.currentThread().getName().equals("t2")){
            mc.doOther();
        }
    }
}

class MyClass{
    //synchronized出现在静态方法上是找类锁
    public synchronized static void doSome(){
        System.out.println("doSome begin");
        try{
            Thread.sleep(1000*10)；
        }catch(InterruptedExcetion e){
            e.printStackTrace();
        }
        System.out.println("doSome over");
    }
    
    public synchronized static void doOther(){
        System.out.println("doOther begin");
        System.out.println("doOther over");
    }
}
```

### 10、死锁

```java
/*
死锁代码要会写
一般面试官要求你会写
只有会写，才会在以后的开发种注意这个是儿
因为死锁很难调试
   synchronized不要嵌套使用，否则容易发生死锁
*/
public class DeadLock{
    public static vod main(String[] args){
        Object o1 = new Object();
        Object o2 = new Object();
        
        //t1和t2两个线程共享o1,o2
        Thread t1 = new MyThread(o1,o2);
        Thread t2 = new MyThread(O1,o2);
    }
}

class MyThread1 extends Thread{
    Object o1;
    Object o2;
    public MyThread1(Object o1, Object o2){
        this.o1=o1;
        this.o2=o2;
    }
    public void run(){
        synchronized(o1){
            try{
                Thread.sleep(1000);
            }catch(InterruptedException e){
                e.printStaceTrace();
            }
            synchronized(o2){
                
            }
        }
    }
}
//造成每个线程都锁不了第二个线程对象，因为在那两个都互相锁住了。
class MyThread extends Thread{
    Object o1;
    Object o2;
    public MyThread(Object o1, Object o2){
        this.o1 = o1;
        this.o2 = o2;
    }
    public void run(){
        synchronized(o1){
            try{
                Thread.sleep(1000);
            }catch(InterruptedException e){
                e.printStaceTrace();
            }
            synchronized(o2){
                
            }
        }
    }
}
```

```mardkown
6、聊一聊，我们以后开发中应该怎么解决线程安全问题?
     是一上来就选择线程同步吗?synchtonizec
        不是,synchronized会让程序的执行兹率降低，用户体验不好。系统的用户存旺量降低。
        用户体验差。在不得已的情况下再选择线程同步机制。
     第一种方案:尽量使用局都变基代替"实例变量和静态变量”。

     第二种方案:如果必须是实例变量，那么可以考虑创建多个对象，这样
               实例变量的内存就不共享了。(一个线程对应1个对象100个线程对应100个对象，对象不
               共享,就没有薮据安全问题了。

     第三种方案:如果不能便用局都变量，.对象也不能创建多个，这个时候就只能选择synchronized了.
               线程间步机制。
```

```java
/*
守护线程
1、线程这块还有那些内容呢?列举一下
   1.1、守护线程
      java语言中线程分为两大类:
        一类是:用户线程
        一类是:守护线程(后台线程)
      其中具有代表性的就是:垃圾回收线程（守护线程)。
      
      守护线程的特点:
         一般守护线程是一个死循环，所有的用户线程只要结束，守护线程自动结束。(用户线程结束，守护线程没必要守护了)
         
         注意:主线程main方法是一个用户线程。守护线程用在什么地方呢?
  
             每天00:00的时候系统数据自动备份。
             这个需要使用到定时器，并且我们可以将定时器设置为守护线程。一直在那里看着，
             每到00:00的时候就备份一次。所有的用户线程如果结束了，守护线程自动退出，
             没有必要进行数据备份了。
*/
public class ThreadTest14{
    public static void main(String[] args){
        Thread t = new BakDateThread();
        t.setName("备份数据得线程");
        //启动线程之前，将线程设置为守护线程
        t.setDaemon(true);
        t.start();
        
        //主线程
        for(int i = 0; i < 10; i++){
            System.out.println(Thread.currentThread().getName() + "-->"+i);
            try{
                Thread.sleep(1000);
            }catch(InterruptedException e){
                e.printStackTrace();
            }
        }
    }
}

class BakDataThread extends Thread{
    public void run(){
        int i = 0;
        while(true){
            System.out.println(Thread.currentThread().getName() + "-->"+(++i));
            try{
                Thread.sleep(1000);
            }catch(InterruptedException e){
                e.printStackTrace();
            }
        }
    }
}
```

### 11、定时器

```markdown
1.2、定时器
     定时器的作用:
     间隔特定的时间,执行特定的程序。
     每周要进行银行账户的总账操作。每天要进行数据的备份操作。

   在实际的开发中，每隔多久执行一段特定的程序，这种需求是很常见的，
   那么在java中其实可以采用多种方式实现:
         可以使用sleep方法，睡眠，设置睡眠时间，没到这个时间点醒来，执行任务。这种方式是最原始的定时器。(比较low)
         在java的类库中已经写好了一个定时器:java.util.Timer，可以直接拿来用。不过，这种方式在目前的开发中也很少用，因为现在有很多高级框架都是支持定时任务的。

        在实际的开发中，目前使用较多的是Spring框架中提供的springTask框架，这个框架只要进行简单的配置，,就可以完成定时器的任务。
```

```java
/*
使用定时器指定定时任务
*/
public class TimerTest{
    public static void main(String[] args){
        //创建定时器对象
        Timer timer = new Timer();
        //Timer timer = new Timer(true);//守护线程的方式
        //指定定时任务
        //timer.schedule(定时任务(可以是定时任务对象)，第一次执行时间，间隔多久执行一次);//时间单位为毫秒
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String firstTime = sdf.prase("2017-03-22 08:24:36");
        timer.schedule(new LogTimerTask(),firstTime,1000*10);//如果想要在定时任务处使用抽象类，则必须在括号后加大括号，使用匿名内部类
    } 
}
//编写一个定时任务类
//假设这是一个记录日志得定时任务
class LogTimerTask extends TimerTask{
    public void run(){
        //编写需要执行的任务就可以了
         SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String strTime = sdf.format(new Date());
        System.out.println(strTime + "成功的完成了一次数据备份！");
    }
}
```

### 12、实现线程的第三种方式

```java
/*1.3、实现线程的第三种方式:实现callable接口。（JDK8新特性。)
      这种方式实现的线程可以获取线程的返回值。
          之前讲解的那两种方式是无法获取线程返回值的，因为run方法返回void.
       思考:
          系统委派一个线程去执行一个任务，该线程执行完任务之后，可能会有一个执行结果,
          我们怎么能拿到这个执行结果呢?
       使用第三种方式:实现callable接口方式。
       这种方式的优点:可以获取到线程的执行结果。
       
       这种方式的缺点:效率比较低，在获取t线程执行结果的
                     时候，当前线程受阻塞，效率较低。
*/
import java.util.concurrent.FutureTask;
public class ThreadTest15{
    public static void main(String[] args)throws Exception{
        //第一步创建一个“未来任务类”对象
        //参数非常重要，需要给出一个Callable接口实现类对象
        FutureTask task = new FutureTask(new Callable(){
            public Object call() throws Excption{//call方法就相当于run方法
                //只不过这个有返回值
                //线程执行一个任务，执行之后可能会有一个执行结果
                //模拟执行
                System.out.println("call method begin");
                Thread.sleep(1000 * 10);
                System.out.println("call method end!");
                int a = 100;
                int b = 200;
                return a + b;//自动装箱（300自动变成Integer）
            }
        });
        
        //创建线程对象
        Thread t = new Thread(task);
        //启动线程
        t.start();
        
        //这里main方法，实在主线程中
        //在主线程中，怎么获取t线程返回结果？
        //get()方法得执行会导致（“当前线程的阻塞”）
        Object obj = task.get();
        System.out.println("线程的执行结果"+obj);
        
        //main方法这里得程序想执行必须等待get()方法结束
        //而get()方法可能需要很久，因为get()方法是为了那另一个线程的执行结果
        //另一个线程执行是需要时间的
        System.out.println("hello world");
    }
}
```

### 13、wait和notify方法（生产者和消费者模式）

```java
/*
1.4、关于object类中的wait和notify方法。（生产者和消费者模式!)
     第一: wait和notify方法不是线程对象的方法，是java中任何一个java对象都有的方法,因为这两个
          方式是object类中自带的。

      wait方法和notify方法不是通过线程对象调用，
     
         不是这样的: t.wait()，也不是这样的: t.notify () ..不对。
         
     第二: wait()方法作用?
          Object o = new Object();
          o.wait();
          表示:
             让正在o对象上活动的线程进入等待状态,无期限等待，直到被唤醒为止。
             o.wait();方法的调用,会让"当前线程(正在o对象上活动的线程）"进入等待状态。

     第三:notify()方法作用?
          Object o =new object() ;
          o . notify () ;
         表示:
         唤醒正在o对象上等待的线程。
         
      还有一个notifyAl1()方法:
      这个方法是唤醒o对象上处于等待的所有线程。


*/
```

![image-20210513105404340](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210513105404340.png)

```java
/*
1、使用wait方法和notify方法实现生产者和消费者模式”
2、什么是“生产者和消费者模式”?
   生产线程负责生产，消费线程负责消费。
   生产线程和消费线程要达到均衡。

   这是一种特殊的业务需求，在这种特殊的情况下需要使用wait方法和notify方法。

3、wait和notify方法不是线程对象的方法，是普通java对象都有的方法。

4、wait方法和notify方法建立在线程同步的基础之上。因为多线程要同时操作一个仓库。
   有线程安全问题。
5、wait方法作用: o.wait()让正在o对象上活动的线程t进入等待状态，
   并且释放掉t线程之前占有的o对象的锁。
6、notify方法作用: o.notify()让正在o对象上等待的线程唤醒，
   只是通知，不会释放o对象上之前占有的锁。
   
7、模拟这样一个需求:
   仓库我们采用List集合。
   
   List集合中假设只能存储1个元素。
   1个元素就表示仓库满了。
   如果List集合中元素个数是0，就表示仓库空了。
   保证List集合中永远都是最多存储1个元素。
   必须做到这种效果:生产1个消费1个。
*/
public class ThreadTest16{
    public static void main(String[] args){
        //创建一个仓库对象，共享的
        List list = new ArrayList();
        //创建两个线程对象
        //生产者线程
        Thread t1 = new Thread(new Producer(list));
        //消费者线程
        Thread t2 = new Thread(new Consumer(listt));
        
        t1.setName("生产者线程");
        t2.serName("消费者线程");
        
        t1.start();
        t2.start();
    }
}
//生产线程
class Producer implements Runnable{
    private List list;
    public Producer(List list){
        this.list = list;
    }
    public void run(){
        //一直生产（使用死循环来模拟一直生产）
        while(true){
            //给仓库list加锁
            synchronized(list){
                if(list.size() > 0){//大于0说明仓库中已经有一个元素了
                    try{
                        //当前线程进入等待状态，并且释放Producer之前占有的list集合的锁
                        list.wait();
                    }catch(InterruptedException e){
                        e.printStackTrace();
                    }  
                    //程序执行到这里说明仓库是空的，可以生产
                    Object obj = new Object();
                    list.add(obj);
                    System.out.println(Thread.currentThread().getName() + "--->" + obj);
                    //唤醒消费者进行消费
                    list.notify();
                }
            }
            
        }
    }
}
//消费线程
class Consumer implements Runnable{
    private List list;
    public Consumer(List list){
        this.list = list;
    }
    public void run(){
         //一直消费（使用死循环来模拟一直消费）
        while(true){
            //给仓库list加锁
            synchronized(list){
                if(list.size() == 0){//说明仓库中空了
                    try{
                        //当前线程进入等待状态，并且释放Consumer之前占有的list集合的锁
                        list.wait();
                    }catch(InterruptedException e){
                        e.printStackTrace();
                    }  
                    //程序执行到这里说明仓库是不空的，可以消费
                    Object obj = new Object();
                    list.remove(0);
                    System.out.println(Thread.currentThread().getName() + "--->" + obj);
                    //唤醒生产者进行生产
                    list.notify();
                }
            }
            
        }
    }
}
```



## 9、网络通信协议

```java
/*
InetAddress类的常用方法
1、getLocalHost()
   public static InetAddress getLocalHost() throws UnknownHostException
    返回本地主机的地址。 这是通过从系统检索主机的名称，然后将该名称解析为InetAddress 。
    
2、getByName()
   public static InetAddress getByName(String host) throws UnknownHostException
   参数 
     host - 指定的主机，或 null 。 
   结果 
    返回给定主机名的IP地址。 
3、getHostAddress()
    public String getHostAddress()
      返回文本显示中的IP地址字符串。 
4、getHostName()
   public String getHostName()
    获取此IP地址的主机名。 
    
5、isReachable()
  public boolean isReachable(int timeout) throws IOException
    测试该地址在timeout秒内是否可达。
    timeout - 呼叫中止之前的时间（以毫秒为单位）
*/

public class Example01{
    public static void main(String[] args)throws Exception{
        //获取IP地址对象
        InetAddress localAddress = InetAddress.getLocalHost();//返回当前主机的IP地址对象（获取IP地址和主机名的方法）
        InetAddress remoteAddress = InetAddress.getByName("www.itcast.cn");//返回指定主机名称的IP地址
        System.out.println("本机的IP地址："+localAddress.getHostAddress());//调用以字符串形式输出的方法
        System.out.println("itcase的IP地址："+remoteAddress.getHostAddress());//调用以字符串形式输出的方法
        System.out.println("itcase3秒是否可达本机:"+remoteAddress.isReachable(3000));
        System.out.println("itcase的主机名为："+remoteAddress.getHostName());
        
    }
}
```

### 1、UDP网络程序

```markdown
UDP是无连接通信协议，在数据传输时，发送端和接收端不建立逻辑关系，简单来说，当一台计算机向另外一台计算机发送数据时，发送端不会确认接收端是否存在，就会发出数据，同样接收端在收到数据时，也不会向发送端反馈是否收到数据，因此通常用于音频，视频，普通数据的传输，当传输重要数据的时候会发生数据丢失，在传输重要数据的时候，不建议用UDP网络程序。
一、Class DatagramPacket，该类主要是发送/接受数据包
   1、常见的构造方法：
     1.DatagramPacket(byte[] buf, int length)
       构造一个 DatagramPacket用于接收长度的数据包 length 。只能用于接收端，用来接受数据，不能用来发送端，发送端需要发送端口号和IP地址等信息。
     2.DatagramPacket(byte[] buf, int length, InetAddress address, int port) 
      构造用于发送长度的分组的数据报包 length指定主机上到指定的端口号。常用于发送端
      
  2、常见的方法；
    1. InetAddress getAddress() 
      返回该数据报发送或接收数据报的计算机的IP地址。
    2. int getLength() 
      返回要发送的数据的长度或接收到的数据的长度。 
      
    3. int getPort() 
      返回发送数据报的远程主机上的端口号，或从中接收数据报的端口号。  
    4、byte[] getData() 
      返回将要接收或者是要发送的数据。返回缓冲区的数据。
      
二、Class DatagramSocket 该类的实例化对象可以发送和接受DatagramPacket数据包。
   1、常见的构造方法：
     1. DatagramSocket() 
       该构造方法主要用于创建 发送端 的DatagramSocket对象，在创建DatagramSocket对象时，没有指定端口号，系统会其分配一个没有其它网络程序使用的的端口号。
       
     2. DatagramSocket(int port) 
       该构造方法用于创建接收端的DatagramSocket对象，又可以创建发送端的DatagramSocket对象，在创建接收端DatagramSocket对象时，必须要指定一个端口号，这样就可以监听指定的端口。
       
     3. DatagramSocket(int port, InetAddress laddr) 
       该构造方法在创建DatagramSocket对象不仅指定了端口号，还制定了IP地址，
       
   2、常见的方法：
     1. void close()  关闭当前的Socket,通知驱动程序释放这个Socket保留的资源。
     
     2. void send(DatagramPacket p)  
       该方法主要用于发送DatagramPacket数据包，发送的数据包中包含将要方法的数据，数据的长度，远程主机的IP地址和端口号。
       
     3. void receive(DatagramPacket p)  
       该方法主要用于接收到数据填充到DatagramPacket数据包中，在所接收到数据包之前一直除于堵塞状态，只有接收到数据包时，该方法才会返回。
```



```java
/*
发送端
*/
public class Sender{
    public static void main(String[] args)
    {
        //1.创建DatagramSocket对象，指定发送端程序的端口号
        DatagramSocket ds = new DatagramSocket(3000);
            
        //2.准备要发送的数据
        String str = "hello world";
        byte[] buf = str.getBytes();
        //3.创建一个DatagramPacket对象，用来封装要发送的数据
        //数据包含：要发送的数据、数据的长度、接收端的IP地址，接收端的端口号
        DatagramPacket dp = new DatagramPacket(buf, buf.length,InetAddress.getByName("localhost"),8954);
        
        //4.发送数据包
        ds.send(dp);
        //释放资源
        ds.close();
            
            
    }
}

/*
接收端
*/
public class Receiver{
    public static void main(String[] args)
    {
        //1、指定一个DatagramSocket对象，指定接受的端口号
        DatagramSocket ds = new DatagramSocket(8954);
        //2、定义一个DatagramPacket对象，用于接收数据
        byte[] buf = new byte[1024];
        DatagramPacket dp = new DatagramPacket(buf,buf.length);
        //3、调用接受数据的1方法
        System.out.println("等待接收数据");
        ds.receive(dp);//等待接收数据，如果没有数据，则会堵塞
        //4、查看接收到的数据信息
        byte[] data = dp.getData();
        int length = dp.getLength();//查看接收数据的长度
        String ip = dp.getAddress().getHostAddress();//获取发送端的IP地址
        int port = dp.getPort();//获取发送端的端口号
        String str = new String(data,0,length);
        System.out.println(str + "from" + ip + ":"port);
        //5、释放资源
        ds.close();
        
    }
}

//注意当出现：Addres already in use:Cannot bind
/*
就意味着：想要使用的端口被占用，因为一个端口只能运行一个程序，遇到这种情况，再DOS命令行窗口上，输入“netstat -ant”命令来查看计算机端口的占用情况，只要把相应的程序关闭即可。
*/
```

### 2、聊天程序设计

```java
/*
聊天室
*/
public class CharRoom{
    public static void main(String[] args){
        System.out.println("欢迎你来到聊天室！");
        Scanner sc = new Scanner(System.in);
        System.lout.print("请输入本程序发送端口号：");
        int sendPort = sc.nextInt();
        System.out.print("请输入本程序接受端口号：");
        int receivePort = sc.nextInt();
        System.out.println("聊天系统启动！！");
        
        new Thread(new SendTask(sendPort),"发送端任务").start();//发送操作
        new Thread(new ReceiveTask(receivePort),"接受端任务").start();//接受操作
    }
}

/*
发送数据的任务类
*/
public class SendTask implements Runnable{
    private int sendPort;//发送端的端口号
    public SendTask(int sendPost){
        this.sendPort = sendPort;
    }
    public void run(){
        try{
            //1、创建DatagramSocket对象
            DatagramSocket ds = new DatagramSocket();
            //输入要发送的数据
            Scanner sc = new Scanner(System.in);
            while(true){
                String data = sc.nextLine();//键盘获取接收数据
                //3、封装数据到DatagramPacket对象中
                byte[] buf = data.getBytes();
                DatagramPacket dp = new DatagramPacket(buf,buf.length,InetAddress.getByName("127.0.0.225"),sendPort);
                //4、发送数据
                ds.send(dp);
            }catch(Exception e){
                e.printStackTrace();
            }
        }
    }
}

/*
接受数据任务类
*/
public class ReceiveTask implements Runnable{
    private int receivePort;
    public ReceiveTask(int receivePort){
        this.receivePost = receivePort;
    }
    public void run(){
        try{
            //1、创建DatagramSocket对象
            DatagramSocket ds = new DatagramSocket(receivePort);
            //2、创建datagramPacket对象
            byte[] buf = new Byte[1024];
            DatagramPacket dp = new DatagramPacket(buf,buf.length);
            //3、接收数据
            while(true){
                ds.receive(dp);
                //显示接受的数据
                String str = new String(dp.getData(),0,dp.getLength());
                System.out.println("收到" + dp.getAddress().getHostAddress() + "--发送的数据--" + str);
            }
        }catch(Exception e){
            e.printStackTrace();
        }
    }
}
```



### 3、TCP通信

```java
/*
一、定义：是面向连接的通信协议，在数据传输前先在发送端和接收端建立逻辑连接，然后再传输数据。在TCP连接中必须要明确客户端与服务器端， 由客户端向服务器端发出连接请求，每次连接的创建都需要经过“三次握手”。[第一次握手， 客户端向服务器端发出连接请求，等待服务器确认; 第二次握手，服务器端向客户端回送一个响应，通知客户端收到了连接请求: 第三次握手，客户端再次向服务器端发送确认信息，确认连接。
二、
  Java提供了用来实现TCP程序的两个类)
  一个是SrverSocket类，用于表示服务器端;另个是Socket用于表示客户端。
  通信时，首先要创建代表服务器端的ServerSocket对象，创建该对象相当于开启个服务，此服务会等待客户端的连接;然后创建代表客户端的Socket对象，使用该对象向服务器端发出连接请求，服务器端响应请求后，两者才建立连接，开始通信.


三、public Class ServerSocket
   1、常见的构造方法
      1. ServerSocket() 
         通过该方法创建一个ServerSocket对象不与任何端口绑定，但是不能直接使用，需要继续调用bind(SocketAddress endpoint)方法将其绑定到指定的端口号上，才能正常使用
      2. ServerSocket(int port) 
        通过该方法创建一个ServerSocket对象时，可以将其绑定到一个指定的端口号上。
      3. ServerSocket(int port, int backlog) 
        再2上增加一个backlog参数，该参数表示服务器忙的时候，可以与之保持连接请求的客户数量，没指定的话，默认为50
      4. ServerSocket(int port, int backlog, InetAddress bindAddr) 
        在3的基础上增加一个bindAddr参数，这个参数用于指定相关的Ip地址，该构造方法适用于计算机上有多块网卡和多个IP地址的情况。
        
   2、常见的方法
     1. Socket accept()  
       该方法用于等待客户端的连接，在客户端连接之前会一直处于阻塞状态， 如果有客户端连接，就会返回一个与之对应的Socket对象
     2. void bind(SocketAddress endpoint) 
       将 ServerSocket绑定到特定地址（IP地址和端口号）其中endpoint是封装好的。
     3. InetAddress getInetAddress()  
        该方法用于返回一个InetAddress对象，该对象中封装了ServerSocket绑定的IP地址
        
     4. boolean isClosed() 
       返回ServerSocket的关闭状态。 
       
    3、 注意事项：
       SeverSocket对象负责监听某台计算机的某个端口号，在创建ServerSocket对象后，需要继续调用该对象的accept( )方法，接收来自客户端的请求。当执行了accept( )方法之后，服务器端程序会发生阻塞，直到客户端发出连接请求时，accept ( )方法才会返回一个Socket对象用于与客户端实现通信，程序才能继续
       
       
四、public class Socket
   1、常见的构造方法
     1. Socket() 
       使用该构造方法时，并没有指定IP地址和端口号，也就意味着只创建了客户端对象，没法去连接任何服务器，通过该构造方法创建对象后还需调用connect(SocketAddress endpoint)方法，才能完成与指定服务器端的连接，其中参数endpoin用于封装IP地址和端口号。
     2. Socket (String host, int port)
       使用该构造方法在创建Socket对象时，会根据参数去连接在指定地址和端口上运行的服务器程序，其中参数host接收的是一个字符串类型的IP地址
     3. Socket ( InetAddress address, int port )
       该构造方法在使用上与第一二个构造方法类似，参数address用于接收一个 InetAddress类型的对象，该对象用于封装一个IP地址。

   2、常见的方法
     1. int getPort( )
       该方法返回一个int类型的对象，该对像是Socket对像与服务器连接的断后号
       
     2. InetAddress getLocalAddress ( )
       该方法用于获取Socket对象绑定的本地IP地址，井将IP地址封装成InetAddress类型的对象返回
     
     3. void close ( )
       该方法用于关闭Socket连接，结束本次通信。在关闭Socket之前，应将与Socket相关的所有的输入输出流全部关闭，这是因为一个良好的程序应该在执行完毕时释放所有的资源
       
     4. InputStream getInputStream( )
       该方法返回一个InputSream类型的输入流对象，如果该对象是由服务器端的Socket返回，就用于读取客户端发送的数据，反之，用于读取服务器端发送的数据
       
     5. OutputStream getOutputStream( )
       该方法返回一个OutputStream类型的输出流对象，如果该对象是由服务器端的Socket返回，就用于向客户端发送数据，反之，用于向服务器端发送数据
       
  3、注意事项
     getlnputstream( )和putOutputStream( )方法分别用于获取输人流和输出流。当客户端和服子容端建立连接后，数据是以IO流的形式进行交互的，从而实现通信
 */
```

![image-20210530185245388](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210530185245388.png)

```java
/*
TCP客户端
*/
public class Cilent{
    public static void main(String[] args){
        //创建一个Socket对象，并连接到指定的服务器IP地址和端口号
        Socket client = new Socket(InetAddress.getLocalHost(),7788);
        //2、发送数据该服务器，或者接收服务器发来的数据
        InputStream in = client.getInputStream();//得到接受的数据流
        byte[] buf = new byte[1024];
        int len = in.read(buf);//将数据读到缓冲数组中
        System.out.println(new String(buf,0,len));
        //3.关闭Socket对象，释放资源
        client.close();
    }
}

/*
服务器端
*/
public class Serve{
    public static void main(String[] args)throws Exception{
        //创建服务器ServerSocket,表示服务器，指定服务器的端口号
        ServerSocket serverSocket = new ServerSocket(7788);
        //2.通过accept（）接受客户端的请求
        Socket client = serverSocket.accept();
        //3获取客户端的输出流或输入流
        OutputStream out = client.getOutputStream();//获取客户端的输出流
        //4通过输出流写数据到客户端，或者通过输入流从客户端中读取发来的数据
        System.out.println("开始与客户端交互数据");
        out.write("创智欢迎你".getBystes());
        Thread.sleep(5000);//模拟执行其他功能，占用时间
        System.out.println("结束与客户短的交互数据");
        //关闭Socket对象，释放资源
        out.close();
        client.close();
        
    }
}
```

### 4、多线程版TCP

```java
/*
服务器端
*/
public class Serve{
    public static void main(String[] args)throws Exception{
        //创建服务器ServerSocket,表示服务器，指定服务器的端口号
        ServerSocket serverSocket = new ServerSocket(7788);
        while(true) {
        	//2.通过accept（）接受客户端的请求
            final Socket client = serverSocket.accept();
            new Thread(new Runnable() {
            	public void run() {
            		try {
            			 //3获取客户端的输出流或输入流
                        OutputStream out = client.getOutputStream();//获取客户端的输出流
                        //4通过输出流写数据到客户端，或者通过输入流从客户端中读取发来的数据
                        String ipAddress = client.getInetAddress().getHostAddress();
                        System.out.println("开始与客户端交互数据"+ ipAddress + "交互数据");
                        out.write("创智欢迎你".getBystes());
                        Thread.sleep(5000);//模拟执行其他功能，占用时间
                        System.out.println("结束与客户短的交互数据" + ipAddress + "交互数据");
                        //关闭Socket对象，释放资源
                        out.close();
                        client.close();
            		}catch(Exception e) {
            			e.printStackTrace();
            		}
            	}
            });
           
        }
        
        
    }
}

/*
TCP客户端
*/
public class Cilent{
    public static void main(String[] args){
        //创建一个Socket对象，并连接到指定的服务器IP地址和端口号
        Socket client = new Socket(InetAddress.getLocalHost(),7788);
        //2、发送数据该服务器，或者接收服务器发来的数据
        InputStream in = client.getInputStream();//得到接受的数据流
        byte[] buf = new byte[1024];
        int len = in.read(buf);//将数据读到缓冲数组中
        System.out.println(new String(buf,0,len));
        //3.关闭Socket对象，释放资源
        client.close();
    }
}
```



## 10、JDBC

### 1、定义

```java
/*
DDL 定义语言， 
DML 操作语言  
DQL 查询语言 
DCL 控制语言
一、定义：
   JDBC的全称是Java数据库连接（Java Database
Connectivity)，它是一套用于执行SQL语句的Java APl。应用程序可通过这套API连接到关系型数据库，并使用SQL语句来完成对数据库中数据的查询、新增、更新和删除等操作。

二、访问注意事项
    应用程序使用JDBC访问特定的数据库时，需要与不同的数据库驱动进行连接。由于不同数据库厂商提供的数据库驱动不同，因此，为了使应用程序与数据库真正建立连接，JDBC不仅需要提供访问数据库的API,还需要封装与各种数据库服务器通信的细节。

三、JDBC常用的API
   1、Driver接口
     是所有JDBC驱动程序必须实现的接口，该接口专门提供给数据库厂商使用。需要注意的是，在编写JDBC程序时，必须要把所使用的数据库驱动程序或类库加载到项目的classpath中(这里指MySQL驱动JAR包）。
     
   2、DriverManager接口
     用于加载JDBC驱动并且创建与数据库的连接。在DriverManager类中，定义了两个比较重要的静态方法
     1. static void registerDriver(Driver driver)
       该方法用于向DriverManager中注册给定的JDBC驱
       
     2. static Connection getConnection(String u1,String user,String pwd)
       该方法用于建立和数据库的连接,并返回表示连接的 Connection对象。
       
   3、 Connection接口
     代表Java程序和数据库的连接;只有获得该连接对象后，才能访问数据库，并操作数据表。在Connection接口中，定义了一系列方法，其常用方法如下所示。
     1.  Statement createStatement()
        用于创建一个Statement对象来将SQL语句发送到数据库
     
     2. PreparedStatement prepareStatement(String sql)
       用于创建一个PreparedStatement对象来将参数化的SQL语句,发送到数据库·
       
     3. CallableStaterment prepareCall(String sql)
       用于创建一个 CallableStatement对象来调用数据库存储过程
       
   4、Statement接口
     用于执行静态的SQL语句，并返回一个结果对象。Statement接口对象可以通过Connection实例的
     createStatement()方法获得，该对象会把静态的SQL语句发送到数据库中编译执行，然后返回数据库的处理结
     果。
     
     在Statement接口中，提供了3个常用的执行SQL语句的方法，具体如下所示。
     1. boolean execute(String sql)
       用于执行各种sQL语句，该方法返回一个 boolean类型的值,如果为true，表示所执行的SQL语句有查询结果,
       可通过 Statement的getResultSet()方法获得查询结果
       
     2. int executeUpdate(String sqD)
       用于执行SQL 中的 insert、update和 delete语句。该方法返回一个int类型的值，表示数据库中受该SQL
       语句影响的记录条数·
       
     3. ResultSet executeQuery(String sql)
       用于执行SQL中的 select语句，该方法返回一个表示查询结果的ResultSet对象
       
   5、PreparedStatement接口
      PreparedStatement接口是Statement的子接口，用于执行预编译的SQL语句。该接口扩展了带有参数SQL语句
      的执行操作，应用该接口中的SQL语句可以使用占位符“?”来代替其参数，然后通过setXxx()方法为SQL语句
      的参数赋值。在PreparedStatement接口中，提供了一些常用方法，具体如下所示。
      
      1. int executeUpdate()  
        在此 PreparedStatement对象中执行SQL语句，该语句必须是一个DML语句或者是无返回内容的SQL语句,如DDL语句
        
      2. ResultSet executeQuery()  
        在此PreparedStatement对象中执行SQL查询,该方法返回的是ResultSet对象
        
      3. void setInt(int parameterIndex, int x) 
        将指定参数设置为给定的 int值
      4. void setFloat(int parameterIndex, float x)  
        将指定参数设香为给定的:float 值
      5. void setString(int parameterIndex, String x)  
        将指定参数设香为给定的String值
      6. void setDate(int parameterIndex, Date x, Calendar cal)  
        将指定参数设置为给定的 Date值
        需要注意的是， setDate()方法可以设置日期内容，但参数Date 的类型是java.sql.Date，而不是java.util.Date。
        在通过setXxx()方法为SQL语句中的参数赋值时，可以通过输入参数与SQL类型相匹配的方法。例如,如果参数具有SQL类型为Integer,那么应该使用setInt()方法,也可以通过setObject()方法设置多种类型的输入参数，具体如下所示。
        String sql = "INSERT INTo users (id,name, email) VALUES (?,?,?) ";
        Preparedstatement prestmt = conn.preparestatement (sql) ;
        preStmt .setInt(1,1);//使用参数的已定义sql类型
        prestmt .setString(2, " zhangsan");//使用参数的已定义sql,类型
        prestmt.setobject(3, "zsesina. com");//使用setObject ()方法设置参数prestmt.executeUpdate();
        
   6、ResultSet接口
     用于保存JDBC执行查询时返回的结果集，该结果集封装在一个逻辑表格中。在ResultSet接口内部有一个指向表格数据行的游标（或指针广，ResultSet对象初始化时，游标在表格的第一行之前，调用next()方法可将游标移动到下一行。如果下一行没有数据，则返回false。在应用程序中经常使用next()方法作为while循环的条件来迭代ResultSet结果集。ResultSet接口中的常用方法如下所示。
     1. String getString(String columnIndex)  
       用于获取指定字段的 String 类型的值，参数 columnindex 代表字段的索引
     2. String getString(int columnName)  
       用于获取指定字段的 String类型的值,参数columnName 代表字段的名称
     3. int getInt(int columnIndex)  
       用于获取指定字段的 int类型的值,参数coiumnIndex代表字段的索引
     4. int getInt(String columnName)  
       用于获取指定字段的 int类型的值，参数columnName 代表字段的名称
     5. boolean next()  
       将游标从当前位置向下移一行
       
     6. boolean absolute(int row) 
       将游标移动到ResultSet对象指定的行
       
     7. void afterLast()
       将游标移动到ResultSet对象的末尾
       
     8、void beforeFirst()
       将游标移动到ResultSet对象的开头
       
     9、boolean previous()
       将游标移动到ResultSet对象的上一行
       
     10. boolean last()
       将游标移动到ResultSet对象的最后一行
    注意：
      ResultSet接口中定义了大量的getXxx()方法,而采用哪种getXxx()方法取决于字段的数据类型。程序既可以通过字段的名称来获取指定数据，也可以通过字段的索引来获取指定的数据，字段的索引是从1开始编号的。例如，数据表的第一列字段名为id，字段类型为int，那么即可以使用getInt(1)获取该列的值，也可以使用getInt(*id")获取该列的值。
     
*/
```

![image-20210530204440581](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210530204440581.png)



![image-20210530204534247](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210530204534247.png)



==JDBC驱动器的API是接口、JDBC驱动器是实现类。==

### 2、实现一个JDBC程序

```java
/*
( 1 ）加载并注册数据库驱动注册数据库驱动的具体方式如下。
    DriverManager.registerDriver (Driver driver) ;或
    Class.forName("DriverName");
 
 (2）通过DriverManager 获取数据库连接获取数据库连接的具体方式如下。
    Connection conn = DriverManager.getConnection (String ur1,String user,Stringpwd);
    
    从上述代码可以看出，getConnection()方法中有3个参数，它们分别表示连接数据库的地址、登录数据库的用户名和密码。以 MySQL 数据库为例，其地址的书写格式如下。
    jdbc:mysql://nostname :port/databasename
    上面代码中，jdbc:mysql:是固定的写法，mysql指的是MySQL 数据库。
    hostname 指的是主机的名称（如果数据库在本机中，hostname 可以为 localhost或127.0.0.1;如果要连接的数据库在其他计算机上，hostname 为所要连接计算机的IP ),
    port 指的是连接数据库的端口号( MySQL端口号默认为3306 ),
    databasename指的是MySQL中相应数据库的名称。

(3 ）通过Connection对象获取Statement对象
   Connection创建Statement的方式有如下3种。.      
   
   createStatement():创建基本的Statement象。
   
   prepareStatement():创建 PreparedStatement对象。
   
   prepareCall():创建CallableStatement 对象。

   以创建基本的Statement对象为例，创建方式如下。
   Statement stmt = conn.createStatement();
   
(4）使用Statement 执行sQL语句
   所有的Statement都有如下.3种执柠SQL语句的方法
   
   execute():可以执行任何sQL语句。
   executeQuery():通常执行查询语句，执行后返回代表结果集的ResultSet对象。
   executeUpdate():主要用于执行DML和DDL语句。执行DML语句,如 INSERT.UPDATE或DELETE时，返回受SQL语句影响的行数，执行 DDL语句返回0。
   以executeQuery()方法为例，其使用方式如下。
   //执行sOL语句,获取结果集 ResultSet
   ResultSet rs = stmt .executeouery (sql):

(5）操作ResultSet结果集
   如果执行的SQL语句是查询语句，执行结果将返回一个ResultSet对象，该对象里保存了SQL语句查询的结果。程序可以通过操作该ResultSet对象来取出查询结果。
   
( 6）关闭连接，释放资源
   每次操作数据库结束后都要关闭数据库连接，释放资源，包括关闭 ResultSet、Statement和Connection等资源。
*/
import java.sql.*;

public class JdbcTest01 {
    public static void main(String[] args) throws SQLException {

        Statement stmt = null;
        ResultSet rs = null;
        Connection conn = null;
        try {
            //1.注册数据库的驱动
            Class.forName("com.mysql.cj.jdbc.Driver");
            //2..通过DirverManager获取数据库连接
            String url =
                    "jdbc:mysql://localhost:3306/jdbc"
                            + "?serverTimezone=GMT%2B8&useSSL=false";
            String username = "root";
            String password = "kdh77585219513";
            conn = DriverManager.getConnection(url,username,password);
            // 3.通过connectiond对象获取statement对象
            stmt = conn.createStatement();
            String sql = "select * from users";
            //4. 使用stmt语句执行sql语句
            rs = stmt.executeQuery(sql);
            System.out.println("id|		name|	passoward"
                    +"|	email		|	birthday");
            while(rs.next()) {
                //5. 通过列名获取指定字段的值
                int id = rs.getInt("id");
                String name = rs.getString("name");
                String psw = rs.getString("passward");
                String email = rs.getString("email");
                Date birthday = rs.getDate("birthday");
                System.out.println(id + " |      " + name + "       |" + psw + "        |" + email
                        +"       |" + birthday + "      |");
            }
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } finally {
            //6. 释放资源
            if(rs != null) {
                try {
                    rs.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
                rs = null;
            }
            if(stmt != null) {
                try {
                    stmt.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
                stmt = null;
            }
            if(conn != null) {
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
                conn = null;
            }
        }

    }
}
/*
以上注意啦：
1、注册驱动：
  方法一：Class.forName("com.mysql.cj.jdbc.Driver");这种方法有两个地方需要解释
  com.mysql.cj.jdbc.Driver这是现代版本特定的写法com.mysql.cj.数据库名称.Driver
  
2、获取数据库连接
   String url ="jdbc:mysql://localhost:3306/jdbc？serverTimezone=GMT%2B8&useSSL=false";//true或者false都可以
   不光写jdbc:mysql://localhost:3306/jdbc原因是因为数据安装的是美国时间，不写serverTimezone=GMT%2B把其设置成背景时间，会报错误。高版本的MySQL需要指名是否进行SSL相连，否则会出现报警信息。只需要在后面加入&useSSL=false/true即可。
   
3、释放资源
  由于数据库资源非常宝贵,数据库允许的并发访问连接数量有限,因此,当数据库资源使用完毕后,一定要记得释放资源。为了保证资源的释放,在Jva程序中,应该将释放资源的操作放在finally代码块中。

*/
```



### 3、PreparedStatement对象

```java
/*
一、
   Statement 提供了一个子类 PreparedStatement。PreparedStatement对象可以对 SQL语句进行预编译，预编译的信息会存储在 PreparedStatement对象中。当相同的SQL语句再次执行时，程序会使用PreparedStatement对象中的数据，而不需要对SQL 语句再次编译去查询数据库，这样就大大提高了数据的访问效率。
*/
import java.sql.*;

public class JdbcTest02 {
    public static void main(String[] args) throws SQLException {

            Connection conn = null;
            //1.注册数据库的驱动
            Class.forName("com.mysql.cj.jdbc.Driver");
            //2..通过DirverManager获取数据库连接
            String url =
                    "jdbc:mysql://localhost:3306/jdbc"
                            + "?serverTimezone=GMT%2B8&useSSL=false";
            String username = "root";
            String password = "kdh77585219513";
            conn = DriverManager.getConnection(url,username,password);
            // 3.通过connectiond对象获取PreparedStatement对象,需要指定sql语句
            String sql = "insert into users(name,password,email,birthday) values(?,?,?,?)";
            PreparedStatement preStmt = conn.prepareStatement(sql);
            
            //为sql语句的参数赋值
            preStmt.setString(1,"za");
            preStmt.setString(2,"123456");
            preStmt.setString(3,"za@qq.com");
            preStmt.setString(4,"1999-04-22");
            //4. 使用PreparedStament语句执行sql语句
            int count= preStmt.executeUpdate();
            System.out.println("影响数据库表中数据条数为"+count);
            //5、操作ResultSet结果集
            //6、关闭连接，释放资源
            preStmt.close();
            con.close();    
            
        

    }
}
```

### 4、ResultSet对象

```java
import java.sql.*;

public class JdbcTest02 {
    public static void main(String[] args) throws SQLException {
        Class.forName("com.mysql.cj.jdbc.Driver");
        String url =
                    "jdbc:mysql://localhost:3306/jdbc"
                            + "?serverTimezone=GMT%2B8&useSSL=false";
        String username = "root";
        String password = "kdh77585219513";
        Connection conn = DriverManager.getConnection(url,username,password);
        
        String sql = "select * from users";
        PreparedStatement preStmt = conn.prepareStatement(sql);
        
        //执行SQL语句
        ResultSet rs = ppstmt.executeQuery();
        //操作查询结果集ResultSet
        rs.absolute(2);//将指针定位到结果集中的第3二行数据
        System.out.println("第2条数据的name值为"+rs.getString("name"));
        
        rs.beforeFirst();//将指针定位到结果集中的第1行数据之前
        System.out.println("第1条数据的name值为"+rs.getString("name"));
        
        re.afterLast();//将指针定位到结果集中的最后一条数据之后
        re.previous();//指针向前一定
        System.out.println("第4条数据的name值为："+rs.getString("name"));
        
    }
}
```





###  5、JDBC一个学生管理系统

```java
/*
一、搭建数据库环境
在mysql中创建一个名为jdbcde1数据库，在jdbc中新建一个users表，创建数据库和表的sql语句
create database jdbc;
use jdbc
create table Student
(
    id int,
    name char(20),
    c_no char(20),
    ranking char(20),
    primary key(id)
);
insert into Student values (123,'小白','1902','2');
insert into Student values (124,'李菁','1902','1');
insert into Student values (125,'小李','1901','3');

输入：select * from users; 查询表结构

二、Mysql连接IDEA方法
   选则想用的modules模块 -> new -> directory -> 把数据库驱动程序.jar复制到这里面
   file -> projecct stucture -> modules -> dependencies -> JARs or directories -> 选则好下载好的Jar包确认，从而完成包添加到依赖项。
   
三、Eclipse如何连接数据库驱动方法
   在Eclipse中新建一个名称为chapter09的Java项目，使用鼠标右键单击项目名称，然后选择【New】→【Folder 文件夹】，在弹出窗口中将该文件夹命名为lib并单击【Finish】按钮，此时项目根目录中就会出现一个名称为lib 的文件夹。将下载好的 MySQL 数据库驱动文件mysql-connector-java-5.0.8-bin.jar复制到项目的lib目录中,并使用鼠标右键单击该JAR包,在弹出框中选择【Build Path 】→【Add to Build Path ]，此时Eclipse 会将该JAR包发布到类路径下( MySQL 驱动文件可以在其官网地址http:/ldev.mysql.com/downloads/ connectorl/页面中下载,在浏览器中输入该地址后即可进入下载页面,点击页面Generally Available (GA)Releases窗口中的Looking for previous GA versions 超链接后，在显示出的下拉框中下载所需的驱动版本即可)。
   
三、在刚才建立的mouules下建立对象的类和包即可
*/

package cn.kong.jdbc;
import java.sql.*;
import java.util.Scanner;
public class Main<ex> {
    public static void main(String[] args)throws ClassNotFoundException, SQLException {
        Connection conn=null;
        Statement stat=null;
        String url =
                "jdbc:mysql://localhost:3306/jdbc"
                        + "?serverTimezone=GMT%2B8&useSSL=false";
        String username="root";
        String password="kdh77585219513";
        Class.forName("com.mysql.cj.jdbc.Driver");
        conn=DriverManager.getConnection(url,username,password);
        stat=conn.createStatement();
        try{
            System.out.println("欢迎进入学生管理系统！");
            System.out.println("如果想要查看全部学生信息，请按1");
            System.out.println("如果想要添加新学生信息，请按2");
            System.out.println("如果想要修改学生信息，请按3");
            System.out.println("如果想要删除学生信息，请按4");
            Scanner sc=new Scanner(System.in);
            int x=sc.nextInt();
            switch (x){
                case 1:Select(stat);break;
                case 2:Add(stat);break;
                case 3:Alter(stat,sc);break;
                case 4:Delete(stat,sc);break;
                default:
                    System.out.println("抱歉，您输入的信息不符合要求！");
                    break;
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    public static void Select(Statement stat)throws SQLException{
        String sql="select * from Student";
        ResultSet re=stat.executeQuery(sql);
        System.out.println("|  学号  |  姓名  |  班级  |  排名  |");
        while(re.next()){
            int id=re.getInt("id");
            String name=re.getString("name");
            String c_no=re.getString("c_no");
            int rank=re.getInt("ranking");
            System.out.println("|  "+id+"  |  "+name+"  |  "+c_no+"  |  "+rank+"  |");
        }
    }
    public static void Add(Statement stat)throws SQLException{
        System.out.println("请输入需要添加的学生信息（学号，姓名，班级，总成绩排名）：");
        Scanner input =new Scanner(System.in);
        String str=input.nextLine();
        String[] arrs=str.split(" ");
        int id=Integer.parseInt(arrs[0]);
        String name=arrs[1];
        String c_no=arrs[2];
        int rank=Integer.parseInt(arrs[3]);
        boolean ex=Exist(stat,id);
        if(!ex){
            String sql="insert into Student values( "+id+",'"+name+"','"+c_no+"',"+rank+");";
            stat.execute(sql);
            System.out.println("添加成功！");
        }


    }
    public static void Alter(Statement stat,Scanner sc)throws SQLException{
        System.out.println("请输入需要修改信息的学生学号：");
        int target=sc.nextInt();
        System.out.println("请输入需要新的信息（班级和排名）");
        Scanner in=new Scanner(System.in);
        String[] new_info=in.nextLine().split(" ");
        if(Exist(stat,target)){
            String sql="update Student set c_no='"+new_info[0]+"' where Student.id="+target;
            String sql2="update Student set ranking="+Integer.parseInt(new_info[1])+" where Student.id="+target;
            stat.execute(sql);
            stat.execute(sql2);
        }
    }
    public static void Delete(Statement stat,Scanner sc)throws SQLException{
        System.out.println("请输入要删除的学生学号：");
        int target=sc.nextInt();
        if(Exist(stat,target)){
            String sql="delete from Student where id="+target;
            stat.execute(sql);
            System.out.println("删除成功！");
        }
    }
    public static boolean Exist(Statement stat,int id) throws SQLException{
        ResultSet re =stat.executeQuery("select id from Student");
        while(re.next()) {
            if (id == re.getInt("id")) {
                return true;
            }
        } return false;
    }

}

```



## 11、GUI

```java
/*
一、Swing顶级容器：
   学习Swing 组件的过程和学习AWT差不多，大部分的Swing组件都是JComponent类的直接或者间接子类，而JComponent类是AWT中 java.awt.Container的子类，说明Swing组件和AWT组件在继承树上形成了一定的关系。接下来通过一张继承关系图来描述一下 AWT和Swing大部分组件的关联关系，
  下图展示了一些常用的Swing组件，不难发现，这些组件的类名和对应的AWT组件类名基本一致，大部分都是在AWT组件类名的前面添加了“J”。但也有一些例外，例如Swing的JComboBox组件对应的是AWT中的 Choice 组件(下拉框)。
  图还可以看出，Swing 中有3个组件继承了AWT的 Window类，而不是继承自JComponent类，它们分别是JWindow、JFrame、和Jdialog。这3个组件是Swing 中的顶级容器，它们都需要依赖本地平台,因此被称为重量级组件。其中，JWindow和AWT中的 Window-样很少被使用，一般都是用JFrame和JDialog。
  
二、JFrame类（窗口）
   在Swing 组件中,最常见的一个就是JFrame,它和Frame 一样是一个独立存在的顶级窗口,不能放置在其他容器之中，JFrame支持通用窗口所有的基本功能，例如窗口最小化、设定窗口大小等。
   1、静态摘要
     static int EXIT_ON_CLOSE 
      退出应用程序默认窗口关闭操作。 
   
   1. 常用的构造方法：
     1、 JFrame() 创建一个普通窗体对象
     2、 JFrame(String title) 
        创建一个窗体对象，并指定标题
   2. 常用的方法
     1、void setDefaultCloseOperation(int operation) 
       设置用户在此框架上启动“关闭”时默认执行的操作。 
     
     2、public void setSize(int width,int height)
       设置窗体大小
       
     3、public void setSize(Dimention d)
       通过Dimention设置窗体大小
   
     4、public void Backgroud(Color c)
       设置窗体的背景颜色
       
     5、public void setLocation(int x, int y)
       设置组件的显示位置
       
     6、public void setLocation(Point p)
       通过Point来设置组件的位置
       
     7、public void setVisible(boolean b)
       显示或隐藏组件
       
     8、public Component add(Component comp)
       向容器中增加组件
       
     9、public setLayout(Component comp)
       设置布局管理器，如果设置为null,表示不使用
       
     10、public void pack()
       调整窗口大小，以适应子组件的首选大小和布局
       
     11、public void Comntainer getContentPane()
       返回此窗体的容器对象
       
     12.setLocationRelativeTo(null);
       让窗体居中显示
       
     13、public void validate()
       验证此容器及其所有子组件。使用 validate 方法会使容器再次布置其子组件。已经布置容器后，
       在修改此容器的子组件的时候（在容器中添加或移除组件，或者更改与布局相关的信息），应该调
       用上述方法。覆盖：类 Component 中的 validate
*/
```

![image-20210531100628248](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210531100628248.png)

### 1、JFrame

```java
package cn.kong.GUL;

import javax.swing.*;

public class Example01 extends JFrame {
    public static void main(String[] args) {
        //使用SwingUtilities工具调用createAndshowGUI()方法显示GUI程序
        SwingUtilities.invokeLater(Example01::createAndShowGUI);

    }
    private static void createAndShowGUI(){
        //创建并设置Jframe窗口
        JFrame frame = new JFrame("JFrameTest");
        //设置关闭窗口的默认操作
        frame.getDefaultCloseOperation(); //默认这里面不跟参数
        //设置窗口标题
        frame.setTitle("JFrameTest");
        //设置窗口的尺寸
        frame.setSize(350,300);
        //设置窗口的显示位置
        frame.setLocation(300,300);
        //让组件显示
        frame.setVisible(true);

    }
}
```

### 2、JDialog

```java
/*
    JDialog 是Swing 的另外一个顶级窗口，它和Dialog 一样都表示对话框。
    对话框是模态或者非模态，可以在创建JDialog对象时为构造方法传入参数来设置，也可以在创建JDialog对象后调用它的setModal()方法来进行设置。
    
1、概念：对话窗口
   分类；
    1. 模态对话框
      用户需要等到处理完对话框后才能继续与其他窗口交互的对话框,
    2. 非模态对话框
       允许用户在处理对话框的同时与其他窗口交互的对话框。
       
 2、常见构造方法
    1、JDialog(Frame owner)
      构造方法，用来创建一个非模态的对话框,owner为对话框所有者(顶级窗口JFrame )
      
    2、JDialog(Frame owner，String title)
       构造方法,创建一个具有指定标题的非模态对话框
       
    3、JDialog(Frame owner,boolean modal)
      创建一个有指定模式的无标题对话框(模态)->不允许点击其它位置，只能再次对话框中进行点击操作
      FRame owner 的方式是:类名.this(如果该类继承了JFrame或者Frame的话)，modal直接true就好。
*/
```

```java
package cn.kong.GUL;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class Example02 {
    public static void main(String[] args) {
        //建立两个按钮
        JButton btn1 = new JButton("模态对话框");
        JButton btn2 = new JButton("非模态对话框");
        JFrame f = new JFrame("DialogDeme");
        f.setSize(300,250);
        f.setLocation(300,300) ;
        f.setLayout(new FlowLayout());//为内容面板增加布局管理器
        //在container对象上增加按钮
        f.add(btn1);
        f.add(btn2);
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);//设置关闭按钮为默认关闭窗口按钮
        f.setVisible(true);
        final JLabel label = new JLabel();
        //定义一个JDialog对话框
        final JDialog dialog = new JDialog(f, "Di alog");
        dialog.setSize(220,150);
        dialog.setLocation(400,500);
        dialog.setLayout(new FlowLayout()); //设置布局管理器
        final JButton btn3 = new JButton("确定");//创建按钮对象
        dialog.add(btn3);
        //为模态按钮添加单机事件
        btn1.addActionListener(new AbstractAction() {
            @Override
            public void actionPerformed(ActionEvent e) {
                //设置对话框模态
                dialog.setModal(true);
                //如果JDialog窗口没添加JLabel标签，就把JLabel标签加上
                if(dialog.getComponents().length == 1){
                    dialog.add(label);
                }
                //否则修改标签内容
                label.setText("模态对话框，单词确定按钮关闭");
                //显示对话框
                dialog.setVisible(true);
            }
        });
        ////为非模态按钮添加单机事件
        btn2.addActionListener(new AbstractAction() {
            @Override
            public void actionPerformed(ActionEvent e) {
                //设置对话框非模态
                dialog.setModal(false);
                //如果JDialog窗口没添加JLabel标签，就把JLabel标签加上
                if(dialog.getComponents().length == 1){
                    dialog.add(label);
                }
                //否则修改标签内容
                label.setText("非模态对话框，单词确定按钮关闭");
                //显示对话框
                dialog.setVisible(true);
            }
        });
        //为对话框中的按钮添加单机事件
        btn3.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                dialog.dispose();
            }
        });
    }
}

```

### 3、布局管理器

```java
/*
一、作用：
    组件不能单独存在，必须放置于容器当中，而组件在容器中的位置和尺寸是由布局管理器来决定的。在 java.awt包中提供了5种布局管理器，但是在Swing中最常用是4个，分别是 FlowLayout（流式布局管理器)、Border Layout(边界布局管理器).GridLayout(网格布局管理器).GridBagLayout（网格包布局管理器）。
    每个容器在创建时都会使用一种默认的布局管理器，在程序中可以通过调用容器对象的setLayout()方法设置布局管理器，通过布局管理器来自动进行组件的布局管理。例如把一个JFrame 窗体的布局管理器设置为FlowLayout,代码如下所示。
    JFrame frame= new JFrame();
    frame.setlayout (new FlowLayout ());
*/
```

#### 1、FlowLayout

```java
/*
一、概念：
    流式布局管理器(FlowLayout)是最简单的布局管理器，在这种布局下，容器会将组件按照添加顺序从左向右放置。当到达容器的边界时，会自动将组件放到下一行的开始位置。这些组件可以左对齐、居中对齐（默认方式）或右对齐的方式排列。
 
二、常用构造方法
   1. FlowLayout() 
     构造一个新的 FlowLayout中心对齐和默认的5单位水平和垂直间隙。 
   2. FlowLayout(int align) 
     构造一个新的 FlowLayout具有指定的对齐和默认的5单位水平和垂直间隙。 
     
   3. FlowLayout(int align, int hgap, int vgap) 
     创建一个新的流程布局管理器，具有指示的对齐方式和指示的水平和垂直间距。
     
三、常用常量
    1. public static final int LEFT
      该值表示每一行的组件应为左对齐。 
    2. public static final int RIGHT
      该值表示组件的每一行都应该是右对齐的。 
      
    3.public static final int CENTER
      该值表示每行的组件应该居中。 
      
    4. public static final int LEADING
      该值表示组件的每一行应该对齐到容器方向的前端，例如从左到右的方向向左。 
      
四、注意事项
    FlowLayout的3个构造方法。参数align 决定组件在每行中相对于容器边界的对齐方式，可以使用该类中提供的常量作为参数传递给构造方法。其中，FlowLayout.LEFT用于表示左对齐,FlowLayout.RIGHT用于表示右对齐, FlowLayout.CENTER 用于表示居中对齐。参数 hgap和参数vgap分别设定组件之间的水平和垂直间隙，可以填入一个任意数值。接下来通过一个添加按钮的案例来学习一下 FlowLayout 布局管理器的用法，
    
 五、特点：
    FlowLayout布局管理器的特点就是可以将所有组件像流水一样依次进行排列，不需要用户明确地设定，但是在灵活性上相对差了点。例如将图8-5中的窗体拉伸变宽，按钮的大小和按钮之间的间距将保持不变，但按钮相对于容器边界的距离会发生变化，
    
*/
package cn.kong.GUL;

import javax.swing.*;
import java.awt.*;

public class Example03 {
    public static void main(String[] args) {
        JFrame frame = new JFrame("hello World");
        //设置窗体的布局管理器为FlowLayout,所有的组件居中对齐，水平和垂直及间距为3
        frame.setLayout(new FlowLayout(FlowLayout.CENTER,3,3));
        JButton button = null;
        for(int i = 0; i < 9; i++){
            button = new JButton("按钮"+i);
            frame.add(button);
        }
        frame.setSize(280,250);
        frame.setVisible(true);
    }
}

```



#### 2、BorderLayout

```java
/*
一、边界布局管理器
   BorderLayout(边界布局管理器）是一种较为复杂的布局方式，它将容器划分为5个区域，分别是东(EAST )、南( SOUTH )、西（WEST)、北（NORTH)、中（CENTER )。组件可以被放置在这5个区域中的任意一个。
    BorderLayout边界布局管理器，将容器划分为5个区域，其中，箭头是指改变容器大小时各个区域需要改变的方向。也就是说，在改变容器时，NORTH和SOUTH 区域高度不变，长度调整，WEST和EAST区域宽度不变，高度调整，CENTER 会相应进行调整。
    当向 BorderLayout布局管理器的容器中添加组件时，需要使用add ( Componentcomp,Object constraints )方法。其中，参数comp表示要添加的组件，constraints 指定将组件添加到布局中的方式和位置的对象，它是一个 Object 类型，在传参时可以使用 BorderLayout类提供的5个常量，它们分别是 EAST、 SOUTH、WEST. NORTH 和 CENTER。
    
二、常用的构造方法：
   1、public BorderLayout()
    构造没有间距得布局器
   2、public BordeerLayout(int align,ing hgap, int vgap)
    构造有水平和垂直间距的布局器
    
三、常用常量
   1、EAST  将组建设置在东区域
   2、WEST  将组建设置在西区域
   3、SOUTH 将组建设置在南区域
   4、NORTH 将组建设置在北区域
   5、CENTER 将组建设置在中间区域
   
四、特点
   BorderLayout的好处就是可以限定各区域的边界，当用户改变容器窗口大小时，各个组件的相对位置不变。但需要注意的是，向BorderLayout 的布局管理器添加组件时，如果不指定添加到哪个区域，则默认添加到 CENTER 区域，并且每个区域只能放置一个组件，如果向一个区域中添加多个组件时,后放入的组件会覆盖先放入的组件。
*/
package cn.kong.GUL;

import javax.swing.*;
import javax.swing.border.Border;
import java.awt.*;

public class BorderLayoutDemo extends JFrame {
    public static void main(String[] args) {
        BorderLayoutDemo f = new BorderLayoutDemo();
        f.setTitle("边界布局");
        f.pack();
        f.setVisible(true);
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        f.setLocationRelativeTo(null);//让窗体居中显示
    }
    //构造函数，初始化对象值
    public BorderLayoutDemo(){
        //设置边界布局，组件件横向、纵向间距均为5个像素
        setLayout(new BorderLayout(5,5));
        setFont(new Font("Helvetica",Font.PLAIN,14));
        //将按钮添加到窗口中
        getContentPane().add("North",new JButton(BorderLayout.NORTH));
        getContentPane().add("South",new JButton(BorderLayout.SOUTH));
        getContentPane().add("East",new JButton(BorderLayout.EAST));
        getContentPane().add("West",new JButton(BorderLayout.WEST));
        getContentPane().add("Center",new JButton(BorderLayout.CENTER));
    }
}
//例二
package cn.kong.GUL;

import javax.swing.*;
import java.awt.*;

public class Example04 {
    public static void main(String[] args) {
        final JFrame f = new JFrame("BorderLayout");
        f.setLayout(new BorderLayout());
        f.setSize(300,300);//设置窗体大小
        f.setLocation(300,300);//窗体显示的位置
        f.setVisible(true);//设置窗体可见
        //5个按钮分别填充到BorderLayout5个区域中
        Button but1 = new Button("East");
        Button but2 = new Button("West");
        Button but3 = new Button("South");
        Button but4 = new Button("North");
        Button but5 = new Button("Center");
        //将创建好的按钮添加到窗体中，并设置位置
        f.add(but1,BorderLayout.EAST);
        f.add(but2,BorderLayout.WEST);
        f.add(but3,BorderLayout.SOUTH);
        f.add(but4,BorderLayout.NORTH);
        f.add(but5,BorderLayout.CENTER);
    }
}

```

#### 3、GridLayout

```java
/*
一、定义；
   GridLayout(网格布局管理器）使用纵横线将容器分成n行m列大小相等的网格，每个网格中放置一个组件。添加到容器中的组件首先放置在第1行第1列(左上角)的网格中,然后在第1行的网格中从左向右依次放置其他组件。行满后，继续在下一行中从左到右放置组件。与FlowLayout 不同的是，放置在GridLayout布局管理器中的组件将自动占据网格的整个区域。
   
二、构造方法：
   1. GridLayout() 
     弄人只有一行，每个组件占一列
   2. GridLayout(int rows, int cols) 
     指定容器的行数和列数
     
   3. GridLayout(int rows, int clos, int hgap, int vgap)
     指定容器的行数和列数以及组件之间的水平，垂直间距
     
三、提示：
  GridLayout的3个构造方法。其中，参数rows代表行数，cols 代表列数,hgap和 vgap 规定水平和垂直方向的间隙。水平间隙指的是网格之间的水平距离，垂直间隙指的是网格之间的垂直距离。
*/
package cn.kong.GUL;

import javax.swing.*;
import java.awt.*;

public class Example05 {
    public static void main(String[] args) {
        JFrame f = new JFrame("GridLayout");
        f.setLayout((new GridLayout(3,3,2,3)));//3*3网格
        f.setSize(300,300);//窗体大小
        f.setLocation(400,300);//位置
        //将9个按钮添加到GridLayout中
        for(int i = 1; i <= 9; i++){
            Button btn = new Button("btn" + i);
            f.add(btn);//像窗体中添加按钮
        }
        f.setVisible(true);
    }
}

```

#### 4、GridBagLayout

```java
/*
一、概念：
   GridBagLayout(网格包布局管理器）是最灵活、最复杂的布局管理器。与GridLayout布局管理器类似，不同的是，它允许网格中的组件大小各不相同，而且允许一个组件跨越一个或者多个网格。
   
二、使用步骤
   1、创建GridBagLayout布局管理器，并使用容器采用该布局管理器
     GridBagLayout layout = new GridBagLayout();
     container.setLayout(layout);
     
   2、创建GridBagContraints对象（布局约束条件)，并设置该对象的相关属性。
     GridBagContraints constraints = new GridBagContraints();
     constraints.gridx = 1; //设置网格的左上角横向索引
     constraints.gridy = 1;//设置网格的左上角纵向索引
     constraints.gridwidth = 1;//设置组件横向跨越网格
     constraints.gridheight = 1;//设置组件纵向跨越网格
     
   3、调用GridBagLayout对象的setConstraints()方法建立GridBagConstraints对象和受控组件之间的关联。
   
     layout.setconstraints (component, constraints);
     
   4、向容器中添加组件
     container.add(conponent);
     
   5、GridBagConstraints对象可以重复使用，只需要改变它的属性即可。如果要向容器中添加多个组件，则重复步骤（2）、步骤（3）、步骤(4）。
     从上面的步骤可以看出，使用GridBagLayout布局管理器的关键在于GridBagConstraints对象，它才是控制容器中每个组件布局的核心类，在GridBagConstraints类中有很多表示约束的属性，
     
     GridBagConstraints常用到的属性
     1. gridx和gridy
       设置组件的左上角所在网格的横向和纵向索引(即所在的行和列）。如果将 gridx和gridy的值设gridBagConstraints.RELATIVE(默认值)，表示当前组件紧跟在上一个组件后面
       
     2. gridwidth和gridheight
       设置组件横向、纵向跨越几个网格,两个属性的默认值都是1。如果把这两个属性的值设为 GridBagConstraints.REMAINER(remainer)，表示当前组件在其行或其列上为最后一个组件。如果把这两个属性的值设为GridBagConstraints.RELATIVE(relative),表示当前组件在其行或列上为倒数第2个组件
       
    3. fill
       如果当组件的显示区域大于组件需要的大小，设置是否以及如何改变组件大小，该属性接收以下几个属性值。
       NONE:默认，不改变组件大小(note)
       HORIZONTAL:使组件水平方向足够长以填充显示区域，但是高度不变(horizontal)
       VERTICAL:使组件垂直方向足够高以填充显示区域,但长度不变(vertical)
       BOTH:使组件足够大，以填充整个显示区域(组件横向纵向可拉伸)
       
    4. weightx和weigthy
       设置组件占领容器中多余的水平方向和垂直方向空白的比例（也称为权重)。假设容器的水平方向放置3个组件，其weightx分别为1、2、3，当容器宽度增加60个像素时,这3个容器分别增加10、20、和30的像素。这两个属性的默认值是0,即不占领多余的空间
       
       列出了GridBagConstraints 的常用属性。其中，gridx和gridy用于设置组件左上角所在网格的横向和纵向索引，gridwidth和 gridheight 用于设置组件横向、纵向跨越几个网格，fill用于设置是否及如何改变组件大小，weightx和 weighty用于设置组件在容器中的水平方向和垂直方向的权重。
       需要注意的是，如果希望组件的大小随着容器的增大而增大，必须同时设置 GridBagConstraints对象的fil属性和weightx、weighty属性。
*/
package cn.kong.GUL;

import javax.swing.*;
import java.awt.*;

public class Example06 {
    public static void main(String[] args) {
        new Layout("GirdBagLayout");
    }
}
class Layout extends JFrame{
    public Layout(String title){
        GridBagLayout layout = new GridBagLayout();
        GridBagConstraints c = new GridBagConstraints();
        this.setLayout(layout); //等价于JFrame.setLayout(new GridBagLayout());因为继承的是JFrame
        c.fill = GridBagConstraints.BOTH;//设置组件横向，纵向可拉伸
        c.weightx = 1;//横向权重为1
        c.weightx = 1; //纵向权重为1
        this.addComponent("btn1",layout,c);
        this.addComponent("btn2",layout,c);
        this.addComponent("btn3",layout,c);
        //添加的组件是本行最后一个组件
        c.gridwidth = GridBagConstraints.REMAINDER; //行上的
        this.addComponent("btn4",layout,c);
        c.weightx = 0;//横向权重为0
        c.weighty = 0;//纵向权重为0
        this.addComponent("btn5",layout,c);
        //添加的组件是本行的最后一个组件
        c.gridwidth = GridBagConstraints.REMAINDER;
        this.addComponent("btn6",layout,c);
        c.gridwidth = 1; //组件横跨1个网格
        c.gridheight = 2;//组件纵跨2个网格
        c.weightx = 2; //横向权重股为2
        c.weighty = 2; //纵向权重为2
        this.addComponent("btn8",layout,c);
        c.gridwidth = GridBagConstraints.REMAINDER;//改行最后一个
        c.gridheight = 1; //纵跨1
        this.addComponent("btn9",layout,c);
        this.addComponent("btn10",layout,c);
        this.setTitle(title);
        this.pack();
        this.setVisible(true);
        this.setLocation(400,500);

    }



    //增加组件的方法
    private void addComponent(String name,GridBagLayout layout, GridBagConstraints c) {
        Button bt = new Button(name);//创建一个名为name的按钮
        layout.setConstraints(bt,c);//设置GridBagConstraint和bt的关联
        this.add(bt);//给JFrame增加组件

    }
}

```



#### 5、不常用的布局管理器

CardLayout卡片布局管理器

- 一个`CardLayout`对象是`CardLayout`的布局管理器。  它将容器中的每个组件视为一张卡。 一次只能看到一张卡片，容器就是一堆卡片。  添加到`CardLayout`对象的第一个组件是首次显示容器时的可见组件。

任何时候只有一张卡片可见。





### 4、事件处理机制

#### 1、事件处理机制

```java
/*
一、概念：
   事件处理机制专门用于响应用户的操作，例如，想要响应用户的单击鼠标、按下键盘等操作,就需要使用Swing 的事件处理机制。在学习如何使用Swing事件处理机制之前，首先向读者介绍几个比较重要的概念，具体如下所示。
   ·事件源（组件Event Source):事件发生的场所，通常就是产生事件的组件,如窗口，按钮，菜单
   ·事件对象(Event ):封装了GUI组件上发生的特定事件（通常就是用户的一次操作)。
   ·监听器( Listener ):负责监听事件源上发生的事件,并对各种事件做出相应处理的对象(对象中包含事件处理器）。
二、
   事件源是一个组件，当用户进行一些操作时，如按下鼠标或者释放键盘等，这些动作会触发相应的事件。如果事件源注册了事件监听器，则触发的相应事件将会被处理。
   在程序中，如果想实现事件的监听机制，首先需要定义一个实现了事件监听器接口的类，例如Window类型的窗口需要实现WindowListener 。接着通过 addWindowListener()方法为事件源注册事件监听器对象，当事件源上发生事件时，便会触发事件监听器对象，由事件监听器调用相应的方法来处理相应的事件。

三、一般步骤：
   1. 编写事件处理类（事件监听者）
   2. 需要给事件处理类实现监听器接口
   3. 在事件处理类重写事件处理方法
   4. 在事件源中指定该事件的监听器（响应者）是谁，即注册监听器
四、以下是案列，实现窗口关闭功能
  
*/
package cn.kong.GUL;

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Example07 {
    public static void main(String[] args) {
        //建立新窗体
        JFrame f = new JFrame("我的窗体");
        //设置窗体的宽和高
        f.setSize(400,300);
        f.setLocation(400,500);
        f.setVisible(true);
        //为窗口组件注册监听器
        MyWindowsListener mw = new MyWindowsListener();
        f.addWindowListener(mw);
    }
}
//1、编写事件处理类
class MyWindowsListener implements WindowListener{ //2.实现监听器接口
    @Override
    public void windowOpened(WindowEvent e) {

    }

    //重写处理方法（监听器监听事件对象做出处理）
    public void windowClosing(WindowEvent e){
        Window window = e.getWindow();
        window.setVisible(false);
        //释放窗口
        window.dispose();
    }
    public void windowActivated(WindowEvent e){

    }
    public void windowClosed(WindowEvent e){

    }
    public void windowDeactivated(WindowEvent e){

    }
    public void windowDeiconified(WindowEvent e){

    }
    public void windowIconified(WindowEvent e){

    }

}

```

![image-20210601092431282](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210601092431282.png)

#### 2、Swing常用事件处理

##### 1、窗体事件

```java
/*
一、定义：
   大部分GUI应用程序都需要使用 Window窗体对象作为最外层的容器，可以说窗体对象是所有GUI应用程序的基础，应用程序中通常都是将其他组件直接或者间接地置于窗体中。
   当对窗体进行操作时，例如窗体的打开、关闭、激活、停用等，这些动作都属于窗体事件,JDK中提供了一个类 WindowEvent用于表示这些窗体事件。在应用程序中，当对窗体事件进行处理时，首先需要定义一个实现了 WindowListener接口的类作为窗体监听器，然后通过addWindowListener()方法将窗体对象与窗体监听器绑定。
*/
package cn.kong.GUL;

import sun.swing.SwingUtilities2;

import javax.swing.*;
import java.awt.event.WindowEvent;
import java.awt.event.WindowListener;

public class Example08 {
    public static void main(String[] args) {
        //使用SwingUtilities.invokeLater工具类调用createAndShowGUI方法，并显示GUI程序
        SwingUtilities.invokeLater(Example08::createAndShowGUI);
    }

    private static void createAndShowGUI() {
        JFrame f = new JFrame("WindowEvent");

        f.setSize(400,300);
        f.setLocation(400,500);
        f.setVisible(true);
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        //使用内部类创建WindowListener实例对象，监听窗口事件
        //为窗口增加监听机制
        f.addWindowListener(new WindowListener() {
            @Override
            public void windowOpened(WindowEvent e) {
                System.out.println("windowOpened--窗口打开事件");
            }

            @Override
            public void windowClosing(WindowEvent e) {
                System.out.println("windowClosing--窗体正在关闭事件");
            }

            @Override
            public void windowClosed(WindowEvent e) {
                System.out.println("windowClosed--窗体关闭事件");

            }

            @Override
            public void windowIconified(WindowEvent e) {
                System.out.println("windowIconified--窗体图标化事件");

            }

            @Override
            public void windowDeiconified(WindowEvent e) {
                System.out.println("windowDeiconified--窗体取消图标化事件");

            }

            @Override
            public void windowActivated(WindowEvent e) {
                System.out.println(" windowActivated--窗体激活事件");

            }

            @Override
            public void windowDeactivated(WindowEvent e) {
                System.out.println("windowDeactivated--窗体停用事件");

            }
        });
    }
}
/*
匿名内部类中对操作的窗口进行监听，当收到特定的操作后，就将所触发的事件的名称打印下来。
*/
```

##### 2、鼠标事件

```java
/*
一、定义：
   在图形用户界面中，用户会经常使用鼠标来进行选择、切换界面等操作，这些操作被定义为鼠标事件，其中包括鼠标按下、鼠标松开、鼠标单击等。JDK中提供了一个MouseEvent类用于表示鼠标事件，几乎所有的组件都可以产生鼠标事件。处理鼠标事件时，首先需要通过实现MouseListener接口定义监听器（也可以通过继承适配器MouseAdapter类来实现)，然后调用addMouseListener()方法将监听器绑定到事件源对象。
 
二、MouseEvent类
   为鼠标的按键定义了对应的常量，可以通过MouseEvent对象的getButton()方法获取被操作的按键的键值，从而判断是哪个案件的操作。
*/
package cn.kong.GUL;

import javax.swing.*;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;

public class Example09 {
    public static void main(String[] args) {
        //使用SwingUtilities.invokeLater工具类调用createAndShowGUI方法，并显示GUI程序
        SwingUtilities.invokeLater(Example09::createAndShowGUI);
    }

    private static void createAndShowGUI() {
        JFrame f = new JFrame("MouseEvent");
        f.setSize(400,300);
        f.setLocation(400,500);
        f.setVisible(true);
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        JButton but = new JButton("Button");//创建按钮对象
        f.add(but);
        //使用内部类创建MouseListener实例对象，监听按钮
        but.addMouseListener(new MouseListener() {
            @Override
            public void mouseClicked(MouseEvent e) {
                if(e.getButton()==MouseEvent.BUTTON1){
                    System.out.println("鼠标左击事件");
                }else if(e.getButton()==MouseEvent.BUTTON3){
                    System.out.println("鼠标右击事件");
                }else if(e.getButton()==MouseEvent.BUTTON2){
                    System.out.println("鼠标中建单机事件");
                }
                System.out.println("mouseClicked--鼠标完成单机");
            }

            @Override
            public void mousePressed(MouseEvent e) {
                System.out.println("mousePressed--鼠标按下事件");

            }

            @Override
            public void mouseReleased(MouseEvent e) {
                System.out.println(" mouseReleased--鼠标放开事件");

            }

            @Override
            public void mouseEntered(MouseEvent e) {
                System.out.println("mouseEntered--鼠标进入按钮区事件");

            }

            @Override
            public void mouseExited(MouseEvent e) {
                System.out.println("mouseExited--鼠标移除按钮区事件");

            }
        });
    }

}


```

##### 3、键盘事件

```java
/*
一、定义：
   键盘操作也是最常用的用户交互方式，例如键盘按下、释放等，这些操作被定义为键盘事件。JDK中提供了一个 KeyEvent类表示键盘事件，处理 KeyEvent事件的监听器对象需要实现KeyListener 接口或者继承KeyAdapter类。
*/
package cn.kong.GUL;

import javax.swing.*;
import java.awt.*;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;

public class Example10 {
    public static void main(String[] args) {
        //使用SwingUtilities.invokeLater工具类调用createAndShowGUI方法，并显示GUI程序
        SwingUtilities.invokeLater(Example10::createAndShowGUI);

    }

    private static void createAndShowGUI() {
        JFrame f = new JFrame("KeyEvent");
        f.setLayout(new FlowLayout());//流式布局管理器
        f.setSize(400,400);
        f.setLocation(450,500);
        JTextField tf = new JTextField(30);//创建文本框对象
        f.add(tf);
        f.setVisible(true);
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        //为文本框添加监听器
        tf.addKeyListener(new KeyListener() {
            @Override
            public void keyTyped(KeyEvent e) {
                //获取对应的键盘字符
                char keyChar = e.getKeyChar();
                //获取对应的键盘字符代码
                int keyCode = e.getKeyCode();
                System.out.println("键盘按下的字符为-->" + keyChar + " ");
                System.out.println("键盘按下的字符代码为-->"+ keyCode);
            }

            @Override
            public void keyPressed(KeyEvent e) {

            }

            @Override
            public void keyReleased(KeyEvent e) {

            }
        });
    }
}

```

##### 4、动作事件

```java
/*
一、定义：
   动作事件与前面3种事件有所不同，它不代表某个具体的动作，只是表示一个动作发生了。例如，在关闭一个文件时，可以通过键盘关闭，也可以通过鼠标关闭。在这里读者不需要关心使用哪种方式对文件进行关闭，只要是对关闭按钮进行操作，即触发了动作事件。
   在Java 中，动作事件用 ActionEvent类表示，处理 ActionEvent 事件的监听器对象需要实现 ActionListener接口。监听器对象在监听动作时，不会像鼠标事件一样处理鼠标的移动和单击的细节，而是去处理类似手“按钮按下”这样“有意义”的事件。关于动作事件的案例在事件处理机制中讲过，再次不在赘述。
   ActionEvent事件和ItemEvent时间的区别
*/
```

![image-20210618154704633](java%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0.assets/image-20210618154704633.png)



### 5、Swing中的绘图

```java
/*
1、  
   很多GUI程序都需要在组件上绘制图形，比如实现一个五子棋的小游戏，就需要在组件上绘制棋盘和棋子。在java.awt包中专门提供了一个Graphics类，它相当于一个抽象的画笔，其中提供了各种绘制图形的方法，使用Graphics类的方法就可以完成在组件上绘制图形
   
2、Graphice类，绘制各种图形的类
  1、常用的方法：
    1. void setColor(Color c)
      将此图形上下文的当前颜色设置为指定颜色
    2. void setFont(Font f)
      将此图形上下文的字体设置为指定字体
    3. void drawLine(int x1,int y1 ,int x2,int y2)
       以(×1,y1)和(×2,y2)为端点绘制一条线段
    4. void drawRect(int x, int y, int width, int height)
      绘制指定矩形的边框。矩形的左边缘和右边缘分别位于×和x+width。上边缘和下边缘分别位于y和y + height
    5. void drawRect(int x, int y, int width, int height)
      绘制椭圆的边框。得到一个圆或椭圆,它刚好能放入由×、y.
width和 height参数指定的矩形中。椭圆覆盖区域的宽度为width+1像素,高度为height +1 像素
    6. void fillRect (int x,int y, int width, int height)
      用当前颜色于填充指定的矩形。该矩形左边缘和右边缘分别位于×和×+width - 1。上边缘和下边缘分别位于y和y + height - 1
      
    7. void fillOval(int x,int y,int width,int height)
       用当前颜色填充外接指定矩形框的椭圆
       
    8. void drawString (String str, int×,int y)
      使用此图形上下文的当前字体和颜色绘制指定的文本 str。最左侧字符左下角位于 (x)坐标.
   
   2、方法的详细说明：
     1. setColor()方法
       用于指定上下文颜色，方法中接收一个Color类型的参数。在AWT 中，Color类代表颜色，其中定义了许多代表各种颜色的常量，例如 Color.RED，Color.BLUE等，这些常量都是Color类型的，可以直接作为参数传递给setColor()方法。
     2. setFont()方法
       用于指定上下文字体，方法中接收一个Font类型的参数。Font类表示字体，可以使用new关键字创建Font对象。Font的构造方法中接收3个参数，第一个是String类型，表示字体名称，如“宋体”“微软雅黑”等;第2个参数是int类型，表示字体的样式，参数接收Font类的3个常量Font.PLAINT、Font.ITALIC 和Font.BOLD;第3个参数为int类型，表示字体的大小。
     3. drawRect()方法和drawOval()方法
        用于绘制矩形和椭圆形的边框
     4. fillRect()和 fillOval()方法
        用于使用当前的颜色填充绘制完成的矩形和椭圆形。        5.drawString()方法
      用于绘制--段文本，第一个参数str表示绘制的文本内容，第2个和第3个参数×、y为绘制文本的左下角坐标。
    
3、目前大部分的网站为了防止用户在注册时重复提交表单，在注册页面都会有一个图片验证码。接下来通过重写JPanel组件的paint()方法，在一个 JPanel面板上绘制一张图片验证码，
*/
package cn.kong.GUL;

import javax.swing.*;
import java.awt.*;
import java.util.Random;

public class Example11 {
    public static void main(String[] args) {
        final JFrame frame = new JFrame("验证码");
        final JPanel panel = new MyPanel();//创建Panel对象
        frame.add(panel);
        frame.setSize(200,200);
        //将Frame窗口居中
        frame.setLocationRelativeTo(null);
        frame.setVisible(true);
    }
}
class MyPanel extends JPanel{
    public void paint(Graphics g){
        int width = 160;//验证码的图片的宽度
        int height = 40;//高度
        g.setColor(Color.LIGHT_GRAY);//设置上下文颜色
        g.fillRect(0,0,width,height);//填充验证码背景
        g.setColor(Color.BLACK);
        g.drawRect(0,0,width -1, height - 1);//绘制边框
        //绘制干扰点
        Random r = new Random();
        for(int i = 0; i < 4; i++){
            int x = r.nextInt(width) - 2;
            int y = r.nextInt(height) - 2;
            g.drawOval(x,y,2,2);
        }
        g.setFont(new Font("黑体",Font.BOLD,30));//验证码字体
        g.setColor(Color.BLUE);
        //随机产生验证码
        char[] chars= ("0123456789abcdefghijkmnopqrstuvwxyzABCDEFG"
                + "HIJKLMNPQRSTUVwXYz").toCharArray();
        StringBuilder sb = new StringBuilder();
        for (int i =0;i<4; i++){
            int pos = r.nextInt (chars. length);
            char c= chars[pos];
            sb. append(c +"");
        }

        g.drawString(sb.toString(),20,30);//写入验证码
    }
}


```



### 6、Swing常用组件(中间容器)

#### 1、面板组件

```java
/*
一、概念：
   Swing组件中不仅具有JFrame和 JDialog这样的顶级窗口，还提供了一些中间容器，这些容器不能单独存在，只能放置在顶级窗口中。其中最常见的中间容器有两种——JPanel和JScrollPane，接下来分别来介绍这两种容器。
   ①JPanel:JPanel和AWT中的 Panel组件使用方法基本一致，它是一个无边框，不能被移动、放大、缩小或者关闭的面板，它的默认布局管理器是 FlowLayout。当然也可以使用JPanel带参数的构造函数JPanel(LayoutManager layout)或者它的setLayout()方法为其制定布局管理器。
   2、JScrollPane:与JPanel 不同的是，JScrollPane是一个带有滚动条的面板容器，而且这个面板只能添加一-个组件。如果想在JScrollPane面板中添加多个组件，应该先将组件添加到JPanel中，然后将JPanel添加到JScrollPane 中。
 
 二、常见的构造方法：
    1. JScrollPane()
      创建一个空的JScrollPane面板
    2. JScrollPane(Component view)
      创建一个显示指定组件的JScrolPane面板，只要组件的内容超过视图大小就会显示水平和垂直滚动条

    3. JScrollPane(Component view,int vsbPolicy,int hsbPolicy)
    创建一个显示指定容器并具有指定滚动条策略的JScrollPane。参数vsbPolicy和hsbPolicy 分别表示垂直滚动条策略和水平滚动条策略，应指定为ScrollPaneConstants的静态常量,如下所示。
    HORIZONTAL_SCROLLBAR_AS_NEEDED:表示水平滚动条只在需要时显示，是默认策略
    HORIZONTAL_SCROLLBAR_NEVER:表示水平滚动条永远不显示         HORIZONTAL_SCROLLBAR_ALWAYS:表示水平滚动条一直显示
三、
    上面列出了JScrollPane 的3个构造方法。其中，第一个构造方法用于创建一个空的JScrollPane面板，第2个构造方法用于创建显示指定组件的JScrollPane面板，这两个方法都比较简单。第3个构造方法是在第2个构造方法的基础上指定滚动条策略。如果在构造方法中没用指定显示组件和滚动条策略,也可以使用JScrolPane提供的方法进行设置，
    
四、常见的方法：
   1. void setHorizontalBarPolicy(int policy)
     指定水平滚动条策略,即水平滚动条何时显示在滚动面板上
   2. void setVerticalBarPolicy(int policy)
     指定垂直滚动条策略,即垂直滚动条何时显示在滚动面板上
     
   3. void setViewportView(Component view)
     设置在滚动面板显示的组件
     
五、上述介绍的的方法JScrollpane面板策略的设置方法，
   ScrollPaneConstants接口声明了很多常量属性
     1.VERTICAL_SCROLLBAR_AS_NEEDED 
      HORIZONTAL_SCROLLBAR_AS_NEEDED 
        以上两个常量：当填充的组件超过客户端窗口大小时，自动显示水平和竖直滚动条
        
    2. VERTICAL_SCROLLBAR_NEVER 
       HORIZONTAL_SCROLLBAR_NEVER 
          无论填充的组件视图大小如何，始终显示水平和竖直滚动条
          
    3. VERTICAL_SCROLLBAR_ALWAYS 
       HORIZONTAL_SCROLLBAR_ALWAYS 
           无论填充的组件试图大小如何，始终不显示水平和竖直滚动条
    4、调用方式：ScrollPaneConstants.VERTICAL_SCROLLBAR_AS_NEEDED 

 五、下面通过一个案例来向中间容器添加按钮
*/

package cn.kong.GUL;

import javax.swing.*;
import java.awt.*;

public class Example12 {
    public static void main(String[] args) {
        //使用SwingUtilities.invokeLater工具类调用createAndShowGUI方法，并显示GUI程序
        SwingUtilities.invokeLater(Example12::createAndShowGUI) ;

    }

    private static void createAndShowGUI() {
        JFrame f = new JFrame("PanelDemo");
        f.setLayout(new BorderLayout());
        f.setSize(300,200);
        f.setLocation(300,200);
        f.setVisible(true);
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        //创建Jscorllpane滚动面板组件
        JScrollPane scrollPane = new JScrollPane();
        //设置水平滚动条策略--滚动条一直显示
        scrollPane.setHorizontalScrollBarPolicy(ScrollPaneConstants.
                HORIZONTAL_SCROLLBAR_AS_NEEDED);
        //设置垂直滚动条策略--滚动条需要时显示
        scrollPane.setVerticalScrollBarPolicy (ScrollPaneConstants.
                VERTICAL_SCROLLBAR_ALWAYS);
        //定义TJPanel 面板
        JPanel panel = new JPanel();
        //在JPanel面板中添加四个按钮
        panel.add(new JButton("按钮1"));
        panel.add(new JButton("按钮2"));
        panel.add (new JButton("按钮3"));
        panel.add (new JButton("按钮4"));
        //设置JPane1面板在滚动面板中显示
        scrollPane.setViewportView (panel);
        //将滚动面板添加到内容面板的CENTER区域
        f.add(scrollPane, BorderLayout.CENTER);
    }
}

```

#### 2、文本组件

```java
/*
一、定义：
   文本组件用于接收用户输入的信息或向用户展示信息，其中包括文本框（JtextField ) 、文本域(JtextArea )等，它们都有一个共同父类JTextComponent。JTextComponent 是一个抽象类，它提供了文本组件常用的方法，如
   JTextComponent抽象类提供的方法
     1. String getText()
       返回文本组件中所有的文本内容
       
     2. String getSelectedText()
       返回文本组件中选定的文本内容
       
     3. void selectAil()
       在文本组件中选中所有内容
       
     4. void setEditable()
       设置文本组件为可编辑或者不可编辑状态
       
     5. void setText(String text)
       设置文本组件的内容
       
     6. void replaceSelection(String content)
       用给定的内容替换当前选定的内容
       
    总结：
      以上是几种对文本组件进行操作的方法，其中包括选中文本内容、设置文本内容以及获取文本内容等。由于JTextField和JTextArea这两个文本组件都继承了JTextComponent飞，因此它们都具有以上的方法，但它们在使用上还有一定的区别。接下来就对这两个文本组件进行详细讲解。
      
二、JTextField:
   JTextField:JTextField称为文本框，它只能接收单行文本的输入。    1. JTextField 常用的构造方法。
     1.  JTextField()
       创建一个空的文本框,初始字符串为null
       
     2. JTextField(int columns)
       创建一个典有指定列数的文本框初始字符串为null
       
     3. JTextField(String text)
       创建一个显示指定初始字符串的文本框
       
     4. JTextField(String text, int column)
       创建一个具有指定列数并显示指定初始字符串的文本框
       
    一个子类：JPasswordText
     JTextField 有一个子类JPasswordText，它表示一个密码框，只能接收用户的单行输入，但是在此框中不显示用户输入的真实信息，而是通过显示指定的回显字符作为占位符。新创建的密码框默认地回显字符为“*”。JPasswordText和JTextField 的构造方法相似，这里就不再介绍了。
     
三、JTextArea
   JTextArea:JTextArea称为文本域，它能接收多行的文本的输入，使用JTextArea构造方法创建对象时可以设定区域的行数、列数。接下来介绍一下JTextArea常用的构造方法，
   1. JTextArea()
     创建一个空的文本域
     
   2. JTextArea(String text)
     创建显示指定初始字符串的文本域
     
   3. JTextArea(int rows,int columns)
     创建具有指定行和列的空的文本域
     
   4. JTextArea(String text, int rows,int columns)
     创建显示指定初始文本并指定了行列的文本域
*/
package cn.kong.GUL;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class Example13  extends JFrame{
    public static void main(String[] args) {
        new Example13();
    }
    JButton sendBt;
    JTextField inputField;
    JTextArea chatContent;
    public Example13(){
        this.setLayout(new BorderLayout());
        chatContent = new JTextArea(12,34);//创建一个文本域
        //创建一个滚动面板，将文本域作为其显示按钮
        JScrollPane showPanel = new JScrollPane(chatContent);
        chatContent.setEditable(false);//设置文本域不可编辑
        JPanel inputPanel = new JPanel();//创建一个JPanel面板
        inputField = new JTextField(20);//创建一个文本框
        sendBt = new JButton("发送");//创建一个发送按钮
        //为按钮添加事件
        sendBt.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String content = inputField.getText();//获取输入文本信息
                //判断输入信息是否为空
                if(content != null && !content.trim().equals("")){
                    chatContent.append("本人：" + content + "\n");
                }else{
                    chatContent.append("聊天信息不能为空" + "\n");
                }
                inputField.setText("");//将输入文本域的内容设置为空
            }
        });

        Label label = new Label("chating");
        inputPanel.add(label);//将标签添加到JPanel面板
        inputPanel.add(inputField);//将文本框添加到JPanel面板
        inputPanel.add(sendBt);//将按钮添加到JPanel面板
        //将滚动面板和JPanel面板添加到JFrame创口
        this.add(showPanel,BorderLayout.CENTER);
        this.add(inputPanel,BorderLayout.SOUTH);
        this.setSize(400,300);
        this.setTitle("聊天窗口");
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        this.setVisible(true);

    }
}

```

#### 3、标签组件&图标组件

```java
/*
一、定义：
   JLabel组件可以显示文本，图象，还可以设置标签内容的垂直和水平对齐方式。
   
二、常用构造方法：
   1. JLabel() 
     创建一个没有图像的 JLabel实例，标题为空字符串。
     
   2. JLabel(Icon image) 
     使用指定的图像创建一个 JLabel实例。
     
   3. JLabel(Icon image, int horizontalAlignment) 
     创建一个具有指定图像和水平对齐的 JLabel实例。
     
   4. JLabel(String text)
     使用指定的文本创建一个 JLabel实例。 
     
   5. JLabel(String text, Icon icon, int horizontalAlignment)
     创建具有 JLabel文本，图像和水平对齐的JLabel实例。 
   
   6. JLabel(String text, int horizontalAlignment) 
     创建一个具有指定文本和水平对齐的 JLabel实例。
     
二、图标组件
   public class ImageIcon
   从图像绘制图标的图标界面的实现。 使用MediaTracker预先从URL，文件名或字节数组创建的图像，以监视图像的加载状态。
   1. 常用构造方法
     1. ImageIcon()
       创建未初始化的图像图标。 
     2， ImageIcon(String filename) 
       从指定的文件创建一个ImageIcon。 
     3. ImageIcon(Image image) 
       从图像对象创建一个ImageIcon。
    
    2.常用的方法：
      1. int getIconHeight() 
         获取图标的高度。
      2. int getIconWidth() 
         获取图标的宽度。 
      3. Image getImage()
        返回此图标的 Image 
      4. void setImage(Image image)
        设置此图标显示的图像。  
*/
package cn.kong.GUL;

import javax.swing.*;
import java.awt.*;

public class Example14 {
    public static void main(String[] args) {
        //使用SwingUtilities.invokeLater工具类调用createAndShowGUI方法，并显示GUI程序
        SwingUtilities.invokeLater(Example14::createAndShowGUI) ;

    }

    private static void createAndShowGUI() {
        JFrame f = new JFrame("PanelDemo");
        f.setLayout(new BorderLayout());
        f.setSize(300,200);
        f.setLocation(300,200);
        f.setVisible(true);
        f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        //创建一个JLabel标签组件,用来显示图片
        JLabel label1 = new JLabel();
        //创建一个ImageIcon图表组件，并加入到JLabel中filename跟的是图片的路径
        ImageIcon icon = new ImageIcon("C:\\Users\\28929\\Pictures\\pic\\动漫\\FruitStore.jpg");
        Image img = icon.getImage();//返回此图标的Image
        //设置图片的大小
        img = img.getScaledInstance(300,150,Image.SCALE_DEFAULT);
        icon.setImage(img);//设置此图标的显示图象
        label1.setIcon(icon);
        //创建一个页尾JPanel面板，并加入到JLabel标签组件
        JPanel panel = new JPanel();
        JLabel label2 = new JLabel("Welcome to here",JLabel.CENTER);
        panel.add(label2);
        //向JFrame顶部和尾部分别加入JLabel和JPanel组件
        f.add(label1,BorderLayout.PAGE_START);
        f.add(panel,BorderLayout.PAGE_END);

    }
}

```

#### 4、按钮组件

```java
/*
一：定义：
   在 Swing 中，常见的按钮组件有JButton、JCheckBox、JRadioButton等，它们都是抽象类AbstractButton类的直接或间接子类。在 AbstractButton类中提供了按钮组件通用的一些方法，
   AbstractButton类常用方法：
    1. lcon getlcon()和void setlcon(Icon icon)
      设置或者获取按钮的图标
    2. String getText()和void setText(String text)
      设置或者获取按钮的文本
    3. setSelected(boolean b)
      设置按钮的状态，当b为true时，按钮是选中状态，反之为未选中
    4. void setEnable(boolean b)
      启用（当b 为true）或禁用〔当b为false)按钮
    5. boolean isSelected(
      返回按钮的状态（ true为选中，反之为未选中)
二、子类中的JButtona按钮
   1.常用构造方法
     1. JButton() 
       创建一个没有设置文本或图标的按钮。
     2. JButton(Icon icon)
       创建一个带有图标的按钮。
     3. JButton(String text)
       创建一个带文本的按钮。 
     4.JButton(String text, Icon icon)
       创建一个带有初始文本和图标的按钮。 
       
三、JCheckBox（复选框按钮）
  1.常用构造方法
    1. JCheckBox() 
      创建一个最初未选择的复选框按钮，没有文字，没有图标。
    2. JCheckBox(String text) 
      创建一个最初未选择的复选框与文本。 
    3. JCheckBox(String text, boolean selected)
      创建一个带有文本的复选框，并指定是否最初选择它。
  2，解释：
    JCheckBox组件被称为复选框，它有选中（是）/未选中（非）两种状态，如果用户想接收的输入只有“是”和“非”，则可以通过复选框来切换状态。如果复选框有多个，则用户可以选中其中一个或者多个。
    
 四、JRadionButton(单选按钮)
    1.概念：
      JRadioButton组件被称为单选按钮，与JCheckBox复选框不同的是，单选按钮只能选中--个。就像随身听上的播放和快进按钮，当按下一个，先前按下的按钮就会自动弹起。对于JRadioButton按钮来说，当一个按钮被选中时，先前被选中的按钮就会自动取消选中。
      由于JRadioButton组件本身并不具备这种功能，因此若想实现JRadioButton 按钮之间的互斥，需要使用javax.swing.ButtonGroup类，它是一个不可见的组件，不需要将其增加到容器中显示，只是在逻辑上表示-个单选按钮组。将多个JRadioButton 按钮添加到同一个单选按钮组对象中，就能实现按钮的单选功能。
    2. 常见的构造方法
       1. JRadioButton() 
         创建一个没有设置文本的最初未选择的单选按钮
         
       2. JRadioButton(Icon icon, boolean selected) 
         创建具有指定图像和选择状态的单选按钮，但不包含文本。
       3、 JRadioButton(String text) 
          使用指定的文本创建一个未选择的单选按钮。
          
       4. JRadioButton(String text, boolean selected) 
         创建具有指定文本和选择状态的单选按钮。
*/
package cn.kong.GUL;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class Example15 extends JFrame {
    private JCheckBox italic;
    private JCheckBox bold;
    private JLabel label;
    public static void main(String[] args) {
        new Example15();
    }
    public Example15(){
        //创建一个 JLabel标签，标签文本居中对齐
        label = new JLabel("传智播客欢迎你!",JLabel.CENTER);
        //设置标签文本的字体
        label.setFont (new Font("宋体", Font.PLAIN,20));
        this.add(label);//在CENTER域添加标签
        JPanel panel = new JPanel();//创建一个JPanel面板
        // 创建两个JCheckBox复选框
        italic = new JCheckBox("ITALIC");
        bold = new JCheckBox("BOLD");
        //为复选框定义ActionListener监听器
        ActionListener listener = new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                int mode = 0;
                if(bold.isSelected()){
                    mode += Font.BOLD;
                }
                if(italic.isSelected()){
                    mode += Font.ITALIC;
                    label.setFont(new Font("宋体",mode,20));
                }
            }
        };
        //文两个复选框增加监听器
        italic.addActionListener(listener);
        bold.addActionListener(listener);
        //在JPanel面板中添加复选框
        panel.add(italic);
        panel.add(bold);
        //在south域中添加JPanel面板
        this.add(panel,BorderLayout.SOUTH);
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        this.setSize(300,300);
        this.setVisible(true);
    }
}


//按例2
package cn.kong.GUL;

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.awt.event.ActionListener;

public class Example16 extends JFrame {
    private ButtonGroup group;//单选按钮组对象
    private JPanel panel;//JPanel面板放置3个JRadioButton按钮
    private JPanel pallet;//JPanel面板作为调色
    public static void main(String[] args) {
        new Example16();
    }
    public Example16(){
        pallet = new JPanel();
        this.add(pallet,BorderLayout.CENTER);
        panel = new JPanel();
        group = new ButtonGroup();
        //调用addJRadioButton方法
        addJRadioButton("灰");
        addJRadioButton("粉");
        addJRadioButton("黄");
        this.add(panel,BorderLayout.SOUTH);
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        this.setSize(300,300);
        this.setVisible(true);
    }

    private void addJRadioButton(final String text) {
        JRadioButton radioButton = new JRadioButton(text);
        group.add(radioButton);
        panel.add(radioButton);
        radioButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                Color color = null;
                if("灰".equals(text)){
                    color = Color.GRAY;
                }else if("粉".equals(text)){
                    color = Color.PINK;
                }else if("黄".equals(text)){
                    color = Color.YELLOW;
                }else{
                    color = Color.WHITE;
                }
                pallet.setBackground(color);
            }
        });
    }
}

```



#### 5、下拉框组件



```java
/*
一、定义：
   JComboBox组件被称为组合框或者下拉列表框，它将所有选项折叠收藏在一起，默认显示的是第一个添加的选项。当用户单击组合框时，会出现下拉式的选择列表，用户可以从中选择其中一项并显示。
   JComboBox组合框组件分为可编辑和不可编辑两种形式，对于不可编辑的组合框，用户只能在现有的选项列表中进行选择;而对于可编辑的组合框，用户既可以在现有的选项中选择，也可以自己输入新的内容。需要注意的是，自己输入的内容只能作为当前项显示，并不会添加到组合框的选项列表中。
   
 二、构造方法：
    1. JComboBox()
      创建一个没有可选项的组合框
    2. JComboBox(Object[] items)
      创建一个组合框，将Object数组中的元素作为组合框的下拉列表选项
    3. JComboBox(Vector items)
      创建一个组合框，将Vector集合中的元素作为组合框的下拉列表选项
三、常用方法
    1. void addItem （Object anObject)
      为组合框添加选项
    2. void insertItemAt(Object anObject,int index)
      在指定的索引处插入选项
      
    3. Objct getItemAt(int index)
      返回指定索引处选项,第一个选项的索引为0
    4. int getItemCount()
      返回组合框中选项的数目
    5. Object getSelectedItem()
      返回当前所选项
    6. void removeAllItems()
      删除组合框中所有的选项
    7. void removeItem(Object object)
      从组合框中删除指定选项 
    8. void removeItemAt(int index)
      移除指定索引处的选项
    9. void setEditable(boolean aFlag)
      设置组合框的选项是否可编辑，aFlag为true 则可编辑,反之则不可编辑
*/
package cn.kong.GUL;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class Example17 extends JFrame {
    private JComboBox comboBox;//定义一个JComboBox组合框
    private JTextField field;//定义一个JTextField文本框
    public static void main(String[] args) {
        new Example17();
    }
    public Example17(){
        JPanel panel = new JPanel();//创建一个JPanel面板
        comboBox = new JComboBox();
        //为组合框添加选项
        comboBox.addItem("请选择城市");
        comboBox.addItem("北京");
        comboBox.addItem("天津");
        comboBox.addItem("南京");
        comboBox.addItem("上海");
        comboBox.addItem("重庆");
        //为组合和框添加监听器
        comboBox.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String item = (String)comboBox.getSelectedItem();
                if("请选择城市".equals(item)){
                    field.setText("");
                }else{
                    field.setText("你选择的城市是："+ item);
                }
            }
        });
        field = new JTextField(20);
        panel.add(comboBox);//在面板中添加组合框
        panel.add(field);//在面板中添加文本框
        //在内容面板中添加JPanel面板
        this.add(panel,BorderLayout.NORTH);
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        this.setSize(350,100);
        this.setVisible(true);
    }
}

```

#### 6、菜单组件

##### 1、下拉式菜单

```java
/*
一、定义：
   对于下拉式菜单，读者肯定很熟悉，因为计算机中很多文件的菜单都是下拉式的，如记事本的菜单。在GUI程序中，创建下拉式菜单需要使用3个组件;JmenuBar(菜单栏).Jmenu（菜单）和Jmenultem（菜单项)
   
二、分类
   ( 1 ) JMenuBar:JMenuBar 表示一个水平的菜单栏，它用来管理菜单，不参与同用户的交互式操作。菜单栏可以放在容器的任何位置,但通常情况下会使用顶级窗口(如 JFrame, Jdialog )的setJMenuBar (JMenuBar menuBar)方法将它放置在顶级窗口的顶部。JMenuBar有一个无参构造函数，创建菜单栏时，只需要使用new关键字创建JMenuBar对象即可。创建完菜单栏对象后，可以调用它的add(JMenu c)方法为其添加JMenu菜单。
   (2 ) JMenu:JMenu表示一个菜单，它用来整合管理菜单项。菜单可以是单一层次的结构，也可以是多层次的结构。大多情况下，会使用构造函数JMenu(String text)创建JMenu菜单，其中的参数text表示菜单上的文本。
    JMenu中还有一些常用的方法,如
    1.  void JMenultem add( JMenultem menultem)
       将菜单项添加到菜单末尾，返回此菜单项
       
    2. void addSeparator()
       将分隔符添加到菜单的末尾
     3. JMenultem getltem(int pos)
        返回指定索引处的菜单项,第一个菜单项的索引为О
    4. int getltemCount()
       返回菜单上的项数,菜单项和分隔符都计算在内
    5. void JMenultem insert(JMenultem menultem,int pos)
      在指定索引处插入菜单项
    6. void insertSeparator(int pos)
      在指定索引处插入分隔符
    7. void remove(int pos)
      从菜单中移除指定索引处的菜单项
    8、 void remove(JMenultem menultem)
      从菜单中移除指定的菜单项
    9. void removeAll()
      从菜单中移除所有的菜单项
  
  ( 3 ) JMenultem:JMenultem表示一个菜单项，它是菜单系统中最基本的组件。和JMenu菜单一样，在创建JMenultem菜单项时，通常会使用构造方法JMenumltem(String text)为菜单项指定文本内容。
   由于JMenultem类是继承自AbstractButton类的，因此可以把它看成是一个按钮。如果使用无参的构造方法创建了一个菜单项，则可以调用从 AbstractButton类中继承的setText(Stringtext)方法和setlcon()方法为其设置文本和图标。

4、创建和添加下拉式菜单，一般分为以下几个步骤。
  (1）创建一个JMenuBar 菜单栏对象，将其放置在JFrame窗口的顶部。   （2）创建JMenu菜单对象，将其添加到JMenuBar 菜单栏中。
  (3）创建JMenultem 菜单项,将其添加到JMenu菜单中。
  
5、一下面的例子为例
   本例中，在JMenu菜单中添加item1（弹出窗口）和item2(关闭）两个菜单项，并调用了JMenu的addSeparator()方法在菜单中添加了一-条分隔符。在代码第13~22行和第23~27行中分别为 item1和 item2添加了事件监听器。当单击item1菜单时，会弹出一个模态的JDialog窗口，当单击item2时会退出程序。
*/
package cn.kong.GUL;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class Example18 extends JFrame {
    public static void main(String[] args) {
        new Example18();
    }
    public Example18(){
        JMenuBar menuBar = new JMenuBar();//创建菜单栏
        this.setJMenuBar(menuBar);//将菜单栏添加到JFrame窗口中
        JMenu menu = new JMenu("操作");//创建菜单
        menuBar.add(menu);
        //创建两个菜单项
        JMenuItem item1 = new JMenuItem("弹出窗口");
        JMenuItem item2 = new JMenuItem("关闭");
        //为菜单项添加事件监听器
        item1.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                //创建一个JDialog窗口
                JDialog dialog = new JDialog(Example18.this,true);
                dialog.setTitle("弹出窗口");
                dialog.setSize(200,200);
                dialog.setLocation(50,50);
                dialog.setVisible(true);
            }
        });
        item2.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.exit(0);
            }
        });
        menu.add(item1);//将选项增加到菜单中
        menu.addSeparator();//添加一个分隔符
        menu.add(item2);
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        this.setSize(300,300);
        this.setVisible(true);
    }
}

```

##### 2、弹出式菜单

```java
/*
一、定义：
   JPopupMenu弹出式菜单和下拉式菜单一样，都通过调用add()方法添加JMenultem菜单项,但它默认是不可见的。如果想要显示出来,则必须调用它的show(Component invoker,int x,inty)方法。该方法中参数invoker表示 JPopupMenur菜单显示位置的参考组件,x和y表示 invoker组件坐标空间中的一个坐标，显示的是 JPopupMenur 菜单的左上角坐标。
二、以下的方法：

   在菜单中右击才可以显示弹出式菜单
*/
package cn.kong.GUL;
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;

public class Example19 extends JFrame {
    public static void main(String[] args) {
        new Example19();
    }
    private JPopupMenu popupMenu;
    public Example19(){
        //创建一个JPopupMenu菜单
        popupMenu = new JPopupMenu();
        //创建三个JMenuItem菜单项
        JMenuItem refreshItem = new JMenuItem("refresh");
        JMenuItem createItem = new JMenuItem("create");
        JMenuItem exitItem = new JMenuItem("exit");
        //为exitItem增加监听器
        exitItem.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.exit(0);
            }
        });
        //往JPopupMenu菜单增加菜单项
        popupMenu.add(refreshItem);
        popupMenu.add(createItem);
        popupMenu.add(exitItem);
        //为JFrame窗口添加clicked鼠标事件监听器
        this.addMouseListener(new MouseListener() {
            @Override
            public void mouseClicked(MouseEvent e) {
                //如果淡季的是鼠标右键，显示JPopupMenu菜单
                if(e.getButton() == e.BUTTON3){
                    popupMenu.show(e.getComponent(),e.getX(),e.getY());
                }
            }

            @Override
            public void mousePressed(MouseEvent e) {
            }

            @Override
            public void mouseReleased(MouseEvent e) {
            }

            @Override
            public void mouseEntered(MouseEvent e) {
            }

            @Override
            public void mouseExited(MouseEvent e) {
            }
        });
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        this.setSize(300,300);
        this.setVisible(true);
    }
}
```

```java
//下拉式弹出菜单 choice 下拉式弹出菜单类
import javax.swing.*;
import java.awt.*;

public class ChoiceTest01 {
    public static void main(String[] args) {
        Choice i = new Choice();
        i.add("Green");
        i.add("Red");
        i.add("Black");
        JFrame j = new JFrame();
        j.add(i);
        j.setVisible(true);
        j.setLocation(300,400);
        j.setSize(500,600);
    }
}

```





#### 7、表格组件

```java
/*
一、 
   表格也是 GUI程序中常用的组件，表格是一个由多行、多列组成的二维显示区。Swing 的JTable 以及相关类提供了对这种表格的支持。使用了JTable以及相关类，程序既可以使用简单代码创建出表格来显示二维数据，也可以开发出功能丰富的表格，还可以为表格定制各种显示外观、编辑特性。
   使用JTable 来创建表格是非常容易的事情，它可以把一个二维数据包装成一个表格，这个二维数据既可以是一个二维数组，也可以是集合元素Vector对象（Vector里面包含Vector形成二维数据)。除此之外，为了给该表格的每一列指定列标题，还需要传入一个一维数据作为列标题，这个一维数据既可以是一维数组，也可以是Vector对象。

二、JTable的构造函数
   1. JTable()
     建立一个新的Jtable，并使用系统默认的 Model
   2. JTable(int numRows,int numColumns)
     建立一个具有numRows 行,numColumns 列的空表格，使用的是 DefaultTableModel
   3. JTable(Object[][] rowData,Object[][] columnNames)
     建立一个显示二维数组数据的表格,且可以显示列的名称
   4. JTable(TableModel dm)
     建立一个Jtable，有默认的字段模式以及选择模式,并设置数据模式
   5. JTable(TableModel dm, TableColumnModel cm)
     建立一个Jtable，设置数据模式与字段模式,并有默认的选择模式
   6. JTable(TableModel dm,TableColumnModel cm,ListSelectionModel sm)
     建立一个Jtable，设置数据模式、字段模式与选择模式
   7. JTable(Vector rowData, Vector columnNames)
     建立一个以Vector为输入来源的数据表格,可显示行的名称
   
三、TableModel
  TableModel是用来存储列表数据的，数据包括表头的标题数据与表体的实体数据。TableModel为功能接口，通常使用其具体的实现类DefaultTableModel，其构造方法如下。
   public DefaultTableModei(Object[][] tbody, Object[] thead)
在上述代码中，tbody表示表体，为一个二维数组;thead表示表头，为一个一维数组。其具体描述如下。
   ·表体:是一个Object类型的二维数组，由于多态的自动类型提升，可以直接使用String[][]来存储数据。
。表头:是一个Object类型的一维数组，同样，可以直接使用String[]来存储所有的标题字符串。
   
*/
package cn.kong.GUL;

import javax.swing.*;

public class Example20 {
    public static void main(String[] args) {
        new Example20().init();
    }
    //创建JFrame窗口
    JFrame jf = new JFrame("简单表格");
    //声明JTable类型的变量table
    JTable table;
    //1.定义一位数组作为列标题
    Object[] columnTitle = {"姓名","年龄","性别"};
    //2.定义二维数组作为表格行对象数据
    Object[][] tableDate = {
            new Object[]{"李清照",29,"女"},
            new Object[]{"苏格拉里",56,"男"},
            new Object[]{"李白",35,"男"},
            new Object[]{"李菁",18,"女"},
            new Object[]{"张三",2,"男"}
    };
    //3.使用JTable对象创建表格
    public void init(){
        //以二维数组和一维数组来创建一个JTable对象
        table = new JTable(tableDate,columnTitle);
        //将JTable对象放在JScrollPane中，并将JScrollPane放在窗口中显示出来
        jf.add(new JScrollPane(table));
        //设置自适应窗体大小
        jf.pack();
        //设置单击关闭按钮是默认为退出
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        jf.setVisible(true);
    }
}

```





## 12、反射机制

```java
/*
2、反射机制
   2.1、反射机制有什么用?
       通过java语言中的反射机制可以操作字节码文件。优点类似于黑客。(可以读和修改字节码文件。)通过反射机制可以操作代码片段。(class文件。）
   2.2、反时机制的相关类在哪个包下?
        java.lang.reflect.*;
   2.3、反射机制相关的重要的类有哪些?
       java.lang.class:代表整个字节码，代表一个类型，代表整个类。
       java.lang.reflect.Method:代表字节码中的方法字节码。代表类中的方法。
       java.lang.reflect.Constructor:代表字节码中的构造方法字节码。代表类中的构造方法
       java.lang.reflect.Field:代表字节码中的属性字节码。代表类中的成员变量（静态变量)
*/
```

```c
package example05;

class Yuangong{
	String name;
	int id;
	int salary;
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public int getSalary() {
		return salary;
	}
	public void setSalary(int salary) {
		this.salary = salary;
	}
	public void print(){
		System.out.println("员工姓名："+name+"，员工工号："+id+"，员工薪水："+salary);
	}
}
class Jingli extends Yuangong{
	int getpay;
	public int getGetpay() {
		return getpay;
	}
	public void setGetpay(int getpay) {
		this.getpay = getpay;
	}
	public void print(){
		System.out.println("经理姓名："+name+"，经理工号："+id+"，经理薪水："+salary+"，经理奖金："+getpay);
	}
}
public class MjTest2{
	public static void main(String arg[]){
		Yuangong A = new Yuangong();
		Jingli B = new Jingli();
		A.setName("张三");
		A.setId(20212001);
		A.setSalary(2000);
		A.print();
		B.setName("李四");
		B.setId(20211001);
		B.setSalary(5000);
		B.setGetpay(1000);
		B.print();
	}
}

```

