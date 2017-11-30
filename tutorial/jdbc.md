# JDBC配置指南

!> 本功能为实验性功能, 请在技术人员指导下使用.

## 环境要求

* Linux
* Java版本 >= 1.8
* 内存 >= 4GB
* CPU >= 4核
* 客户端版本 >= 2.1.0.1

## 配置指南

### 下载安装驱动

1. 在**客户端根目录**下新建目录

    ```bash
    mkdir -p resource/executor/pdbc/jar/driver
    ```

2. 下载驱动

    ```bash
    wget http://noah.bj.bcebos.com/doc/resource/executor/pdbc/pdbc-1.1.0.jar -O resource/executor/pdbc/jar/driver/pdbc-1.1.0.jar
    ```

3. 下载依赖

    ```bash
    wget http://noah.bj.bcebos.com/doc/resource/executor/pdbc/pdbc-1.1.x_dependency.zip
    ```

4. 解压依赖到目录

    ```bash
    unzip pdbc-1.1.x_dependency.zip -d resource/executor/pdbc/jar/driver
    ```

5. 将需要同步的数据库的驱动放入`resource/executor/pdbc/jar/driver/jdbc/`目录

    例如oracle:

    ```bash
    mkdir resource/executor/pdbc/jar/driver/jdbc/
    cp $ORACLE_HOME/ojdbc6.jar resource/executor/pdbc/jar/driver/jdbc
    ```

5. 验证安装路径

    ```bash
    tree resource
    ```

    输出结果:

    ```
    resource
    ├── executor
    │   └── pdbc
    │       └── jar
    │           └── driver
    │               ├── dependency
    │               │   ├── accessors-smart-1.1.jar
    │               │   ├── android-json-0.0.20131108.vaadin1.jar
    ...
    ...
    │               │   └── validation-api-1.1.0.Final.jar
    │               ├── jdbc
    │               │   └── ojdbc6.jar
    │               └── pdbc-1.1.0.jar

    ```

### 切换同步方式

切换到客户端根目录, 执行一下命令:

```bash
./bdpcmd setting set global_executor pdbc
```

切换回普通模式:
```bash
./bdpcmd setting unset global_executor
```

!> 切换后所有的表同步都会使用jdbc进行, 所以必须提供所有需要同步的数据库的jdbc驱动
