# Figma 使用指南（每步含示例）

> 适用版本：Figma 桌面版 / 网页版。快捷键以 **Windows** 为例，macOS 把 `Ctrl` 换成 `Cmd`、`Alt` 换成 `Option`。
> 本指南所有示例都可以在你**现在这台电脑已打开的 Figma**里直接照做。
> 关联笔记：[[Obsidian使用指南]]

---

## 0. 先看你机器上 Figma 现在的状态

打开 Figma 桌面版后（本机截图见下），当前界面是**文件浏览器（File Browser）**，不是编辑器：

![[Figma-主界面截图.png]]

截图里能确认的信息，后面每一步都会用到：

| 位置 | 你机器上的实际内容 | 说明 |
|---|---|---|
| 左上角头像 | `chuzhufu` | 当前登录账号，个人空间叫 Personal |
| 左侧栏第二块 | `chuzhufu's team`（蓝标 `Free`） | 免费计划团队 |
| 左侧栏 | `Recents` / `Community` / `Drafts` / `All folders` / `Resources` / `Trash` | 最近、社区、草稿、全部文件夹、资源、回收站 |
| 顶部按钮 | `Create`、`Share`、`Export`图标、`Play`▶ | 新建文件、分享、导出、打开原型演示 |
| 中间列表 | `Untitled`（2 个月前编辑）、`chuzhufu's team library`（团队库） | 团队文件夹里已有 2 个文件 |
| 右上角 | `All types` / `Last modified` / 列表-网格切换 | 排序与视图切换 |

**结论**：你现在处在「Team folder」里，接下来示例就用这个 `Untitled` 空白文件当画布。

---

## 1. 新建文件：从文件浏览器进编辑器

**操作步骤**

1. 在文件浏览器点右上角蓝色 **`Create`**（或 `Drafts` → `+`）
2. 选 **Design**（Figma 设计文件；Jam 是白板、Slides 是演示稿）
3. 文件自动打开，名字是 `Untitled`，直接双击标题可改名

**示例**

```text
Create → Design
双击左上角 "Untitled" → 输入：登录页 - 练习
右侧 Share 旁边的位置会显示 "Only you"（仅自己可见）
```

**提示**：`Drafts` 里的文件默认只有你自己能看，想给团队看要 **Move to team** 或直接 `Share` 链接。

---

## 2. 认识编辑器界面

进入设计文件后，屏幕被切成 4 块：

| 区域 | 位置 | 主要内容 |
|---|---|---|
| 工具栏 | 顶部（悬停文件标题后出现） | 移动、框架、形状、钢笔、文字、评论、Dev Mode |
| 图层面板 | 左侧 | Page、图层树、Assets（组件/样式） |
| 画布 | 中间 | 无边界，按 `Shift+1` 一键回到全部内容 |
| 属性面板 | 右侧 | 对齐、尺寸、填充、描边、效果、原型、导出 |

**示例：验证三个面板联动**

1. 按 `F`，在画布拖出一个 `400 × 300` 的框 → 左侧多出 `Frame 1`
2. 点中它，右侧 **Design** 标签里把 `W` 改成 `1440`
3. 左侧图层名双击改成 `Desktop` → 画布上的标签同步变成 `Desktop`

---

## 3. 画布导航：缩放与移动

