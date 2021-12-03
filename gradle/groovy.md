### 定义变量
* 指定类型

        int a = 1
        a.toString //groovy定义的基础数据类型实际上也是对象
* 弱类型
  
        def a = 1 //如果不指定类型，需要初始化

### 字符串
* 三种表示
    * `‘hello’`**单引号**使用跟java一样
    * `‘’‘hello “ \’‘’`**三引号**原始输出（不会转义)
    * `"hello${name}"`**双引号**支持运算，表达式等，实际是GString接口的实现类
* 常用api
    * `string1〉string2`比较asc码大小
    * `string[1..2]`取角标1-2的字串
    * `string1.minus(String2)`剔除string2的字串
    * `string.capitalize()`首字母大写

### 闭包
* 匿名内联函数，本质上闭包是将函数内部与函数外部连接的桥梁
* 闭包的定义与使用
  
        def closure = {
            String name,int age -> println("name:${name},age:${age}")
            return "selina“
        }
        closure(name,age)//用法1
        closure.call(name,age)//用法2
        def result = closure(name,age)//接收闭包的返回值
* String的常用闭包
    * `each`逐个遍历
    * `find`查找第一个
    * `findAll`查找所有
    * `any`满足一个
    * `every`每个都满足
    * `collect`逐个操作、转换，返回变换后的集合
* 闭包的三个重要变量
    * this 定义闭包处的类
    * owner 定义闭包处的类或对象
    * delegate 代表任意对象，默认owner指向的对象
  
        如果只有一个闭包，那么三者一样的，如果存在嵌套，则this指当前的，owner指最外层的
    * 闭包的委托策略

        将另一对象（A）赋值给闭包的`deletage`，将闭包的`resolveStrategy`设置为`Closure.DELEGATE_FIRST`,
        则闭包内使用的对象就为之前赋值的变量（A）
  
        ```
        def closure = {

        }
        closure.deletage = //
        closure.resolveStrategy = Closure.DELEGATE_FIRST
        ```

        
### 集合操作
* List常见用法
    * 添加
        * `list.add`
        * `list << e`
        * `list + e`
        * `list.add(index,e)`
    * 删除
        * `list.remove`
        * `list.removeElement`
        * removeAll
        ```
        //举个例子，删除所有基数
        list.removeAll{
            return it%2!=0
        }
        ```
    * 查找
        * `list.find`
        * `list.findAll`
        * `list.any`
        * `list.every`
        * `list.max`
        * `list.min`
        * `list.count`
    * 排序
        * sort
        ```
        //举个例子，按照绝对值排序
        list.sort{ a,b->
            return a == b ? 0 : abs(a)>abs(b) ? 1: -1
        }
        ```    