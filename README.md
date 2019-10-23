# GitFlowApp
多人协作开发app流程


## 创建主分支 
1. 为主分支绑定标签版本 `git tag -a v1 -m '初版v1'`
2. 将标签由本地推送到线上master分支 `git push origin --tags`

## 开发项目
1. 切换到开发分支 `git checkout dev`
2. 本地切换自己分支用于开发 `git checkout -b 分支名`
3. 开发完或者过程中 `git push origin 分支名` 将本地代码推送到远程
4. 开发结束后，全部推送远程，报告需要review代码

5. github settings 设置branches 规则`merge` dev前需要`review`
6. `review` 通过github界面进行`review`,或者通过命令进行`review merge`
```
// 拉取代码到本地
1. git fetch origin // 更新代码
2. git checkout -b 分支名 origin/分支名 // 切换到分支 同步远端
3. git merge dev // 合并dev分支
// 本地解决分支bug后合并到本地dev并推送到远程dev
4. git checkout dev // 本地切换dev分支
5. git merge --no-ff 分支名 反向merge分支并删除合并完的分支
6. git push origin dev 推送dev分支到远程
```

## 提测阶段
1. 切换到开发分支dev `git checkout -b release` 切出预上线版本
2. 将本地预上线版本release 提交到远程 `git push origin release`
3. 注意提测后不允许新增功能，可以修改bug，此时不允许大幅度修改
4. 出现bug修改后release分支为正确分支后将release分支合并到master分支
6. 注意 release分支作为临时分支用来 修改测试后出现的bug 稳定后合并maser

## 更新开发分支dev
1. 线上代码为稳定版最新后，同步merge`dev`分支，使dev分支为最新稳定版本
2. `git checkout dev` + `git merge release`
3. `git branch -d release` // 删除release 临时测试分支

## 为master打上版本标签
1. `git checkout master` 切换回master分支
2. `git pull origin master` 拉取master分支
3. `git tag -a v2 -m '版本2'` 本地打上版本标签
4. `git push orgin --tags` 将标签推送到远程

## 上线时 切换版本号代码进行上线
