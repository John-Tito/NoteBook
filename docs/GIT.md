# GIT 入门

## Git状态

```shell
git status
```

1. Untrack  
未记录 新文件，使用git add命令，增加track  
2. Modified  
发生改动 使用git add命令来更新，使用git restore来放弃更改  
3. Staged  
暂存
4. Committed
 已提交

------

## GIT 常见问题

1. 撤销commit push
   1. 查看日志，获取需要回退的版本号  

      ```shell
      git log
      ```

   2. 重置至指定版本的提交  

      ```shell
      git reset –-soft <版本号>
      #举例
      git reset --soft 4f5e9a90edeadcc45d85f43bd861a837fa7ce4c7
      #保留更改,撤回提交
      git reset –-soft <版本号>
      #撤销更改,撤销提交
      git reset –-hard <版本号>
      #撤回上次提交
      git reset [–-soft|–-hard] HEAD~
      #撤回上n次提交
      git reset [–-soft|–-hard] HEAD~n
      ```

   3. 强制提交当前版本号

      ```shell
      git push <仓库名> <分支名> –-force
      ```

2. 删除本地分支

   ```shell
   git branch --delete <分支名>
   git branch -d <分支名>
   git branch -D <分支名>
   ```

   1. -d是--delete的缩写,在使用--delete删除分支时,该分支必须完全和它的上游分支merge完成,如果没有上游分支,必须要和HEAD完全merge

   2. -D是--delete --force的缩写,这样写可以在不检查merge状态的情况下删除分支 --force简写-f,作用是将当前branch重置到初始点(startpoint),如果不使用--force的话,git分支无法修改一个已经存在的分支.

3. 删除远程分支

   ```shell
   git push <仓库名> --delete <分支名>
   ```

   该指令也会删除追踪分支

4. 删除追踪分支

   ```shell
   git branch --delete --remotes <仓库名>/<分支名>
   ```

   该操作并没有真正删除远程分支,而是删除的本地分支和远程分支的关联关系,即追踪分支

5. 关联远程仓库

   1. 设置账号

      ```shell
      git config --global user.name "<name>"
      git config --global user.email <email>
      ```

   2. 生成SSH指纹

      ```shell
      ssh-keygen -t rsa -b 4096 -C "<email>"
      ```

   3. 添加ssh到ssh-agent中

      ```shell
      eval "$(ssh-agent -s)"
      ```

   4. 设置Github SSH and GPG keys

   5. 关联远程仓库

      ```shell
      git remote add <仓库名> git@github.com:***
      git remote add mirror https://gitee.com/***
      ```

   6. 查看远程仓库信息

      ```shell
      git remote show <仓库名>
      ```

   7. 查看远程仓库地址

      ```shell
      git remote -v
      ```

   8. 取消关联远程仓库

    ```shell
    git remote rm <仓库名>
    ```

6. 推送到远程仓库

   ```shell
   git push -u <仓库名> <分支名>
   git push -u mirror master
   #-u:将<仓库名> 仓库的master 分支设置为本地仓库当前分支的upstream
   ```

7. 推送到分支

   ```shell
   git checkout <分支名>
   git push -u <仓库名> <分支名>
   ```

8. 从远处仓库获取分支

   ```shell
   git checkout -b fa <仓库名>/fa
   git clone git@github.com:lenve/test.git
   ```

9. 从远程仓库更新

   ```shell
   git pull
   ```

10. The authenticity of host 'github.com(13.250.177.223)' can't be established

   没有生成公钥或公钥错误,没有与远程仓库成功关联

11. 添加所有新文件

   ```shell
   git add .
   ```

12. 提交修改

   ```shell
   git commit
   #Press Insert Key and then Enter Key. This will allow you to type a message
   #Once you have done that Press Esace (Esc) then :wq to exit
   ```

13. 创建新分支

   ```shell
   git branch #查看现有分支
   git branch <new branch name> #创建新分支    
   ```

14. 子模块

  ```shell
   git submodule add <https://github.com/yyy/xxx> .\location
   ```

15. 添加子模块报错

   ```shell
   "xxx" already exists in the index
   ```

   ```shell
   git rm -r --cached xxx
   ```

16.  添加多个远程仓库

   ```shell
   git remote set-url --add <仓库名> <仓库地址>
   ```

18. git error：invalid path

   ```shell
   git config core.protectNTFS false
   ```