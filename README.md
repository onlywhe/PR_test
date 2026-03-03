## PR（Pull Request）完整流程

PR（Pull Request）是 GitHub 上协作开发的核心功能，用于向项目贡献代码或建议修改。下面是完整的 PR 流程：

---

### 📋 一、PR 前的准备

#### 1. **复刻（Fork）仓库**（如果是外部贡献者）
- 访问目标仓库，点击右上角的 **Fork** 按钮
- 将仓库复制到你的 GitHub 账户下

#### 2. **克隆到本地**
```bash
git clone https://github.com/你的用户名/仓库名.git
cd 仓库名
```

#### 3. **添加上游仓库**（保持与原仓库同步）
```bash
git remote add upstream https://github.com/原所有者/原仓库名.git
```

#### 4. **创建新分支**（重要！不要在 main/master 上直接修改）
```bash
git checkout -b feature/你的功能名
# 或 fix/修复的问题
```

---

### ✏️ 二、进行修改

1. 在本地修改代码
2. 添加并提交更改
```bash
git add .
git commit -m "清晰描述你的改动"
```
3. 推送分支到你的 GitHub 仓库
```bash
git push origin feature/你的功能名
```

---

### 🔄 三、创建 Pull Request

1. 在 GitHub 上进入你复刻的仓库
2. 会看到提示："feature/你的功能名 had recent pushes"，点击 **Compare & pull request**
   - 如果没有提示，手动切换到该分支，点击 **Contribute** → **Open Pull Request**
3. 填写 PR 信息：
   - **标题**：简明扼要的概括
   - **描述**：详细说明改动内容、原因、测试情况等
   - **关联 Issue**（如果有）：在描述中输入 `#` 选择关联的 Issue 编号
4. 选择基础分支和目标分支：
   - **base repository**：原仓库（目标）
   - **base**：原仓库的目标分支（通常是 main 或 develop）
   - **head repository**：你的仓库
   - **compare**：你的功能分支
5. 点击 **Create pull request**

---

### 💬 四、PR 后的沟通与修改

#### 1. **等待审核**
- 项目维护者会收到通知并审查你的代码
- 可能会在 PR 评论区提出修改意见

#### 2. **根据反馈修改**
- 在本地同一分支继续修改
- 提交并推送：
```bash
git add .
git commit -m "根据反馈修改xxx"
git push origin feature/你的功能名
```
- **无需重新创建 PR**，推送会自动更新到同一个 PR 中

#### 3. **处理合并冲突**（如果有）
- 同步上游更新：
```bash
git fetch upstream
git checkout main
git merge upstream/main
git checkout feature/你的功能名
git merge main  # 或 git rebase main
# 解决冲突后
git add .
git commit -m "解决合并冲突"
git push origin feature/你的功能名
```

---

### ✅ 五、PR 合并

当 PR 通过审核后，项目维护者会进行合并。合并方式通常有三种：

1. **Create a merge commit**：保留所有提交历史，添加一个合并提交
2. **Squash and merge**：将你的所有提交压缩成一个提交再合并（更整洁）
3. **Rebase and merge**：将你的提交变基到目标分支顶部再合并（线性历史）

合并后，你的贡献就正式成为项目的一部分了！

---

### 🧹 六、PR 合并后的清理

1. **删除本地分支**（可选但推荐）
```bash
git checkout main
git branch -d feature/你的功能名
```

2. **删除远程分支**（可选）
```bash
git push origin --delete feature/你的功能名
```

3. **同步更新的主分支**
```bash
git pull upstream main
git push origin main
```

---

### 📝 优秀的 PR 实践

| 要点 | 说明 |
|------|------|
| **小而精** | 一个 PR 只解决一个问题，避免超大 PR |
| **清晰描述** | 说明“为什么”而不是“做了什么” |
| **关联 Issue** | 如果有对应的 Issue，记得关联 |
| **自测通过** | 提交前确保代码可以正常运行 |
| **遵循规范** | 遵守项目的代码风格、提交信息规范 |
| **及时响应** | 对审核意见及时回应和修改 |

---

### 🔍 PR 状态图解

```
你（复刻/分支） → 创建 Pull Request → 原仓库（目标分支）
                            ↓
                      👀 维护者审核
                            ↓
                    ┌──────┴──────┐
                    ↓              ↓
                ✅ 通过        ❌ 需要修改
                    ↓              ↓
                合并 PR      🔄 你修改代码并推送
                    ↓              ↓
                完成 🎉        ← 返回审核
```
