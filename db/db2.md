# DB2驱动安装及数据库连接

> 支持版本: 9.5+

!> 驱动安装完成需要重启数据同步客户端使之生效

## Windows

### 下载

[下载地址](http://noah.bj.bcebos.com/doc/resource/driver/windows/db2/ibm_data_server_runtime_client_win32_v11.1.exe)

### 安装

直接运行exe安装即可

## Linux

```bash
# 下载
wget http://noah.bj.bcebos.com/doc/resource/driver/linux/db2/ibm_data_server_driver_package_linuxx64_v11.1.zip

# 解压
unzip ibm_data_server_driver_package_linuxx64_v11.1.zip

# 安装

./dsdriver/installDsDriver

# 永久导入环境变量
echo "source dsdriver/db2profile" >> ~/.bashrc
source ~/.bashrc

```
