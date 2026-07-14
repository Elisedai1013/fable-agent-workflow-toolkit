<div align="center">

<sub>AI BUILDERS 解读 01 · FIELD GUIDE TO FABLE</sub>

# Steer Agent Workflow

**让 Agent 先识别自己处于哪个工作阶段，再用最小必要方法推进：执行前找未知，执行中留偏差，完成后确认理解。**

<p>
  <a href="https://agentskills.io/"><img src="https://img.shields.io/badge/Agent_Skills-compatible-111827?style=flat-square" alt="Agent Skills compatible"></a>
  <img src="https://img.shields.io/badge/Methods-6-C65F35?style=flat-square" alt="6 methods">
  <img src="https://img.shields.io/badge/Language-中文-555555?style=flat-square" alt="Language: Chinese">
</p>

<a href="https://www.youtube.com/watch?v=9fubhllmsBU">
  <img src="assets/ai-builders-01-cover-landscape.jpg" alt="AI Builders 解读 01：模型变强，人机协作也要重做" width="760">
</a>

<p>
  <a href="skills/steer-agent-workflow/SKILL.md"><strong>查看 Skill</strong></a>
  &nbsp;·&nbsp;
  <a href="skills/steer-agent-workflow/references/method-cards.md">查看方法卡</a>
  &nbsp;·&nbsp;
  <a href="https://www.youtube.com/watch?v=9fubhllmsBU">观看原演讲</a>
  &nbsp;·&nbsp;
  <a href="#关于创作者">Elisedai在创造</a>
</p>

</div>

---

模型越强、Agent 能自主穿越的范围越大，它遇到“地图之外”问题的机会也越多。这个 Skill 不靠一段越来越长的 Prompt 控制所有步骤，而是先判断工作阶段，再自动选择最小必要方法，把未知点、执行偏差、验证证据和关键的人类决策重新变得可见。

## 这个 Skill 会带来什么

| 执行前 | 执行中 | 完成后 |
| :--- | :--- | :--- |
| 发现会改变方案的未知点，探索真正不同的方向，补齐隐含决策 | 记录迫使方案变化的证据、偏差、影响与升级决定 | 核验实际变更，并通过反向测验找出人的理解缺口 |
| **产出：** 更完整的任务说明、原型或执行规格 | **产出：** 可追踪的 implementation notes | **产出：** 决策就绪的验证总结与测验 |

它不会强迫每个任务完整跑完六步。用户处于哪个阶段，就只加载和使用匹配的方法。

## 安装

核心 Skill 位于 [`skills/steer-agent-workflow`](skills/steer-agent-workflow)。请复制整个目录，而不是只复制 `SKILL.md`，否则 Agent 无法读取完整方法卡。

`SKILL.md` 使用平台无关的工作流指令，不依赖 Codex 专属工具。`agents/openai.yaml` 只提供可选的 OpenAI/Codex 客户端展示信息，不影响其他 Agent 使用。

<details>
<summary><strong>查看不同 Agent 的安装方式</strong></summary>

| 使用环境 | 安装位置 | 调用方式 |
| --- | --- | --- |
| Agent Skills-compatible client | 按该客户端规定的 Skill 目录复制完整文件夹 | 自然语言或客户端规定的调用方式 |
| GitHub Copilot | 项目内 `.agents/skills/steer-agent-workflow/` 或个人目录 `~/.agents/skills/steer-agent-workflow/` | 根据 `description` 自动选择 |
| Claude Code | `~/.claude/skills/steer-agent-workflow/` 或项目内 `.claude/skills/` | `/steer-agent-workflow` |
| OpenAI Codex | `~/.codex/skills/steer-agent-workflow/` | `$steer-agent-workflow` |
| 其他 Agent | 将整个目录加入 Agent 可读取的上下文 | 要求先读取 `SKILL.md` |

