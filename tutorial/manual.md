# 手动触发同步

通过点击数据源界面上的同步按钮, 可以手动触发同步

![](http://noah.bj.bcebos.com/doc/img/884a48a6f58b9c3a36b496254e10d44c.png)


## 同步部分表

触发的时候可以选择这次任务需要同步的表:

![](http://noah.bj.bcebos.com/doc/img/da1983a0981fba0bdad36718e6cb3fa0.png)

## 临时全量同步

临时全量同步会忽略已选表的增量信息(包括`相对时间增量`和`最大值`增量)进行全量同步.

!> 其他配置信息, 包括筛选条件, 高级配置等正常生效.
