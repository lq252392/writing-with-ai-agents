---
name: novel-scene-drafting
description: Use when 用户已经有场景计划、章节目标或稳定约束，要写某一场正文首稿，而不是 brainstorming、review、summary 或定向修订时使用。
---

# 分场景扩写

## Overview

按场景写正文首稿，而不是一口气写整章。先读约束、状态和计划，再写一场；写完后交给独立审稿。起草只负责把这场戏立住，不负责给自己下通过结论。

## Trigger Keywords

- 写这一场
- 扩写正文
- 把场景写出来
- 根据计划出稿
- 先出首稿

## Do Not Use When

- 只有模糊想法，还没定目标
- 只是整理设定或总结状态
- 已经拿到 review 问题包，要定向修订，转 `novel-scene-revising`

## State Contract: Inputs

必读字段：

- `next_stage_entry`
- `carry_over_risks`
- `confirmed_constraints_touched`
- `state_version`
- `constraints_version`
- `based_on_constraints_version`

可选字段：

- `scene_summary`
- `character_state_updates`

忽略字段：

- 未列入上述字段的自由评论
- 已过时的旧版草稿点评

## Drafting Order

1. 读取最相关的约束材料
2. 读取最新状态摘要
3. 读取本章或本场目标
4. 确认这次是写首稿，不是修订稿
5. 明确这场戏只推进什么
6. 写正文
7. 生成待独立审稿的交接包
8. 交给独立 review

## Writing Rules

- 一次只写一场戏，除非用户明确要求整章且计划已稳定。
- 先保证动作链和信息链成立，再追求表达强度。
- 不要把正文写成提纲扩句。
- 不要把解释作者意图的话塞进正文。
- 角色说话方式要能区分，不能人人一个口气。
- **防止场景规模塌缩**：多角色互动场景严禁自动收缩为双人戏，必须维持原定的博弈规模与多人在场状态，兼顾旁观角色的反应。
- 警惕流水账：如果一段只是顺序交代动作和对白，却没有推进关系、信息或情绪，优先重写这一段。
- 警惕硬拔高：如果一句话的力度超过当前动作、感知和场景本身能撑住的程度，先压回具体细节。
- 若约束、状态摘要、章节计划三者互相冲突，立即停止扩写，先把冲突抛回上游，不要靠正文临场硬补。

## Collapse Example

多人场景的常见错误不是"写少了"，而是把复杂博弈写扁了。

```text
塌缩前：
包厢里明明坐着四个人，正文却只剩她和周临在对话，另外两人的在场状态完全消失。

修复后：
对话焦点仍然落在她和周临之间，但许栀一直在拨弄打火机，像是在数谁先露怯；程雁没有插话，只在周临说到第三句时抬眼，逼得桌上的沉默跟着变了方向。
```

修复点不在"多写几个人名"，而在于让其他在场角色继续施压，维持原定博弈规模。

## Red Flags - STOP and Start Over

- "我觉得不需要送审，这段写得很好"
- "角色太多太乱了，我先只写男女主对话吧"
- "我直接把大纲里的动作扩成句子就行"
- "既然没有子智能体，我就顺手把文笔也查了吧"

**如果出现以上情况：立即停止，遵守独立 review 和多角色状态维持。**

## Independent Review Rule

- **生成正文的智能体，不负责给自己的稿子做最终审稿判定。**
- 起草完成后，不要由同一个智能体直接调用两类 review skill 给自己下结论；review 必须由上层入口或独立调度者转交给别的智能体。
- 两类 review 中只要有一类返回关键或重要问题，就不要把这场戏标记为完成，转给 `novel-scene-revising`。
- 若环境不支持子智能体：
  - 可以完成草稿
  - 但 `review_status` 只能写 `pending_independent_review`
  - 不能宣称"已经审过"
  - 必须附上可粘贴到新会话的 review 启动 prompt

降级模板：

```text
请独立审这份场景草稿。

草稿版本：<draft_version>
约束版本：<constraints_version>
状态版本：<state_version>
检查范围：<scene_range>
草稿正文：<draft_text>
相关约束与状态：<relevant_context>

要求：
- 你不是起草者
- 使用 `novel-continuity-review` 或 `novel-prose-flow-review`
- 只做独立审稿，不直接改写正文
- 若无法独立审稿，返回 pending_independent_review
```

## Completion Gate

只有下面条件满足，才能宣称这一场戏当前轮完成：

- 草稿已生成
- `review_status` 不是 `pending_independent_review`
- 连续性 review 已完成，或明确未完成原因
- 文笔与流畅性 review 已完成，或明确未完成原因
- 重要问题已修，或明确保留理由

## Output

输出至少包含：

- 正文草稿
- `review_status`
- 需要交给 review 的材料范围
- review 启动 prompt 或 review 交接包

起草阶段不要输出"修订摘要"。修订工作由 `novel-scene-revising` 负责。