通用格式与具体路径可参考 [Agent Skills 规范](https://agentskills.io/specification)、[Claude Code Skills](https://code.claude.com/docs/en/slash-commands) 与 [GitHub Copilot Agent Skills](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/add-skills)。

在 Codex 中也可以直接说：

```text
请使用 $skill-installer 安装这个 Skill：
https://github.com/Elisedai1013/steer-agent-workflow-skill/tree/main/skills/steer-agent-workflow
```

</details>

## 30 秒开始使用

可以直接用自然语言点名 Skill：

```text
使用 Steer Agent Workflow Skill。

我准备让 Agent 完成一个我不熟悉的认证模块。先识别当前阶段，选择最小必要方法，帮我找出会改变架构、安全或权限设计的盲点；先不要实现。
```

也可以直接描述需求。只要任务涉及以下情形，Agent 就可以自动触发它：

- 开始复杂任务前找盲点；
- 用差异化原型暴露偏好；
- 通过逐题访谈补齐关键决策；
- 根据参考实现迁移行为与意图；
- 长任务执行中记录实质偏差；
- 审查、合并或发布前确认自己真正理解结果。

## Skill 如何选择方法

| 当前信号 | 自动选择 | 可观察结果 |
| --- | --- | --- |
| 任务未开始，可能存在 unknown unknowns | **盲点扫描** | 待核验未知点与修订后的任务说明 |
| 目标明确，但方向或偏好难以表达 | **差异化原型** | 真正不同的方向、取舍与比较问题 |
| 关键判断仍隐含、矛盾或缺失 | **决策访谈** | 已确认、仍未知、需人决定与执行规格 |
| 用户提供代码、页面或产品参考 | **参考实现** | 语义提取或授权后的重实现，以及差异、假设和授权边界 |
| Agent 正在自主推进较长任务 | **执行偏差记录** | 偏差的触发证据、影响与升级决定 |
| 用户明确要在审查、合并或发布前确认理解 | **完成后反向测验** | 验证总结、问题与理解缺口 |

[打开六种方法的完整执行规则 →](skills/steer-agent-workflow/references/method-cards.md)

## 三个工作阶段

<p align="center">
  <img src="assets/agent-workflow-checkpoints.svg" alt="执行前补全任务地图，执行中记录偏差，完成后确认理解" width="900">
</p>

## 证据与人类决策边界

Skill 会把工作区分为四层：

- **已核验证据：** 来自文件、工具输出、第一方资料或测试；用户陈述对其意图与选择有效，涉及外部状态的说法仍标为待独立核验；
- **AI 假设：** 仍需核验的盲点、解释、风险和方向；
- **需要人决定：** 价值取舍、权限变化、重大范围变化、不可逆动作和风险接受；
- **下一步：** 不隐藏未决事项的最小推进动作。

盲点扫描得到的是待验证问题，不是事实；原型不等于用户验证；参考不等于复制许可；偏差记录不会扩大 Agent 权限；反向测验不能替代代码审查、自动化测试、安全检查、专业审查或真实用户验证。

## Skill 文件

```text
skills/steer-agent-workflow/
├── SKILL.md                 # 触发条件、阶段路由、证据分层和输出契约
├── agents/
│   └── openai.yaml          # 可选：OpenAI/Codex 客户端展示信息
└── references/
    └── method-cards.md      # 六种方法的触发条件、执行步骤、产出和边界
```

仓库根目录只保留 Skill 的发布说明、来源归属和展示素材；不再提供一份需要手动复制的 Prompt 合集。通用运行逻辑只依赖 `SKILL.md` 及其相对引用的 `references/`，其他客户端可以忽略 `agents/openai.yaml`。

## 方法来源与归属

本 Skill 源自 Thariq Shihipar 在 AI Engineer World’s Fair 2026 Main Stage 的分享 *Field Guide to Fable*。官方议程将他的身份标为 `Anthropic, Claude Code`。

- [YouTube｜观看 AI Engineer 发布的原演讲](https://www.youtube.com/watch?v=9fubhllmsBU)
- [AI Engineer World’s Fair 2026｜查看官方议程](https://www.ai.engineer/worldsfair/schedule?q=Field%20Guide%20to%20Fable)

`blind spot pass`、`brainstorms and prototypes`、`interviews`、`references`、`implementation notes` 与 `quiz me` 来自 Thariq 的原分享。中文方法卡、固定输出结构、扩展的安全与权限规则，以及执行前／执行中／完成后的组合路由，由「AI Builders 解读 01」编辑整理，并非 Thariq Shihipar 或 Anthropic 发布的官方 Skill 或工作流。

详见 [NOTICE](NOTICE.md)。

## 关于创作者

<table>
  <tr>
    <td width="230" align="center">
      <img src="assets/wechat-channels-elisedai-qr.jpg" alt="微信视频号 Elisedai在创造 二维码" width="190">
    </td>
    <td>
      <h3>Elisedai在创造</h3>
      <p>大厂 AI 产品经理，Agent 大赛冠军。</p>
      <p>关注全球 AI Builders，分享我的思考，以及正在创造的产品。</p>
      <p><strong>扫码关注微信视频号</strong></p>
    </td>
  </tr>
</table>

## License

本仓库中由 Elisedai 创作的 Skill 指令、中文方法卡与文字说明当前采用 [MIT License](LICENSE)。原演讲、人物、品牌与第三方材料不在该许可范围内，详见 [NOTICE](NOTICE.md)。

---

<div align="center">
  <sub>AI Builders 解读 01 · The map is not the territory.</sub>
</div>
