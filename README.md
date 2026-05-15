# 5 个任务实践指南 - Famous Repos Tour

## 💡 快速理解
这 5 个任务的目标是：通过实际操作 Git 命令，体验开源项目的历史、贡献者、健康度、以及参与机制。

---

## 📋 任务 1：第一次克隆 - 用 Git 克隆 Git

### 目标
最元的体验：用 Git 这个工具去克隆 Git 这个项目本身。

### 执行步骤

```powershell
# 1. 创建工作目录
mkdir famous-repos-tour
cd famous-repos-tour

# 2. 克隆 Git 仓库
git clone https://github.com/git/git.git
cd git

# 3. 查看总提交数
git log --oneline | Measure-Object -Line

# 4. 查看最初 5 个提交
git log --reverse --oneline | Select-Object -First 5

# 5. 查看第一个提交的详细信息
git log --reverse | head -1    # 先看最早的提交
git show <first-commit-hash>   # 查看详细内容
```

### 📝 需要记录的内容

**记录到 `README.md` 中：**

```markdown
## Mission 1: 第一次克隆

### 总提交数
[运行 git log --oneline | wc -l 的结果]

### 最初 5 个提交
[粘贴输出]

### 第一个提交信息
- 日期: [从 git show 提取]
- 作者: [从 git show 提取]
- 消息: [完整消息]
```

### 💻 PowerShell 一键命令

```powershell
cd "C:\Users\DCU\Desktop\123\famous-repos-tour\git"
$count = git log --oneline | Measure-Object -Line
Write-Host "总提交数: $($count.Lines)"
Write-Host "`n最初 5 个提交:" 
git log --reverse --oneline | Select-Object -First 5
Write-Host "`n第一个提交详情:"
git log --reverse --pretty=format:'%h %an %ad %s' | Select-Object -First 1
```

---

## 📋 任务 2：探索 Linux 内核历史

### 目标
了解最大的开源项目之一：Linux。使用浅克隆节省时间和空间。

### 执行步骤

```powershell
# 1. 回到工作目录
cd ..   # 回到 famous-repos-tour

# 2. 浅克隆 Linux（只克隆最新历史，节省空间）
git clone --depth=1 https://github.com/torvalds/linux.git
cd linux

# 3. 查看贡献最多的 10 个开发者
git shortlog -sn | Select-Object -First 10

# 4. 查看项目结构
Get-ChildItem -Force

# 5. 查看维护者信息
Get-Content MAINTAINERS | Select-Object -First 50
```

### 📝 需要记录的内容

```markdown
## Mission 2: Linux 内核探索

### TOP 10 贡献者
[粘贴 git shortlog -sn 的前 10 行]

