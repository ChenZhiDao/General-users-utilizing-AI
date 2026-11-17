# Hermes Agent 上手指南（Windows · 桌面版）

> 适用版本：v0.23.2（本机实测）。本机 Hermes 主目录：`C:\Users\ASUS\AppData\Local\hermes`

---

## 0. 先建立正确的心智模型（30 秒）

Hermes 不是一个"聊天机器人"，而是**一个能动手的助手**：你说一句话，它会自己决定调用哪些工具（读文件、跑命令、开浏览器、查网页、写代码、定时任务），执行完再告诉你结果。

它和普通 AI 对话的三个关键差别：

| | 普通 AI 聊天 | Hermes |
|---|---|---|
| 能力 | 只能回文字 | 能读写**你电脑上的文件**、执行命令、开浏览器、发消息 |
| 记忆 | 关掉就忘 | **跨会话长期记忆** + 可复用的**技能**（skills） |
| 交付 | 给你一段文字 | 给你**跑通的代码、生成的文件、看得到的结果** |

所以最重要的使用原则只有一条：

> **不要问它"怎么做"，直接告诉它"做这件事，做完给我看结果"。**

---

## 1. 你有四个入口

| 入口 | 启动方式 | 适合 |
|---|---|---|
| **桌面 App**（你正在用的） | `hermes desktop`（或开始菜单） | 日常主力：流式对话、拖文件、会话列表、`Ctrl+K` 命令面板 |
| **终端 CLI** | 终端里输 `hermes` | 在项目目录里干活，边看代码边聊 |
| **TUI** | `hermes --tui` | 想要更炫的终端界面 + 小挂件 |
| **网页后台** | `hermes dashboard` | 管渠道、MCP、定时任务、记忆，也有内嵌聊天 |

四个入口是**同一个 agent、同一份记忆和技能**，只是外壳不同。

---

## 2. 第一次对话：怎么开口

### 2.1 在桌面 App 里

直接在输入框打字，回车。下面这些是**可以直接复制粘贴**的：

```
帮我看一下我这台 Windows 机器的配置：CPU、内存、磁盘剩余空间，
用一张 markdown 表格列出来，并指出哪一项快满了。
```

它应该会调用终端执行命令，然后把**真实输出**整理成表格给你。注意看它调用了什么工具——这就是 Hermes 的工作方式。

### 2.2 在终端里（单次执行，适合脚本/批量）

```bash
hermes chat -q "把 ~/Downloads 里大于 100MB 的文件列出来，按大小排序"
hermes -z "总结一下 ~/project/README.md"      # -z：只打印最终答案，无装饰，适合管道
```

### 2.3 拖文件

桌面 App 支持**直接把文件/文件夹拖进聊天框**，然后用自然语言指挥它：

```
这是刚拖进来的 sales.xlsx，读出全部数据，按月份汇总销售额，
找出环比下降超过 20% 的月份，结果写成 report.md 给我。
```

---

## 3. 五个核心概念（这也是它跟别家最大的区别）

### 3.1 工具（Tools）

它能调用的"手"。本机已启用的主要工具：终端、文件读写、网页搜索/抓取、真实浏览器、子代理、定时任务、记忆、技能、语音、图像生成（部分缺 API key，见第 7 节）。

查看与开关：

```bash
hermes tools list
hermes tools disable browser     # 关掉某个工具集
```

会话内也可以：`/tools`、`/toolsets`。

**要点**：需要联网/开浏览器/跑脚本的活，它会自己挑工具，你不用指定。只有当某个工具被关掉或缺少依赖时才会说"做不到"。

### 3.2 技能（Skills）

**技能 = 一份写好的操作手册**，只在相关时加载，教它"这类活在我们这儿该怎么做"。

本机已内置 ~30 个技能（`hermes skills list` 可看），例如：
`pdf`（PDF 生成/填写/OCR）、`microsoft-office`（Word/Excel/PPT）、`github`、`arxiv`、`manim-video`、`humanizer`、`systematic-debugging`…

```bash
hermes skills list                 # 我装了哪些
hermes skills browse               # 技能商店
hermes skills search pdf           # 搜索
hermes skills install <ID或URL>    # 安装
```

