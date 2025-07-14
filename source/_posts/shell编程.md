---
title: shell编程
date: 2022-05-25 16:34:12
tags:
- 操作系统
- Linux
categories:
- 学习
- 操作系统
---

#### if [ $# -eq 0 ]该语句是什么含义?

#### 1.commands含义

```shell
$0: shell或shell脚本的名字
$*: 以一对双引号给出参数列表
$@: 将各个参数分别加双引号返回
$#: 参数的个数
$_: 代表上一个命令的最后一个参数
$$: 代表所在命令的PID
$!: 代表最后执行的后台命令的PID
$?: 代表上一个命令执行后的退出状态
```

#### 2.options含义

```shell
-eq //equals等于
-ne //no equals不等于
-gt //greater than 大于
-lt //less than小于
-ge //greater equals大于等于
-le //less equals小于等于
```

