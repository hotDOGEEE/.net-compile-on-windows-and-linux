# 解决.net项目在windows和Linux上的编译问题

其实对于开发.net项目，常写C#的人来说，环境问题怎么搞应该是比较清楚的。

但其实现在写C#的都是开发游戏，用unity里面带的那套进行操作。

作为一个小白，要在一般的win或者centos环境中编译出一个可用的文件就得不断碰壁了。

这里记录一下现在这两者的流程。网上资料杂，自己总结一遍总是好的

# Windows

vs或者vscode都可以。

vscode的话需要先安装dotnet

https://www.cnblogs.com/springsnow/p/12881499.html

dotnet new project_name -o file_path

需要注意版本，会在输入该命令后提示。编译的文件是需要对应解释器的，所以多端使用情况下一定要统一。



vs安装 Mobile development with .NET模块。

具体采用哪个.NET版本，在创建项目的时候可以自行选择，这是比vscode使用dotnet创建要更为灵活的地方。

vs下项目的文件目录只能看到项目文件，并不能看到编译目录和项目配置文件。这点还得自行打开资源管理器进行查看。



编译通过后的bin目录，是需要整个进行拷贝的。为防止移动时遇到权限问题，提醒一下各位采用的通常做法是先压缩，移动到对应设备上后解压，可以避免掉一些权限问题。

# Centos

从编译的角度来看，只要解释器是通的，能在对应平台上运行，就可以实现跨平台运行同一套程序了。

windows上编译的产物是运行exe，linux下可就不是了。

先执行如下命令：

```
 sudo yum install libunwind libicu

 curl -sSL -o dotnet.tar.gz https://aka.ms/dotnet-sdk-2.0.0-linux-x64
```

（这里安装的2.0.0，实际使用下载对应版本的就好）

下载完成后进行解压

```
 mkdir dotnet
 cp dotnet.tar.gz dotnet
 cd dotnet && tar -xzvf dotnet.tar.gz
 vim /.bashrc 选择O，进入
 
 文件底部加入这两行
 export DOTNET_HOME=/root/con/dotnet
 export PATH=$DOTNET_HOME:$PATH
 退出保存，输入命令重新加载配置文件
 source ~//bashrc
 
 命令行输入dotnet --help验证成功没有

```



在centos这种没有图形界面的系统上开发.net不是常用的做法（其实在这上面运行都不算常用）。

所以一般还是在windows或者ubuntu上开发成功后将bin文件拉过来运行。

运行dll而不是exe。

```
dotnet objectfile.dll
```

如果后面要带参数直接跟就好，亲测可以直接运行成功。