**大招**：干完一件复杂的活之后，让它把这套流程存成技能，下次自动复用：

```
把你刚才排查这个 bug 的完整流程（包括踩的坑）存成一个技能，
名字叫 debug-windows-node，以后我遇到类似问题你自动用。
```

### 3.3 记忆（Memory）

分两层，别混：

- **用户档案**：你是谁、偏好、环境（"我主要用 Windows + git-bash，Python 项目"）
- **我的笔记**：环境坑、约定、教训

它在合适的时机**自己**写记忆。你也可以直接命令：

```
记住：以后给我写代码一律用中文注释，变量名用英文。
```

```bash
hermes memory status               # 看记忆后端状态
```

会话内用 `/memory` 可以审查/批准待写入的记忆。**记忆有字数上限**，所以它只存"每次会话都用得上"的事实；一次性任务的过程不会进记忆（会进技能或会话记录）。

### 3.4 会话（Sessions）

所有对话存在 SQLite 里（`state.db`），可全文搜索、可恢复、可分支。

```bash
hermes --continue                  # 接着上次的聊
hermes --resume <会话ID或标题>      # 恢复指定会话
hermes sessions list               # 列出历史
hermes sessions browse             # 交互式浏览
```

会话内斜杠命令（桌面/CLI 通用）：`/new` 新会话、`/status` 看 token 用量、`/compress` 压缩上下文、`/branch` 分叉、`/undo` 回退一轮、`/model` 临时换模型。

### 3.5 子代理（delegate_task）

一个任务可以拆给**多个隔离的子代理并行**干，各自有独立上下文，最后只把结论回传给你。适合"同时调研 5 个东西"这类活：

```
同时调研这三个 Python 异步框架的最新版本、star 数、维护状态，
让三个子代理并行去查，最后给我一张对比表。
```

⚠️ 子代理的汇报是**自述**，不是已验证事实。对"上传成功/已发布"这类结论，要求它给可验证的句柄（URL、绝对路径），并让它自己读回来确认。

---

## 4. 跟着做：10 个练习（从易到难）

> 每个练习都写了**目标 / 怎么发 / 你应该看到什么**。建议按顺序做一遍，30 分钟内能全部跑完。

### 练习 1 · 自检环境

```bash
hermes status --full
hermes doctor
```

**你会看到**：模型、provider、gateway 状态、各工具是否可用。
**本机实测结果**：`deepseek-v4-pro`（DeepSeek）在跑，gateway 运行中；`vision` / `video` / `image_gen` / `x_search` 因缺依赖或 API key 而不可用，`hermes doctor --fix` 建议跑一次配置迁移。

👉 跟着做：运行 `hermes doctor --fix`，然后再 `hermes doctor` 对比差异。

---

### 练习 2 · 让它读你的文件并总结（最常用）

在桌面聊天框：

```
读一下 C:/Users/ASUS/AppData/Local/hermes/config.yaml，
用中文给我解释：现在用的是哪个模型、哪些工具集开着、
有没有明显配错的地方。不要改任何东西。
```

**学到**：给**绝对路径**（Windows 下用正斜杠 `/` 最稳），并明确"不要改"——只读任务要说出边界。

---

### 练习 3 · 让它写代码并**真实运行**

```
在 C:/Users/ASUS/demo/ 下写一个 Python 脚本 sysinfo.py，
输出 CPU 核心数、内存占用、磁盘剩余空间，格式化成对齐的表格。
写完立刻运行它，把真实的运行结果贴给我。
如果我机器上缺依赖，你自己装。
```

**你应该看到**：文件真的出现在 `C:\Users\ASUS\demo\sysinfo.py`，并且它贴出的是**真实执行输出**（不是编的）。
**学到**：这就是"交付物"原则——要文件、要跑通的结果，而不是"你可以这样写"。

---

### 练习 4 · 验证记忆是否真的生效

第一轮：

```
记住两条我的偏好：1) 我在这台机器上用 git-bash，别给 PowerShell 命令；
2) 回复默认用中文，代码块保留英文。存进长期记忆。
```

然后**开一个新会话**（`/new` 或关掉重开），只问：

```
我上次让你记住的偏好是什么？
```

