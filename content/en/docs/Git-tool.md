---
title: Github Usage
slug: Github-Usage
lastmod: 2025-07-01T00:00:00+00:00
---

### **一、安装git**

- 官网下载 git
    
    https://git-scm.com/
    
    ![Untitled](Untitled.png)
    
    选择好操作系统和稳定的版本
    
    ![Untitled](Untitled%201.png)
    
    双击下载后的 Git-2.37.3-64-bit.exe，开始安装
    
    ![Untitled](Untitled%202.png)
    
- 配置用户名邮箱和ssh证书
    
    ```jsx
    # 安装
    brew install git
    
    # 配置账户信息
    git config --global user.name "zcy530"
    git config --global user.email "zhangcaiyii@163.com"
    
    # 配置ssh公钥，这里一路空格，选择默认设置
    ssh-keygen -t rsa -C "zhangcaiyii@163.com"
    
    # 获取公钥，复制
    cat ~/.ssh/id_rsa.pub
    
    #github 官网找到 ssh 证书，新建 ssh，把这个公钥复制进去
    
    # 测试
    ssh -T git@github.com
    ```
    

### **二、远程仓库**

- 在 github 里创建一个新的仓库
    
    以 test_repository 为例
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812233931.png)
    
- 或者使用远程仓库的地址
    
    在创建完仓库后，复制它的远程仓库地址，这里使用 HTTP 地址
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812235122.png)
    

### **三、本地仓库**

- 认识文件的四种状态
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812233924.PNG)
    
- git init 创建本地仓库
    
    ```jsx
    # 创建本地仓库
    git init
    ```
    
    在你想上传的文件夹中空白处右键 -> git bash here
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812220003.png)
    
    在命令行中输入 *git init* 就会看到文件夹当中生成了一个 *.git* 的隐藏文件，它所在的文件夹就是仓库，它会记录你所有的变更行为
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812220022.png)
    
- git clone 把远程仓库下载下来
    
    把一个repo的项目拷贝到本地，并且连接该仓库
    
    ```jsx
    git clone https://github.com/xxx/xxx.git
    ```
    
- git remote add origin 连接远程仓库
    
    用于添加远端仓库地址
    
    git clone 之后自动链接好的，可以省略这一步
    
    ```
    git remote add origin(给远程仓库地址起的别名) 你的远程仓库地址
    ```
    
    **实际演示：**
    
    *git remote add origin* 把远程仓库地址保存起来，表示以后就可以用 origin 代替你这一长串的远程仓库地址
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812235521.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210813093640.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210813093900.png)
    
- git remote -v 查看仓库的地址
    
    查看远程仓库
    
    ```jsx
    gti remote -v
    ```
    

### **四、项目代码变动提交**

- git add
    
    ```jsx
    # 将单个文件添加到暂存区
    git add filename
    
    # 将所有文件添加到暂存区
    git add .
    ```
    
- git push
    
    ```jsx
    # 推送提交
    git push -u origin(远程仓库) master(分支信息)
    ```
    
- git log
    
    ```jsx
    # 查看所有的 commit 记录
    git log 
    ```
    
- git reflog
    
    ```jsx
    # 查看所有的操作记录
    git reflog
    ```
    
- 使用 token push
    
    你原先的密码凭证从2021年8月13日开始就不能用了，必须使用个人访问令牌（personal access token），就是把你的密码替换成token！
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214163442.png)
    
    setting -> developer setting -> personal access tokens
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214163626.png)
    
    生成一个token
    
    要使用token从命令行访问仓库，请选择repo
    
    要使用token从命令行删除仓库，请选择delete_repo
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20211214164715.png)
    
    生成之后记得把你的token保存下来，因为你再次刷新网页的时候，你已经没有办法看到它了
    
    然后在 git push -u origin master弹出的窗口里面，输入username，密码复制粘贴你生成的token就行了
    
    参考教程
    
    [https://blog.csdn.net/weixin_41010198/article/details/119698015](https://blog.csdn.net/weixin_41010198/article/details/119698015)
    
- 实际操作如下
    
    接下来我们尝试创建两个文件 *index.html 和 index.js*，在命令行中输入 *git status* 可以查看当前仓库的状态信息
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812215934.png)
    
    我们用 *git add index.html* 命令把单个文件 *index.html* 加到缓存区里
    
    再用  *git status* 查看当前仓库的状态信息，发现 *index.html* 已经绿了
    
    如果想把项目里所有的文件都上传到缓存区，可以用 *git add .* 来实现
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812220735.png)
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812221125.png)
    
    接下来就可以提交这次变更了 -m 是 message 的意思，后面跟上跟此次变更信息有关的描述
    
    在提交后通过 *git log* 查看日志，通过日志我们可以查看什么人在什么时间，提交了一个什么样的commit
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812233909.png)
    
    *git push -u origin  master* 将本地仓库推向远程仓库，如果网络不好可能会失败
    
    成功后会弹出一个GitHub的登录框， 输入邮箱和密码
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210813092633.png)
    
    上传成功！可以在你的GitHub远程仓库看到我们在本地添加的 *index.html 和 index.js* 文件了
    
