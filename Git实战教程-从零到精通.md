# Git实战教程 - 从零到精通
## 复制粘贴即可掌握的完整Git技能体系

---

## 教程说明

本教程通过一系列精心设计的命令序列，让您从零开始掌握Git的所有核心技能。每个命令都有详细讲解，您只需要复制粘贴执行即可。

### 学习目标
- 掌握Git的核心概念和操作
- 能够独立管理个人项目
- 具备团队协作的基本技能
- 了解高级Git功能和最佳实践

### 环境要求
- macOS/Linux/Windows系统
- 已安装Git
- 有GitHub账号

---

## 第一阶段：环境准备与基础配置

### 1.1 检查Git环境
```bash
# 检查Git版本
git --version
```

**讲解**：这个命令检查Git是否正确安装。如果显示版本号（如git version 2.34.1），说明Git已安装。如果没有安装，请先安装Git。

### 1.2 配置用户信息
```bash
# 配置全局用户名
git config --global user.name "yawenyao"

# 配置全局邮箱
git config --global user.email "y_yawen@163.com"

# 验证配置
git config --list | grep user
```

**讲解**：这些命令配置您的Git身份信息。用户名和邮箱将出现在所有提交记录中，建议使用真实信息。

### 1.3 配置编辑器和其他设置
```bash
# 设置默认编辑器为VS Code
git config --global core.editor "code --wait"

# 设置默认分支名为main
git config --global init.defaultBranch main

# 设置换行符处理（macOS/Linux）
git config --global core.autocrlf input

# 设置凭据缓存
git config --global credential.helper osxkeychain

# 查看所有配置
git config --list
```

**讲解**：这些配置优化您的Git使用体验。VS Code编辑器提供更好的提交信息编辑体验，main分支是现代Git的标准，换行符设置确保跨平台兼容性。

---

## 第二阶段：创建第一个Git仓库

### 2.1 创建项目目录
```bash
# 创建项目目录
mkdir git-tutorial-project
cd git-tutorial-project

# 查看当前目录
pwd
ls -la
```

**讲解**：创建一个专门用于学习Git的项目目录。`pwd`显示当前路径，`ls -la`显示目录内容。

### 2.2 初始化Git仓库
```bash
# 初始化Git仓库
git init

# 查看Git状态
git status

# 查看隐藏的.git目录
ls -la
```

**讲解**：`git init`在当前目录创建Git仓库，生成.git隐藏目录。`git status`显示仓库状态，这是最常用的命令之一。

### 2.3 创建第一个文件
```bash
# 创建README文件
echo "# Git Tutorial Project" > README.md

# 创建项目文件
echo "console.log('Hello, Git!');" > app.js

# 创建配置文件
echo "{
  \"name\": \"git-tutorial-project\",
  \"version\": \"1.0.0\",
  \"description\": \"A project to learn Git\"
}" > package.json

# 查看文件内容
cat README.md
cat app.js
cat package.json
```

**讲解**：创建一些示例文件来练习Git操作。这些文件代表一个典型的项目结构。

---

## 第三阶段：基础Git操作

### 3.1 查看文件状态
```bash
# 查看Git状态
git status

# 查看文件差异
git diff

# 查看暂存区状态
git diff --cached
```

**讲解**：`git status`显示工作区、暂存区、版本库的状态。`git diff`显示工作区与暂存区的差异，`git diff --cached`显示暂存区与版本库的差异。

### 3.2 添加文件到暂存区
```bash
# 添加单个文件
git add README.md

# 查看状态变化
git status

# 添加所有文件
git add .

# 再次查看状态
git status
```

**讲解**：`git add`将文件添加到暂存区。可以添加单个文件或使用`.`添加所有文件。暂存区是提交前的准备区域。

### 3.3 提交文件到版本库
```bash
# 提交文件
git commit -m "Initial commit: Add project files"

# 查看提交历史
git log --oneline

# 查看详细提交信息
git log
```

**讲解**：`git commit`将暂存区的文件提交到版本库。`-m`参数直接指定提交信息。`git log`查看提交历史。

### 3.4 修改文件并再次提交
```bash
# 修改README文件
echo "
## 项目描述
这是一个用于学习Git的项目。

## 功能特性
- 基础Git操作
- 分支管理
- 团队协作" >> README.md

# 查看修改
git diff

# 添加修改
git add README.md

# 提交修改
git commit -m "docs: Update README with project description"
```

**讲解**：这个流程展示了日常开发中最常见的操作：修改文件→查看差异→添加修改→提交修改。

---

## 第四阶段：分支管理

### 4.1 查看分支信息
```bash
# 查看当前分支
git branch

# 查看所有分支
git branch -a

# 查看分支详细信息
git branch -v
```

