# Business Knowledge Base | 业务知识索引

This file should work as an index-first business knowledge layer.  
这个文件更适合作为**索引优先**的业务知识层，而不是一篇一口气读完的大长文。

Use it to locate the right topic first, then read only the needed knowledge.  
更推荐的使用方式是：**先查索引，再按需取用**。

## What Belongs Here

- business terminology,
- product mechanism notes,
- recurring domain patterns,
- PRD reading hints,
- scenario definitions.

## How To Use This File | 怎么使用这个文件

- Do not treat the whole file as mandatory reading for every case.
- Start from the topic that matches the current experiment.
- Pull only the terms, mechanism notes, and domain concepts that are relevant.

- 不要把整份文件都当成每次必须通读的内容。
- 先从当前实验最相关的 topic 开始看。
- 只拿这次分析真正需要的术语、机制说明和业务概念。

## What Does Not Belong Here

- experiment-local conclusions,
- reused final judgments from old cases,
- copied A / B / C / D outputs from finished experiments.

---

## Partially Ingested Stable Terms | 已分批入库的稳定术语

These terms are stable enough to enter the formal business knowledge base even though the full DM glossary is still evolving.  
下面这些术语已经足够稳定，可以先正式进入 business knowledge；完整 DM glossary 仍可继续在 drafts 中迭代。

### MUF

- 中文：双关
- 英文：Mutual Follow
- 含义：指用户间互为关注的关系，是私信核心互动的基础关系。
- Notes: confirmed in round-1 glossary review.

### Pair

- 中文：私信关系对
- 英文：DM pair
- 含义：指存在私信行为的一对关系，包含发送方和接收方，存在方向。
- Notes:
  - `A -> B` 和 `B -> A` 记为两个 pair
  - 重复的 `A -> B` 行为去重后仍记为一个 pair

### Message Requests

- 中文：消息请求
- 英文：Message Requests
- 含义：TikTok 防范陌生人骚扰的机制；对未互关用户发消息时，对方先收到消息请求。

### Sticker-related Terms To Keep Separate

These terms should stay separate instead of being merged into one generic `Sticker` entry:

- `Big-moji`
- `UGC sticker`
- `Sticker panel`

Their detailed definitions can remain in `drafts/` until fully confirmed.
