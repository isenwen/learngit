## Git常用命令回顾

#### 配置用户信息

- 查看用户信息

```java
git config --list // 查看所有
git config user.name //查看用户名
```

- 配置全局信息

```java
git config --global user.name 'Iwen'
git config --global user.email '742729764@qq.com'
```



#### 基本操作

![](img\gitoper.png)





#### 查看文件状态

```
git status
```

- workspace：工作区
- staging area：暂存区/缓存区
- local repository：版本库或本地仓库
- remote repository：远程仓库



#### 创建仓库

1️⃣ git init 初始化仓库

2️⃣ git clone拷贝一份远程仓库，也就是下载一个项目。

```JAVA
git clone [url]
git clone url newname
```



#### 提交与修改

1️⃣ git add 添加文件到暂存区

```txt

git add [file1] [file2] ... //指定文件
git add [dir]   //指定目录
git add .      //所有文件
```

2️⃣ git diff比较文件的不同(工作区与暂存区的差异)

```java

git diff [file]
git diff --cached [file]
git diff [first-branch]...[second-branch]
```

3️⃣ git commit提交暂存区到本地仓库

```java
git commit -m [message]
git commit [file1] [file2] ... -m [message]
git commit -a //跳过 git add 这一步
```

4️⃣ git reset回退

```txt
git reset [--soft | --mixed | --hard] [HEAD]

```

–mixed 为默认，可以不用带该参数，用于重置暂存区的文件与上一次的提交(commit)保持一致，工作区文件内容保持不变。

–soft 参数用于回退到某个版本

–hard 参数撤销工作区中所有未提交的修改内容，将暂存区与工作区都回到上一次版本，并删除之前的所有信息提交

**注意：**谨慎使用 –hard 参数，它会删除回退点之前的所有信息。

```TXT
HEAD 说明：
	HEAD 表示当前版本

	HEAD^ 上一个版本

	HEAD^^ 上上一个版本

	HEAD^^^ 上上上一个版本

以此类推...

可以使用 ～数字表示
	HEAD~0 表示当前版本

	HEAD~1 上一个版本

	HEAD^2 上上一个版本

	HEAD^3 上上上一个版本

以此类推...

git reset HEAD
git reset HEAD 命令用于取消已缓存的内容。

```





5️⃣`git rm`删除文件

6️⃣`git mv`移动或重命名

#### 提交日志

1️⃣ `git log`查看历史提交记录

2️⃣ `git blame <file>`- 以列表形式查看指定文件的历史修改记录。

#### 远程操作

1️⃣`git remote`远程仓库操作



```TXT
$ git clone https://gitee.com/y_project/RuoYi-Vue.git
Cloning into 'RuoYi-Vue'...
remote: Enumerating objects: 10119, done.
remote: Total 10119 (delta 0), reused 0 (delta 0), pack-reused 10119
Receiving objects: 100% (10119/10119), 2.92 MiB | 590.00 KiB/s, done.
Resolving deltas: 100% (5121/5121), done.

$ cd RuoYi-Vue

$ git remote -v //显示所有远程仓库
origin  https://gitee.com/y_project/RuoYi-Vue.git (fetch)
origin  https://gitee.com/y_project/RuoYi-Vue.git (push)

```



**origin** 为远程地址的别名。

显示某个远程仓库的信息：

```TXT
git remote show [remote]
```

添加远程版本库：

```
git remote add [版本库名字] [url]

# 提交到 Github
$ git remote add origin git@github.com:tianqixin/runoob-git-test.git
$ git push -u origin master

```

其他命令：

```
git remote rm name  # 删除远程仓库
git remote rename old_name new_name  # 修改仓库名

```

2️⃣`git fetch` 从远程获取代码库

该命令执行完后需要执行 git merge 远程分支到你所在的分支。

从远端仓库提取数据并尝试合并到当前分支：

```TXT
git merge
```

该命令就是在执行 git fetch 之后紧接着执行 git merge 远程分支到你所在的任意分支。

假设你配置好了一个远程仓库，并且你想要提取更新的数据，你可以首先执行:

```TXT
git fetch [alias]
git fetch origin //在本地更新修改

```

以上命令告诉 Git 去获取它有你没有的数据，然后你可以执行：

```
git merge [alias]/[branch]
git merge origin/master //master分支已经被更新，将更新同步到本地

```

以上命令将服务器上的任何更新（假设有人这时候推送到服务器了）合并到你的当前分支。

3️⃣ `git pull`下载远程代码并合并

```
git pull <远程主机名> <远程分支名>:<本地分支名>

# 将远程主机 origin 的 master 分支拉取过来，与本地的 brantest 分支合并。
git pull origin master:brantest 

# 如果远程分支是与当前分支合并，则冒号后面的部分可以省略。
git pull origin master

```

4️⃣`git push`上传远程代码并合并

```
git push <远程主机名> <本地分支名>:<远程分支名>
$ git push origin master:master

# 如果本地版本与远程版本有差异，但又要强制推送可以使用 --force 参数：
git push --force origin master

#删除主机的分支可以使用 --delete 参数
git push origin --delete master

```

#### Git分支管理

几乎每一种版本控制系统都以某种形式支持分支。使用分支意味着你可以从开发主线上分离开来，然后在不影响主线的同时继续工作。

有人把 Git 的分支模型称为**必杀技特性**，而正是因为它，将 **Git** 从版本控制系统家族里区分出来。

查看分支命令

```TXT
git branch  //查看本地分支
git barnch -r //查看远程分支
git branch -a //查看所有分支

```

创建分支命令：

```TXT
git branch 分支名
```

切换分支命令:

```TXT
git checkout  分支名
```


使用 git checkout -b (branchname) 命令来创建新分支并立即切换到该分支下

合并分支命令:

```TXT
git merge 
```

把新建的分支push到远端

```TXT
git push origin 分支名
```


删除分支

```TXT
git branch -d 分支名
```



#### Git实战

##### 1.多人协作工作流程

![](IMG/1.png)

##### 2.实战总结



程序员版：

- 克隆远程仓库 —> git clone url
- 选择到需要的分支—> git checkout 分支名
- 新建一个自己的分支—> git branch 分支名
- 切换到自己的分支 —> git checkout 分支名
- 编码编码…—> ......
- 提交到本地仓库 —> git add . git commit -m '提交信息'
- （防止冲突多pull）把分支的代码提交到要求的分支 ----> git checkout dev git merge 本地分支
- 把要求的分支推送到远程 —> git push