**学到**：记忆是跨会话的。如果它答不上来，说明写入被审批门挡住了 → `/memory pending` 看队列。

---

### 练习 5 · 用技能干一件专业活

```
用 pdf 技能，把 C:/Users/ASUS/demo/ 下的所有 .txt 文件合并成一个 PDF，
加页码和目录，输出 report.pdf。
```

**学到**：它不会自己"猜"该怎么做，而是先加载 `pdf` 技能读操作手册，再执行。你也可以强制预加载：

```bash
hermes chat --skills pdf,microsoft-office -q "把这份 Word 转成排版好的 PDF"
```

---

### 练习 6 · 定时任务（cron）

```bash
hermes cron create "0 9 * * *" "检查 C:/Users/ASUS/demo 目录下今天有修改的文件，生成一份变更摘要" --name "每日变更摘要" --deliver local
```

`0 9 * * *` = 每天 9:00。`--deliver local` = 结果留在本地会话。

```bash
hermes cron list
hermes cron run <ID>       # 立刻试跑一次，别等明天
hermes cron remove <ID>
```

**学到**：定时任务必须有**完全自包含**的 prompt（它开跑时没有你此刻的上下文），写清路径和产物。

---

### 练习 7 · 并行子代理

```
帮我并行调研 3 个开源 OCR 方案（Tesseract、PaddleOCR、docTR）：
最新版本、许可证、中文识别准确率评价、典型坑。
用三个子代理并行查，最后合成一张对比表 + 一句推荐。
```

**学到**：任务可以"扇出"。你看它调了多少个子代理，可以用 `/agents` 看运行中的任务。

---

### 练习 8 · 换模型 / 换主题 / 换人格

```bash
hermes model                       # 交互式选模型+provider
hermes config set display.skin <名字>   # 换主题（立刻生效，不用重启）
hermes skin list
```

会话内：`/model gpt-5`（本次会话临时换）、`/reasoning high`（调推理强度）、`/fast`（快速档）。

**学到**：模型是**可换的零件**。贵的模型做规划，便宜的做批量。

---

### 练习 9 · 项目上下文文件（长期项目必做）

在项目根目录建 `AGENTS.md`，写下这个项目的规矩：

```markdown
# 项目约定
- 技术栈：Python 3.12 + FastAPI + PostgreSQL
- 测试：pytest，提交前必须 `pytest -q` 全绿
- 代码风格：ruff check 必须过；禁止 print 调试，用 logging
- 不要改动 migrations/ 下的历史迁移文件
```

然后在该目录启动 `hermes`，它会**自动读入**这些规则并一直遵守。

**学到**：这是让 agent"记住项目规矩"的最低成本方式，比每次口述靠谱得多。

---

### 练习 10 · 接一个消息平台（可选，威力最大）

```bash
hermes gateway setup      # 选平台（Telegram/Discord/Slack/飞书/微信/邮件…）
hermes gateway start
```

接好之后，你在手机上给它发一句话，它就能**在你的电脑上**跑任务、改文件、把结果发回手机。

```bash
hermes send --to telegram "构建完成了，日志在 ~/build/last.log"
```

**学到**：同一套工具能力延伸到手机端。这是 Hermes 和网页版 AI 最大的体验差距。

---

## 5. 提示词写法：让它真的把活干成

### 三件套模板

```
【目标】做什么（一句话，动词开头）
【约束】在哪做、不能碰什么、用什么技术/格式
【验收】怎么算完成（要看到什么结果、放哪个文件）
```

实例：

```
【目标】把 api_server.py 里所有同步数据库调用改成异步
【约束】只改这个文件；保持现有函数签名；不要动测试
【验收】pytest -q 全绿，并把改动前后的耗时对比贴出来
```

### 四个高频失误

| 失误 | 改法 |
|---|---|
| "帮我优化一下代码" | 说清优化什么：启动速度？内存？可读性？给出可测指标 |
| 一次给 10 个不相关的任务 | 拆开说，或明确"先做 A，做完停下等我说" |
| 不给验收标准 | 加一句"做完自己验证，把验证输出贴给我" |
| 出错只发"失败了" | 把**完整报错**贴回聊天，它需要原文才能定位 |

