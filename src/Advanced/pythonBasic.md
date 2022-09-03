# Python开发环境的搭建

在阅读本文以前，我们认为你已经完成了[brew和iTerm2的设置](https://macguide.leavelet.io/Advanced/developmentEnvFromScratch.html)，并对[如何让一门语言跑起来](https://macguide.leavelet.io/Advanced/commonLanguage.html)有所了解。

另：本文写作仓促，欢迎修改！

## 思路

先安装`Python`和`miniforge`，然后使用`vscode`和`Pycharm`编写`Python`代码

## `Python`和`miniforge`的安装

### `Python`

通常来说，我们学习的`Python`版本为`Python3`。我们使用`brew`安装，命令如下。这样你的电脑上就有一个`Python`环境，在终端输入`python3`就可以正常运行代码了。

```shell
brew install python3
```

### `miniforge`

`Conda`是用来管理电脑环境的管理器，在`Windows`上广泛运行的是`Anaconda`。因为`Anaconda`对m系列芯片的Mac支持并不完善，我们使用`miniforge`这一`Conda`的精简版。你可以在miniforge的[Github地址](https://github.com/conda-forge/miniforge)查看更具体的Readme。

#### 安装步骤

参考资料：[Apple提供的tensorflow安装方法]（https://developer.apple.com/metal/tensorflow-plugin/）

1. 下载安装脚本

地址如下，打不开请使用代理服务器。下文用*shellFile*指代下载到的文件，请自行替换。

Intel芯片地址：`https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-x86_64.sh`

Apple芯片地址：`https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-MacOSX-arm64.sh`


2. 执行安装命令

```shell
chmod +x shellFile
sh shellFile
```

3. 验证安装成功

```shell
conda info
```

## `Conda`简介

参考资料：[Getting started with Conda](https://docs.conda.io/projects/conda/en/latest/user-guide/getting-started.html)

### 基本概念

使用`Python`的过程中，最常见的一个问题就是他人写好的内容因为版本不同无法执行或者报错。这是`Python`的特点导致的，这里不过多赘述。为了解决这个问题，`Conda`应运而生。

`Conda`的概念就是：通过虚拟环境的方式运行相关的内容，使多个版本的Python及依赖可以同时存在，避免了安装卸载的麻烦。

### 使用概述

记得修改`ENVNAME`。

1. 创建环境

```shell
conda create --name ENVNAME
```

2. 激活环境
 
```shell
conda activate ENVNAME
```

3. 关闭这个环境回到系统级的python

```shell
conda deactivate ENVNAME
```

4. 从`environment.yml`等文件中中安装环境

```shell
conda env create -f environment.yml
```

## `vscode`插件

关于`vscode`的介绍、安装和文件组织体系，见[vscode的安装](https://macguide.leavelet.io/Advanced/cppcoding.html#vscode的安装)

`vscode`有`Python`系列插件，安装之后即可使用，个人认为易用度还是挺高的。

常用的插件有

```
python
Pylance
Python Environment Manager
Jupyter（插件包）
```

## `Pycharm`安装和使用

到[jetbrains官网](https://www.jetbrains.com/pycharm/)下载Pycharm。在校学生具有免费使用专业版的资格，可以到`https://www.jetbrains.com/community/education/#students`申请。新建项目之前，在设置里面找到`Python Interpreter`，选择`conda`即可。新建或者使用现有的都可以。推荐日常学习的时候维护只要一个虚拟环境就可以了，不需要每次都重新安装依赖。

## 机器学习包安装指南

1. tensorflow

[Apple提供的tensorflow安装方法](https://developer.apple.com/metal/tensorflow-plugin/)很详细，笔者就不赘述了。

2. pytorch

在MacOS 12.3以上的版本，可以使用GPU加速运算。选择`nightly`版本的pytorch即可使用。在[pytorch的主页](https://pytorch.org)有写到这一点。