- git reset
    
    ```
    # 取消我的commit
    git reset commitID --hard
    git reset commitID --soft
    git reset commitID --mixed
    
    # 如果回退了commit，用这个把回退push到远端
    git push -f
    ```
    
    **reset --hard/soft/mixed 三个参数对比：**
    
    hard：在本地库移动 HEAD 指针，也会重置暂存区，也会重置工作区
    
    soft：仅仅是在本地库移动 HEAD 指针
    
    mixed：在本地库移动 HEAD 指针，也会重置暂存区
    
    **实际演示：**
    
    我们修改一下index.js文件几行代码之后再查看状态，会发现又出现了红色的文件，红色的文件代表有新的变更
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812233904.png)
    
    我们需要重复以上的操作，先用 git add . 将所有文件提交到暂存区，再提交 *git commit -m* ，通过 *git log* 可以看到的确已经提交了
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812233900.png)
    
    如果想要取消一个commit，恢复到 first commit 的版本，就在 git log 里找到第一次的 commitID
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812233856.png)
    
    如果想要取消一个commit，恢复到 first commit 的版本，也可以在 *git reflog* 里面找到一个短的索引值，这样引用比较方便
    
    ![](https://caiyiimg.oss-cn-shanghai.aliyuncs.com/typora/20210812233852.png)
    

### 五、协作开发

- Fork
    
    把当前作者的项目拷贝到我的仓库里面去
    
    ![Untitled](Untitled%203.png)
    
- Pull request
    1. fork 到自己的仓库之后，可以在自己本地仓库进行文件代码的修改，然后把对项目的修改提交给原项目的过程就是 pull request
    2. 原项目作者可以对 pull request 进行 merge，当合并之后原项目的代码也会进行修改
    3. PR可以通过 #530 关联 issue，PR关联issue后，issue的状态会自动更改为进行中，当PR被合并后，issue会更改为关闭状态。一个 PR 可以关联多个 issue
    
- git pull
    
    拉取最新的代码到本地
    
- git rebase
    
    git pull 和 git rebase 都用于同步本地分支和远程分支
    
    - **git pull**：拉取远程的 main 分支，并将其和当前分支合并，如果有本地提交，会创建一个 merge commit，保留了历史的分叉结构，不是线性的
        
        优点：保留所有分支的提交历史，不会改写历史，merge 提交清楚地标记了什么时候哪个分支合并进来了，便于回溯
        
        缺点：会产生很多“merge commit”，导致 git log 显得很乱，难以阅读。造成分叉结构（非线性历史），不利于定位 bug
        
        ```jsx
        等价于
        git fetch origin
        git merge origin/main
        
        现在是
        A---B---C  (local)
             \
              D---E (origin/main)
              
        git pull 之后是
        A---B---C-------M  (local)
             \         /
              D---E (origin/main)
        ```
        
    - **git rebase**: 将本地提交“移到”最新远程提交之后，结果是一个线性的提交历史，也避免多个 merge commit，历史清爽
        
        优点：线性历史，没有 merge commit，看起来就像你一个人完成了所有开发
        
        缺点：每个 commit 都可能冲突，你要一个个解决，如果你和别人共同维护某个分支，不应随意 rebase，否则会导致别人的历史失效
        
        ```jsx
        等价于
        git fetch origin
        git rebase origin/main
        
        现在是
        A---B---C---F   ← origin/main
                 \
                  D---E   ← 你的本地 feature 分支（落后了）
        
        git rebase 之后
        A---B---C---F
                     \
                      D'---E'   ← rebased feature（新的提交）
        ```
        
- Merge conflict
- cherry-pick
    
    `git cherry-pick` 可以理解为”挑拣”提交，它会获取某一个分支的单笔提交，并作为一个新的提交引入到你当前分支上。当我们需要在本地合入其他分支的提交时，如果我们不想对整个分支进行合并，而是只想将某一次提交合入到本地当前分支上，那么就要使用 `git cherry-pick`
    

### 六、创建分支

- git branch
    
    ```jsx
    # 创建一个名叫 manager 的分支
    git branch manager
    
    # 进入新创建的分支
    git checkout manager
    
    # 查看当前分支名称
    git branch -a
    
    # 删除分支
    git branch -D zhangcaiyi2
    ```
    
- git push —set-upstream
    
    ```java
    # add 和 commit 之后提交到远程
    git push origin manager
    
    #分支push提交
    git push --set-upstream origin user/t-caiyizhang/graduate_killswtiches
    ```
    
- branch 的命名规范
    
    ```jsx
    in case you dont know, sum up for you:
    feat: 新增特性、功能
    fix:  bug修补
    docs: 更新了文档
    release: 发布某个大版本
    hotfix: 基于master分支的紧急修复
    build: 仅与构建过程严格相关的，通常如 config,makefile 这种
    chore: 流程（与build相近）、依赖、辅助工具的变化，或者无法归类的变更
    style: 纯格式，变动不影响代码运行
    test: 增加测试
    refactor: 重构（不增加新功能）
    breakchange: 会严重影响/打断其它模块功能的变动
    revert: 回退
    merge: 代码合并
    rebase 或 sync：同步其它分支的代码变动
    pref:提高性能相关
    ci: 与CI有关的变动
    ```