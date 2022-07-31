# 基本开发环境配置（终端与brew）

这篇文章原本应该是进阶的内容，但是mac的入门文章鸽了这么多天，仍然是千头万绪至今没有写完。

实在不好意思再鸽下去，就先写了这篇，分享下从零搭建mac的开发环境的经验。

我使用自己重置系统后的电脑进行了测试，尽量保证还原从头配置的各种细节。如果有没有考虑到的部分，欢迎大家发邮件给我。（过几天搭好评论区或许就可以在评论区留言了

主要框架大概是：

1. 命令行的优化（iTerm2安装和配置）,包管理器brew的安装的配置
2. vscode写c++的配置
3. python部分
   1. pip的换源
   2. conda的安装和使用

重要提醒：已尽量避免墙对配置环境的影响，但是为了省心，仍然建议使用代理工具，并在无法访问时，对终端进行代理。可以参考brew部分，有教程（订阅自备）

### 命令行优化

自带的命令行比较朴素，也缺少很多重要的功能。我们先安装iTerm2，并进行配置。

先上一张图：看下我简单配置完的效果。我的主要目的是简单好用，如果想要炫酷效果可以自行研究哈哈

![我的iTerm2配置图](https://macguide.leavelet.io/assets/myiterm.png)

步骤:

#### 0. 安装command line tools

在自带终端中输入 `xcode-select --install`即可安装。

#### 1. iTerm2

iTerm2是终端模拟器，提供了许多个性化选项和附加功能。这里只介绍安装方法，具体的功能大家可以自己去体验。

1. 到[iterm2下载页](https://iterm2.com/downloads.html)下载Stable Release的最新版本，解压后拖放到应用程序文件夹。
2. 设置颜色和字体
   1.  颜色

       在`iTerm2` -> `Perferences` -> `Profiles` ->`Colors` -> `Color Presets`中可以看到默认的色彩配置方案。获得推荐较多的方案是Solarized系列。但是我个人喜欢使用原有的黑色界面，比较简约。
   2.  字体

       到[这个github仓库](https://github.com/romkatv/dotfiles-public/tree/master/.local/share/fonts/NerdFonts)下载并安装字体，后续powerlevel10k会用到。当然使用其他字体也可以，只要满足powerlevel10k的需要都可以。

       然后在`iTerm2` -> `Perferences` -> `Profiles` -> `Text` -> `Font` -> `MesloLGS NF`可以设置字体
   3. 背景图：在设置中可以自己找到

#### 2. 安装Oh My Zsh

简称omz，官方地址是 [github/ohmyzsh](https://github.com/ohmyzsh/ohmyzsh)

omz是设置zsh环境的工具，可以安装和管理各种zsh插件。安装omz的命令是，复制到iTerm2中就可以安装了。如果因为网络环境问题无法安装，请先安装brew

```
 sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

#### 3. brew

**安装**

配置环境先放一边，为了简化下面的步骤，我们先安装brew

1. 如果网络环境良好，可以用以下命令直接安装：

```
 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

1. 如果网络环境不好:
   1. 先可以参考[清华镜像站，Homebrew安装说明](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/) 安装
   2. 然后参考[清华镜像站的这个页面](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew-bottles/) 更换包镜像

上面的教程十分详细，我就不再赘述了，有问题的话可以在评论区留言(正在建)

**使用**

1.  安装一个包:`brew install`例：

    ```
     brew install python3
    ```
2.  卸载一个包：`brew uninstall`,例：

    ```
     brew uninstall ffmpeg
    ```
3. 查看包的说明信息:`brew info`
4. 查找包：`brew search`

`此时，可以解决网络不好的问题：`

```
brew install clash
wget -O config.yaml 你的订阅地址
clash -d .
```

#### 4.继续zsh的配置

1.  安装powerlevel10k(建议代理)

    我们使用brew安装，先引入powerlevel10k的源，然后安装。

    ```
     brew tap romkatv/powerlevel10k brew install romkatv/powerlevel10k/powerlevel10k
    ```

    然后按照安装说明，在终端中执行命令。在我的环境下，命令是这样的:

    ```
     source /opt/homebrew/opt/powerlevel10k/powerlevel10k.zsh-theme
    ```

    此时，再次打开iTerm2就会出现powerlevel10k的配置界面，可以自行选择
2.  按照终端高亮插件，还是使用brew

    ```
     brew install zsh-syntax-highlighting
    ```

    然后安装完的说明执行，在我的环境下说明是这样的

    ```
     To activate the syntax highlighting, add the following at the end of your .zshrc:  

     source /opt/homebrew/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh ​ 

     If you receive "highlighters directory not found" error message, you may need to add the following to your .zshenv:  
      
     export ZSH_HIGHLIGHT_HIGHLIGHTERS_DIR=/opt/homebrew/share/zsh-syntax-highlighting/highlighters
    ```
3.  安装自动填充插件zsh-autosuggestions，安装后可以按tab补全命令

    也是用brew（这下只要告诉名字，你应该就会安装了吧）

    不过提一句，使用这个插件会导致粘贴变慢，解决方法来自[https://github.com/zsh-users/zsh-autosuggestions/issues/238](https://github.com/zsh-users/zsh-autosuggestions/issues/238)，可以在.zshrc中添加如下设置

    ```
    # This speeds up pasting w/ autosuggest
    pasteinit() {
    OLD_SELF_INSERT=${${(s.:.)widgets[self-insert]}[2,3]}
    zle -N self-insert url-quote-magic # I wonder if you'd need `.url-quote-magic`?
    }

    pastefinish() {
    zle -N self-insert $OLD_SELF_INSERT
    }
    zstyle :bracketed-paste-magic paste-init pasteinit
    zstyle :bracketed-paste-magic paste-finish pastefinish
    ```

这就是本文的全部内容啦，python和c++准备都放在下一期，欢迎大家催更