| 目的 | 操作 |
|---|---|
| 按住空格拖动 | 平移画布（最常用） |
| `Ctrl + 滚轮` | 以鼠标为中心缩放 |
| `Shift + 1` | 缩放到全部内容（Fit to screen） |
| `Shift + 2` | 缩放选中物体 |
| `Shift + 0` | 100% 原始比例 |
| 滚轮 / 触控板双指 | 上下滚动（不缩放） |
| `Ctrl + \` | 隐藏/显示左右面板，看整体效果 |

**示例**

```text
打开 登录页 - 练习 → 按 Shift+1（一片空白居中）
按 F 拖出一个 1440×1024 的框架 → 按 Shift+2 铺满屏幕
双击框架名改成 "Desktop 1440" → 右上角缩放下拉选 50% 检查整体留白
```

---

## 4. 框架 Frame：Figma 的“画板”

框架是 Figma 的核心容器：可以导出、可以滚动、可以套原型的就都是 Frame。矩形（Rectangle）不是。

**操作步骤**

1. 按 `F`，右侧预设面板出现（Desktop / Tablet / Phone / Social Media…）
2. 点一个预设，或直接在画布拖出任意尺寸
3. 右侧面板勾选 **Clip content**，内容超出框架会被裁掉（做卡片、做手机屏必勾）

**示例**

```text
按 F → 选 "Desktop" 预设 1440 × 1024
名称改为：Desktop 1440
勾选 Clip content
里面再按 F 画一个 480 × 520 的框架 → 命名 LoginCard
```

**区别示例**：把 `LoginCard` 拖到 `Desktop 1440` 之外再拖回来，观察图层树——拖进去时它会缩进到 `Desktop 1440` 底下，说明已成为子层级。

---

## 5. 形状、填充、描边、圆角

| 形状 | 快捷键 |
|---|---|
| 矩形 | `R` |
| 椭圆 | `O` |
| 直线 | `L` |
| 多边形 / 星形 | 工具栏「形状」下拉 |

右侧 **Design** 面板常用项：

- **Fill**：纯色、线性渐变、图片、视频
- **Stroke**：边框，可设 1px 内/外/居中
- **Corner radius**：四角联动，点右侧图标可单独设角
- **Effects**：Drop shadow / Inner shadow / Layer blur
- **数值可直接输入算式**：`400-32` 回车得到 `368`

**示例：做一个卡片底板**

```text
R 拖出 480 × 520 → 圆角 24
Fill：FFFFFF，Opacity 100%
Stroke：Inside，1px，#E5E7EB
Effects → Drop shadow：X 0 / Y 8 / Blur 24 / Spread 0，颜色 #000000 @ 12%
```

---

## 6. 文字：排版的最小单位

**操作步骤**

1. 按 `T`，在画布点一下（自动宽度）或拖一个框（固定宽度）
2. 输入内容，右侧选字体、字重、字号、行高、字间距
3. 「文本自动尺寸」下拉三选一：`Auto width`（随文字变宽）、`Auto height`（定宽换行）、`Fixed size`

**示例：卡片里的标题**

```text
T → 拖出宽 400 的框 → 输入 "登录你的账号"
字体 Inter，字重 Semi Bold，字号 28，行高 36，颜色 #111827
尺寸模式选 Auto height
再按 T 输入 "使用邮箱继续" → 字号 14，行高 20，颜色 #6B7280
```

**字号等级建议（可直接抄）**

| 用途 | 字号 / 行高 |
|---|---|
| 页面标题 | 32 / 40 |
| 卡片标题 | 28 / 36 |
| 正文 | 16 / 24 |
| 辅助说明 | 14 / 20 |
| 标签 / 角标 | 12 / 16 |

---

## 7. 图片、图标与蒙版

- **拖入图片**：直接把文件从资源管理器拖到画布，会成为矩形填充（Image fill）
- **裁剪模式**：双击图片进入 crop，四周出现裁剪柄，拖动调整可见区域，`Esc` 退出
- **蒙版（Mask）**：选中「形状 + 图片」，按 `Ctrl + Alt + M`，上方形状成为蒙版
- **图标**：左侧 `Assets` 面板搜社区图标库，或从 `Community` 复制现成图标组件

**示例：头像圆形头像**

```text
O 画 64 × 64 圆 → 拖入 portrait.jpg 到圆内（自动填充）
双击图片微调位置 → Esc 退出裁剪
选中圆 → Fill 面板里把图片的 Fill mode 改成 Fill（铺满）而不是 Fit
```

---

## 8. 图层组织：命名、编组、查找

| 操作 | 快捷键 |
|---|---|
| 编组 | `Ctrl + G` |
| 解组 | `Ctrl + Shift + G` |
| 选中内容装进 Frame | `Ctrl + Alt + G` |
| 重命名 | `Ctrl + R` |
| 隐藏 / 锁定 | `Ctrl + Shift + H` / `Ctrl + Shift + L` |
| 复制 | `Ctrl + D`（Alt+拖动同样效果） |
| 复制属性（填充/描边/效果） | `Ctrl + Alt + C` / `Ctrl + Alt + V` |
| 搜索图层 | 左侧面板顶部放大镜 |

**示例**

```text
框选三个输入框 → Ctrl+G → Ctrl+R 改名 "InputGroup"
选中 InputGroup → Ctrl+Alt+G → 变成框架 "InputGroup"，勾 Clip content
Ctrl+C 其中一个输入框 → 到画布按 Ctrl+Alt+V，只粘贴填充/描边/圆角属性
```

**命名规则（团队协作必备）**：`类型/用途/状态`，例如 `Button/Primary/Default`、`Input/Email/Error`。

---

## 9. 自动布局 Auto Layout：不用手摆位置

自动布局 = 容器按内容自动排布，改文案、加条目都不用手动挪。

**操作步骤**

1. 选中若干元素（或一个 Frame），按 `Shift + A`
2. 右侧出现 **Auto layout** 区块：`Direction`（水平/垂直）、`Gap`、`Padding`、对齐
3. 容器尺寸三选一：`Hug contents`（包住内容）、`Fixed`（固定）、`Fill container`（撑满父级）

**示例：把卡片内容改成自动布局**

```text
选中 LoginCard 里 标题 + 副标题 + 2 个输入框 + 按钮 → Shift + A
Direction：Vertical，Gap：24
Padding：上下 40，左右 40
宽度：Fixed 480；高度：Hug contents
结果：把标题文案改长/删掉一行，卡片高度自动变化
```

**间距替代**：卡片里的「输入框 + 错误提示」这类紧密组合，先用 `Shift+A` 包成小容器（Gap 8），再放进大容器（Gap 24），层次比全靠 Gap 更清晰。

---

## 10. 约束 Constraints 与响应式

只有放在「非自动布局」框架里的子元素才有 Constraints（右侧面板底部）：

| 约束 | 效果 | 典型用途 |
|---|---|---|
| Left + Top | 钉在左上 | 卡片内元素 |
| Left & Right（Stretch） | 随宽度拉伸 | 输入框、分割线 |
| Center | 水平居中 | 弹窗内容 |
| Right | 钉在右侧 | 关闭按钮、角标 |

**示例**

```text
Desktop 1440 里放 LoginCard，Constraints 设为 Center
把 Desktop 宽度从 1440 改成 1200 → 卡片自动保持居中
输入框宽度设为 Fill container → 卡片变宽时输入框跟着变宽
```

---

## 11. 组件 Components 与实例

组件 = 母版；实例 = 引用。改母版，所有实例同步。

**操作步骤**

1. 选中设计好的元素，按 `Ctrl + Alt + K` → 变成组件（紫色四角图标）
2. 从左侧 `Assets` 面板拖到画布 → 得到实例（紫色描边、无四角）
3. 右键实例 → `Detach instance` 可断开（断开后不再同步，谨慎）

**示例**

```text
选中做好的按钮 Frame → Ctrl+Alt+K → 命名 "Button/Primary"
左侧 Assets 面板出现 Button/Primary → 拖两个实例到画布
改母版圆角 8 → 24 → 两个实例同时变
在实例上改文字 "登录" → "注册"（文字覆盖，只影响这个实例）
```

**覆盖规则**：文字、填充、图片可以单实例覆盖；几何属性（尺寸、间距）默认跟随母版，改成不同值会出现「重置」按钮。

---

## 12. 变体 Variants：一个组件管多种状态

**操作步骤**

1. 做好两个形状相似的状态（如默认按钮、悬停按钮）
2. 同时选中 → 右键 **Combine as variants**
3. 右侧 **Variant** 面板里改名，命名格式 `属性=值, 属性=值`

**示例**

```text
两个按钮：填充 #2563EB 与 #1D4ED8
同时选中 → Combine as variants → 组件名 "Button"
变体属性改为：State=Default / State=Hover，Size=Medium 统一
切换：选中实例，右侧 Variant 下拉切 State=Hover，秒变悬停态
```

**进阶**：加 `Size=Small/Large` 后就是二维矩阵，原型里做悬停/按下动画的基础。

---

## 13. 样式 Styles 与变量 Variables

**样式**（右侧面板四个小圆点图标 → `+`）适合颜色、文字、阴影的复用：

```text
选中标题文字 → Text 样式 "Heading/H1"（Inter Semi Bold 28/36）
选中卡片 → Effect 样式 "Shadow/Card"
以后改样式一次，全站同步
```

**变量**（左侧面板 `Local variables`）适合做明暗主题、品牌色：

```text
新建集合 "Color"
  color/bg/default = #FFFFFF
  color/text/primary = #111827
