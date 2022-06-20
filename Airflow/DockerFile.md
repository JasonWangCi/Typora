保留字：

<img src="/Users/jason/Library/Application Support/typora-user-images/image-20220620080723660.png" alt="image-20220620080723660" style="zoom:30%;" />

FROM: 一般作为第一行，引用的是哪个镜像；

ENV:    设置变量

RUN:  	

​		在终端使用的shell命令

​		exec格式（json格式）

EXPOSE	 暴露的端口，-P，-p

WORKER： 登陆后的落脚点/path

<img src="/Users/jason/Library/Application Support/typora-user-images/image-20220620080356669.png" alt="image-20220620080356669" style="zoom:30%;" />





USER: 默认root 

VOLUME： 容器卷， -v 用于数据保存和持久化

ADD：COPY+解压文件

COPY：

CMD：

​	容器启动后执行（是在docker run 时运行）（RUN是在docker build时运行）

​	可有多个命令，只有最后一条命令有效，前面被覆盖



<img src="/Users/jason/Library/Application Support/typora-user-images/image-20220620080951213.png" alt="image-20220620080951213" style="zoom:40%;" />

<img src="/Users/jason/Library/Application Support/typora-user-images/image-20220620081445747.png" alt="image-20220620081445747" style="zoom:50%;" />



ENTRYPOINT:

<img src="/Users/jason/Library/Application Support/typora-user-images/image-20220620081721386.png" alt="image-20220620081721386" style="zoom:50%;" />

![image-20220620082027642](/Users/jason/Library/Application Support/typora-user-images/image-20220620082027642.png)