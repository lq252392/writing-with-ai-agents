---
name: novel-summary-state
description: Use when 一场戏或一章正文已经通过独立 review，需要把事件、人物状态、线索变化、版本号和作废约束沉淀成后续可复用状态时使用。
---

# 摘要与状态回写

## Overview

把正文压成后续协作真正需要的状态。目标不是复述好看，而是给下一章、下一场和新会话留下稳定入口。它负责快变量，也负责告诉约束层哪些旧约束该作废。

## Trigger Keywords

- 回写状态
- 做摘要
- 接住这一场
- 更新人物状态
- 更新线索

## When to Use

适用于：

- 一场戏已经过完独立 review，准备继续往后写
- 一章完成并过完独立 review 后，需要接住人物关系和线索推进
- 正文越来越长，不能每次都整段回灌

## Extract

优先提取这些东西：

- 已发生的关键事件
- 人物关系和认知变化
- 新增线索与未解决问题
- 已兑现与未兑现的承诺
- 下一个阶段的起始状态
- 哪些旧约束因此失效

## Output

输出不要写成文学评论，必须是稳定且结构化的状态材料。建议使用 JSON：

```json
{
  "state_version": "state-v8",
  "based_on_constraints_version": "constraints-v3",
  "scene_summary": "本场戏发生的客观事件",
  "character_state_updates": [
    {
      "character": "角色A",
      "new_knowledge": "得知了某事",
      "relationship_shift": "对角色B产生怀疑"
    }
  ],
  "clues_and_unresolved": [
    "新增的线索C",
    "未兑现的承诺D"
  ],
  "next_stage_entry": "下一步写作前必须知道的起始状态事实",
  "confirmed_constraints_touched": [
    "本场戏再次确认、且会继续约束后文的规则或关系"
  ],
  "constraints_to_invalidate": [
    "本轮正文已经推翻或作废的旧约束"
  ],
  "carry_over_risks": [
    "下一场最容易写错或忘记的边界"
  ]
}
```

其中要分清两件事：

- `character_state_updates` 和 `next_stage_entry` 记录的是这轮新增的稳定变化
- `confirmed_constraints_touched` 只写被本轮再次确认或新近兑现、足以影响后文的硬边界
- `constraints_to_invalidate` 只写已被正文稳定推翻的旧约束，不写猜测

不要把一时情绪波动、修辞气氛或未过审的猜测写进长期状态。

## Red Flags - STOP and Start Over

- "这段写得真好，让我用华丽的辞藻总结一下"
- "草稿还没复审，我先急着总结吧"
- "这个细节不重要，我就不记进状态里了"
- "我直接把原文压缩一下发出来，不提取结构化状态了"

**如果出现以上情况：立即停止，恢复状态提取视角，必须输出结构化状态摘要。**

## Rules

- 这是**增量回写**，负责把新正文带来的变化写回状态层。
- 如果用户需要重整整个项目的长期规则、人物总表和世界边界，转给 `novel-constraints-organizer`，不要在这里代替它做全量整理。
- 正文未经过独立 review 时，不要直接把不稳定事实写回长期状态。
- 不要把正文换种说法再重写一遍。
- 区分事实变化和情绪色彩，不要混写。
- 若某个变化会限制后续写法，明确写出来。
- 如果本轮正文只是局部修辞调整，没有新增稳定事实，不要制造"状态更新"；可以明确写本轮无新增状态。
- 若发现旧约束已被正文稳定推翻，必须写入 `constraints_to_invalidate`，交给 `novel-constraints-organizer` 归档和作废。
