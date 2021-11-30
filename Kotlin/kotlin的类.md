## Kotlin的类
### 构造方法
    //使用constructor关键字
    constructor(name:String,age:Int)
    constructor(name:String):this(name,18)

    //主构造器 class Singer constructor(var name:String,age:Int){
    //如果主构造器变量加了var，则会生成对应的成员变量（构造属性）
        init{//init代码块如果用到需要初始化的成员变量，则放在下面
            this.name = name
            this.age = age
        }
    }
### get set方法
    kotlin的类申明变量自带get set函数(private修饰的除外)，如果想让java也能直接调用变量，使用@jvmField
    get(){
        return field 
    }
    set(value){
        field = value
    }
    //如果不想外部修改成员变量
    private set
### 各种类的申明
    //申明枚举 
    enum class
    //申明注解 
    annotation class
    //模块类访问修饰符，只能在module内访问
    internal class 
    //内部类 默认内部类是静态的，如果是嵌套内部类，则用inner class修饰，嵌套内部类不能有伴生对象
    //数据类 不可被继承，具有一些扩展功能 copy方法，解构
    data class   
    //解构 将一个对象拆解成多个变量并分别赋值 fun component1() = 成员变量
    //component  var(name,age) = Singer() 实际上编译的时候生成了主构造器的component方法，
    //如果不定义date class，想要用到解构，可以自己写
    fun component1():String{
            return name
    } 

    //继承某个类的时候需要使用调用该类的构造函数（如果自己定义了constructor，则不需要调用构造函数）,接口则不需要
    //kotlin的类默认是public final的，如果要使其可继承，使用open关键字
    open class MainActivity:Activity(),OnClickListener


    //动态代理 by关键字 
    //属性委托 将统一的操作委托给统一的对象，by后面跟一个对象
    //一个常用的用法 懒加载
    val star:Star by lazy{//这个变量只会被创建一次，在第一次访问该变量的时候创建
        Star()
    }
    interface Star{}
    class SuperStar(Star star):Star by star{
        
    }
    //密闭类 sealed关键字 可以有子类，但是必须和密闭类写在同一个文件里

### object,companion object关键字（伴生对象）
    //object实际上是定义了一个类，然后创建了这个类的单例对象INSTANCE
    object Marry{
        //@jvmStatic 添加这个注解可以直接调用，不用INSTANCE
        fun print(name:String){
            println("$name你是我的老婆");
        }
    }
    Test.print("selina");
    //java调用 实际上就是调用这个单例对象的方法和变量
    Marry.INSTANCE.print();

    companion object//伴生对象  一个类只有一个伴生对象，创建一个静态的内部类Companion
    class Marry{
        companion object{
            fun print(name:String){
                println("$name你是我的老婆")
            }
        }
    }
    //java调用
    Marry.companion.print("selina")

    //object还可以用来创建匿名内部类
    setOnClickListener(object:OnClickListener{
        override fun onClick(){
            
        }
    })

    //伴生对象 1.一定要在一个类的内部 2.companion object修饰 3.编译时会在类里生成一个静态对象Companion
    class StringUtils{
        companion object{
            fun isEmpty(str:String):Boolean{
                return ""==str
            }
        }
    }
    //伴生对象写单例
    class Single private constructor(){
        companion object{
            fun getInstance():Single{
                return Holder.instance
            }
        }
        object Holder{
            val instance = Single()
        }
    }
### 接口
* _kotlin 的接口可以定义抽象属性_