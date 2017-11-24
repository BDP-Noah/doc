# DB2驱动安装及数据库连接

!> 支持版本: 9.5+

!> 驱动安装完成需要重启数据同步客户端使之生效

## Windows

### 下载

点击[下载地址]()下载

### 安装

直接运行exe安装即可

## Linux

```bash
# 下载
wget

# 解压
unzip db2.zip -d db2

# 临时导入环境变量
echo "source db2/dbprofile" >> ~/.bashrc
source ~/.bashrc

```
