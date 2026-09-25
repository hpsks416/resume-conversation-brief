# resume-conversation-brief

继承既有对话的**主干**。用法：`/resume-conversation-brief <对话名>`。只读、不搬移。

## 适用对象

- DeepSeek Harness（DSH）用户：一个可由 AI agent 按需自动加载的 skill，克隆即用、无需构建。
- 需要继承既有对话主干（结论/决策/待办）的人

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
