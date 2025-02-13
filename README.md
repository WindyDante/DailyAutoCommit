

# GitHub 仓库描述 (Description)

**DailyAutoCommit - 智能仓库活跃守护者**
🔥 每日自动提交 | 🛡️ 防止仓库休眠 | 🚀 零配置部署
通过 GitHub Actions 实现全自动定时提交，智能解决代码冲突，支持私有仓库与多时段配置，新手友好型设计，3 分钟完成配置，让您的仓库永远保持活跃状态！

---

# 📘 超详细使用指南（小白必看）

## 🌟 一键式部署流程

### 第一步：获取配置文件
```bash
# 克隆仓库（推荐）
git clone https://github.com/WindyDante/DailyAutoCommit.git

# 或直接下载文件
[.github/workflows/main.yml](https://github.com/WindyDante/DailyAutoCommit/blob/master/.github/workflows/main.yml)
```

### 第二步：配置到你的仓库
1. 在你的仓库创建目录：
   `.github/workflows/`
   📂 目录结构示例：
   ```
   your-repo/
   └── .github/
       └── workflows/
           └── auto-commit.yml  ← 把文件放在这里
   ```
   具体可参考本项目中的路径

### 第三步：激活工作流
1. 打开仓库 **Settings** → **Actions** → **General**
2. 开启这些选项：
   ✅ **Allow all actions**
   ✅ **Read and write permissions**
   ✅ **Allow GitHub Actions to create and approve pull requests**

3. 手动触发首次运行：
   **Actions** → 选择 **Daily Auto Commit** → 点击 **Run workflow**

## 🔧 深度配置详解

### 1. 时间设置（含时区换算表）
修改 `auto-commit.yml` 中的 cron 表达式：
```yaml
schedule:
  - cron: '0 1 * * *'  # 北京时间 09:00
  - cron: '0 9 * * *'  # 北京时间 17:00
```

🕒 常用时间配置示例：
| 北京时间 | UTC 时间 | cron 表达式   |
|----------|----------|--------------|
| 08:00    | 00:00    | `'0 0 * * *'`|
| 12:00    | 04:00    | `'0 4 * * *'`|
| 20:00    | 12:00    | `'0 12 * * *'`|

### 2. 身份定制（重要！）
修改 Configure Git 步骤：
```yaml
- name: Configure Git
  run: |
    git config user.name "你的机器人名字"  # 建议格式：用户名+Bot
    git config user.email "你的GitHub账号@users.noreply.github.com"
```
❗ 注意：
- 邮箱必须与 GitHub 账号关联的备用邮箱一致
- 推荐使用 `用户名+bot@users.noreply.github.com` 格式

### 3. 提交信息个性化
```yaml
- run: |
    git commit --allow-empty \
      -m "🏷️ 活跃打卡 ${commit_time} #仓库守护 [skip ci]" \
```
支持插入 Emoji 和自定义标签：
✅ 正确示例：`"🚀 每日活跃 ${commit_time} #自动维护"`
❌ 错误示例：`"update"`（过于简单可能被标记为无效提交）

## 🛠️ 故障排查手册

### 常见问题解决方案
| 问题现象                | 解决方法                     |
|-------------------------|------------------------------|
| 工作流未触发           | 检查是否开启 Actions 权限    |
| 出现 403 权限错误      | 确认 contents: write 权限开启|
| 提交时间不正确         | 检查 TZ: Asia/Shanghai 配置  |
| 推送失败               | 查看 Push with Retry 步骤日志|

### 日志查看指南
1. 进入 **Actions** 标签页
2. 点击失败的 workflow 运行记录
3. 展开 **Sync and Commit** 步骤查看详细错误

## 💡 六大核心优势

1. **智能冲突处理**
   自动执行 `git pull --rebase` 解决常规冲突，无需人工干预

2. **三级重试机制**
   重试机制：失败→等待→同步→重试

3. **合规提交规范**
   - 使用 `[skip ci]` 避免触发 CI/CD 消耗资源
   - 规范化的提交信息格式

4. **资源优化设计**
   单次运行仅需约 30 秒 Actions 时长，月消耗不足 1 小时

5. **全平台兼容**
   ✅ 私有仓库 ✅ 组织仓库 ✅ 多分支支持

6. **透明化操作**
   所有操作记录可追溯，提交信息包含精确时间戳

---

🙌 **如果这个项目对您有帮助，请点击右上角的 Star 支持我们！**
✨ **您的支持是我们持续优化的动力！**

---

## 📜 使用协议
本项目采用 MIT 开源协议，欢迎 fork 和二次开发，但请保留原始作者信息。遇到问题请到 [Issues](https://github.com/WindyDante/DailyAutoCommit/issues/new) 反馈。
