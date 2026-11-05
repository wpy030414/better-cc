# SPECS — 模块规格索引

每个模块一份 spec，说明「要做什么、做到什么程度算完成」。规格定稿后不再保留悬而未决的讨论，讨论过程见 `docs/researches/`。

## 登记规则

- 一个模块一个文件，命名 `module-<kebab-name>.md`（如 `module-auth-gateway.md`）。
- 模块名必须与 `docs/ARCHITECTURE.md` 的「核心模块」表一致，不得出现架构里没有的模块。
- 状态变更时只改索引行的状态，不在 spec 正文里写进度日志。

## 条目

| 模块 | 文件 | 一句话职责 | 状态 | 更新日期 |
|------|------|------------|------|----------|
| 交互式安装向导（src/index.ts） | module-wizard.md | 四阶段编排：Init（检测/备份/核心安装）→ 多选 → 依赖链执行 → 动态汇总；生成 wrapper/trust-poke/启动器 | 已实现 | 2026-11-05 |
| 主题与共享定义（src/theme.ts） | module-theme.md | Sakura Pink 配色/终端主题/Claude 主题、PowerClaude profile 工厂与背景图查找的单一事实源 | 已实现 | 2026-11-05 |
| CLI 探测领域服务（src/claude-installation.ts） | module-claude-installation.md | 跨安装源分层探测 Claude Code CLI（native/npm/path），纯逻辑、环境全注入 | 已实现 | 2026-11-05 |
| Claude Code 主题写入器（src/claude-settings.ts） | module-claude-settings.md | 写 themes/sakura-pink.json + settings.json theme 字段，Windows 重启 daemon | 已实现 | 2026-11-05 |
| Windows 安装链路（src/terminal/windows.ts） | module-windows-terminal.md | settings.json 定位/读写/备份、PowerClaude profile 去重安装、Sakura Pink 主题应用 | 已实现 | 2026-11-05 |
| macOS Terminal.app 安装器（src/terminal/macos.ts + macos.swift） | module-macos-terminal.md | 退出 Terminal → 刷 cfprefsd → Swift 直写偏好（bookmark + 合成背景图）→ 冷启动 | 已实现 | 2026-11-05 |
