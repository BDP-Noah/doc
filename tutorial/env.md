# 如何设置环境变量

## Windows

### 打开环境变量设置页面

1. 右键`我的电脑`或`计算机`, 打开`属性`

    ![](img/d7e3bb7ec12422c64a96242b67f37470.png)

2. 单击`高级系统设置`

    ![](img/8495aea25687d0a10235460521330c31.png)

3. 打开`环境变量`, 推荐设置用户变量

    ![](img/43b4ae638b66df6b90f3ce5926fdf4a7.png)

### 新建环境变量

!> 若设置的环境变量已经存在, 新建变量会清空已有的值, 例如`PATH`, 所以应直接修改

单击`新建`, 这里假设要新建环境变量`ORACLE_HOME` = `D:\instantclient`, 则如下图所示设置

![](img/5ddabfa0b5e68cb3a2d8608a908e1f61.png)

### 修改环境变量

1. 选中需要修改的变量, 单击`编辑`

!> "Windows下环境变量多个值之间用英文分号(`;`)隔开"

![](img/982649429b9bc31aeab68d43c78a666f.png)


## Linux
Linux下通过命令`export`来设置环境变量

1. 打开终端, 这里假设需要设置环境变量`ORACLE_HOME` = `/etc/oracle/instantclient`, 则运行以下命令即可

```bash
export ORACLE_HOME=/etc/oracle/instantclient
```

!> 直接执行`export`设置的环境变量是临时的
        
当您关闭终端后, 该变量就失效了, 若要使环境变量在当前登录用户下永久生效, 使用以下命令:
```bash
echo "export ORACLE_HOME=/etc/oracle/instantclient" >> ~/.bashrc
source ~/.bashrc
```

!> `export`会覆盖已有变量, 若该变量已存在, 则应该修改而不是直接覆盖

修改方式即是使用冒号`:`来连接多个变量值, 例如:
```bash
export PATH=$PATH:/etc/oracle/instanceclient
```
