# 自然接话 · Natural Dialogue

一个给 Codex 用的中文交流插件，处理接话、转发、反馈和对话连续性，同时保留查证、工具执行与文件交付能力。

它把日常交流里几种反复出现的问题整理成可读取的技能：把私聊转发误当群聊、连续自嘲检讨、每轮硬追问、用固定短句敷衍，以及把推测写成事实。

## 能做什么

| 情况 | 处理方向 |
| --- | --- |
| 私聊分享群聊记录 | 区分当前会话、转发者和原发言人，正常回应分享的内容 |
| 用户吐槽“太 AI、太死板” | 调整后续回应，避免反复检讨或复用同一个笑话 |
| 闲聊与正式任务切换 | 按内容决定长短；调研、代码和文件照常完成 |
| 用户纠正旧信息 | 保留时间、主体、来源和适用范围，避免新旧偏好互相冲突 |
| 学到某种说法 | 根据语境决定是否使用，允许完全不用 |

这是指令型技能插件，不是新模型、模型训练或独立聊天服务器。它不启动后台服务、不自动发消息，也没有自己调用付费 API 的代码。Codex 的正常模型调用仍按你使用的渠道计费。

## 安装为 Codex 插件

本仓库提供原生插件清单和 Git marketplace。已在 **Codex CLI 0.164.0** 上完成插件安装和技能发现检查；其他版本应先确认支持 `codex plugin`。

```bash
codex plugin marketplace add ceshi3hao/codex-natural-dialogue --ref main
codex plugin add natural-dialogue@natural-dialogue-plugins
codex plugin list --marketplace natural-dialogue-plugins --json
```

如果仓库为私有，需要当前 GitHub 账号有访问权限。CLI 通过现有 GitHub/Git 登录处理认证，不要把 token 写进安装命令或提交到仓库。

安装后，在新会话中使用。默认允许 Codex 根据描述自动选择技能；也可明确引用完整技能名：

```text
使用 $natural-dialogue:natural-dialogue，按当前语境正常交流。
```

插件加载不会修改模型权重，也不意味着每条消息都会自动套用所有规则。

### 让某个工作区日常采用

在需要采用的工作区 `AGENTS.md` 中添加路由，不需要复制整份技能内容：

```markdown
中文日常交流、转发分享和聊天方式反馈时，使用已安装的
natural-dialogue:natural-dialogue 技能。读取后沿用，上下文丢失时再读。
它补充接话与场景判断，不替代真实任务执行、领域技能或关系边界。
```

已有类似规则时合并对应段落，避免层层追加冲突要求。

### 仅安装技能

不使用原生插件时，可以把本仓库的
`plugins/natural-dialogue/skills/natural-dialogue/`
复制到 Codex 的用户技能目录，例如 `~/.agents/skills/natural-dialogue/`。
此时显式调用名为 `$natural-dialogue`。选择插件或独立技能一种方式即可，避免重复发现。

## 仓库结构

```text
.agents/plugins/marketplace.json
plugins/natural-dialogue/
├── plugin.json
├── .codex-plugin/plugin.json
├── README.md
└── skills/natural-dialogue/
    ├── SKILL.md
    ├── agents/openai.yaml
    └── references/
        ├── memory.md
        ├── review-cases.json
        └── sources.md
docs/DESIGN.md
```

核心技能约 1500 个字符。记忆说明、来源和审阅案例按需读取，不要求每轮加载整份资料。

## 验证范围

1. 插件通过 `codex plugin add` 安装，列表显示 `installed=true`、`enabled=true`。
2. Codex App Server 的 `skills/list` 识别到唯一的 `natural-dialogue:natural-dialogue` 技能，无解析错误。
3. `SKILL.md` 通过 Skill Creator 格式校验；插件文件与本机安装副本一致，相对参考链接可解析。
4. 附带 **16 个行为审阅案例**，覆盖转发、真实群聊、连续反馈、事实时间差、任务完成、偏好修正等。

这些案例是评估材料，本次没有额外调用模型逐项跑聊天评测。安装通过不能写成“16 项真人化效果全部通过”；改善程度需要看后续连续交流。

## 设计与来源

设计取舍见 [docs/DESIGN.md](docs/DESIGN.md)。

参考了 MaiBot、DSH QQ 项目、AstrBot 生态、SillyTavern、记忆组件及 Humanizer 系列的机制，并重新撰写为适合 Codex 的指导；没有把那些项目的运行代码打包进来。

具体版本、文件和行号见 [来源说明](plugins/natural-dialogue/skills/natural-dialogue/references/sources.md)。功能存在不代表聊天效果最好，用户 Issue 也不作为普遍故障率的证据。

## 移除

```bash
codex plugin remove natural-dialogue@natural-dialogue-plugins
```

手动添加过工作区路由时，移除对应路由。是否移除 marketplace，取决于它是否仍有其他插件在使用。

## 范围

插件沿用用户已指定的身份、称呼和关系边界，不擅自升级关系，不虚构现实经历，不靠随机脾气、错别字或延迟制造真人感。它不会替代领域技能或降低真实任务的验证要求。

未指定额外开源许可证；公开源码或提供下载本身不构成额外许可。引用项目分别遵循各自许可证。
