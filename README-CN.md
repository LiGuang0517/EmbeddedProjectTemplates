# 说明

[English](README.md) | [中文]()

本项目主要的包含一些驱动程序、外设的使用。

**软件环境：** Windows 11、CLion、STM32CubeMX、openocd

**硬件环境：** WeAct STM32H750VBT6、STM32F407ZGT6【最小系统板和正点原子开发板】。


# LVGLSimulator

在CLion中实现LVGL模拟器环境。对应的文章：[在CLion中搭建LVGL模拟器](https://blog.csdn.net/qq_44656481/article/details/125208978?spm=1001.2014.3001.5501)

# BootLoader_Application

具体请查看对应文件夹里的文档——[在CLion上实现STM32H750VBT6的Bootloader.md](BootLoader_Application/在CLion上实现STM32H750VBT6的Bootloader.md)

在CLion中完成了BootLoader的实现，花费了很多时间和精力。最后能够跑通的时候还是觉得很高兴的。

# ExFlashLVGL

实现将LVGL下载到外部Flash中。

# InternalFlash

写了段程序测量并验证了`STM32H750VBT6的内部`Flash，我的开发板是1,024KB，超过此容量就会进入到`HardFault_Handler`。

具体请查看对应文件夹里的文档——[测量验证STM32H750VBT6的内部Flash](InternalFlash/测量验证STM32H750VBT6的内部Flash.md)

# STM32_DSP_Library

移植Github上的最新DSP到STM32H750上,STM32CubeMX中的版本为1.3，Github上版本为1.14, 最新版本拥有窗函数，而1.3版本需要自己实现窗函数。

需要注意的是直接在`CMakeLists.txt`中的`file(GLOB_RECURSE SOURCES)`加入`"CMSIS-DSP/Source/*.*"`，编译会出现问题，原因是`CMSIS-DSP\Source`这个文件夹下的一些文件使用了`#include "xxxx.c"`，编译会导致多重定义。

比如`BasicMathFunctions`文件夹下的`BasicMathFunctions.c`和`BasicMathFunctionsF16.c`就包含了一些源文件。
解决办法是删除这些和文件名同名的文件。

有点笨拙，但是我做了很多尝试后发现，这个是最简单的。已经给Arm提了一个issue。

[在CLion中移植最新的DSP库](STM32_DSP_Library/在CLion中移植最新的DSP库.md)
