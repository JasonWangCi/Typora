Compliant 

NonCompliant



1.log.error(“异常信息：”+e.getMessage);

2.log.error(“异常信息：”+e);

3.log.error(“异常信息：”,e);



Warn

Error

Info

Debug

Trace



Log

private static final Logger *logger* = LoggerFactory.*getLogger*(CiSelfTokenInterceptor.class);



Static: 不管new了多少个实例，也只创建一次，节省空间

Final: 表示不可更改，常量。 本logger不能再指向其他logger对象；



Try catch finally

如果在异常处理的代码中执行了，system.exit(1)（退出JVM）语句来推出虚拟机，则finally块将失去执行的机会；



可以使用e.printStackTrace() 打印异常的堆栈信息，但是后面不要在使用log.error("测试：" ,e);  //这样异常堆栈信息会打印重复

可以使用log.error("查询账户资产时：" +e.getMessage()); 这种只会打印异常的字符串