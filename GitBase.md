### Git安装
#### Windows
对于Windwos系统，安装方法如下：
1. 访问`https://git-scm.com/`
   ![image](https://github.com/user-attachments/assets/7e7660e5-c4fb-44b6-8207-8cb6e46d0c1b)

2. 直接点击为windows安装
   ![image](https://github.com/user-attachments/assets/28cb45ee-0e65-4057-b4ec-5cfa5296e7b8)

3. 选择适合自己的Git版本
  ![image](https://github.com/user-attachments/assets/8a481899-f348-4366-831c-c8924900254e)

4. 在安装时，需要选择组件（Select Components）。要保证有勾选其中的两个框：即“Windows Explorer integration”中的 **“Git Bash Here”和“Git GUI Here”** 。其它保持默认即可
![image](https://github.com/user-attachments/assets/f86e4cbc-828d-41c5-aea8-964a93e0f059)

5. 安装后，右键可以看到两个图标（当然如果是win11，别忘记点击“显示更多选项”）
   ![image](https://github.com/user-attachments/assets/e9ba249c-8239-446e-851d-1bf54b4d5008)

1. 点击“Git Bash Here”，会看到一个类似windows中cmd命令行窗口的页面（许多和git相关的命令，就是在这个小窗口输入与执行的）。输入`git version`，可以看到git的版本号
![image](https://github.com/user-attachments/assets/98ef0190-11e1-4679-a2d1-4ac674afa7fe)


### Git配置

```bash
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

`git config`命令的`--global`参数，表明这台机器上的所有Git仓库都会使用这个配置，也可以对某个仓库指定不同的用户名和邮箱地址。

检查配置

```bash
git config --list
```


### 工作区、暂存区和版本库的区别
- 工作区：在电脑里能看到的目录；
- 版本库：在工作区有一个隐藏目录`.git`，是Git的版本库。  

Git的版本库中存了很多东西，其中最重要的就是称为stage（或者称为index）的**暂存区**，还有Git自动创建的`master`，以及指向`master`的指针`HEAD`。

![理解](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907720458e56751df1c474485b697575073c40ae9000/0)

进一步解释一些命令：
- `git add`实际上是把文件添加到暂存区
- `git commit`实际上是把暂存区的所有内容提交到当前分支
### 撤销修改
#### 丢弃工作区的修改
```bash
$ git checkout -- <file>
如
$ git checkout -- README.md
```
该命令是指将文件在工作区的修改全部撤销，这里有两种情况：
1. 一种是file自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
2. 一种是file已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次git commit前暂存区的状态。

#### 丢弃暂存区的修改
```bash
$ git reset HEAD <file>
如：
$ git reset HEAD README.md
```

该命令将已经add到暂存区的修改撤销掉（unstage），重新放回工作区


### 克隆仓库

```bash
$ git clone https://github.com/user/repositoryname.git
```

### 删除文件

```bash
$ git rm <file>
```

`git rm <file>`相当于执行

```bash
$ rm <file>
$ git add <file>
```

#### 删除文件解释
Q：比如执行了`rm text.txt` 误删了怎么恢复？
A：执行`git checkout -- text.txt` 把暂存区的东西重新写回工作区就行了
Q：如果执行了`git rm text.txt`我们会发现暂存区的text.txt也删除了，怎么恢复？
A：先撤销暂存区修改，重新放回暂存区，然后再从暂存区写回到工作区
```bash
$ git reset HEAD text.txt
$ git checkout -- text.txt
```
Q：如果真的想从版本库里面删除文件怎么做？
A：执行`git commit -m "delete text.txt"`，提交后最新的版本库将不包含这个文件

### 查看本次修改内容
`git show`
