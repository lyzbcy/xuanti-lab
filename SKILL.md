---
name: xuanti-lab-dev
description: 毕设选题工具站的开发技能。当用户要开发、修改、排障、更新该网站时使用。
---

# 毕设选题工具站（xuanti-lab）开发 Skill

## 项目一句话
帮设计类毕设做选题发散的两个交互工具（发散器 + 思维导图）+ 门户页组成的纯静态网站，部署在 GitHub Pages，给捞鱼和星星布丁（及同学）用。

## 技术栈
纯 HTML/CSS/JS 单文件页面，无构建、无依赖；GitHub Pages 托管（main 分支根目录）；版本核对走根目录 version.json + 页内 `PAGE_VERSION` 常量（强制刷新组件，规范副本在 reference/强制刷新组件.md）。

## 目录地图
- SKILL.md — 本文件
- docs/ — 知识库（先读 agent.md）
- reference/ — 强制刷新组件.md（组件规范副本，保证项目自包含）
- index.html — 门户页（含全量更新日志渲染）
- fashe.html — 选题发散器（四轴摇号 + 收藏打分，数据存 localStorage）
- mindmap.html — 发散思维导图（SVG 树 + 随机路径高亮）
- version.json — 全站版本号与更新日志（唯一权威来源）

## 开发流程（任何 Agent 必须遵守）
1. 开发任何功能前，先读 docs/ 下对应文档；没有就先建。
2. 改动完成后：更新代码 + 更新模块文档 + 更新版本号 + 推送远端，四者缺一不算完成：
   - 版本号位置：`version.json` 的 `version`（整数递增）与 `changelog`（新条目插最前），**以及所改页面里的 `PAGE_VERSION` 常量**，必须同步更新。
   - 只改 version.json 不改页面常量（或反之）会导致用户端循环刷新或收不到更新，属于红线事故。
3. 本地源头文件在 `E:\共享\星星布丁\毕业设计\选题发散器.html` 与 `选题思维导图.html`（未匿名化的全量版）；同步改动时先改本地版，再把改动套用到站内页面并保持匿名化。
4. 日志约定：纯前端 console，等级 `[DEBUG]/[INFO]/[WARN]/[ERROR]` 前缀（详见 docs/tech.md）。

## 红线
- `version.json` 与各页面 `PAGE_VERSION` 必须同步更新（原因见上）。
- **毕业设计文件夹里的开题报告 PDF/PPT/DOC 是别人的私人资料，永远不要复制进本仓库或推送任何远端。**
- 站内页面不得出现真实同学姓名、导师姓名（用「同学A-E」「导师组」代替）——本仓库是公开的。

## 当前状态
- 版本：1 ｜ 进度详见 docs/roadmap.md
