# 做法来源与取舍

查阅日期：2026-11-25。这里是设计依据，日常聊天无需加载。以下链接固定到调研时的版本；只借鉴机制并重新撰写指导，没有复制项目运行代码。代码可证明某机制存在，不能单凭它证明真人感或端到端速度。

麦麦：借鉴按语境选择表达、允许零选择、区分聊天规划和回复。保留任务工具；不把多阶段模型调用作为每条私聊的必需步骤。

DSH QQ 项目：借鉴会话、转发、发言对象、记忆来源与修正的区分。稳定人格与临时状态分开；不采用固定等待、随机情绪或模拟生活来制造真人感。DSH 是宿主名称，不是本插件选择或替换的模型。

AstrBot 及插件：借鉴 ContextAware 的场景区分、来源可查的记忆。Giftia 的批处理和接管方式有等待与工具能力的取舍，本插件不接管或削弱现有任务管线；Private Companion 的生活模拟也不移植。

SillyTavern / elizaOS：借鉴分场景风格和对话样例。审阅案例只检验行为，不作为必念台词；长背景按需读取。

Mem0 / Graphiti / Letta：借鉴来源、时间、修订与变更可追踪。它们的数据库和后台机制不打包进本插件；助手自己的推测不能靠重复写入变成事实。

AIRi / Open-LLM-VTuber：可打断和轮次同步值得语音系统单独实现，本插件没有声称增加全双工语音。VTuber 的固定短答、优先追问提示词不适合这里，故不采用。

Humanizer 系列：用于审阅已经写出的模板文字，不负责识别当前会话或证明作者身份。已有同类技能时各司其职，不把禁词当成自然表达的全部。

## 固定版本来源

