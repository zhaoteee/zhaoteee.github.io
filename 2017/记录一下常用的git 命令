## github上git提交分支的命令
1. git config配置本地仓库

常用git config --global user.name、git config --global user.email

2. git config --list查看配置详情

3. git init 初始一个仓库，添加--bare可以初始化一个共享（裸）仓库

4. git status 可以查看当前仓库的状态

5. git add“文件” 将工作区中的文件添加到暂存区中，其中file可是一个单独的文件，也可以是一个目录、“*”、-A

6. git commit -m '备注信息' 将暂存区的文件，提交到本地仓库

7. git log 可以查看本地仓库的提交历史

8. git branch查看分支

9. git branch“分支名称” 创建一个新的分支

10. git checkout“分支名称” 切换分支

11. git checkout -b deeveloper 他健并切到developer分支

12. git merge“分支名称” 合并分支

13. git branch -d “分支名称” 删除分支

14. git clone “仓库地址”获取已有仓库的副本

15. git push origin “本地分支名称:远程分支名称”将本地分支推送至远程仓库，

16. git push origin hotfix（通常的写法）相当于

17. git push origin hotfix:hotfix

18. git push origin hotfix:newfeature

本地仓库分支名称和远程仓库分支名称一样的情况下可以简写成一个，即git push “仓库地址” “分支名称”，如果远程仓库没有对应分支，将会自动创建

19. git remote add “主机名称” “远程仓库地址”添加远程主机，即给远程主机起个别名，方便使用

20. git remote 可以查看已添加的远程主机

21. git remote show “主机名称”可以查看远程主机的信息
```
#### 在项目开发过程中，经常性的会遇到远程（共享）仓库和本地仓库不一致，我们可以通过git fetch 命令来更新本地仓库，使本地仓库和远程（共享）仓库保持一致。
git fetch  “远程主机”
或者
git fetch “远程主机” “分支名称”

#### 我们要注意的是，利用git fetch 获取的更新会保存在本地仓库中，但是并没有体现到我们的工作目录中，需要我们再次利用git merge来将对应的分支合并（融合）到特定分支。如下

#### git pull origin 某个分支， 上操作相当于下面两步
* git fetch
* git merge origin/某个分支


#### 问题：如何查看远程主机上总共有多少个分支？
git branch -a 便可以查看所有(本地+远程仓库)分支了

### 删除远程分支git push origin --delete 分支名称
### 刚创建的github版本库，在push代码时出错：

```
$ git push -u origin master
To git@github.com:******/Demo.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'git@github.com:******/Demo.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
hint: before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
因为远程repository和我本地的repository冲突导致的
有如下几种解决方法：

1. 使用强制push的方法：

$ git push -u origin master -f 

这样会使远程修改丢失，一般是不可取的，尤其是多人协作开发的时候。

2. push前先将远程repository修改pull下来

$ git pull origin master

$ git push -u origin master

3. 若不想merge远程和本地修改，可以先创建新的分支：

$ git branch [name]

然后push

$ git push -u origin [name]
