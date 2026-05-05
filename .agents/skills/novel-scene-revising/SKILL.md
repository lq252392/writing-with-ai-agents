---
name: novel-scene-revising
description: Use when 独立 review 已返回问题包，需要在不改乱既有状态的前提下对现有场景草稿做定向修订时使用。
---

# 分场景修订

## Overview

这不是重新起草。它的职责是按 review 问题包定向打补丁，在不漂移状态的前提下修正文段、动作链、信息链和局部节奏。

**核心原则：只改被授权的范围；没被点名的稳定段落，不顺手重写。**

## Trigger Keywords

- 修订这一场
- 按 review 改
- 打补丁
- 根据审稿意见改稿
- 只修这些问题

## Do Not Use When

- 还没有首稿，先用 `novel-scene-drafting`
- 只有模糊想法，还没形成可审草稿
- 想大幅改方向、改章目标、改设定，先回 `novel-brainstorming` 或 `novel-chapter-planning`

## Required Inputs

输入必须显式包含：

- 原稿
- review 问题包
- 修订范围白名单
- 相关约束
- 最新状态摘要
- 本章或本场计划

缺任何一项，都不要假装能稳修。先停下补材料。

## State Contract: Inputs

必读字段：

- `next_stage_entry`
- `carry_over_risks`
- `confirmed_constraints_touched`
- `constraints_to_invalidate`
- review 问题包中的严重级别、证据、最小修订建议

可选字段：

- `scene_summary`
- `character_state_updates`

忽略字段：

- 与本轮修订无关的自由评论
- 没进白名单的大范围重写建议

## Revising Order

1. 先确认这是不是修订任务，而不是重新起草
2. 读取原稿、review 问题包、修订白名单
3. 按严重级别排序，先处理关键，再处理重要
4. 逐条核对白名单，超出范围的改动先放弃
5. 定向修订最小必要段落
6. 输出修订稿、diff 摘要、未触碰区域声明
7. 把修订稿重新交给独立 review

## White-List Rule

- 白名单未授权的段落，不要顺手改风格
- review 没点名的问题，不要借机整体换写法
- 若发现真正无法只靠白名单修复的结构冲突，先停下并上抛，不要偷扩修订范围

## Output

输出至少包含：

- 修订稿正文
- `review_status`：固定写 `pending_independent_review`
- `diff_summary`：逐条对应 review 问题说明改了什么
- `untouched_areas`：明确哪些段落刻意未动
- `open_items`：仍未解决、需上游裁决的问题

若保留某条问题，必须说明：

- 为什么保留
- 保留后会留下什么风险
- 下一步该回到哪个 skill 处理

## Example

场景塌缩类修订，不是把整场戏重写，而是补回被吃掉的在场角色状态。

```text
塌缩前：
牌桌边只剩她和林澈在说话，其他人像突然消失了。

修订后：
牌桌边的话锋仍然落在她和林澈之间，但沈雁把杯口轻轻磕在桌沿，像是在提醒规则还没从场上退掉；宋晚没有插话，只把视线停在记分板上，等他们谁先露出破绽。
```

这里修的是"在场角色状态缺失"，不是借机改掉整场对白结构。

## Red Flags - STOP and Start Over

- "这段既然要修，我顺便把整场气质都换掉吧"
- "review 只点了两句，我直接整场重写更顺"
- "这条建议我不同意，我就不处理了"
- "修订时顺手改了几个设定，反正更合理"

**如果出现以上情况：立即停止，恢复最小修订原则。**

## Independent Review Rule

- 修订者不是终审者。
- 修订完成后，必须重新交给独立 review。
- 若环境不支持子智能体，结论只能写 `pending_independent_review`，不能写 `passed`。

## Completion Gate

只有满足下面条件，才能宣称这轮修订完成：

- 已逐条回应关键和重要问题，或明确保留理由
- 已输出 `diff_summary`
- 已输出 `untouched_areas`
- 已重新进入独立 review 队列，或明确写出 `pending_independent_review`
