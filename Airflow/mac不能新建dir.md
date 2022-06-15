解决：

- 打开终端

  - 输入：`sudo vim /etc/auto_master`

- 修改（注释

  ```
  /home
  ```

  这一行）：

  - 修改前：`/home auto_home -nobrowse,hidefromfinder`
  - 修改后：`#/home auto_home -nobrowse,hidefromfinder`

- 回到根目录（这一步很重要）：

  - `cd /`

- 执行：

  - `sudo automount`

- 可以操作home文件了：

  - `mkdir /home/lim`