**讲解**：`git branch`显示分支信息。当前分支前有`*`标记。`-a`显示所有分支，`-v`显示每个分支的最后一次提交。

### 4.2 创建和切换分支
```bash
# 创建新分支
git branch feature/user-login

# 切换到新分支
git checkout feature/user-login

# 查看当前分支
git branch

# 在新分支上工作
echo "function login(username, password) {
  // 用户登录逻辑
  console.log('用户登录:', username);
  return true;
}" > login.js

# 添加并提交
git add login.js
git commit -m "feat: Add user login function"
```

**讲解**：分支是Git的核心功能，允许并行开发。`git branch`创建分支，`git checkout`切换分支。在新分支上的修改不会影响其他分支。

### 4.3 合并分支
```bash
# 切换回主分支
git checkout main

# 合并功能分支
git merge feature/user-login

# 查看合并结果
git log --oneline --graph

# 删除已合并的分支
git branch -d feature/user-login
```

**讲解**：`git merge`将分支的修改合并到当前分支。合并后可以删除功能分支。`--graph`参数显示分支图形。

### 4.4 处理合并冲突
```bash
# 创建冲突分支
git checkout -b feature/conflict-demo

# 修改文件
echo "// 在功能分支中修改
function login(username, password) {
  console.log('功能分支修改:', username);
  return { success: true, token: 'abc123' };
}" > login.js

# 提交修改
git add login.js
git commit -m "feat: Update login function in feature branch"

# 切换回主分支
git checkout main

# 在主分支中修改同一文件
echo "// 在主分支中修改
function login(username, password) {
  console.log('主分支修改:', username);
  return true;
}" > login.js

# 提交修改
git add login.js
git commit -m "refactor: Update login function in main branch"

# 尝试合并（会产生冲突）
git merge feature/conflict-demo
```

**讲解**：当两个分支修改了同一文件的同一部分时，会产生合并冲突。Git会标记冲突内容，需要手动解决。

### 4.5 解决合并冲突
```bash
# 查看冲突文件
cat login.js

# 手动编辑文件解决冲突
echo "// 解决冲突后的代码
function login(username, password) {
  console.log('合并后的登录函数:', username);
  return { success: true, token: 'abc123' };
}" > login.js

# 标记冲突已解决
git add login.js

# 完成合并
git commit -m "resolve: Merge conflict in login.js"

# 删除冲突分支
git branch -d feature/conflict-demo
```

**讲解**：解决冲突需要手动编辑文件，选择保留的内容，然后使用`git add`标记冲突已解决，最后完成合并。

---

## 第五阶段：远程仓库操作

### 5.1 创建GitHub仓库
```bash
# 在GitHub上创建新仓库（手动操作）
# 仓库名：git-tutorial-project
# 描述：Git学习项目
# 设置为公开仓库

# 添加远程仓库
git remote add origin https://github.com/yawenyao/git-tutorial-project.git

# 查看远程仓库
git remote -v
```

**讲解**：远程仓库用于备份代码和团队协作。`git remote add`添加远程仓库，`git remote -v`查看远程仓库信息。

### 5.2 推送到远程仓库
```bash
# 推送主分支到远程
git push -u origin main

# 查看远程分支
git branch -r

# 查看所有分支
git branch -a
```

**讲解**：`git push`将本地分支推送到远程仓库。`-u`参数设置上游分支，后续可以直接使用`git push`。

### 5.3 从远程仓库拉取
```bash
# 模拟远程修改（在GitHub网页上修改文件）
# 然后拉取远程修改
git pull origin main

# 查看拉取结果
git log --oneline -3
```

**讲解**：`git pull`从远程仓库拉取最新修改并合并到当前分支。这是团队协作中常用的命令。

### 5.4 克隆远程仓库
```bash
# 切换到上级目录
cd ..

# 克隆远程仓库
git clone https://github.com/yawenyao/git-tutorial-project.git git-tutorial-clone

# 进入克隆的仓库
cd git-tutorial-clone

# 查看仓库信息
git remote -v
git log --oneline
```

**讲解**：`git clone`复制远程仓库到本地。这是获取他人代码的标准方式。

---

## 第六阶段：高级Git操作

### 6.1 查看提交历史
```bash
# 返回原项目目录
cd ../git-tutorial-project

# 查看提交历史
git log --oneline

# 查看图形化历史
git log --graph --oneline --all

# 查看特定文件的修改历史
git log --oneline -- README.md

# 查看提交的详细信息
git show HEAD
```

**讲解**：`git log`有多种参数来查看提交历史。`--graph`显示分支图，`--oneline`简化显示，`--all`显示所有分支。

