---
name: novel-continuity-review
description: Use when 需要对非当前起草者生成的小说草稿做独立连续性审稿，检查人物认知、时间顺序、规则边界、多人在场状态和版本一致性时使用。
---

# 连续性检查

## Overview

这是独立审稿 skill，不负责写正文。它只负责找出连续性问题、规则冲突和状态错位，并给出证据与最小修订建议。

## Trigger Keywords

- 查逻辑
- 查连续性
- 看有没有穿帮
- 规则对不对
- 状态有没有串

## State Contract: Inputs

必读字段：

- `state_version`
- `based_on_constraints_version`
- `next_stage_entry`
- `carry_over_risks`
- `confirmed_constraints_touched`
- 当前草稿版本

可选字段：

- `scene_summary`
- `character_state_updates`
- `target_word_range`

忽略字段：

- 与连续性无关的文风偏好评论
- 没有证据支撑的主观猜测

## What to Check

重点检查：

- 人物身份、关系、称呼是否一致
- 谁在何时知道什么，是否写乱
- 时间顺序、空间位置、人数计数是否一致
- **场景规模塌缩**：多角色场景是否在行文中悄悄缩减成双人对白，遗漏了其他在场角色的反应和状态
- 世界规则、能力规则、游戏规则是否中途变形
- 线索、承诺、伏笔是否前后打架
- 场景结尾状态是否与计划一致
- 草稿引用的状态版本与约束版本是否匹配

## Output Format

每条问题都要包含：

- 严重级别：关键 / 重要 / 次要
- 问题描述
- 证据位置或证据句
- 为什么它会造成连续性问题
- 最小修订建议

整份审稿结果还应额外给出：

- 审稿结论：`passed` / `needs_revision` / `pending_independent_review`
- 本轮检查范围：检查了哪一场、哪一段或哪一版草稿
- 若判定通过：明确写出本轮连续性上已确认无冲突的关键点，方便回写状态

## Few-Shot

通过样例：

```text
结论：passed
关键点：
- 四名在场角色都持续存在，各自反应没有中途消失
- 角色 A 直到最后一句才得知暗号，符合前文认知边界
- 场景出口状态与计划一致，下一场入口清晰
```

需修订样例：

```text
严重级别：重要
问题描述：多人场景在中段塌缩为双人对白
证据句：前文写"桌上四人都在"，但中段连续三段只剩主角和林澈对话，沈雁与宋晚没有任何反应或位置更新
为什么有问题：在场人数与博弈压力被正文悄悄改写，后续角色判断会失真
最小修订建议：补回沈雁与宋晚在关键对话节点的观察、动作或压迫反应，不必整场重写
结论：needs_revision
```

## Red Flags - STOP and Start Over

- "我自己写的草稿，顺手检查一下吧"
- "既然逻辑没问题，我就不指出少了一个角色的事了"
- "这点设定冲突不严重，我直接帮作者圆过去吧"
- "文风太干了，我要在连续性审稿里重写正文"

**如果出现以上情况：立即停止，恢复独立、客观、只针对逻辑和连续性的审稿视角。**

## Independent Review Rule

- 这是**独立审稿 skill**。如果你就是当前草稿的起草者，立刻停止，不做连续性判定。
- 自查场景下，结论字段只能写 `pending_independent_review`，绝不允许写 `passed`。
- 若当前环境没有子智能体或第二个独立智能体，不要输出"待审清单"就结束，必须输出一份可粘贴到新会话的审稿启动 prompt。

降级模板：

```text
请使用 `novel-continuity-review` 独立审这份草稿。

草稿版本：<draft_version>
状态版本：<state_version>
约束版本：<constraints_version>
检查范围：<scene_or_paragraph_range>
草稿正文：<draft_text>
相关状态与约束：<relevant_context>

要求：
- 你不是起草者
- 只做连续性审稿
- 结论只允许是 passed / needs_revision / pending_independent_review
- 若发现问题，给出严重级别、证据、原因、最小修订建议
```

## Rules

- 不要因为文风喜好去打断连续性审稿。
- 没有证据就不要断言有 bug。
- 除非用户明确要求，不要直接重写整章。
- 如果稿子是由另一个智能体生成，保持独立审稿视角，不要替它圆。
- 如果问题只涉及局部段落，也只给最小修订范围，不要把整场戏推倒重来。
