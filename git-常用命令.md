1. clone 全部文件:  git clone "/xxx"
2. 新建分支：git branch tiantian
3. 转换分支：git checkout master
4. 查看所有分支：git branch
5. 添加到暂存区
   - git add .   : 添加所有
   - git add index.html index.js  : 添加 index.html,index.js 到暂存区
6. 提交暂存区到 本地仓库： git commit -m "提交信息"
7. 提交tiantian到远程仓库：git push origin tiantian
8. 查看状态：git status



一般流程

1. 克隆项目到本地：`git clone  "地址"`
2. 增加一个新的远程仓库，并命名：
   -  `git remote add [webstream] [url]`
3. 拉去远程代码： `git fetch webstream `
4. 新建develop分支开发：`git checkout -b develop `
5. 添加到暂存区
   - `git add . `  : 添加所有
   - `git add index.html index.js`  : 添加 index.html,index.js 到暂存区
6. 提交暂存区到 本地仓库：` git commit -m "提交信息"`
7. 提交tiantian到远程仓库：`git push origin tiantian`