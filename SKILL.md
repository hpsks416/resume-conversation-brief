---
name: resume-conversation-brief
description: 在对话中用 `/resume-conversation-brief <对话名>` 继承既有迁移对话的主干——按对话名定位 conversations/*.md，分段 map-reduce 精炼成可追溯快照（每结论引用来源），不搬移项目文件。Use when the user types "/resume-conversation-brief <名字>" or asks for a migrated conversation's distilled gist. Not for full-detail reading or moving files.
---

# Resume Conversation (Brief)

继承既有迁移对话的**主干**。用法：`/resume-conversation-brief <对话名>`。只读、不搬移。

## 何时用

- 用户输入 `/resume-conversation-brief 3D管线` 这类斜杠指令。
- 只要**主干**（结论、进展、决策、待办），不读全部细节。

## 何时不用

- 要精确细节 → 用 `resume-conversation-full`。
- 要搬移/复制项目文件 → 本 skill 不做，直接拒绝。

## 定位对话（三级回退，同 full 版）

> ⚠️ 坑：`glob` 在 Windows 绝对路径 + 反斜杠 + `**` 下会静默返回空。递归找文件改用 `pwsh Get-ChildItem -Recurse`。

1. **第一级：Codex 迁移 .md**——`G:\CodexDS\DSH\MAIN` 下 pwsh 递归找 `conversations\*.md`，文件名去 .md 前缀匹配对话名。
2. **第二级：索引映射**——无语义名读 `_migrated_codex\conversations\index.md` 标题列映射。
3. **第三级：DSH 原生会话回退**——前两级找不到，用 `session_query`（query=对话名）查原生会话，命中后读 `~/.dsh\storages\session_projcache\sessions\<session-id>.json`（turn outline 即可，brief 够用，不必解压 .zstd）。
4. 三级都失败：报告「未找到」，列出可用清单，不猜测。

## 精炼快照（map-reduce，每结论引用来源）

**源 A：Codex 迁移 .md**
- 文件 ≤ 约 40k 字符：直接读，然后精炼。
- 文件 > 40k 字符：**分段读（read offset/limit），逐段提炼「段摘要」，最后合并成总快照**——不静默丢中间内容（map-reduce，借鉴 claude-handoff 的大会话分块总结）。

**源 B：DSH 原生会话**
- 直接读 projcache JSON 的 turn outline（prompt/response 摘要 + 统计），据此精炼，无需分段读 .zstd 全文。

快照固定结构，且**每一条结论标注来源**（哪个 .md 或哪个 session-id）：

```markdown
# 对话快照：<对话名>

- 来源：<文件路径>

## 这是什么
（一句话：对话在做什么/解决什么）

## 当前进展
- <结论1>（据 <文件名>）
- <结论2>（据 <文件名>）

## 关键决策
- <决策 + 为什么>（据 <文件名>）

## 待办 / 未解决
- <待办1>
- <待办2>

## 环境/约束
- <关键环境、路径、凭据约定>
```

## 铁律

- **只读、不搬移**：绝不复制、移动、修改任何文件。
- **每结论可追溯**：快照里的每一条结论/决策/待办，标注出自哪个 .md 或哪个 session-id（借鉴 claude-handoff 的「每 bullet 引用来源」）。
- **不静默丢内容**：大文件分段读完再合并，读不完明说。
- **快照是摘要，不是原文**：明确告诉用户「这是主干，需要细节请用 resume-conversation-full」。
- **定位优先三级回退**：Codex .md → 索引映射 → session_query 原生会话，不要只在 MAIN 找 .md 就放弃。
