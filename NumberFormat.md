nested exception is **java.lang.NumberFormatException**: For input string: "8a0c4a27811e8b2801811e8bc5210000"

![image-20220609090708911](/Users/jason/Library/Application Support/typora-user-images/image-20220609090708911.png)



**原因**： Long  - > String 解析出错，首先排查类型

![image-20220609105520906](/Users/jason/Library/Application Support/typora-user-images/image-20220609105520906.png)



解决办法：

![image-20220609105506157](/Users/jason/Library/Application Support/typora-user-images/image-20220609105506157.png)