新建集合 "Radius"：radius/card = 24
再建模式 Dark：把 color/bg/default 改成 #0B0B0F
切换模式 → 整个界面从浅色变深色
```

**示例**：把卡片背景从写死的 `#FFFFFF` 改成绑定 `color/bg/default`，然后切 Dark 模式，卡片自动变黑。

---

## 14. 原型 Prototyping：让设计能点

**操作步骤**

1. 右侧切到 **Prototype** 标签
2. 选中触发元素（按钮），拖右侧的「圆形连接点」到目标框架
3. 在 **Interaction** 里设：`On click` → `Navigate to` → 目标框架
4. 点顶部 `▶`（或 `Ctrl + Alt + Enter`）演示

**示例：登录按钮跳转 + 悬停变色**

```text
框架：Login（登录页）、Home（首页）、Error（错误提示）
选中 Login 里的按钮 → On click → Navigate to：Home → Animation：Smart animate，300ms，Ease out
再给按钮加：While hovering → Change to：Button 变体 State=Hover
选中 Login 框架 → Overflow：Vertical scrolling（页面内容超出时可滚）
▶ 演示：点按钮 → 淡入切换；鼠标移到按钮 → 变深色
```

**常用交互速查**

| Trigger | Action | 场景 |
|---|---|---|
| On click | Navigate to | 页面跳转 |
| While hovering | Change to（变体） | 悬停态 |
| On drag | Navigate to（带 Smart animate） | 轮播、滑动页 |
| After delay 3s | Close overlay | 提示气泡自动消失 |
| On click | Open overlay + 位置居中 | 弹窗、菜单 |