### 最有意思的 3 个文件夹
1. **docs/** - 原因：包含所有文档...
2. **drivers/** - 原因：设备驱动...
3. **fs/** - 原因：文件系统实现...

### MAINTAINERS 文件中有趣的一行
[选择一行有趣的维护者信息]
```

### 💻 PowerShell 完整命令

```powershell
cd "C:\Users\DCU\Desktop\123\famous-repos-tour\linux"
Write-Host "=== TOP 10 贡献者 ===" -ForegroundColor Cyan
git shortlog -sn | Select-Object -First 10
Write-Host "`n=== 项目目录结构 ===" -ForegroundColor Cyan
Get-ChildItem | Select-Object Name | Sort-Object Name
```

---

## 📋 任务 3：选择自己领域的仓库

### 目标
从自己感兴趣的领域选择一个活跃的项目，深入了解。

### 选择建议

可以选择以下领域之一（或自选）：

- **前端**: React, Vue, Angular, Svelte
- **后端**: Django, FastAPI, Express.js, Spring Boot
- **数据科学**: NumPy, Pandas, TensorFlow, PyTorch
- **DevOps**: Docker, Kubernetes, Ansible
- **游戏**: Unity, Godot, Unreal Engine
- **AI/ML**: LLaMA, Stable Diffusion, GPT2

**示例：选择 Vue 3**

```powershell
cd ..
git clone https://github.com/vuejs/core.git
cd core

# 查看最近一个月的活动
$date = (Get-Date).AddMonths(-1).ToString('yyyy-MM-dd')
git log --since=$date --oneline | Measure-Object -Line

# 查看最近 20 个提交
git log --pretty=format:'%h %an %ad %s' --date=short | Select-Object -First 20
```

### 📝 需要记录的内容

```markdown
## Mission 3: 选择的仓库分析

### 基本信息
- **仓库名**: [项目名称]
- **URL**: [GitHub 链接]
- **选择理由**: [为什么选择这个项目]

### 活动统计
- 最近一个月提交数: [数字]
- 活跃贡献者数: [查看 git shortlog -sn 的行数]

### 8 项健康检查清单
- [ ] 正常的提交频率（每天/每周）
- [ ] 多位活跃的维护者（≥3 人）
- [ ] 清晰的 README
- [ ] 存在 CONTRIBUTING.md
- [ ] 开放的 Issue 讨论
- [ ] 代码审查制度（PR comments）
- [ ] 按语义版本号发布
- [ ] 友好的社区氛围

**评分**: [8/8 ✅ 或其他]
```

---

## 📋 任务 4：跟踪一个贡献者

### 目标
从众多贡献者中选一个，深入了解他/她的贡献痕迹。

### 执行步骤

```powershell
cd "C:\Users\DCU\Desktop\123\famous-repos-tour\core"  # 或你选的仓库

# 1. 查看贡献者排名
git shortlog -sn | Select-Object -First 20

# 2. 选择其中一个有趣的贡献者，例如 "Evan You"
$author = "Evan You"

# 3. 查看该贡献者的所有提交
git log --author=$author --oneline | Select-Object -First 20

# 4. 查看统计信息
git log --author=$author --stat | Select-Object -First 50

# 5. 查看一个具体提交
# git show <commit-hash>
```

### 📝 需要记录的内容

```markdown
## Mission 4: 贡献者足迹

### 选中的贡献者
- **姓名**: [名字]
- **总提交数**: [数字]
- **主要活跃期**: [时间范围]

### 最值得分享的提交
- **提交哈希**: [hash]
- **提交消息**: [消息]
- **影响**: [这个提交做了什么]

### 主要修改的区域
- 文件: [xxx.js, xxx.ts 等]
- 文件夹: [docs/, src/ 等]
- 贡献类型: [bugfix/feature/refactor]
```

### 💻 完整脚本示例

```powershell
$repo = "C:\Users\DCU\Desktop\123\famous-repos-tour\core"
cd $repo

Write-Host "=== 贡献者排名 ===" -ForegroundColor Green
git shortlog -sn | Select-Object -First 20

$author = Read-Host "输入要追踪的贡献者名称"

Write-Host "`n=== $author 的提交 ===" -ForegroundColor Green
git log --author=$author --oneline | Select-Object -First 20

Write-Host "`n=== $author 的统计 ===" -ForegroundColor Green
git log --author=$author --stat | Select-Object -First 100
```

---

## 📋 任务 5：测量距离你的第一个 PR

### 目标
找到"good first issue"，评估自己是否能上手。

### 执行步骤

#### 方式 1：浏览器查找（最直接）

```
打开这个 URL（替换 owner/repo）：
https://github.com/vuejs/core/issues?q=is:open+label:%22good+first+issue%22
```

#### 方式 2：GitHub CLI 查找（如果安装了）

```powershell
# 需要先安装 GitHub CLI: https://cli.github.com/
gh repo clone vuejs/core
cd core
gh issue list --label "good first issue" --limit 10
```

#### 方式 3：阅读 CONTRIBUTING.md

```powershell
cd "C:\Users\DCU\Desktop\123\famous-repos-tour\core"

# 查看如何贡献的指南
Get-Content CONTRIBUTING.md | Select-Object -First 100
```

### 📝 需要记录的内容

```markdown
## Mission 5: 第一个 PR 距离

### 选中的 3 个 Good First Issue

#### Issue 1
- **标题**: [标题]
- **URL**: [链接]
- **所需技能**: [Vue/TypeScript/CSS 等]
- **复杂度**: [容易/中等/困难]
- **我能做吗**: [是/否，原因]

#### Issue 2
- **标题**: [标题]
- **URL**: [链接]
- ...

#### Issue 3
- ...

### 贡献指南总结（CONTRIBUTING.md）

这个项目的贡献流程是：
1. [步骤 1]
2. [步骤 2]
3. [步骤 3]

### 我的 Ready 状态

- [ ] 已阅读 CONTRIBUTING.md
- [ ] 已设置本地开发环境
- [ ] 已选定目标 Issue
- [ ] 理解该 Issue 的需求
- [ ] 知道如何提交 PR
```

---

## 📋 最终整理：创建 Markdown 总结

在 `famous-repos-tour/README.md` 中创建完整的记录：

```markdown
# 🚀 Famous Repos Tour

## Mission 1: 第一次克隆 ✅
[详细结果]

## Mission 2: Linux 内核探索 ✅
[详细结果]

## Mission 3: 选择的仓库 ✅
[详细结果]

## Mission 4: 贡献者足迹 ✅
[详细结果]

## Mission 5: 第一个 PR ✅
[详细结果]

---

**完成时间**: 2026年5月15日
**个人感受**: [写下你学到了什么]
```

---

## 🎯 快速开始（复制粘贴版本）

### 打开 PowerShell，运行以下命令：

```powershell
# 创建工作目录
cd "C:\Users\DCU\Desktop\123"
mkdir famous-repos-tour
cd famous-repos-tour

# Mission 1
Write-Host "=== Mission 1: Git ===" -ForegroundColor Cyan
git clone https://github.com/git/git.git
cd git
Write-Host "总提交数："
git log --oneline | Measure-Object -Line
Write-Host "最初 5 个提交："
git log --reverse --oneline | Select-Object -First 5
cd ..

# Mission 2
Write-Host "`n=== Mission 2: Linux ===" -ForegroundColor Cyan
git clone --depth=1 https://github.com/torvalds/linux.git
cd linux
Write-Host "TOP 10 贡献者："
git shortlog -sn | Select-Object -First 10
cd ..

# Mission 3 (以 Vue 为例)
Write-Host "`n=== Mission 3: Vue ===" -ForegroundColor Cyan
git clone https://github.com/vuejs/core.git
cd core
$date = (Get-Date).AddMonths(-1).ToString('yyyy-MM-dd')
Write-Host "最近一个月提交数："
git log --since=$date --oneline | Measure-Object -Line
Write-Host "最近 20 个提交："
git log --pretty=format:'%h %an %ad %s' --date=short | Select-Object -First 20
cd ..

Write-Host "`n✅ 所有克隆完成！" -ForegroundColor Green
Write-Host "现在打开浏览器找 good first issue..."
Write-Host "https://github.com/vuejs/core/issues?q=label:%22good+first+issue%22"
```

---

## 📚 常用 Git 命令速查表

| 命令 | 说明 |
|------|------|
| `git log --oneline` | 简洁提交历史 |
| `git log --reverse` | 按时间正序显示 |
| `git shortlog -sn` | 按贡献次数排序的贡献者列表 |
| `git log --author=名字` | 筛选特定作者 |
| `git log --since='1 month ago'` | 最近一个月的提交 |
| `git log --pretty=format:'%h %an %ad %s'` | 自定义格式输出 |
| `git show <commit>` | 查看提交详情 |

---

✨ **祝你探索顺利！任何错误或问题都可以继续问我！**
