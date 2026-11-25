# Natural Dialogue / 自然接话

面向 Codex 的中文交流技能插件，版本 1.0.0。

核心指导位于 [SKILL.md](skills/natural-dialogue/SKILL.md)，处理当前会话与转发的区分、连续话题、聊天反馈以及有来源的偏好。任务执行和事实核验继续遵守宿主指令。

从仓库安装时请阅读[根目录 README](../../README.md)。该目录也可独立作为插件包使用；原生插件清单为 `plugin.json`，`.codex-plugin/plugin.json` 提供兼容格式。

[审阅案例](skills/natural-dialogue/references/review-cases.json)包含 16 个场景，没有规定唯一台词，也不代表已通过真实模型评测。

插件本身不启动服务、不请求模型 API、不建独立记忆库，不修改模型权重。做法来源见 [sources.md](skills/natural-dialogue/references/sources.md)。
