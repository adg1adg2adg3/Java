## 继承：
    1、子类可以拥有父类可继承的内容（成员方法和成员变量）,但不可直接访问父类中的private内容。
    2、子类可以拥有自己特有的内容。
    3、子类构造器第一行默认隐含super();即先调用父类无参构造方法(也可以进行手动调用父类有参构造方法)。

    使用is-a规则判断是否可以使用继承：子类的每个对象也是父类的对象。

    在覆盖一个方法的时候，子类方法不能低于超类方法的可见性。

    成员变量：访问局部成员变量
    this.成员变量：访问本类成员变量
    super.父类成员变量：访问父类成员变量
    super.父类成员方法.访问父类方法

    继承中的方法调用：
        虚拟机预先为每个类创建了一个方法表, 其中列出了所有方法的签名(方法的名字和参数列表称为方法的签名)。
        1、编译器査看对象的声明类型和方法名，获得所有可能被调用的候选方法。
        2、编译器将査看调用方法时提供的参数类型，如果在方法中存在一个与提供的参数类型完全匹配，就选择这个方法(动态绑定)。
        3、如果是private方法、static方法、final方法或者构造器，那么编译器将可以准确地知道应该调用哪个方法(静态绑定)。然后调用的方法依赖于隐式参数的实际类型， 并且在运行时实现动态绑定。
        4、重名方法使用优先本类，没有则向上寻找父类。

## 多态
    一个对象变量可以指示多种实际类型的现象被称为多态，例如：一个父类变量既可以引用一个父类对象，也可以引用一个父类的任何一个子类的对象，但此时只可使用父类中的内容，要想使用字类特有内容可以使用强制转换转回子类(使用前可以使用instanceof操作符)。
    
    在运行时能够自动地选择调用哪个方法的现象称为动态绑定。
    可以声明一个接口，接口变量必须引用实现了接口的对象。
    is-a规则表明程序中出现超类对象的任何地方都可以用子类对象置换。

## 抽象类：
    抽象方法充当着占位的角色，它们的具体实现在子类中。
    抽象类可以有构造方法(供子类创建对象)和具体方法。

### equals方法：
    Java 语言规范要求equals方法具有下面的特性：
    1)自反性:对于任何非空引用x, x.equals(x)应该返回true。
    2)对称性:对于任何引用x和y,当且仅当y.equals(x)返回true,x.equals(y)也应该返回true。
    3)传递性:对于任何引用x、y和z,如果x.equals(y)返回true,y.equals(z)返回true,x.equals(z)也应该返回true。
    4)一致性:如果x和y引用的对象没有发生变化，反复调用x.equals(y)应该返回同样的结果。
    5)对于任意非空引用x,x.equals(null)应该返回false。
    可以使用getClass过instanceof方法比较两个对象是否属于同一个类。

## 可变参数(jdk1.5以上)：
    方法定义时，参数的数据类型已经确定，但是参数的个数不确定。
    相当于创建一个长度为[0,n)的数组，然后把变量放进去，此时方法里的变量名等于数组地址。
    格式：
    权限 返回值类型 方法名(数据类型...变量名){
    .......
    }
    注意：一个方法的参数列表只能有一个可变参数。如果有多个参数，可变参数放在末尾。

    特殊写法：
    权限 返回值类型 方法名(Object...变量名){
    .......
    }

## 枚举类（JDK1.5）：

    枚举类默认继承java.lang.Enum
    每一个枚举值都为该枚举类的一个对象。
    枚举的构造方法为私有方法。
    所以枚举对象以大写的形式定义，之间用逗号分隔且在该枚举类的第一行。
    枚举类可以有方法和成员变量。

    定义类：
    权限 enum 类名称{
    .......
    }

https://blog.csdn.net/mengtianqq/article/details/80971580
https://www.cnblogs.com/hemingwang0902/archive/2011/12/29/2306263.html#title-7
http://www.manongjc.com/article/46342.html

