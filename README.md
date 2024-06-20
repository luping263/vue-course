Vue 课程

第一部分 预备知识 —— git
https://github.com/lilichao/vue-course

一.Git简介

  Git--免费开源的版本控制系统

  1.Git安装    
      https://git-scm.com/
      官网下载 win：32位 or 64位  
      
      打开命令行，输入git -v，能看到正常输出即表示安装成功。

  2.配置
    01.配置 name 和 email
      git config --global user.name "xxxx"
      git config --global user.email "xxx@xxx.xxx"

  3.使用 git （VScode可直接图形化使用）
    在项目文件夹目录中打开Terminal，进入正确目录。
    -查看当前仓库的状态
      git status
      
    -初始化仓库    
      git init
      会生成隐藏.git文件夹
  
    -文件状态：
      未跟踪
      已跟踪
          暂存
          未修改
          已修改
      
      
      刚刚添加到项目中的文件处于未跟踪状态,需要切换
        01.未跟踪状态 → 已跟踪(暂存)
            git add <filename> 将文件切换到暂存的状态 
            git add * 将所有已修改（未跟踪）的文件暂存
        02.暂存 → 未修改
            git commit -m "xxxx" 将暂存的文件存储到仓库中 m→message
            git commit -a -m "xxxx" 提交所有已修改的文件（未跟踪的文件不会提交）
        03.未修改 → 修改
            修改代码后，文件会变为修改状态

            git log:能看到每一次的提交记录
      
      <常用的命令>

      1.重置文件
        git restore <filename> # 恢复文件
        git restore --staged <filename> # 取消暂存状态

      2.删除文件
        git rm <filename> # 删除文件
        git rm <filename> -f # 强制删除

      3.恢复文件(./1.txt)
        01.git restore --staged ./1.txt
        02.git restore 1.txt # 恢复文件

      4.移动文件(重命名文件)
        git mv from to # 移动文件 重命名文件
        比如: 将1.txt改名为2.txt
              git mv .\1.txt .\2.txt

二.分支 （Branch）
  分支概念
    git 在存储文件时，每一次代码代码的提交都会创建一个与之对应的节点，
      git 就是通过一个一个的节点来记录代码的状态的。
    
    节点会构成一个树状结构，树状结构就意味着这个树会存在分支，
      默认情况下仓库只有一个分支，命名为main或master(不好)。
    
    在使用 git 时，可以创建多个分支，分支与分支之间相互独立，
      在一个分支上修改代码不会影响其他的分支.

  1.查看/切换/创建并切换分分支
      git branch # 查看当前分支
      git branch <branch name> # 创建新的分支
      git branch -d <branch name> # 删除分支
      git switch <branch name> # 切换分支
      git switch -c <branch name> # 创建并切换分支

  2. 合并分支⭐  
      01.进入主分支 git switch main
      02.合并分支 🖊 git merge iss1
     
      在开发中，都是在自己的分支上编写代码，代码编写完成后，在将自己的分支合并到主分支中。
  
  3.合并的两种方法
     merge（优先使用）
     rebase

三.变基(rebase)  ❗rebase一定要本地操作，不要直接在远程仓库操作
   branch分支 iss1 经过多次改动后，想和main合并，并且不留下过往iss1的提交记录。
   这时就要使用(rebase)。
 
  1.方法
      01.切换到iss1（rebase）
        <1> git switch iss1
            git rebase main
        <2> 根据需要处理冲突
        <3> 暂存 （快捷键 + ） 和提交    // 这里变基完成，但是合并分支还未完成
      
      02.切换到main (合并删除)
            git switch main
            git merge iss1
            git branch -d iss1
   
    ⭐和普通的合并分支区别在，没有多余的提交记录，更整洁更清晰

        普通合并分支⭐  
        01.进入主分支 git switch main
        02.合并分支 🖊 git merge iss1

  2.原理（变基时发生了什么）：
    Ⅰ.当我们发起变基时，git 会首先找到两条分支的最近的共同祖先
    Ⅱ.对比当前分支相对于祖先的历史提交，并且将它们提取出来存储到一个临时文件中
    Ⅲ.将当前部分指向目标的基底
    Ⅳ.以当前基底开始，重新执行历史操作

  3.注意❗
    大部分情况下合并和变基是可以互换的，
    但是如果分支已经提交给了远程仓库，那么这时尽量不要变基。

四.远程仓库（remote）
  目前我对于 git 所有操作都是在本地进行的。在开发中显然不能这样的，这时我们就需要一个远程的 git 仓库。
   远程的 git 仓库和本地的本质没有什么区别，不同点在于远程的仓库可以被多人同时访问使用，方便我们协同开发。
    在实际工作中，git 的服务器通常由公司搭建内部使用或是购买一些公共的私有 git 服务器。
     我们学习阶段，直接使用一些开放的公共 git 仓库。目前我们常用的库有两个：GitHub 和 Gitee（码云）


  1.将本地库上传 github：

      01.git remote add origin https://github.com/lilichao/git-demo.git
      # git remote add <remote name> <url>

      02.git branch -M main (非必须)
      # 修改分支的名字的为main

      03.git push -u origin main
      # git push 将代码上传服务器上

      ⭐vsCode有【publish Branch】一键上传

  2.从github上下载代码
      01.复制链接
      02.目标文件夹终端打开输入 git clone 链接
    
  3.删除GitHub某个仓库
     GitHub--sett--页面下拉到最后一行Delete this repository