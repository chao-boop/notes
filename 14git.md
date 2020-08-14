# git 版本管理工具  github相当于一个仓库用来存储git发送过来的代码



http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html  git常用命令


  关于grihub访问不到问题 https://www.xjyili.cn/2546  命令行 ping github.com
git 设置一个名称  git config --global user.name "chao-boop"
    绑定一个邮箱git config --global user.email "2531240441@qq.com"
    密码git config --global user.password "25312404bb"

## 基础linux命令
        clear :清除屏幕
        ll :将当前目录下的子文件及其子目录平铺在控制台  ls-al的简写 查看文件详情
        ls ：查看目录
        find 目录名 :将指定平铺其目录下的文件及其子目录平铺
        find 目录名 -type f :将对应目录下的文件平铺在控制台
        rm 文件名 ：删除文件
        mv 源文件 重命名文件  ：文件重命名
        cat 文件的url  ：查看对应文件的内容
        vim 文件名.txt   :创建一个记事本
                    进入文件后的相关操作：按 i 进入插入模式 进行文本编辑
                                        按esc或&键 后出入冒号 加以下操作：
                                                            :q! 强制退出（不保存）
                                                            :wq 保存退出
                                                            :set nu 设置行号


## git命令
git init  主要用来初始化一个空的git本地仓库  要对现有的某个项目开始使用git管理 只需要在此项目的目录执行此操作
git clone 创建本地仓库
git add 添加代码 将工作区文件提交到暂存区stage
git pull 拉取代码
git commit 推送到本地仓库
git push 推到远程仓库
git merge 合并分支
git checkout 切换分支
git reset 回到过去


## 流程 
在GitHub上新建一个工程  -> 在git上 git clone https://github.com/chao-boop/textone.git 克隆一个本地仓库 地址是工程的地址 也可以是ssh
-> 然后 cd 工程名  进入文件分支 完成后会显示（master） 
-> 可以用Linux的命令来查看文件相关内容 可以创建文件 比如 vim a.txt 创建一个名为a的文本文件  编辑完之后 摁esc后冒号然后输入相关命令退出
-> 但是现在Git是不认这个文件的 所以要 git add 文件名 将这个文件推送到缓存区
-> 然后 git commit -am "init" 将该文件推送至本地仓库  -am "init" =》-a -m "init" -m是备注 “init是备注内容”  //了解git commit -m与git commit -am的区别
-> git push 推送至远程仓库
-> git branch 查询所有分支 并查询当前所处分支      
-> gie checkout -b texte    可以创建一个分支 后面是分支名 -b的意思是创建并切换到该分支  创建分支： $ git branch texte   切换分支： $ git checkout texte
                        包括一系列命令（合并 删除 推送 查看 更新）
-> git merge 分支名   将选中的分支合并到当前分支上  
                        会产生冲突 这里要解决冲突




粘贴代码
git checkout -b 分支名      创建并切换分支
git add 文件名              推入到缓存区   
git commit -m '备注信息'      提交到本地仓库
git push origin 分支名      到远程仓库


https://blog.csdn.net/huanhuaqian/article/details/81986064




https://blog.csdn.net/winnershili/article/details/78888548