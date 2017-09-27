# Win10的ubuntu子系统，搭建前端自动化工具

## 一、Win10安装ubuntu子系统

[Win10安装ubuntu子系统步骤](http://www.cnblogs.com/Jay-CFD/p/6067274.html)

## 二、Ubuntu安装Nodejs {#ubuntu更新安装nodejs}

我们选择用NVM安装和管理nodejs。

nvm是一个开源的Node版本管理器，通过简单的bash脚本来管理、切换多个Node.js版本。和nvm提供类似功能的还有tj写的n，它们的功能大同小异，整体来说nvm要稍强大一下。值得注意的是nvm和n目前都不支持windows版本。

* 使用nvm安裝Node.js
* 使用nvm无痛切换Node.js版本

### 1.安装nvm

在安装Node.js之前，需要先安装nvm，然后通过nvm去安装多个版本的Node.js。 首先，在终端里执行如下命令：

通过curl下载install.sh脚本，并执行它。待执行完成后，它会把nvm命令的执行路径放到~/.bashrc文件里 检查nvm版本,

```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
......
nvm --version   //检查当前是否安装成功
```

### 2.安装Node.js

```bash
nvm install v8.4.0  //安装node8.4.0
......
node -v             //检查nodejs是否安装成功
```

```
nvm use 8.4.0 //切换版本
nvm alias default 8.4.0  //设置默认版本：default -> 8.4.0 (-> v8.4.0)
```

### 3.磁盘跳转

```
cd /mnt/d/www/front    //切换到对应项目文件夹
```



