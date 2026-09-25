# resume-conversation-brief

继承既有对话的**主干**。用法：`/resume-conversation-brief <对话名>`。只读、不搬移。

## 环境依赖

- 操作系统：Windows
- 运行时：无（纯指令型 skill，由 agent 直接执行）
- 第三方软件：无（仅依赖系统自带的 PowerShell / 标准库）

## 目录结构

    resume-conversation-brief/
    ├── SKILL.md    技能入口与工作流
    ├── evals.yaml
    ├── references\conversation-sources.md

## 安装

    # GitHub
    git clone https://github.com/hpsks416/resume-conversation-brief.git "$env:USERPROFILE\.dsh\skills\resume-conversation-brief"
    # 或 Gitee（国内直连）
    git clone https://gitee.com/hpsks416/resume-conversation-brief.git "$env:USERPROFILE\.dsh\skills\resume-conversation-brief"

克隆后 DSH 自动重新发现，无需构建。

## License

MIT License. See [LICENSE](LICENSE).
