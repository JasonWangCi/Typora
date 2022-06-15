### Serializable:

````java
public class Person extends Human implements Serializable {
  private Teacher teacher;
}
````

#### **1、什么是序列化和反序列化**

Serialization（序列化）是一种将对象以一连串的字节描述的过程；反序列化deserialization是一种将这些字节重建成一个对象的过程。

#### **2、什么情况下需要序列化** 

a）当你想把的内存中的对象保存到一个文件中或者数据库中时候；
b）当你想用套接字在网络上传送对象的时候；
c）当你想通过RMI传输对象的时候；

#### 3、序列化的原则：

1. 当一个父类 (Human) 实现序列化，子类 (Person) 自动实现序列化，不需要显式实现Serializable接口；
2. 被 **static** , **transient** 修饰后的变量不能被序列化，被**transient**修饰的变量在程序运行时不被序列化，自然不可以被反序列化读取；
3. 如果引用对象不可以序列化（即没有实现Serializable），则本类（Person）不可被序列化；

