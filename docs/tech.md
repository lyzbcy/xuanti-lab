> 现状：稳定 ｜ 负责人：捞鱼（+Agent） ｜ 最后更新：2026-09-15

# 技术方案

## 架构
纯静态三页 + 一份版本清单，无构建无依赖，GitHub Pages 从 main 根目录直出。

```
浏览器 ── fetch version.json?t=<ts>（防缓存）── 版本核对
        └─ 页内 PAGE_VERSION 常量参与比对
```

## 选型决策
| 决策 | 选择 | 备选 | 原因 |
|---|---|---|---|
| 页面文件名 | ASCII（fashe/mindmap） | 中文名 | Pages 子路径 + URL 分享免百分号编码 |
| 版本号形态 | 整数递增 | semver | 对齐 JNU-Toolkit 参考实现，静态页无需语义化版本 |
| 数据存储 | localStorage（键 `bishe_fasan_v1`） | 无后端 | 纯静态约束；换浏览器/设备不跟随是已知取舍 |
| 思维导图 | 手写 SVG 树 | markmap CDN | 零依赖、离线可用、样式可控 |

## 强制刷新组件（核心约定）
规范原件：`reference/强制刷新组件.md`（复制自 E:\共享\tools\软件开发\自用静态网页组件\）。

- 每页嵌入：`PAGE_VERSION` 常量 + `checkVersion()` + 右上角 `.refresh-box`（一键刷新一级按钮 + 最近更新一行）。
- 远端：`version.json` 的 `version`（整数）、`date`、`changelog`（新条目在最前）。
- 防循环：sessionStorage 键 `xuanti_refreshed_for`，同一目标版本每会话最多自动刷新一次；用户可手动点一键刷新兜底。
- fetch 一律带 `?t=Date.now()` 防缓存；刷新用 `location.replace` + `?v=` 参数破缓存。
- **改版铁律**：`version.json` 与所改页面的 `PAGE_VERSION` 必须同步更新。

## 日志约定
纯前端 console，统一等级前缀：`[DEBUG]` 开发排查 / `[INFO]` 关键流程 / `[WARN]` 可恢复异常 / `[ERROR]` 功能不可用。面向用户的等待与反馈一律走页内 toast/横幅，不用 console 代替。

## 匿名化约定（公开仓库红线）
站内页面引用开题样例时：真实姓名 → 同学A（绘本）/ B（文创）/ C（动画）/ D（装置）/ E（社群）；导师 → 「导师组」；不出现学校全称。本地全量版（含真名）只存在于 E:\共享\星星布丁\毕业设计\ 的原件里，永不入库。
