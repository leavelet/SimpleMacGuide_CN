# C++环境配置

在阅读本文以前，我们认为你已经完成了[brew和iTerm2的设置](https://macguide.leavelet.io/Advanced/developmentEnvFromScratch.html)，并对[如何让一门语言跑起来](https://macguide.leavelet.io/Advanced/commonLanguage.html)有所了解。

本文中我们使用`vscode`作为文本编辑器，使用macOS的`CommandLine Tools`中的`clang`作为编译器和自动补全后端，并介绍一些常用的`vscode插件`。 

此处特别感谢[谷雨同学](https://guyutongxue.github.io)开发的`VS Code Config Helper`，方便了我们的C++环境配置。特别值得一提的是，他的[c++教程](https://cpp-tutorial.vercel.app)也值得一读。

## `vscode`的安装

撰写本文时，软件安装章节还未完成。于是我们提一下如何安装`vscode`

1. 访问[vscode官网](https://code.visualstudio.com)，下载适用于macOS的最新版
2. 在下载文件夹中找到下载到的文件，在笔者电脑上为`VSCode-darwin-universal.zip`
3. 双击解压，拖动至`Applications`文件夹
4. Done！

## 理解`vscode`的“工作区和文件夹”逻辑

`vscode`分为全局和工作区两部分组成，结构如下图所示。每次打开`vscode`都会新建一个窗口，叫做“工作区”。工作区中包含一个或多个文件夹，可以拥有与全局不同的设置。

如果工作区只有一个文件夹，配置会被放在该文件夹下`.vscode`文件夹中。如果有多文件夹，工作区配置会用一个`code-workspace`结尾的文件保存。

![vscode结构示意图](http://macguide.leavelet.io/assets/vscode.png)

## 使用`VS Code Config Helper`进行`vscode`基础配置

1. 请点击[这里](https://v4.vscch.tk)下载`VS Code Config Helper`。
   
   虽然v4版仍在测试阶段，但比起前代有很大的升级，笔者测试后推荐这一版本。如果遇到问题，欢迎给我发邮件。

2. 打开dmg，将app拖动到“应用程序”文件夹，打开app。
   
   如果如遇到打不开的情况，请参考[百科-无法打开App的可能解决方法](https://macguide.leavelet.io/Bike/appnotopen.html)

3. 按软件提示，配置有关内容。、
   
   其中，选择一个文件夹作为工作区文件夹，所有配置都会写在该文件夹中。以后打开新窗口时“打开该文件夹“，就可以愉快地写C++啦。在`Hello World.cpp`中按`F6`运行吧！   

安装成功的效果如下图：

![安装成功图](https://macguide.leavelet.io/assets/vscodeInstallOK.png)

注：`VS Code Config Helper`对全局设置的影响为：安装了插件`C/C++`与`CodeLLDB`，增加了快捷键`F6`编译运行。

初次打开时，CodeLLDB会自动下载平台对应的package，如果下载失败，`vscode`会提示从对应链接下载一个拓展名为`vsix`的文件，然后在vs code插件页面选择从vsix安装（install from VSIX）即可。

## `vscode`插件安装，卸载与禁用方法

上图左侧边栏第五个图标，即是vscode插件管理器。可以在里面下载并安装插件使用，或管理插件状态。选中已安装的插件，可以点击`Inable`将插件状态改变为`Disable`，或者将其卸载。无需笔者多言，动手试一试吧！

## 常用`vscode`插件

### `clangd`: 语法高亮与自动补全

`VS Code Config Helper`中使用的自动补全工具是微软开发的`C/C++ IntelliSense`。这是一款很好的工具，刚学编程时使用十分合适。但是笔者试图使用`vscode`写Qt的时候，发现了一些小问题。`clangd`可以很方便得解决这一问题，并可替代`C/C++ IntelliSense`的全部功能。

由于我们安装`CommandLine Tools`时安装过`clang`。直接在左边栏打开“插件”，搜索并安装`clangd`即可。由于`clangd`与`C/C++`冲突，需要将`C/C++`禁用。

### `C/C++ Compile Run`: 一键编译运行C和C++代码

`VS Code Config Helper`使用了非常cool的方法实现在单独窗口运行程序。`C/C++ Compile Run`则是在vscode自带终端中运行程序。可以将编译运行的快捷键设为`command+R`，也可以实现一键编译运行。

### `编程网格`: P大计算概论看题助手

也是谷雨同学写的，可以在`vscode`里以分屏的形式同时看到题目和代码，还支持一键提交，省去了复制粘贴的麻烦。对P大信科同学强烈推荐。（并没有题解，别高兴太早哈哈哈）

### 任何以语言名称命名的插件和插件包

如果用`vscode`写其他语言，可以安装相应插件，如`Python`,`c#`, `Go`等。但是`Rust`语言的推荐插件为`rust-analyzer`。

### 各种主题

可按自己的审美选择。笔者正在使用的是`Chinolor Theme`插件中的`Chinolor Light`。