---

## 15. 协作：评论、分享、跟随

**评论**

```text
按 C → 在画布任意位置点一下 → 输入 "@chuzhufu 这里的按钮间距是不是 16？"
左侧图层上方出现评论串，可 Resolve 关闭
```

**分享**

```text
右上角 Share → 输入对方邮箱 → 权限选 "Can view" / "Can edit"
或点 "Copy link" 发链接（可设 "Anyone with the link"）
演示模式：Share → Present → 观众自动跟随你的光标
```

**示例**：把 `登录页 - 练习` 分享给同事，权限 `Can view`，让他用 `C` 在按钮上留评论，你按评论里的 `@` 回复。

---

## 16. Dev Mode：交付给开发

**操作步骤**

1. 右上角切 **Dev Mode**（或 `Shift + D`）
2. 点任意图层 → 右侧给出尺寸、颜色（HEX/RGB）、间距、字体、可复制的 CSS/iOS/Android 代码
3. 需要切图的元素，在 Dev Mode 里标 **Ready for dev** 并 `Export`

**示例**

```text
Dev Mode 下点按钮实例 → 右侧读到：
  width 400 / height 48 / radius 8 / fill #2563EB
  Code 区：background: #2563EB; border-radius: 8px;
点卡片图层 → Export → PNG 2x → 得到 card@2x.png
```

---

## 17. 导出资源

| 场景 | 操作 |
|---|---|
| 单张图 | 选中 Frame → 右侧 `Export` → `+` 选 PNG 2x / SVG / PDF → Export |
| 批量 | 同时选中多个 Frame → Export 面板会列出全部 → 一次导出 |
| 快捷入口 | `Ctrl + Shift + E` |
| 整页 PDF | 文件菜单 `File → Export frames to PDF` |

**示例**

```text
选中 LoginCard → Export 1x（PNG）、2x（PNG）、SVG 三个尺寸
导出后文件名为 LoginCard.png / LoginCard@2x.png / LoginCard.svg
图标一律导出 SVG，图片位图一律 2x
```

---

## 18. 插件与社区

- `Community`（文件浏览器左侧）：搜 "Unsplash"、"Iconify"、"Remove BG"，点 `Open in…` 复制到自己的文件
- `Resources` → `Plugins`：安装后右键画布 → `Plugins → 运行`
- 常用三件套：**Unsplash**（配图）、**Iconify**（图标）、**Content Reel**（批量假数据）

**示例**：安装 Iconify → 选中一个 Frame → 运行插件 → 插入 `lucide:mail` 图标，颜色设为 `#6B7280`，尺寸 20。

---

## 19. Figma 连接 Codex（MCP）

