---
type: meta
domain: 元
tags: [meta, log]
created: 2026-06-12
updated: 2026-06-12
sources: []
summary: "知识库按时间顺序的活动日志。"
status: 成长中
---

# 日志

## [2026-06-12] init | 知识库初始化

- 创建 `raw/articles/`、`raw/books/`、`raw/courses/`、`raw/other/` 来源分类目录
- 创建 `CLAUDE.md`，含学习场景专属规范（技术、语言、哲学）
- 创建 `index.md`，按领域分节的索引
- 创建 `log.md`
- 新增 `wiki/skills/` 存放实用技巧、`wiki/journal/` 存放定期反思
- 引入 `domain` 和 `status` 前置元数据字段
- 增加原始资料文件命名规范（日期/作者/平台前缀）
- 将 `index.md` 和 `log.md` 移至仓库根目录（属系统导航文件，非 wiki 内容）

**知识库定位：** 个人成长——技术、外语、哲学及其他智识探索。

## [2026-06-12] lint | 首次健康检查

- **修复**: `index.md` 和 `log.md` 的 `type` 从 `synthesis` 改为 `meta`（同时在 CLAUDE.md 中补充 `meta` 类型）
- **修复**: 索引条目链接格式改为全路径（`[[wiki/entities/Page]]`），避免跨目录重名
- **修复**: CLAUDE.md 中 `llm-wiki.md` 的链接从 markdown 格式改为 wiki-link `[[llm-wiki]]`
- **新增**: `.gitignore`，排除 `workspace.json`、session 数据、系统文件
- **验证**: 目录结构完整、各文件一致、无孤立页面或断裂引用

## [2026-06-12] lint | 前置元数据及索引中文化

- **修改**: `domain` 值 — `tech→技术`、`language→语言`、`philosophy→哲学`、`meta→元`、`general→通用`
- **修改**: `status` 值 — `seed→种子`、`growing→成长中`、`mature→成熟`
- **修改**: `index.md` — 所有分类标题与描述翻译为中文
- **修改**: `log.md` — 前置元数据中文化；正文全量翻译为中文
- **不动**: CLAUDE.md 正文保持英文（LLM 主读者）、目录名、字段名、标签（自由混用）
- **理由**: 用户以中文思维学习；前置元数据和索引是面向人的界面；CLAUDE.md 面向 LLM，保持英文以减少路径歧义

## [2026-06-12] lint | 补全 log 前缀规范

- **修复**: CLAUDE.md 中 log 有效前缀补上 `init`，与 `log.md` 实际使用及 Legend 表一致

## [2026-06-12] 摄入 | LLM Wiki 构想文档

- 将 `llm-wiki.md` 从根目录移至 `raw/llm-wiki.md`（属原始资料，非系统文件）
- 更新 CLAUDE.md 链接：`[[llm-wiki]]` → `[[raw/llm-wiki]]`
- 创建 `wiki/sources/llm-wiki.md`——来源摘要页，记录从该构想中提取的结构决策
- 首次摄入完成——三层架构闭环：原始资料 → LLM 维护 wiki → 模式治理

## [2026-06-12] lint | 附件路径分离

- **修复**: Obsidian 附件路径恢复为 `raw/assets`（Web Clipper 主场景）
- **新增**: `wiki/assets/` 目录——wiki 页面专用图片（图表、截图等）
- **更新**: CLAUDE.md 目录树和摄入流程反映双附件路径
- **原则**: 原始资料图片归 `raw/assets/`，wiki 内容图片归 `wiki/assets/`，各不混杂

## [2026-06-12] lint | 消除命名歧义

- **修改**: index.md 中 `## 日志` 分类标题改为 `## 反思`——与根目录 `log.md`（系统活动日志）区分，避免同名混淆
- `log.md` = 系统操作记录（摄入/检查/复习）
- `## 反思` → `wiki/journal/` = 你的学习反思、回顾、里程碑

## [2026-06-12] lint | 清理断裂索引

- **修复**: 移除 index.md 中两条已失效的索引条目——指向已删除的 `wiki/sources/llm-wiki.md` 和 `wiki/syntheses/VaultGrowth 知识库总览.md`
- 知识库回归纯净状态：零内容页，零断裂引用

## 图例

| 前缀 | 含义 |
|------|------|
| `ingest` | 摄入新原始资料 |
| `query` | 回答问题；可能将结果归档 |
| `lint` | 健康检查 |
| `review` | 间隔复习 / 强化 |
| `init` | 系统初始化 / 配置 |