- [S01: Mai-with-u/MaiBot / prompts/zh-CN/main/planner/default/private/planner_default_private.prompt](https://github.com/Mai-with-u/MaiBot/blob/edf42446f123149c57fc79765dd5a8b004b8524c/prompts/zh-CN/main/planner/default/private/planner_default_private.prompt#L3-L9)
- [S02: Mai-with-u/MaiBot / prompts/zh-CN/main/reply/common/maisaka_expression_selector.prompt](https://github.com/Mai-with-u/MaiBot/blob/edf42446f123149c57fc79765dd5a8b004b8524c/prompts/zh-CN/main/reply/common/maisaka_expression_selector.prompt#L1-L8)
- [S03: Mai-with-u/MaiBot / docs/replyer-prompt-profiles.md](https://github.com/Mai-with-u/MaiBot/blob/edf42446f123149c57fc79765dd5a8b004b8524c/docs/replyer-prompt-profiles.md#L3-L15)
- [S05: Derpyu520/qq-bridge / dsh/agent-presets/qq-chat-v2/agent.cordis.yml](https://github.com/Derpyu520/qq-bridge/blob/12e66d2cdbea1158c085e68c13e80e004989a099/dsh/agent-presets/qq-chat-v2/agent.cordis.yml#L42-L107)
- [S06: Derpyu520/qq-bridge / src/preset-prompt.js](https://github.com/Derpyu520/qq-bridge/blob/12e66d2cdbea1158c085e68c13e80e004989a099/src/preset-prompt.js#L1-L9)
- [S07: aureth-labs/dsh-aurabot-qq / docs/DESIGN.md](https://github.com/aureth-labs/dsh-aurabot-qq/blob/a138d14e3215f052dfa7d6a9dd16c0e409d9752d/docs/DESIGN.md#L5-L17)
- [S08: Britneycode/dsh-fish-soul / lib/behavior.js](https://github.com/Britneycode/dsh-fish-soul/blob/3985eac7426408c4ae20bf6be48aa7fbbc8994c7/lib/behavior.js#L1-L20)
- [S09: Britneycode/dsh-fish-soul / lib/soul-memory.js](https://github.com/Britneycode/dsh-fish-soul/blob/3985eac7426408c4ae20bf6be48aa7fbbc8994c7/lib/soul-memory.js#L550-L588)
- [S11: menglimi/astrbot_plugin_private_companion / README.md](https://github.com/menglimi/astrbot_plugin_private_companion/blob/f305dbcf016b41d99299c878a2028108a1726625/README.md#L59-L72)
- [S12: menglimi/astrbot_plugin_memory_companion / docs/MEMORY_PRECISION_REVIEW_20260906.md](https://github.com/menglimi/astrbot_plugin_memory_companion/blob/3638162dcea045b5621b4891bddfc5cb3137bba2/docs/MEMORY_PRECISION_REVIEW_20260906.md#L3-L15)
- [S13: muyouzhi6/astrbot_plugin_context_aware / README.md](https://github.com/muyouzhi6/astrbot_plugin_context_aware/blob/604bef903b3432e1fdab1407ed2720ae2c855fd2/README.md#L1-L15)
- [S15: Giftia-Lab/astrbot_plugin_giftia / core/memory/atomic.py](https://github.com/Giftia-Lab/astrbot_plugin_giftia/blob/e58eb76093dae3035b0b3dda4fac07f7e64bc958/core/memory/atomic.py#L176-L249)
- [S16: Giftia-Lab/astrbot_plugin_giftia / README.md](https://github.com/Giftia-Lab/astrbot_plugin_giftia/blob/e58eb76093dae3035b0b3dda4fac07f7e64bc958/README.md#L18-L26)
- [S17: SillyTavern/SillyTavern-Docs / Usage/Characters/characterdesign.md](https://github.com/SillyTavern/SillyTavern-Docs/blob/2148f90c413ab379185d869bee23c86caf8048a7/Usage/Characters/characterdesign.md#L31-L67)
- [S18: moeru-ai/airi / packages/stage-layouts/src/composables/use-chat-interruption.ts](https://github.com/moeru-ai/airi/blob/68b35a7b4e7f90fb5e3d6bcbe98c98b17c1cfa9f/packages/stage-layouts/src/composables/use-chat-interruption.ts#L26-L34)
- [S19: Open-LLM-VTuber/Open-LLM-VTuber / prompts/utils/concise_style_prompt.txt](https://github.com/Open-LLM-VTuber/Open-LLM-VTuber/blob/992309c0aa19845960228f880013d4685fde93b5/prompts/utils/concise_style_prompt.txt#L1-L18)
- [S21: mem0ai/mem0 / mem0/configs/prompts.py](https://github.com/mem0ai/mem0/blob/8096993d69396bf97311249206915cadb2eb998f/mem0/configs/prompts.py#L67-L116)
- [S22: getzep/graphiti / graphiti_core/prompts/extract_edges.py](https://github.com/getzep/graphiti/blob/89036119e25624c0db28d89052d72ea3528a641e/graphiti_core/prompts/extract_edges.py#L37-L52)
- [S23: letta-ai/letta-code / README.md](https://github.com/letta-ai/letta-code/blob/c67a0d59263262a947b3dce3420b2c35b46bd829/README.md#L3-L23)
- [S24: elizaOS/eliza / packages/core/src/character-schema.vibe](https://github.com/elizaOS/eliza/blob/47a8001e82edef84b74e4ec194753fe5346d207c/packages/core/src/character-schema.vibe#L128-L145)
- [S25: op7418/Humanizer-zh / SKILL.md](https://github.com/op7418/Humanizer-zh/blob/f4518a8eab97b8bfebc66a89d34320a89bef6930/SKILL.md#L1-L40)
- [S26: blader/humanizer / SKILL.md](https://github.com/blader/humanizer/blob/a32f24407364c74c812b43c15926d638bee1e072/SKILL.md#L1-L40)
- [S27: Giftia-Lab/astrbot_plugin_giftia / docs/zh/session-batching.md](https://github.com/Giftia-Lab/astrbot_plugin_giftia/blob/e58eb76093dae3035b0b3dda4fac07f7e64bc958/docs/zh/session-batching.md#L3-L14)

## 公开反馈的使用范围

[MaiBot #2540](https://github.com/Mai-with-u/MaiBot/issues/2540) 报告表达补充步骤异常可能连带丢弃正文；[Private Companion #730](https://github.com/menglimi/astrbot_plugin_private_companion/issues/730) 讨论固定表达规则与追加要求的冲突。均为查阅时的用户报告，本次没有复现，不据此推断普遍发生率或当前版本仍未修复。

本技能不设置“最像真人”的排名，也不保证提示词可以抹掉模型差异。结构检查、插件发现和后续真实聊天效果分别记录。