一句话原理：把 Figma 当成 Codex 的「数据源」——Codex 通过 **MCP（Model Context Protocol）** 调用 Figma 暴露的工具，读取选中图层/链接的结构、变量、截图，然后直接生成代码；远程服务器还能反过来把代码写成 Figma 图层。

### 19.1 两条接入路线（先选一条）

| | 远程 MCP 服务器（**推荐**） | 桌面 MCP 服务器 |
|---|---|---|
| 地址 | `https://mcp.figma.com/mcp` | `http://127.0.0.1:3845/mcp` |
| 前提 | 浏览器登录授权即可，**Starter/免费计划可用** | 必须装 Figma 桌面版 **且** 有 Dev 或 Full 座位（专业版及以上付费计划） |
| 工具完整度 | 最全，含写回画布、读评论、搜设计系统库 | 只支持一部分（读设计为主） |
| 识别方式 | 必须在提示词里带**图层/框架链接** | 可以直接问「当前选中的框架」 |
| 生命周期 | 一直可用 | 只有 Figma 桌面版开着且启用了服务器时才可用 |

**你当前情况**：`chuzhufu's team` 是 Free 计划，且我查过本机 **3845 端口没有监听**（桌面服务器没开）。所以走**远程**这条路。

### 19.2 接入操作（每步带命令/点击路径）

**方式 A：命令行（Codex CLI）**

```bash
# 本机 codex.exe 在：C:\Users\ASUS\AppData\Local\OpenAI\Codex\bin\9e1da79431da526b\codex.exe
codex mcp add figma --url https://mcp.figma.com/mcp
codex mcp list          # 确认列表里出现 figma，Auth 列显示已授权
```

浏览器会弹 Figma 登录页 → 选对账号（`chuzhufu`）→ **Allow access**。这条命令会在 `~/.codex/config.toml` 里写下：

```toml
[mcp_servers.figma]
url = "https://mcp.figma.com/mcp"
```

不需要了就用 `codex mcp remove figma`。

**方式 B：Codex 桌面 app（你机器上装的就是这个）**

```text
左上角 Plugins → Figma 右边的 + → Install Figma → 弹窗点 Allow access
```

或手动添加（等价于桌面服务器那套 UI）：

```text
左下角 Settings → Settings → 左侧 MCP servers → Add server
类型从 STDIO 改成 Streamable HTTP
Name：figma-desktop
URL：http://127.0.0.1:3845/mcp
Save
```

**方式 C：桌面服务器本体（付费座位才用）**

```text
Figma 桌面版打开任意设计文件 → 不选中任何东西 → 按 Shift + D 进 Dev Mode
右侧栏 MCP server 区块 → Enable desktop MCP server
底部提示 "server is running"，地址 http://127.0.0.1:3845/mcp
```

**示例：验证是否真的连通**

```bash
codex exec "调用 whoami 工具，告诉我当前 Figma 账号、计划、座位类型"
```

预期输出类似：`chuzhufu / 2260712782@qq.com · Starter · Editor seat`。返回了真实信息 = 整条链路通了。

### 19.3 能用的工具（Codex 会自动选，不必记名字）

| 工具 | 作用 | 典型提示词 |
|---|---|---|
| `get_design_context` | 主工具：把图层转成设计上下文 + 代码（默认 React + Tailwind） | 「实现我的 Figma 选中内容，用 Vue」 |
| `get_metadata` | 轻量 XML 大纲：结构、尺寸、层级，不写代码 | 「只给我这个节点的图层结构和尺寸」 |
| `get_screenshot` | 对选区截图 | 「先截图，再对比我的实现差在哪」 |
| `get_variable_defs` | 列出选区用到的变量/样式 | 「导出这个框架的颜色和圆角变量为 CSS 变量」 |
| `download_assets` | 导出图片/图标原图 | 「把图标导成 SVG 到 src/assets/icons」 |
| `get_code_connect_map` | 读 Code Connect 组件映射 | 「这个按钮对应哪个代码组件？」 |
| `search_design_system` | 在团队库里搜组件/变量/样式（远程独有） | 「在团队库搜 Button，列出变体」 |
| `get_comments` | 读评论串（远程独有） | 「总结这个文件里未解决的评论」 |
| `use_figma` | 写回画布：新建/修改图层、组件、自动布局（远程 + Full 座位） | 「按这份 React 组件在 Figma 里建 LoginCard」 |
| `html_to_figma` | 把 HTML 变成 Figma 图层（远程独有） | 「把这个页面抓成 Figma 设计稿」 |

