[Pixiv: 831501570]: # 'https://pan.dctblog.xyz/Aucl/Pictures/Pixiv/其它/831501570.jpg'

### VS Code 食用方法

> 该编辑器也集成了所有一款现代编辑器所应该具备的特性，包括语法高亮（syntax high lighting），可定制的热键绑定（customizable keyboard bindings），括号匹配（bracket matching）以及代码片段收集（snippets）。Somasegar 也告诉笔者这款编辑器也拥有对 Git 的开箱即用的支持。Microsoft Docs（微软文档）提供了相应的学习教程帮助用户在 Visual Studio Code 中登陆 GitHub `--百度百科`

**博主折腾了一晚上终于搞明白了，ohhhhhh，记录下来以防忘记**

### 下载

![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-1.png)
VS Code 官网:[Visual Studio Code](https://code.visualstudio.com/)

### 安装

1. 建议安装到 D 盘或者其盘，反正就不要 C 盘。
   ![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-2.png)
2. 这里把所有都勾上，然后就开始安装。
   ![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-3.png)
   到此 VS Code 已经安装完。

### 配置 VS Code 编译运行 C/C++

**运行 VS Code**

打开的界面是英文的,右下角会有提示安装中文字体，选`安装并重启`
![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-4.png)

**配置 Mingw-w64**

1. 下载`Mingw-w64`，可以到[Mingw-w64 官网](http://www.mingw-w64.org)下载，但可能需要挂梯子，比较麻烦。所以这提供一个官方版本版本[点我下载](https://pan.dctblog.xyz/Aucl/工具/mingw64.7z)。下载好后把文件解压到`D盘`的`Program Files`文件夹里。
2. 用 win10 左下角的搜索`高级系统设置`，点开。
   ![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-6.png)
3. 点`环境变量`，双击`Path`那一栏
   ![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-7.png)
4. `新建`，把 mingw64 的 bin 文件夹所在目录放进去，我的 bin 文件夹路径如下
   ![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-8.png)
5. 然后一路`确定`就行，再看检查环境配置成功没有，按下`win+r`输入`cmd`，回车
   ![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-9.png)
6. 输入`g++ -v`，如果输出如下那就配置 mingw-w64 成功了
   ![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-10.png)

**配置编译运行 C/C++**

1. 按下 Ctrl+Shift+X 打开`扩展`，搜索 C，安装第一个
   ![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-5.png)
2. 在任意一个地方建个文件夹，我这是在 D 盘里建立`VS Code_C`，然后到 VS Code 里打开文件夹，或者在`文件`菜单里也有

   ![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-11.png)

3. 把这个勾上，然后点信任
   ![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-12.png)
4. 创建一个文件命名为`hello world.c`，可以随便命名，这里只是展示，**这里最好不要中文名，不然会出错，到文章末会有中文名编译运行的解决方法**。
   ![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-13.png)
5. 点左边的这个调试与运行，然后点`运行和调试`，VS Code 会弹出选择环境，都选第一个。
   ![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-14.png)
   ![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-15.png)
6. 没有意外的话就可以直接使用了，然后按`F5`运行（好像配置完了会自己编译运行，记不清了，没有运行就自己按）

   ![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-16.png)

### 自定义配置和解决中文乱码

配置完后当前目录下就会生成`launch.json`和`tasks.json`两个文件，第一个是运行编译生成的 exe，第二个是`编译源码`

![VS Code](https://pan.dctblog.xyz/Aucl/blog/vscode-17.png)

**tasks.json 的配置**

这是打开`tasks.json`的配置，推荐用 g++。为了防止中文路径，中文名编译运行时报错，要进行如下更改
![tasks.json](https://pan.dctblog.xyz/Aucl/blog/vscode-19.png)
- `label`标签那的数值改为`C/C++: g++.exe 生成活动文件`
- `command`那的`gcc.exe`改为`g++.exe`
- `args`里的最后一行全部改为`D:\\VS Code_C\\debug.exe`
- 在 args 里继续添加`"-Wall"`, 这是开启额外警告
- 如果要用 win 的 cmd 显示编译运行程序的结果，那就再把`"-fexec-charset=GBK"`加上去,因为 win 的 cmd 的编码是 gbk，而 VS Code 码的编码为 UTF-8，编码不同，会导致中文乱码，如果是用 VS Code 里内置的终端运行程序，那就不要加
- 如果想生成 64 位的程序，就加上`"-m64"`
- `"-D\_\_USE_MINGW_ANSI_STDIO"`, 用 MinGW 写 C 时留着，否则不需要，用于支持 printf 的%zd 和%Lf 等
- `"-static-libgcc"`, 静态链接 libgcc，一般都会加上

**其它的更改，需要的就自行百度**
最终更改如下，我要用内置的终端，所以没有加`"-fexec-charset=GBK"`
![最终更改](https://pan.dctblog.xyz/Aucl/blog/vscode-20.png)

**launch.json 的配置**

这是打开`launch.json`的配置，这个改的就比较少
![launch.json](https://pan.dctblog.xyz/Aucl/blog/vscode-18.png)
- `gcc.exe  - 生成和调试活动文件`改为`g++.exe - 生成和调试活动文件`
- `${fileDirname}\\${fileBasenameNoExtension}.exe`改为`D:\\VS Code_C\\debug.exe`
- `C/C++: gcc.exe 生成活动文件`改为`C/C++: g++.exe 生成活动文件`

**其它的更改，需要的就自行百度**
最终更改如下
![最终更改](https://pan.dctblog.xyz/Aucl/blog/vscode-21.png)