[pixiv: 88125344]: # 'https://cdn.jsdelivr.net/gh/tofu2333/Bolg-Cover/pixiv/88125344_p0_master1200.jpg'

记录自己在食用 `git` 时产生的一些 `问题` 和 `解决办法` ，防止下次碰到相同情况找不到解决办法。

---

# git clone
拷贝一个 Git 仓库到本地，让自己能够查看该项目，或者进行修改。
```
git clone [url]
```
`[url]` 是要克隆的项目地址

- 报错情况
> Cloning into '***********'...
fatal: unable to access 'https://github.com/*************.git/': OpenSSL SSL_connect: Connection was reset in connection to github.com:443
- 解决方案
>只需把链接的 `http` 或 `https` 改成 `git` 即可

---

# git push
命用于从将本地的分支版本上传到远程并合并。
```
cd ooxx //转到要push的目录下
git init //初始化git仓库
git add -A //将目录下的所有文件，包括文件夹添加到暂存区 git add . 也可实现
git commit -m '豆腐最帅' //把所有文件和文件夹打上”豆腐最帅“的标签
git push git@github.com:tofu2333/Bolg-Cover master 
//push上github的tofu2333的Bolg-Cover库
```

`git push <远程主机名> <本地分支名>:<远程分支名>`
如果本地分支名与远程分支名相同，则可以省略冒号: `git push <远程主机名> <本地分支名>`
单个或多个文件添加到暂存区 `git add [file1] [file2] ...`  , 添加指定目录到暂存区，包括子目录 `git add [dir]` 。

强推食用指南 `git push -f git@github.com:tofu2333/Bolg-Cover master` 强推会覆盖该分支下的所有文件。

- 报错情况
> error: failed to push some refs to 'https://github.com/...
- 解决方案
>远程库与本地库不一致所造成 `git pull origin master` 即可解决。

- 报错情况
>fatal: remote error: You can't push to git://github.com/user/xxx.git
- 解决方案
>git remote set-url origin https://github.com/user/xxx.git
然后再 `git push` 。

- 报错情况
>fatal: destination path '**' already exists and is not an empty directory.
- 解决方案
>如果已经在在clone就不用删除删除或者重新命名已经存在的本地文件。进入目录 `git init` 初始化，`git remote add origin  (address)` 远程仓库地址，然后再 `git push` 。

---

# git pull
命令用于从远程获取代码并合并本地的版本,同步远程仓库。

```
git pull origin master:test 
```

`git pull <远程主机名> <远程分支名>:<本地分支名>`

`git pull` 是 `git fetch` 和 `git merge` 命令的一个组合

 ---

# git 查看暂存区(缓存区)
`git ls-files` 查看暂存区中文件信息   
`--cached` (-c) 查看暂存区中文件，`git ls-files` 命令默认是此命令    
`--midified` (-m) 查看修改的文件   
`--delete` (-d) 查看删除过的文件    
`--other` (-o) 查看没有被git跟踪的文件    
`--stage` (-s) 显示mode以及文件对应的Blob对象，进而我们可以获取暂存区中对应文件里面的内容。   
`git ls-files -c` 或者 `git ls-files --cached`  其他类似

#### 删除暂存区文件
`git rm --cached <file>` 用来修改暂存区目录(不修改工作区目录),相当于 `git add` 的一个逆过程

# 其他
查看远程链接 `git remote -v`  
查看分支 `git branch -a`