注意：客户端**不会真的打开** Figma 链接，它只是从中提取 `node-id` 交给 MCP。

### 19.4 使用示例（对着 §21 那个登录页练）

**示例 1：从框架生成代码**

```text
# 1. Figma 里右键 LoginCard 框架 → Copy link to selection，拿到形如
#    https://www.figma.com/design/AbC123/登录页-练习?node-id=12-345
# 2. 在 Codex 里：
实现这个设计：https://www.figma.com/design/AbC123/登录页-练习?node-id=12-345
技术栈 React + TypeScript + Tailwind，组件放 src/components/LoginCard.tsx，
输入框和按钮复用 src/components/ui 里已有的组件，不要引入新依赖。
```

**示例 2：只要结构，不要代码**

```text
用 get_metadata 看 https://www.figma.com/design/AbC123/...?node-id=12-345，
输出：每个图层的名字、尺寸、间距、圆角，用 markdown 表格。
```

**示例 3：要设计变量**

```text
用 get_variable_defs 读出这个框架用到的所有变量，
输出成 :root { --color-bg: ...; --radius-card: ... } 形式。
```

**示例 4：截图 → 自查实现**

```text
先 get_screenshot 保存这个框架截图，再检查我刚生成的 LoginCard.tsx：
对比圆角、内边距、字号、阴影，列出不一致的 5 条以内，并直接改代码。
```

**示例 5：导出资源**

```text
用 download_assets 把这个框架里的 lucide 图标导成 SVG 到 src/assets/icons/，
头像图片导出 2x PNG 到 src/assets/img/。
```

**示例 6：写回画布（远程 + Full 座位才可用）**

```text
用 use_figma 在文件 https://www.figma.com/design/AbC123/登录页-练习 里
新建 1440×1024 框架 "Login/Error"：一个 480 宽卡片，自动布局 Vertical / Gap 24 / Padding 40，
红色描边输入框 + 一行 12px 错误提示。
```

### 19.5 提示词写法（决定了输出质量）

1. **一条提示里给全四件事**：链接/`node-id`、技术栈、目标文件路径、可复用组件路径
2. **远程服务器必须带链接**，桌面服务器才认「我当前选中的框架」
3. **默认吐 React + Tailwind**；要别的就明说：`用 Vue`、`纯 HTML + CSS`、`iOS / SwiftUI`
4. **别选整页巨型框架**（1440×8000 那种）：先 `get_metadata` 看结构，再逐个组件做
5. **要变量就直说「只要变量，不要代码」**，否则它默认给代码
6. 想让生成结果贴合代码库：上 **Code Connect**，把 Figma 组件映射到真实组件文件

### 19.6 排错对照表

| 现象 | 原因 / 处理 |
|---|---|
| `codex mcp list` 里没有 figma | 配置没写进 `~/.codex/config.toml`；`codex mcp remove figma` 后重新 add，改完重启 codex |
| 工具列表为空 / 一直 loading | OAuth 没走完；重新 `codex mcp add` 并在浏览器点 Allow access，确认选的是 `chuzhufu` 账号 |
| `127.0.0.1:3845` 连不上 | 桌面版没开、没进 Dev Mode、没点 Enable desktop MCP server；免费计划本身不支持桌面服务器 |
| 只返回代码，读不到颜色/变量 | 提示词里明确「用 get_variable_defs，只返回变量」 |
| 500 / 卡住 | 选的框架太大或含视频、复杂实例；缩小选区或换 `node-id` 重试 |
| 生成的 class 名全是 `div` | 指定 `src/components/ui` 复用，或建 Code Connect 映射 |
| 要写回画布却报权限 | 写画布需要远程服务器 + **Full 座位**，当前 Free 计划只能读 |

---

## 20. 快捷键速查表

