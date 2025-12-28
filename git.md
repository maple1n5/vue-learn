~~~shell
git config --global user.name maple

git config --global user.email "maple1n555@gmail.com"

git config --list

git status
git status -s  # 简洁模式

git add filename.txt          # 添加单个文件
git add *.js                 # 添加所有js文件
git add src/                 # 添加整个目录
git add .                    # 添加所有更改
git add -p                   # 交互式添加（推荐！）

git commit -m "添加用户登录功能"

git remote -v
git remote add origin https://github.com/maple1n5/vue-learn.git

# 推送代码
git push -u origin main    # 首次推送，设置上游分支
git push                   # 后续推送

# 拉取更新
git pull                   # 拉取并合并
git fetch                  # 只拉取不合并
git pull --rebase          # 拉取并使用变基

# 设置代理
git config --global http.proxy http://127.0.0.1:7897
git config --global https.proxy https://127.0.0.1:7897
~~~