## 反射：

    运行时类型识别(RTTI)与Class文件与反射：
        Java中除了int这种基本类型外，其他类型的都是某种类(包括接口)，比如String等等。
        Java在运行时只会加载我们需要的类，当JVM要加载一个类时，它会首先读取**.class文件到内存，然后为这个类创建一个Class实例并关连起来(自己无法创建Class实例，这个实例即为运行时类型识别)，因为这个Class实例包含了此类的所有完整信息，我们就可以使用这个Class实例来获取这个类的相关信息(反射)。

    java.lang.reflect
    java.lang.Class<T>

    获取class对象的方式：
    1、class.forName("包名和类名")
    2、类名.class
    3、对象.getClass()

    同一个字节码文件（*.class）在程序运行中，只会被加载一次，即通过以上三种方式获取的对象都为同一个对象。

    可以用反射来获取成员变量、构造方法、成员方法和类名称。



## 异常：
    根类:java.lang.Throwable,根类的两个子类分别为java.lang.Error和java.lang.Exception，根类的父类为Object。

    Error：错误，不能纠正。
    Exception：异常，可以纠正。

    受查异常(Exception除去RuntimeException剩下的部分):是指程序员已经足够小心的检查了他的代码，但是还是不能保证代码不出现异常；如，程序要访问某个文件，但访问时文件不存在，这和程序本身没有太大关系；再如，程序要进行网络连接，但执行时没有连接网线，这些问题都是已检查异常。
    非受查异常(RuntimeException类和Error类):一般是由程序员没有细心检查代码，而导致的如空指针异常、数组越界、类型转换异常等都是由于程序员粗心大意造成的。这些异常是在编码过程中是能够避免的。

    异常在java中的解决机制：
        1、jvm检测出异常后会创建出一个相应的异常对象，这个对象包含了异常的内容、原因、位置。
        2、如果在出现异常的方法中没有异常的处理逻辑(try...catch)，那么将按照方法-main-JVM的顺序逐级抛出，试图让更高层次的调用者解决异常。
        3、当异常传递给JVM时，JVM的解决方式为把异常对象(内容、原因、位置)以红色字体打印输出，并终止当前程序(中断处理)。

    异常的处理：
        1、throw
            作用：使用throw关键字在指定的方法抛出指定的异常。
            格式：
            throw new Exception或Exception的子类对象("异常的原因")
            注意：
                1、必须写在方法的内部。
                2、throw创建的对象必须是Exception或Exception的子类对象("异常的原因")；
                3、必须处理throw抛出的对象。
                如果是非受查，我们可以默认交给JVM处理。
                如果是编译异常(写代码报错)，我们可以使用throws或使用try...catch来处理。
        2、throws
            作用：当方法内部抛出异常对象时，可以使用throws关键字处理对象。
            throws会逐级的让调用者处理异常，最终交给JVM。
            格式：
            权限 返回值类型 方法名称(参数列表) throws Exception或Exception的子类对象(可以有多个，用逗号分隔){
            ........		//通常搭配throw使用，让throw抛出异常throws处理。
            }
            注意：
                1、当方法内部抛出多个异常时，throws也必须声明对应的多个异常，如果多个异常有继承关系，则throws声明父类即可。
                2、当调用了一个抛出异常的方法之后，要么使用throws继续向上抛出直到JVM，要么使用try...catch自己处理。(throws主要作用就是向上抛出收到的异常。)
        3、try...catch
            作用：当方法内部抛出异常对象时，可以使用try...catch关键字处理对象。
            格式：
            try{
            可能会产生异常的代码
            }catch(异常类型 异常变量){
            处理异常
            }(catch结构可以有多个）
            注意：catch处理完异常之后会继续执行try...catch后面的代码。
            或者使用catch(异常类型|异常类型 异常变量)捕获多个不具有继承关系的异常对象，且异常变量在语句体中不能再次赋值。

            finally关键字放在catch后面
            try{
            可能会产生异常的代码
            }catch(异常变量){
            处理异常
            }finally{
            无论出否出现异常都会执行
            一般用于资源释放
            避免写return语句
            }

            多个异常的处理方式：
                1、一个异常对一捕获一次处理
                2、多个异常对一次捕获多次处理。注意：catch里面的异常如果有继承关系，子类要写在父类上面。
                3、多个异常对一次捕获一次处理。（写一个可以处理多种异常的父类）

            注意：
                1、一般运行时的异常不会进行捕获。
                2、父类定义抛出异常时，子类可以定义抛出异常或此异常类的子类。
                父类没有定义抛出异常时，子类只能捕获处理，不能抛出异常。


    Throwable类的3个异常处理方法：
        String getMessage()
        String toString()
        void printStackTrace()

    自定义异常类：
        格式：
            public class 某某Exception extends Exception或RuntimeException{
            空参构造方法
            调用父类带异常信息的构造方法
            }
        注意：
            如果继承Exception，就必须捕获处理或抛出。
            如果继承RuntimeException，无需处理。

    另：在父类转换到子类时会发生ClassCastException异常
    
    再次抛出异常与异常链(包装技术)：
        catch(SQLException e)
        {
            throw new ServletException("data error : " + e.getMessage());
        }
        可以看到这里改变了抛出的异常类型，或者使用更好的方法：
        try
        {}
        catch(SQLException e)
        {
            Throwable se = new ServletException("database error");
            se.initCause(e);
            throw se;
        }
        当捕获到这个异常时(可以使用一个if语句)， 就可以使用下面的语句重新得到原始异常：
        Throwable e = se.getCause();
        强烈建议使用， 这样可以让用户抛出子系统中的高级异常， 而不会丢失原始异常的小细节。
        如果在一个方法中发生了一个受查异常， 而不允许抛出它， 那么我们可以捕获这个受查异常，并将它包装成一个运行时异常。

        在JSK7以前异常变量的类型要小于方法抛出类型的范围。

        强烈建议解耦合try/catch和try/finally语句块。这样可以提高代码的清晰
度。例如：
    InputStream in = . . .;
    try
    {
        try
        {
            code that might throw exceptions
        }
        finally
        {
        in.doseO;
        }
    }
    catch (IOException e)
    {
    show error message
    }
    内层的try语句块只有一个职责，就是确保关闭输入流。外层的 try语句块也只有一个职责，就是确保报告出现的错误。这种设计方式不仅清楚，而且还具有一个功能，就是将会报告finally子句中出现的错误。

    然而，try/finally也会带来麻烦。当try和finally都会抛出异常时，外层只会捕获finally里面的异常。

    实现了AutoCloseable接口的类可以使用带资源的try，现以Resource类为例：
        try (Resource res = ...)
        {
            work with res
        }
    try块退出时会会自动调用res.close()，当指定多个资源时，try括号内语句可用分号 ; 分隔。res.close抛出的异常会被addSuppressed方法抑制和同时保存起来了，我们可以使用getSuppressed方法获得。

### 分析堆栈轨迹：
    堆栈轨迹(stack trace)是一个方法调用过程的列表， 它包含了程序执行过程中方法调用的特定位置。
    Throwable t = new Throwable();
    StringWriter out = new StringWriter();
    t.printStackTrace(new PrintWriter(out));
    String description = out.toString();
    一种更灵活的方式是使用getStackTrace方法，会得到一个StackTraceElement对象的一个数组。StackTraceElement类含有能够获取文件名和当前执行的代码行号的方法，还含有能够获取类名和方法名的方法。toString方法将产生一个格式化的字符串，其中包含所获得的信息。
    Throwable t = new Throwable();
    StackTraceElement[] frames = t.getStackTraceElement();
    for(StackTraceElement frame :frames)
        *code...*
    静态的Thread.getAllStackTraces方法，返回一个Map集合，它可以产生所有线程的堆栈轨迹。
    Map<Thread, StackTraceElement[]> map = Thread.getAllStackTraces();
    for(Thread t : map.keySet()){
    StackTraceElement[] frames = map.get(t);
        *code...*
    }

## 断言：
    断言机制允许在测试期间向代码中插入一些检査语句。当代码发布时，这些插人的检测语句将会被自动地移走。
    assert 条件;
    assert 条件:表达式;
    这两种形式都会对条件进行检测，如果结果为false, 抛出一个 AssertionError 异常。
    在第二种形式中，表达式将被传入AssertionError的构造器， 并转换成一个消息字符串。
    在默认情况下， 断言被禁用。可以在运行程序时用 -enableassertions 或 -ea 选项启用。

## 记录日志：
    基本日志：
        要生成简单的日志记录，可以使用全局日志记录器并调用其info方法： Logger.getGlobal().info("File->Open menu item selected");
        但是，如果在适当的地方(如main开始)调用
        Logger.getGlobal().setLevel(Level.OFF);
        将会取消所有的日志。

    