### 几句万能的追加指令

- `先别动手，把方案讲给我听，我确认后再执行。`
- `做完自己验证一遍，把真实的命令输出贴给我，不要复述。`
- `这件事以后还会重复，做完存成技能。`
- `如果中间有需要我决策的地方，停下来问我，别自己猜。`

---

## 6. 进阶地图

| 想要 | 命令/入口 |
|---|---|
| 隔离多个身份（工作/个人） | `hermes profile create work` → `hermes -p work` |
| 接外部工具（数据库、Figma、Sentry…） | `hermes mcp catalog` → `hermes mcp install NAME` |
| 让 IDE（VS Code/Zed）用上它 | `hermes acp` |
| 给它加界面/挂件 | 桌面插件 `~/.hermes/desktop-plugins/`，TUI 挂件 |
| 事件驱动（webhook 触发） | `hermes webhook subscribe ...` |
| 把 Hermes 当 OpenAI 兼容 API 用 | `hermes proxy`（本机起一个免 key 端点） |
| 多智能体协作看板 | `hermes kanban` |
| 长期记忆换后端 | `hermes memory setup` |

**注意**：Hermes 功能极多，别凭记忆判断"它做不到"。完整索引在
<https://hermes-agent.nousresearch.com/docs/llms.txt>，问它"能不能做 X"，它会去查。

---

## 7. 排障

| 现象 | 处理 |
|---|---|
| 某个工具说"不可用" | `hermes doctor`；本机 `vision`/`video` 缺系统依赖，`image_gen` 缺 key |
| 行为很怪、怀疑配置坏了 | `hermes --safe-mode`（禁用所有自定义）对比 |
| 命令被拦下要审批 | 正常安全机制；本项目内可 `/approvals` 加白，或临时 `--yolo`（慎用） |
| 上下文快满了 | `/compress`，或 `/new` 开新会话 |
| 卡住/死循环 | `/stop` 杀后台进程；`hermes pause` 紧急全停 |
| 想看它到底干了什么 | `hermes logs -f`，会话内 `/verbose` |
| 改配置 | **永远用** `hermes config set KEY VAL`，不要手改 `config.yaml`（一个缩进就能搞坏） |

日志/配置位置：
`C:\Users\ASUS\AppData\Local\hermes\{config.yaml, .env, logs\, state.db, skills\}`

**红线**：密钥只进 `.env`，普通设置只进 `config.yaml`。

---

## 8. 速查表

```bash
# 入口
hermes                     # 终端对话
hermes desktop             # 桌面 App
hermes --tui               # 终端 UI
hermes dashboard           # 网页后台

# 单次
hermes chat -q "..."       # 一问一答
hermes -z "..."            # 只要答案，适合管道/脚本

# 配置
hermes setup / model / doctor / status [--full]
hermes config set KEY VAL

# 能力
hermes skills list|browse|search|install
hermes tools list|enable|disable
hermes mcp list|add|catalog
hermes memory status

# 自动化
hermes cron list|create|run|remove
hermes webhook subscribe|list

# 会话
hermes --continue / --resume ID / sessions list

# 多身份
hermes profile list|create|use
```

会话内常用：`/new` `/status` `/model` `/compress` `/memory` `/skills` `/tools` `/agents` `/stop` `/help`

---

## 9. 一周上手路线

| 天 | 做什么 |
|---|---|
| 第 1 天 | 练习 1–3：自检、读文件、写并运行脚本。建立"它真会动手"的直觉 |
| 第 2 天 | 练习 4–5：记忆 + 技能。让它记住你的偏好和工作方式 |
| 第 3 天 | 练习 6：配一个每天自动跑的定时任务 |
| 第 4 天 | 练习 7：用子代理并行做一次多路调研 |
| 第 5 天 | 练习 9：给主力项目写 `AGENTS.md` |
| 第 6 天 | 练习 10：接一个消息平台，体验手机指挥电脑 |
| 第 7 天 | 回头让它"把这一周的重复劳动存成 2 个技能" |

---

**文档**：<https://hermes-agent.nousresearch.com/docs>
**一句总结**：少问"怎么办"，多说"去做，做完给我看结果，并把流程存下来"。
