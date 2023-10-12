## SpringBoot 项目的一点总结

### 1.Service层：

处理Controller层的业务， 对数据进行校验、计算、转换等操作 

连接的是Controller层和Mapper层

![1686555009038](C:\Users\明丶月\AppData\Roaming\Typora\typora-user-images\1686555009038.png)

### 2.Mapper层：

连接的是Service层和数据库层



![1686555199957](C:\Users\明丶月\AppData\Roaming\Typora\typora-user-images\1686555199957.png)

### 3.ps：

mybatis提供了很多方法可以调用用来处理数据库数据，也可以自己定义；

先在Controller层定义，然后找到Service接口定义抽象方法，再在ServiceImpl书写方法体；

在ServiceImpl注入Mapper,使用Mapper的自定义方法，而Mapper的自定义方法的实现可以在

resources定义Mapper目录，配置各个Mapper的xml配置文件，实现mybatis的自定义方法。

### 4.POST和GET的区别和选择

get和post方法功能类似的，使用建议：
1、get方式的安全性较Post方式要差些，包含机密信息的话，建议用Post数据提交方式；
2、在做数据查询时，建议用Get方式；而在做数据添加、修改或删除时，建议用Post方式；
区别表现如下：

get是从服务器上获取数据，post是向服务器传送数据。
get是把参数数据队列加到提交表单的ACTION属性所指的URL中，值和表单内各个字段一一对应，在URL中可以看到。post是通过HTTP post机制，将表单内各个字段与其内容放置在HTML HEADER内一起传送到ACTION属性所指的URL地址。用户看不到这个过程。
对于get方式，服务器端用Request.QueryString获取变量的值，对于post方式，服务器端用Request.Form获取提交的数据。
get传送的数据量较小，不能大于2KB。post传送的数据量较大，一般被默认为不受限制。但理论上，IIS4中最大量为80KB，IIS5中为100KB。
get安全性非常低，post安全性较高。但是执行效率却比Post方法好。
若符合下列任一情况，则用POST方法：

* 请求的结果有持续性的副作用，例如，数据库内添加新的数据行。
* 若使用GET方法，则表单上收集的数据可能让URL过长。
* 要传送的数据不是采用7位的ASCII编码。

若符合下列任一情况，则用GET方法：

* 请求是为了查找资源，HTML表单数据仅用来帮助搜索。
* 请求结果无持续性的副作用。
* 收集的数据及HTML表单内的输入字段名称的总长不超过1024个字符。

### 5.关于PostMapping和PutMapping

给dto类中的实体类传参只能用PutMapping，用PostMapping话传不进去，但可以传进HashMap中。