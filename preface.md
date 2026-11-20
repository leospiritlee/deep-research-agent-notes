## 序：从一个问题，到一份能逐条核验的报告

一次检索给出几个链接，一次对话给出一段答案，深度研究给出的是一份交付物：有研究计划、有证据链、有内联引用、有明确边界，有人能顺着每条论断回到它真正的来源。这不是把搜索多调几次，而是把「查资料」变成一条有账本、有终止条件、有预算的工程链路。

这本专题精读写的是这条链路的十二道关：先判断该不该上 `deep research`，再走 `query decomposition`、多轮检索、网页浏览、证据图、引用绑定、上下文裁剪、分节写作、一致性账本、成本延迟、评测，最后落到有状态可恢复的上线形态。每关回答同一个问题——多走一步，换来了什么证据，又带来什么新代价。

**分工**：与两本 Agent 书不同，那两本讲单 Agent 的循环、工具、上下文，以及多 Agent 之间的协作协议；这本只讲一个研究问题从提问到带引用长报告的证据链，Agent 协作只作为可并行时的手段出现。与《AI 数据工程精读》《推理模型精读》也不同：那两本讲训练数据与回答那一刻的算力，这本讲回答之前的检索与证据。

## 研究链路全景图

+----------------------------------------------------------------------+
| DEEP RESEARCH: FROM A QUESTION TO A CITED REPORT                      |
|                                                                      |
| [1] boundary -> [2] plan -> [3] search -> [4] browse                  |
| [5] evidence -> [6] citation -> [7] context -> [8] write              |
| [9] ledger -> [10] cost -> [11] eval -> [12] serving                  |
|                                                                      |
| one question -> evidence graph -> claim by claim cited report         |
+----------------------------------------------------------------------+

这张图不是调用顺序，而是「一个问题变成一份报告时，新出现的代价依次落在哪里」：先问该不该做，再问怎么拆、去哪找、找到的东西怎么存、怎么引、怎么写、怎么算账、怎么验、怎么上线。越往后，代价越隐性，也越需要在上线前想清楚。

## 十二关速查表

| 关 | 主题 | 一句话 |
|---|---|---|
| 1 | 边界 | `deep research` 只在任务可拆、信息求新、交付是长报告时才划算 |
| 2 | 规划 | `query decomposition` 先宽后窄，`search budget` 写进提示 |
| 3 | 检索 | `rerank` 与 `diversity` 防住「搜得多却证据重叠」 |
| 4 | 浏览 | `WebArena` 类环境里，每一步都要有 `checkpoint` |
| 5 | 证据 | `evidence graph` 让 `evidence coverage` 可测 |
| 6 | 引用 | `citation accuracy` 与 `effective citation count` 分开看 |
| 7 | 上下文 | `Lost in the Middle` 之前先做早期裁剪 |
| 8 | 写作 | `composer` 起草、`prosecutor` 红队，无人给自己判分 |
| 9 | 一致性 | `metric ledger` 让同一指标结构上只有一个值 |
| 10 | 成本 | `token budget` 按整任务算，`prefix caching` 看路由 |
| 11 | 评测 | `BrowseComp` 测找、`DeepResearch Bench` 测写与引 |
| 12 | 上线 | `resume-from-checkpoint` 加 `rainbow deployment` |

## 三层读法：机制、工程、判断

看到一个新方法，先问它属于哪一层。`ReAct`、`Reflexion`、`Toolformer` 是机制层，论文讨论 agent 怎么推理、怎么反思、怎么用工具；`WebArena`、`WebVoyager`、`DeepResearch Bench` 与 `Search-R1` 是工程与评测层，给出环境、接口与打分方式；`evidence coverage`、`effort scaling`、`effective citation count` 是判断层，告诉你什么时候这些方法根本不该上。

三层不能互相替代。机制漂亮不等于工程上跑得稳，工程能跑也不等于这笔账划算。综合报告口径建议按「先单次检索基线、再 `agentic search`、最后才 `deep research`」的顺序推进，每一步都用自己的题库做对照，而不是照搬别人的基准分数。

## 一个可验收的出口

读完十二关，出口标准不是记住某个框架名，而是能对着一个具体研究任务回答四句话：哪些论断需要支撑、哪些已有 `evidence coverage`、每条引用能不能走回同一次 run 的 `retrieval event`、多花的 `token budget` 有没有换来单检索基线拿不到的证据。四句都答得出，说明这条链路已经能用于判断，而不只是读过一篇综述。

对做系统的人还要多一句：长会话的 `prefix caching` 命中取决于下一次调用落到哪个部署；路由一换，缓存复用率会掉。这一句答不出来，前面四句答得再好也算不对成本。

## 语料边界与口径

一手论文逐字留存，用于机制与术语的精确写法：DeepResearcher、BrowseComp、Search-R1、R1-Searcher、WebDancer、WebWalker、Mind2Web、WebVoyager、WebArena、Humanity's Last Exam、FActScore、DeepResearch Bench、长文本事实性与 Lost in the Middle，以及 ReAct、Reflexion、Toolformer 与一篇深度研究综述。官方文档给出上线形态：OpenAI Deep Research、Gemini Deep Research、Anthropic 的网页搜索工具与研究系统实践、LangChain Open Deep Research、Exa、smolagents、browser-use 等。

综合报告只补工程判断，比例、成本与趋势一律标注「综合报告口径」。十二关的顺序、场景与速查表属于「延伸，非语料原文」，不加行内代码标记；行内代码只用语料中确实出现的标识符。安全与合规内容只作工程提示，不构成法律意见。