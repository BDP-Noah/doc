# 数据同步客户端帮助中心

本文档包含以下内容

* 客户端的下载, 安装, 配置
* 数据库驱动下载, 安装, 配置
* 常见同步场景解决方案
* 常见问题排查方案


## 最新版本: 2.1.0

1. 新数据库支持:
    * MongoDB
    * SAP Hana
    * Sybase ASE
    * Redshift
    * Greenplum
1. 全新的数据源管理界面
1. 支持临时全量同步, 单次触发部分表同步
1. 支持日期字段`最近几天`增量方式
1. 开放API
1. 稳定性优化
1. 历史BUG修复

## 快速开始

### Windows

访问[下载页面](https://www.bdp.cn/index.html#/database_noah/)下载最新版并安装

安装成功后点击图标启动


### Linux

使用下载命令下载

```bash
wget https://update.bdp.cn/BDP_Noah_setup.bin
```

安装

```bash
bash BDP_Noah_setup.bin
```

### 开始使用

使用Chrome(其他浏览器可能有部分功能不兼容)打开安装机器的ip:端口

> 如安装在本机, 端口号配置为9999的话, 浏览器输入 http://127.0.0.1:9999 回车, 即可打开页面
