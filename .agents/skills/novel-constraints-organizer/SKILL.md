---
name: novel-constraints-organizer
description: Use when 用户已有小说材料，但人物、规则、线索、文风锚点和写作禁区散乱，需要整理成稳定长期约束时使用。
---

# 小说约束整理

## Overview

把散落材料整理成长期可复用的小说约束。重点是稳定，不是扩写。它负责慢变量，也负责接收状态层发来的作废标记，更新哪些旧约束已经失效。

## Trigger Keywords

- 整理设定
- 角色表
- 世界规则
- 线索总表
- 写作禁区
- 文风锚点

## When to Use

适用于：

- 人物设定、世界规则、线索记录散在聊天和笔记里
- 写到中段后，开始记不清哪些事实已经成立
- 多角色、多关系、多规则体系容易串线
- 需要固定作者文风锚点，防止后文口气飘掉

不适用于：

- 只是要写一个场景
- 只是做文学润色

## What to Organize

优先整理这些层：

- 人物身份、关系、已知信息、禁区
- 世界规则、能力边界、社会约束
- 线索、承诺、伏笔、未兑现事项
- 当前故事阶段已经形成的稳定慢变量
- 文风和叙事硬约束

## Output Shape

输出应尽量稳定、短、可查找。建议使用带版本号的结构化约束集：

```json
{
  "constraints_version": "v3",
  "based_on_state_version": "state-v7",
  "confirmed_constraints": [],
  "likely_constraints": [],
  "undecided_questions": [],
  "style_anchors": {
    "representative_sentences": [],
    "sentence_length_preference": "短句偏多，关键处允许拉长",
    "inner_monologue_density": "低到中",
    "banned_words_or_phrases": []
  },
  "invalidated_constraints_archive": [],
  "conflicts_to_resolve": []
}
```

建议固定这三类标签，避免后续 skill 混读：

- 已确认：可以直接约束后续写作的事实
- 高度怀疑：大概率成立，但还不能当铁律
- 尚未决定：只能保留为问题，不能写进正文当既定事实

`style_anchors` 至少要能回答四个问题：

- 代表性句式长什么样
- 句长大致偏短还是偏长
- 内心独白密度应落在哪个区间
- 哪些词或腔调要避免

## Invalidation Flow

长期约束不是只增不减。接到 `novel-summary-state` 的 `constraints_to_invalidate` 后，必须执行这步：

1. 核对作废项是否有正文证据
2. 将原约束从有效区移出
3. 写入 `invalidated_constraints_archive`
4. 标注由哪个状态版本触发作废

例如：

- 第 5 章写入"角色 A 持有武器"
- 第 12 章正文确认武器已被销毁
- `novel-summary-state` 输出 `constraints_to_invalidate`
- 本 skill 负责把"角色 A 持有武器"从有效约束中移除并归档

## Red Flags - STOP and Start Over

- "作者忘了写这里，我替他编一段人物背景吧"
- "这个设定太老套，我改一改让它更合理"
- "我直接把原文长篇大论复制过来当约束"
- "把所有未确认的脑洞都当成事实写进设定里"

**如果出现以上情况：立即停止，约束整理只能基于已确认事实，绝对禁止主动扩写和二创。**

## Rules

- 只整理已有事实，不主动扩展世界。
- 区分"已确认""高度怀疑""尚未决定"。
- 如果某条规则会限制后续写法，明确写出代价，不要只写优点。
- 尽量把长期稳定约束和本章临时状态分开写，避免一份文档同时承担设定总表和场景摘要。
- 若发现已有长期约束与最新正文状态冲突，不要替作者圆；把冲突点单独列出，等待上游修正或裁决。
- `style_anchors` 只记录作者稳定偏好，不记录一次性的局部修辞灵感。
