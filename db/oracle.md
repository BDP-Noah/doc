# Oracle驱动安装及数据库连接

> 支持版本: 10.0+

## Windows

### 下载驱动文件

[点击下载](http://noah.bj.bcebos.com/doc/resource/driver/windows/oracle/instantclient_11_2.zip)

### 配置环境变量

系统为了识别oracle驱动, 需要配置环境变量, 例如将驱动解压至`C:\oracle\instantclient_11_2`

![](http://noah.bj.bcebos.com/doc/img/abc3bab6a637b891f1f310a72ba4b524.png)

则需要将以下两个值添加到环境变量:

> [查看如何设置环境变量](/faq/how-to-set-env)

* `PATH` = `C:\oracle\instantclient_11_2`
* `TNS_ADMIN` = `C:\oracle\instantclient_11_2`


!> `PATH`是很重要的系统环境变量, 在配置的时候注意不要清空原有的值, 应该修改之前的变量, 使用`;`连接多个值.

## Linux

### 下载驱动文件

```bash
# 下载
wget http://noah.bj.bcebos.com/doc/resource/driver/linux/oracle/instantclient_11_2.zip

# 解压
unzip instantclient.zip -d /etc/oracle/instantclient
```

向环境变量中添加值:

* `PATH` = `/etc/oracle/instantclient`
* `TNS_ADMIN` = `/etc/oracle/instantclient`
* `LD_LIBRARY_PATH` = `/etc/oracle/instantclient`

## 注意事项

* 配置好环境变量后需要重启客户端才会生效.