| 分类 | 快捷键 | 作用 |
|---|---|---|
| 工具 | `V` / `F` / `R` / `O` / `L` / `T` / `P` / `C` | 移动 / 框架 / 矩形 / 椭圆 / 直线 / 文字 / 钢笔 / 评论 |
| 布局 | `Shift + A` | 自动布局 |
| 布局 | `Ctrl + Alt + G` | 用 Frame 包裹选中内容 |
| 组件 | `Ctrl + Alt + K` | 创建组件 |
| 组件 | `Ctrl + Alt + B` | 分离实例（Detach） |
| 视图 | `Shift + 1` / `Shift + 2` / `Shift + 0` | 全览 / 看选中 / 100% |
| 视图 | `Ctrl + \` | 收起左右面板 |
| 视图 | `Ctrl + Y` | 线框模式（看结构） |
| 编辑 | `Ctrl + D` / `Alt + 拖动` | 复制 |
| 编辑 | `Ctrl + R` | 重命名图层 |
| 编辑 | `Ctrl + G` / `Ctrl + Shift + G` | 编组 / 解组 |
| 编辑 | `Ctrl + Alt + C` / `Ctrl + Alt + V` | 复制 / 粘贴属性 |
| 层级 | `Ctrl + ]` / `Ctrl + [` | 上移 / 下移一层 |
| 演示 | `Ctrl + Alt + Enter` | 打开原型演示 |
| 交付 | `Shift + D` | 切换 Dev Mode |

---

## 21. 实战：把 `Untitled` 做成一个登录页（全流程 15 步）

按顺序照做，每步都有确定的数值，做完就是一个能演示的登录页。

1. 文件浏览器点 `Untitled` 打开 → 双击标题改名 `登录页 - 练习`
2. `F` → Desktop 预设 → `W 1440 / H 1024`，命名 `Desktop 1440`，勾 Clip content
3. `F` → 拖出 `480 × 520` → 命名 `LoginCard`，圆角 24，填充 `#FFFFFF`
4. `R` → `400 × 48` → 命名 `Input/Email`，圆角 8，描边 1px `#E5E7EB`
5. `Ctrl + D` 复制出第二个输入框 → 改名 `Input/Password`，Y 轴间距 16（用自动布局更省事）
6. `T` → 输入 "登录你的账号"，Inter Semi Bold 28/36，颜色 `#111827`
7. `T` → 输入 "使用邮箱继续"，14/20，`#6B7280`
8. `R` → `400 × 48` → 命名 `Button/Primary`，圆角 8，填充 `#2563EB`；`T` 写 "登录"，白色 16px 居中
9. 选中按钮形状 + 文字 → `Ctrl + Alt + K` 变成组件
10. 选中卡片内所有元素 → `Shift + A` → Vertical / Gap 24 / Padding 40/40
11. 卡片宽度改 Fixed 480，高度 Hug contents；卡片在 Desktop 里 Constraints 设 Center
12. 复制一个 `LoginCard` 命名 `Error 状态`，把输入框描边改成 `#DC2626`，加一行提示 "邮箱格式不正确"（12/16，红色）
13. 新建 `Home` 框架 `1440 × 1024`，中间放一句 "欢迎回来"，作为跳转目标
14. Prototype 标签：选中登录按钮实例 → `On click → Navigate to: Home`，Smart animate 300ms
15. `▶` 演示，点按钮跳到 Home；Dev Mode（`Shift + D`）读按钮的 `#2563EB`、`radius 8`；Export 卡片 2x PNG

---

## 22. 常见问题

| 现象 | 原因与解决 |
|---|---|
| 免费计划受限 | 团队协作文件数量、版本历史长度、共享库有额度；文件浏览器左下 `Upgrade` 看详情。个人 `Drafts` 不受团队额度影响 |
| 改组件实例，其他实例不跟着变 | 该实例被 `Detach instance` 断开了，或只改了该项的 override；删掉 override（选中图层右侧「重置」）即恢复 |
| 字体显示成方框 / 提示缺失 | 用了本机没装的字体，`Assets → Text styles` 里替换为 Inter / 思源黑体，或让对方安装字体 |
| 自动布局里的元素跑位 | 检查 Direction 与 `Fill container` / `Hug contents` 三者的组合，不要给自动布局子元素写死绝对坐标 |
| 导出的图片模糊 | 导出用 2x/3x，或导出 SVG；位图素材本身分辨率不够也会糊 |
| 原型点了没反应 | 交互挂在形状上而不是框架上；或演示框选错了起始框架 |
| 图层面板一片 `Frame 123` | 养成随手 `Ctrl + R` 改名的习惯，图层名是协作里最低成本的沟通 |