### 6.2 撤销操作
```bash
# 修改文件
echo "// 添加新功能
function logout() {
  console.log('用户登出');
  return true;
}" >> app.js

# 添加到暂存区
git add app.js

# 撤销暂存区的修改
git reset HEAD app.js

# 查看状态
git status

# 撤销工作区的修改
git checkout -- app.js

# 查看文件内容
cat app.js
```

**讲解**：`git reset`撤销暂存区的修改，`git checkout --`撤销工作区的修改。这些命令可以回退到上次提交的状态。

### 6.3 修改提交历史
```bash
# 修改文件
echo "// 添加新功能
function logout() {
  console.log('用户登出');
  return true;
}" >> app.js

# 添加并提交
git add app.js
git commit -m "feat: Add logout function"

# 修改最后一次提交
echo "// 添加注释
function logout() {
  console.log('用户登出');
  return true;
}" > app.js

git add app.js
git commit --amend -m "feat: Add logout function with comments"
```

**讲解**：`git commit --amend`修改最后一次提交。这在提交信息有误或需要添加文件时很有用。

### 6.4 标签管理
```bash
# 创建轻量标签
git tag v1.0.0

# 创建带注释的标签
git tag -a v1.1.0 -m "Release version 1.1.0"

# 查看标签
git tag

# 查看标签详细信息
git show v1.1.0

# 推送标签到远程
git push origin v1.0.0 v1.1.0
```

**讲解**：标签用于标记重要的提交点，如版本发布。轻量标签只是提交的引用，带注释的标签包含更多信息。

---

## 第七阶段：团队协作流程

### 7.1 创建功能分支
```bash
# 确保在主分支
git checkout main

# 拉取最新代码
git pull origin main

# 创建功能分支
git checkout -b feature/user-registration

# 在新分支上开发
echo "function register(username, email, password) {
  // 用户注册逻辑
  console.log('用户注册:', username, email);
  return { success: true, userId: 123 };
}" > register.js

# 提交修改
git add register.js
git commit -m "feat: Add user registration function"
```

**讲解**：这是标准的团队协作流程：从主分支创建功能分支，在功能分支上开发，然后通过Pull Request合并。

### 7.2 推送功能分支
```bash
# 推送功能分支到远程
git push -u origin feature/user-registration

# 查看远程分支
git branch -r
```

**讲解**：推送功能分支到远程，其他人可以看到您的开发进度，也可以进行代码审查。

### 7.3 模拟Pull Request流程
```bash
# 切换回主分支
git checkout main

# 模拟合并功能分支
git merge feature/user-registration

# 推送合并结果
git push origin main

# 删除本地功能分支
git branch -d feature/user-registration

# 删除远程功能分支
git push origin --delete feature/user-registration
```

**讲解**：在实际工作中，合并通过GitHub的Pull Request进行，这里模拟了合并过程。

---

## 第八阶段：Git配置优化

### 8.1 设置别名
```bash
# 设置常用别名
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'

# 测试别名
git st
git co main
git br
```

**讲解**：别名可以简化常用命令。`git st`等同于`git status`，`git co`等同于`git checkout`。

### 8.2 设置提交模板
```bash
# 创建提交信息模板
echo "# <类型>(<范围>): <简短描述>
#
# <详细描述>
#
# <相关Issue>
# Closes #123
# Related to #456
#
# <变更类型>
# feat: 新功能
# fix: 修复bug
# docs: 文档更新
# style: 代码格式调整
# refactor: 代码重构
# test: 测试相关
# chore: 构建过程或辅助工具的变动" > ~/.gitmessage

# 设置提交模板
git config --global commit.template ~/.gitmessage

# 测试提交模板
git ci
```

**讲解**：提交模板确保提交信息的一致性。使用`git ci`时会打开编辑器显示模板。

### 8.3 设置忽略文件
```bash
# 创建.gitignore文件
echo "# 依赖文件
node_modules/
npm-debug.log*

# 构建输出
dist/
build/

# 环境配置
.env
.env.local

# IDE文件
.vscode/
.idea/
*.swp
*.swo

# 系统文件
.DS_Store
Thumbs.db" > .gitignore

# 添加并提交
git add .gitignore
git commit -m "chore: Add .gitignore file"
```

**讲解**：`.gitignore`文件指定Git忽略的文件。这些文件不会被Git跟踪，避免提交不必要的文件。

---

## 第九阶段：高级功能实践

### 9.1 暂存工作
```bash
# 修改文件
echo "// 临时修改
console.log('临时修改');" >> app.js

# 暂存当前工作
git stash push -m "临时修改app.js"

# 查看暂存列表
git stash list

# 查看工作区状态
git status

# 恢复暂存的工作
git stash pop

# 查看文件内容
cat app.js
```

