# PRD — better-cc（终端 + Claude Code 樱花粉一键美化）

## 产品目标

- 用一条命令把「终端 + Claude Code CLI」统一成樱花粉主题，并让终端启动即进入 Claude Code；过程自动备份、随时可恢复、可重复执行。

## 用户与使用场景

- 目标用户：
  - 主要：项目所有者本人——在 Windows 与 macOS 间切换、重度使用 Claude Code 的个人用户
  - 次要：想要同款「粉色终端 + 粉色 Claude Code」的其他 Claude Code 用户
- 典型场景：
  - 新机器 / 重装系统后，一条命令复原整套粉色环境
  - 换背景图：把新图丢进 `public/` 重跑一次安装即可
  - Claude Code 升级导致主题 token 变化后，跟随适配重写调色板

## 核心问题

- Windows Terminal `settings.json`、macOS Terminal.app 偏好、Claude Code 主题三处配置分散，手工改写繁琐易错，且无法跨平台复用
- 新版 macOS Terminal.app 不再认外部导入的明文背景图路径，背景图自动化安装存在真实技术障碍
- Claude Code 在新 git 仓库反复弹 workspace 信任提示，祖先信任链对 git 仓库不生效

## 功能及其意义

| 功能 | 解决什么 | 为什么需要 |
|------|----------|------------|
| PowerClaude 终端 profile / powerclaude profile（macOS） | 打开终端还要手敲 `claude` | 启动即进入 Claude Code，省一步 |
| 设为默认启动项 | 新开终端不是 PowerClaude | 让粉色环境成为默认体验（Windows 另含 Ctrl+Tab 最近使用优先、新标签菜单置顶） |
| Sakura Pink 终端主题（可选装） | 终端配色割裂 | scheme / 标签栏 / 窗口主题一次应用（macOS 配色烘焙在 profile 内） |
| Sakura Pink Claude Code 主题（可选装） | CLI 界面配色割裂 | 主题文件写入 `~/.claude/themes/`，基于 light-daltonized 最小覆盖 |
| System Prompt 定制（可选装） | 每次启动要手传 prompt | PATH 拦截（wrapper + 启动器），启动即携带定制 prompt |
| 信任工作区（可选装） | 新仓库反复弹信任提示 | 存量条目翻 true + home 信任根；新目录由 trust-poke 启动前自动补信任 |
| 自动备份 | 配置写坏无法回退 | 安装前强制留底，恢复有据 |
| 背景图（`public/` 自动查找，双平台共用） | 背景图配置门槛高 | 丢图即用，扩展名 / 路径自动处理 |
| macOS 无感安装 | `open` 导入弹窗、需手动操作 | 直写偏好 plist，全自动无弹窗 |

## 功能之间的关系

- 「核心配置安装」是其余功能的前置：Windows 的 profile + 背景图 + 默认项在 Init 阶段完成；macOS 的 profile 随「终端主题」步骤安装
- 四个可选功能相互独立、可多选，但按固定依赖链顺序执行（终端主题 → Claude 主题 → System Prompt → 信任工作区）
- 「背景图」复用同一套查找与缓存逻辑，两平台共用 `public/` 约定
- System Prompt 定制与信任工作区共用 `~/.powerclaude/` 下的 wrapper 机制（trust-poke 随 wrapper 每次 spawn 前执行）

## 范围与非目标

- 范围内：Windows Terminal、macOS Terminal.app、Claude Code CLI（主题 / System Prompt / 信任）三处配置的安装 / 更新 / 备份
- 范围外：其他终端模拟器、Linux 桌面终端、GUI 安装器、主题分发市场、自动更新
