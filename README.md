# resume-conversation-brief

在对话中用 `/resume-conversation-brief <对话名>` 继承既有迁移对话的主干——按对话名定位 conversations/*.md，分段 map-reduce 精炼成可追溯快照（每结论引用来源），不搬移项目文件。Use when the user types "/resume-conversation-brief <名字>" or asks for a migrated conversation's distilled gist. Not for full-detail reading or moving files.

## 这是什么

DSH（DeepSeek Harness）skill —— 一个可由 AI agent 按需自动加载的能力单元。克隆到 skill 目录后，DSH 会依据上方描述自动发现并触发它，无需构建。

## 安装

最简单：用 [dsh-config](https://github.com/hpsks416/dsh-config) 的一键脚本 `install.ps1` 批量安装全部 skill。单个安装：

    # GitHub
    git clone https://github.com/hpsks416/resume-conversation-brief.git "$env:USERPROFILE\.dsh\skills\resume-conversation-brief"
    # 或 Gitee（国内直连更快）
    git clone https://gitee.com/hpsks416/resume-conversation-brief.git "$env:USERPROFILE\.dsh\skills\resume-conversation-brief"

克隆后 DSH 会自动重新发现，无需重启。更新用：

    git -C "$env:USERPROFILE\.dsh\skills\resume-conversation-brief" pull

## 目录结构

    resume-conversation-brief/
    ├── SKILL.md    技能入口与工作流
    ├── evals.yaml

## 依赖

无运行时依赖，纯指令型 skill（由 agent 直接执行 Markdown 工作流）。

## License

MIT License. See [LICENSE](LICENSE).