**讲解**：`git stash`临时保存工作区的修改，在需要切换分支或拉取代码时很有用。`git stash pop`恢复暂存的工作。

### 9.2 查看文件历史
```bash
# 查看文件的修改历史
git log --oneline -- app.js

# 查看文件的详细修改
git log -p -- app.js

# 查看文件的每一行修改历史
git blame app.js
```

**讲解**：`git log`可以查看特定文件的修改历史，`git blame`显示每一行的最后修改信息。

### 9.3 比较不同版本
```bash
# 比较工作区与暂存区
git diff

# 比较暂存区与版本库
git diff --cached

# 比较不同提交
git diff HEAD~1 HEAD

# 比较不同分支
git diff main feature/user-registration
```

**讲解**：`git diff`可以比较不同版本的文件差异，是代码审查和问题排查的重要工具。

---

## 第十阶段：环境清理

### 10.1 清理本地仓库
```bash
# 查看当前状态
git status

# 清理未跟踪的文件
git clean -n

# 实际清理未跟踪的文件
git clean -f

# 清理未跟踪的目录
git clean -fd
```

**讲解**：`git clean`清理未跟踪的文件。`-n`参数预览要清理的文件，`-f`强制执行，`-d`包含目录。

### 10.2 重置仓库状态
```bash
# 查看提交历史
git log --oneline

# 重置到特定提交
git reset --hard HEAD~2

# 查看当前状态
git log --oneline
git status
```

**讲解**：`git reset --hard`重置到指定提交，会丢失之后的所有修改。请谨慎使用。

### 10.3 删除远程仓库
```bash
# 查看远程仓库
git remote -v

# 删除远程仓库
git remote remove origin

# 验证删除
git remote -v
```

**讲解**：`git remote remove`删除远程仓库配置。这不会删除远程仓库本身，只是断开本地与远程的连接。

### 10.4 完全清理项目
```bash
# 返回上级目录
cd ..

# 删除项目目录
rm -rf git-tutorial-project

# 删除克隆的目录
rm -rf git-tutorial-clone

# 验证清理
ls -la | grep git-tutorial
```

**讲解**：`rm -rf`删除目录及其所有内容。这是最后的清理步骤，确保没有残留文件。

---

## 第十一阶段：最佳实践总结

### 11.1 日常Git工作流
```bash
# 1. 开始新的一天
git checkout main
git pull origin main

# 2. 创建功能分支
git checkout -b feature/new-feature

# 3. 开发功能
# ... 编写代码 ...

# 4. 提交修改
git add .
git commit -m "feat: Add new feature"

# 5. 推送分支
git push -u origin feature/new-feature

# 6. 创建Pull Request（在GitHub上操作）

# 7. 合并后清理
git checkout main
git pull origin main
git branch -d feature/new-feature
```

**讲解**：这是标准的日常Git工作流，适用于大多数开发场景。

### 11.2 紧急修复流程
```bash
# 1. 从主分支创建热修复分支
git checkout main
git checkout -b hotfix/critical-bug

# 2. 修复问题
# ... 修复代码 ...

# 3. 提交修复
git add .
git commit -m "fix: Critical bug fix"

# 4. 推送并合并
git push -u origin hotfix/critical-bug
# 在GitHub上快速合并

# 5. 清理
git checkout main
git pull origin main
git branch -d hotfix/critical-bug
```

**讲解**：热修复流程用于紧急问题修复，需要快速合并到主分支。

### 11.3 代码审查流程
```bash
# 1. 查看修改
git diff

# 2. 查看提交历史
git log --oneline -5

# 3. 查看特定提交
git show <commit-hash>

# 4. 比较分支
git diff main feature/branch-name

# 5. 测试修改
# ... 运行测试 ...
```

**讲解**：代码审查是团队协作的重要环节，这些命令帮助审查代码修改。

---

## 总结

通过这个教程，您已经掌握了Git的所有核心技能：

### 基础技能
- ✅ 仓库初始化和配置
- ✅ 文件添加、提交、修改
- ✅ 分支创建、切换、合并
- ✅ 冲突解决

### 协作技能
- ✅ 远程仓库操作
- ✅ 推送、拉取、克隆
- ✅ 团队协作流程

### 高级技能
- ✅ 提交历史查看
- ✅ 撤销操作
- ✅ 标签管理
- ✅ 暂存工作

### 最佳实践
- ✅ 配置优化
- ✅ 工作流程
- ✅ 代码审查
- ✅ 环境清理

现在您可以自信地使用Git进行个人项目管理和团队协作了！

---

*这个教程提供了完整的Git学习路径，通过复制粘贴命令即可掌握所有核心技能。建议您在实际项目中多加练习，将理论知识转化为实际能力。*
