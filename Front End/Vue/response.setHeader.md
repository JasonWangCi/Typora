```
response.setContentType
```

**response.setHeader**各种用法详解

本文主要介绍了response.setHeader各种用法。具有很好的参考价值，下面跟着小编一起来看下吧

一秒刷新页面一次 response.setHeader("refresh","1"); 二秒跳到其他页面 response.setHeader("refresh","2;URL=otherPagename"); 没有缓存：

response.setHeader("Pragma", "No-cache"); response.setHeader("Cache-Control", "no-cache");

设置过期的时间期限 

response.setDateHeader("Expires", System.currentTimeMillis()+自己设置的时间期限);

 访问别的页面：response.setStatus（302）; 

response.setHeader("location","url"); 

通知浏览器数据采用的压缩格式：response.setHeader("Content-Encoding","压缩后的数据"); 

高速浏览器压缩数据的长度：response.setHeader("Content-Length",压缩后的数据.length+""); 

高速浏览器图片或视频：response.setHeader("Content-type","这个参数在tomcat里conf下的web.xml里面找");

inputstream in= this.getServletContext.getResourceAsStream("/2.jpg"); int len=0; byte buffer[]= new byte[1024] outputStream out = response.getOutputStream(); while(len=in.read(buffer)>0){ out.write(buffer,0,len)

}

高速浏览器已下载的形式：response.setHeader("Content-disposition","attachment;filename=2.jpg");

inputstream in= this.getServletContext.getResourceAsStream("/2.jpg"); int len=0; byte buffer[]= new byte[1024] outputStream out = response.getOutputStream(); while(len=in.read(buffer)>0){ out.write(buffer,0,len)

}

以上就是本文的全部内容，希望本文的内容对大家的学习或者工作能带来一定的帮助，同时也希望多多支持我们！