# 更新日志

## v0.2.1 — 2026-10-29

**修：工作层时间戳补全年份**

- `stamp()` 从 `MM-dd HH:mm` 改为 `yyyy-MM-dd HH:mm`
- 为什么：写入端写 `MM-dd`、检查端（verify）要求 `yyyy-MM-dd`，两端不一致 → 检查报假绿/假红。同批把 `notebook.ps1` 的 stamp 也改了
- 注意：`package.json` 必须无 BOM（加了 BOM 会让 bundle 加载失败：`Unexpected token '﻿'`）

## v0.2.0 — 2026-10-28

**新增：`notebook_tomb`（第五个动词）**

- 给一条作废的旧规矩立墓碑，三段式：`旧说法|为什么作废|现在按什么来`
- 自动补日期，写进 `3-墓碑.md`；文件不存在就先建表头
- 为什么加：删除不管用 —— 旧规矩还躺在旧笔记里，下次读到会照着错的做

**修：`package.json` 不带 BOM**

- 加 BOM 会让 JSON 解析失败，整条 bundle 变 error 状态（diagnostic: `Unexpected token '﻿'`）
- 只有 `.ps1` 需要 BOM，`.json` 一律无 BOM

## v0.1.0 — 2026-10-27

**首版：四个动词**

- `notebook_wake` — 读核心层（我是谁、要什么、纪律、本机陷阱）
- `notebook_work` — 在工作层追加一条「在做什么」
- `notebook_pit` — 记一个坑，三段式：`现象|根因|修法`
- `notebook_close` — 收工标记，提醒跑快照和备份

**设计取向：不给参数，给习惯**

- 参数是给不认识的人用的；每天就是这四步，做成动词比做成配置快
- 分层固定：`0-核心` 每次读 / `1-工作` 读一屏 / `2-档案` 按需查

**修：必须声明 `inject=['tools']`**

- 不写 inject 就取 `ctx.tools` 会抛，entry 整条失败，界面只显示「异常」
- 真实原因在 `plugin_manager install_bundle` 的 diagnostic 字段里
