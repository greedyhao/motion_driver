# MotionDriver

## 1、介绍

这是一个移植 InvenSense 公司的 MotionDriver 到 RT-Thread 上的， MPU-6000, 6050, 6500, 9150, and 9250系列的使用DMP的程序

当前的example基于f7与mpu6050

测试效果

![](/docs/figures/motion_driver_test.gif)

版本：Embedded MotionDriver 6.12

### 1.1 目录结构

| 名称 | 说明 |
| ---- | ---- |
| core | MotionDriver 核心代码 |
| docs  | 文档目录 |
| documentation | MotionDriver的应用笔记 |
| eMPL-pythonclient | python客户端 |
| examples | 例子目录，并有相应的一些说明 |
| mpl libraries | mpl库的预编译库，使用MotionDriver的高级特性时需要手动添加相应架构的库文件到工程中|
| port | 移植代码目录 |

### 1.2 许可证

MotionDriver package 遵循 LGPLv2.1 许可，详见 `LICENSE` 文件。

### 1.3 依赖

- RT-Thread 3.0+

## 2、如何打开 MotionDriver

使用 MotionDriver package 需要在 RT-Thread 的包管理器中选择它，具体路径如下：

```
RT-Thread online packages
    peripheral libraries and drivers  --->
        mpu6xxx: Universal 6-axis sensor driver library  --->
```

然后让 RT-Thread 的包管理器自动更新，或者使用 `pkgs --update` 命令更新包到 BSP 中。

## 3、使用 MotionDriver

> 说明：在这里介绍 package 的移植步骤、使用方法、初始化流程、准备工作、API 等等，如果移植或 API 文档内容较多，可以将其独立至 `docs` 目录下。

在打开 MotionDriver package 后，当进行 bsp 编译时，它会被加入到 bsp 工程中进行编译。

* 完整的 API 手册可以访问这个[链接](docs/api.md)
* 更多文档位于 [`/docs`](/docs) 下，使用前 **务必查看**
* MotionDriver的应用手册在[`/documentation`](/documentation)下，快速翻阅可以方便使用

## 4、注意事项

### fifo溢出问题

线程轮转时间要与mpu的采样率对应，出现fifo溢出的时候，减少线程的轮转时间或者增加fifo的大小

fifo的大小定义在[inv_mpu.c](motion_driver\core\driver\eMPL\inv_mpu.c)中的508行处

```
const struct hw_s hw = {
    .addr           = 0x68,
    .max_fifo       = 2048,
    ...
#endif
};
```

### mpl高级特性库问题

目前mpl库需要手动添加到工程，使用SConscript添加不进工程，暂时不知道怎么解决

## 5、联系方式 & 感谢

* 维护：greedyhao
* 主页：https://github.com/greedyhao/MotionDriver2RTT
