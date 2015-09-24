git 用法总结
这里新建一个名为bookstore的项目为例
<!--more-->

1. git 配置
--------
初始化git根目录
<pre class="lang:zsh decode:true ">mkdir bookstore
cd bookstore    ＃在当前位置生成 git 根目录
git init
# or    
git init bookstore    ＃直接生成目录
</pre>
**git的配置文件：**
git config 有三个级别
仓库级的config，对应git config --local
全局级的config，对应git config --global
系统级的config，对应git config --system

一般情况下我们只使用 local和global, local和global对应的配置文件又是不同的
local对应 bookstore/.git/config
global对应/home/sheng/.gitconfig

以下是本人常用的git config
<pre class="lang:zsh decode:true ">
git config --global core.editor "vim"    #设置 core info editor
git config --global core.filemode false    #不追踪文件mode的改变
git config --global user.name "Christian Sheng"    #设置 user info
git config --global user.email "christian.leo.sheng@gmail.com"

git config --global alias.st status    #设置 别名（缩写）
git config --global alias.cm commit
git config --global alias.ck checkout
git config --global alias.br branch
git config --global alias.la "log --oneline --decorate --graph --all"
git config --global alias.lg "log --oneline --decorate --graph"

git config --list    #查看 配置
</pre>
本人的配置文件如下/home/sheng/.gitconfig
<pre class="nums:false lang:default decode:true ">[user]
    name = Christian Sheng
    email = christian.leo.sheng@gmail.com
[alias]
    st = status
    ck = checkout
    cm = commit
    br = branch
    last = log -1
    lg = log --oneline --decorate --graph
    la = log --oneline --decorate --graph --all
[core]
    editor = vim
    autocrlf = input
    filemode = false
</pre>
2. git 本地操作
--------
<pre class="lang:zsh decode:true "># 把文件加到暂存区
git add file_name
git add .   #All Files
git rm file_name
git rm --cached file_name

# 提交到git仓库
git commit -m "commend text here"

# 查看 创建 切换至该分支
git branch
git branch branch_name
git checkout branch_name
# git checkout命令加上-b参数表示创建并切换，等于上面两条
git checkout -b branch_name     

# 把branch_name分支删掉
git branch -d branch_name
git branch -D branch_name       # 强制删除

# 查看 日志 和 命令记录
git log
git reflog

# 带参数的git log也可以看到分支的合并情况：
git log --graph --pretty=oneline --abbrev-commit

#回到最近一次git commit或git add时的状态
git checkout -- file_name

# 把暂存区的修改撤销掉（unstage），重新放回工作区，不会修改file_name
git reset HEAD file_name

# 把分支(branch_name)的工作成果合并到当前分支上
git merge branch_name

# 回退 或 跳转

git reset --hard HEAD^        #回退1个
git reset --hard HEAD^^       #回退2个
git reset --hard HEAD~8       #回退8个
git reset --hard 3628164      #Jump to specific hashnumber(3628164)
</pre>
3. git 远程协作
--------
关联github，其中origin: 远程库的名字；christiansheng: github账号；git-school: github文件夹名
<pre class="lang:zsh decode:true ">git remote add origin git@github.com:christiansheng/git-school.git

git push -u origin master   # for first time
git push origin master      # for later push

git fetch    ＃从远程分支得到更新
git merge    ＃并合并

git pull    ＃等于上面两条
</pre>
4. git 几个高级命令
--------
<pre class="lang:zsh decode:true">git blame filename    ＃查看每个用户对该文件的修改，从字面上看，出了问题该blame谁
git show 3628164    #查看hashnumber(3628164)对应的详情

git rebase rel01    #将所在分支rebase到rel01分支
# Delete local new files
git clean -df
git clean -f -d -x

# git cmmit的高级
git cm -a    #经常用于cherry-pick他人的change时的commit
git cm --amend    #修改最近一次commit的注释，多次commit合并，并更新commit message

git log -- file_name    ＃查看文件历史，本人经常用来查看文件何时被删除
git tag "v0.1" HEAD    #对于当前HEAD打一个tag，往往作为版本发布用
</pre>
本文由 **Christian Sheng** 写于 **2015-09-20**。转载请注明出处: <a href="http://www.christiansheng.com" target="_blank">**希恩印象** www.christiansheng.com</a>。
