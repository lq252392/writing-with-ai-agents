# Writing With AI Agents / 与 AI 智能体共写

> **AI Agent Writing Framework for Novelists**  
> **长篇小说 AI 辅助写作框架**

**写作 Skill** | **Agent 写作法** | 长篇小说实战指南
---

## 这是什么 / What is this?

**English**: A reusable writing infrastructure that helps novelists use AI Agents and structured workspaces to organize long-form fiction writing.

**中文**: 一套可复用的写作基础设施，帮助小说作者使用 AI Agent 和工作区结构来组织长篇小说创作。

---

## 核心概念 / Core Concepts

| 中文 | English | 说明 |
|------|---------|------|
| Skill 模板 | Skill Templates | 固化常见写作动作的可复用模板 |
| 工作区 | Workspace | 组织大纲、设定、章节、摘要的目录结构 |
| AGENTS.md | AGENTS.md | 确保 Agent 协作稳定性的长期规则 |

---

## 目录结构 / Directory Structure

```
.agents/
└── skills/                        # Skill 模板 / Skill Templates
    ├── novel-workflow-gateway/     # 小说工作流入口 / Novel Workflow Gateway
    ├── novel-brainstorming/        # 小说头脑风暴 / Novel Brainstorming
    ├── novel-constraints-organizer/ # 小说约束整理 / Novel Constraints Organizer
    ├── novel-chapter-planning/     # 章节规划 / Chapter Planning
    ├── novel-scene-drafting/       # 分场景扩写 / Scene Drafting
    ├── novel-continuity-review/    # 连续性检查 / Continuity Review
    ├── novel-prose-flow-review/    # 文笔与流畅性复审 / Prose Flow Review
    ├── novel-scene-revising/       # 分场景修订 / Scene Revising
    └── novel-summary-state/        # 摘要与状态回写 / Summary State

大纲/                                # Outline / 大纲
├── 总纲.md                         # Main Outline

设定/                                # Settings / 设定
├── 人物设定.md                     # Character Settings
└── 世界观.md                        # World Building

章节/                                # Chapters / 章节
摘要/                                # Summaries / 摘要
线索/                                # Plot Threads / 线索

AGENTS.md                           # Project Rules / 项目规则
README.md                           # This file / 本文件
```

---

## 使用方法 / Usage

### 对于框架维护者 / For Framework Maintainers
1. 完善 Skill 模板 / Refine Skill templates
2. 维护 AGENTS.md 规则 / Maintain AGENTS.md rules
3. 更新方法论文档 / Update methodology documentation

### 对于小说作者 / For Novelists
1. 复制本框架到新目录 / Copy this framework to a new project
2. 使用 `初始化小说工作区` Skill 初始化 / Initialize with "Initialize Novel Workspace" Skill
3. 填写基础文档 / Fill in base documents (outline, settings)
4. 使用其他 Skill 辅助创作 / Use other Skills as needed

---

## Skill 清单 / Skill List

| Skill | 用途 / Purpose |
|-------|----------------|
| [novel-workflow-gateway](.agents/skills/novel-workflow-gateway/SKILL.md) | Workflow entry point / 工作流入口 |
| [novel-brainstorming](.agents/skills/novel-brainstorming/SKILL.md) | Brainstorm ideas / 头脑风暴 |
| [novel-constraints-organizer](.agents/skills/novel-constraints-organizer/SKILL.md) | Organize constraints / 整理约束 |
| [novel-chapter-planning](.agents/skills/novel-chapter-planning/SKILL.md) | Plan chapters / 章节规划 |
| [novel-scene-drafting](.agents/skills/novel-scene-drafting/SKILL.md) | Draft scenes / 场景扩写 |
| [novel-continuity-review](.agents/skills/novel-continuity-review/SKILL.md) | Check continuity / 连续性检查 |
| [novel-prose-flow-review](.agents/skills/novel-prose-flow-review/SKILL.md) | Review prose flow / 文笔复审 |
| [novel-scene-revising](.agents/skills/novel-scene-revising/SKILL.md) | Revise scenes / 场景修订 |
| [novel-summary-state](.agents/skills/novel-summary-state/SKILL.md) | Summarize state / 状态摘要 |

---

## 工作流程 / Workflow

```
模糊想法 / Vague Idea
    ↓
novel-workflow-gateway (分流任务)
    ↓
novel-brainstorming (头脑风暴)
    ↓
novel-constraints-organizer (整理约束)
    ↓
novel-chapter-planning (章节规划)
    ↓
novel-scene-drafting (场景扩写)
    ↓
novel-continuity-review + novel-prose-flow-review (双重审稿)
    ↓
novel-scene-revising (定向修订，如有问题)
    ↓
novel-summary-state (状态回写)
    ↓
进入下一章 / Next Chapter
```

---

## 核心原则 / Core Principles

**中文**:
- **先读后写**: 扩写前先读取总纲、设定、前文摘要
- **保守处理**: 信息不足时不擅自发明关键设定
- **局部修改**: 优先局部修改，避免整章推翻重写
- **生成与检查分离**: 写完后再单独检查，不混合进行

**English**:
- **Read Before Write**: Read outline, settings, and previous summaries before drafting
- **Conservative Approach**: Don't invent key settings when information is insufficient
- **Local Edits**: Prefer local modifications over full rewrites
- **Separate Generation and Review**: Check separately after writing, don't mix

---

## 关键词 / Keywords

`AI Writing` `Agent Writing` `Novel Writing` `Longform Writing` `Writing Workflow` `AI-assisted Writing` `Structured Writing` `Writing Framework` `LLM Writing` `Collaborative Writing` `写作 Skill` `Agent 写作法`

---

## 相关链接 / Links

- **GitHub**: https://github.com/lq252392/writing-with-ai-agents
- **Gitee**: https://gitee.com/lq2523/writing-with-ai-agents

---

## 注意事项 / Notes

- Skill 采用标准格式: `/skills/名字/SKILL.md`
- Skill format: `/skills/name/SKILL.md`
- 作者应根据自己的写作习惯定制 Skill 和工作区结构
- Authors should customize Skills and workspace structure according to their habits
