# better-cc 🌸

> 把终端与 Claude Code 一起换成樱花粉主题——PowerClaude 是为终端创建的配置名。

## 这是什么？

**better-cc** 是一套跨平台配置方案，使用 TypeScript 编写，实现：

- **Windows Terminal** 中新增专属终端配置（名为 **PowerClaude**），PowerShell 直接启动 [Claude Code CLI](https://github.com/anthropics/claude-code)
- **Claude Code CLI** 自定义主题（基于 `light-daltonized` 明亮色盲，只覆盖需要变粉的颜色）
- 交互式安装向导，**Windows / macOS 双平台**完整支持（终端 + Claude Code 一次配齐）

## 为什么存在？

- 背景 / 动机：终端外观、启动行为、Claude Code 主题分散在三份配置里，手工改写繁琐易错、重装系统后无法快速复原；新版 macOS Terminal.app 又不再认外部导入的明文背景图路径。本项目把这套「粉色环境」沉淀成一条命令——自动备份、幂等可重跑、双平台共用同一份 `public/` 背景图约定。

## 如何安装和运行？

- 前置要求：
  - **Windows**: Windows 10/11 + [Windows Terminal](https://aka.ms/terminal-download)（推荐 1.20+）
  - **macOS**: Terminal.app + Claude Code CLI（安装会自动直写偏好，过程中会退出并重启 Terminal）
  - [Node.js](https://nodejs.org/) 26+（原生 TypeScript 运行）
  - Claude Code CLI：`npm install -g @anthropic-ai/claude-code`
- 安装步骤：`pnpm install`
- 运行 / 启动：`pnpm run apply`（交互式向导，唯一参数 `-h/--help`）

## 当前状态

- 阶段：开发中（个人工具，随 Claude Code / 终端版本跟进适配）
- 已知限制：
  - 终端部分仅支持 Windows Terminal 与 macOS Terminal.app，不支持 iTerm2 / VS Code 等其他终端
  - macOS 安装会主动退出并冷启动 Terminal.app（直写偏好的硬前提）
  - Claude Code 主题 token 随上游版本变化，可能需要跟随适配
  - 备份文件自动累积，不自动清理

## 核心技术

- 语言 / 框架 / 关键依赖：TypeScript（strict + ESM），Node.js 26+ 原生 TS 直跑（无 tsx）；`@clack/prompts`（交互界面）、`picocolors`（终端着色）、`typescript`（仅类型检查）

## 恢复默认

```powershell
# Windows：从备份恢复（路径按 ADR-010 多版本解析，以下为商店稳定版示例）
Copy-Item "$env:LOCALAPPDATA\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState\settings.json.bak-*" `
  "$env:LOCALAPPDATA\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState\settings.json"
```

```bash
# macOS：从备份恢复（先退出 Terminal.app）
defaults import com.apple.Terminal ~/com.apple.Terminal.bak-<时间戳>.plist
```

## 声明

本项目与 Claude Code CLI 或 Anthropic 官方无直接关联，仅提供配置方案。

> 完整文档见 `docs/`（PRD / ARCHITECTURE / DECISIONS / specs / researches）。
