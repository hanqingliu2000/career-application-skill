# 求职申请 Skill

[English](README.md)

一个可复用的求职工作流 skill：从申请者提供的材料建立经历资料库，研究目标企业和岗位，并为具体职位定制和审阅简历。使用通用 Agent Skills `SKILL.md` 格式，面向 Codex 与 Claude Code。

## 功能

- **经历资料库**：整合用户提供的旧简历、申请材料及其他证据，保留原件、来源和未解决的冲突。
- **经历访谈**：使用必需的 `grilling` skill 分轮挖掘工作背景、个人贡献、决策和可验证的成果，不替申请者编造事实。
- **企业与岗位研究**：优先核查官方来源、岗位时效和实际要求，分别记录匹配程度、申请状态和未知信息。
- **简历定制**：根据岗位和证据构建叙事，解释内部术语，保持职责、指标及项目阶段的真实边界。
- **三位独立 reviewer**：分别审阅表达与一致性、招聘匹配度、实际渲染版式；主 agent 负责事实核验，并在修改前向用户展示意见、等待确认。
- **投递检查**：获得明确授权后检查当前岗位、实际附件和自动填入的信息；只有看到提交确认才报告已投递。

各阶段可单独使用。本项目提供工作流程指令，并非自动投递程序，也不保证获得面试。

## 使用条件

- **必需 skill：** [Matt Pocock 的 `grilling`](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md)。需要单独安装并让同一个 agent 能够调用。经历访谈必须使用该依赖；缺失时暂停访谈，但可继续其他独立工作。提问不能为个人经历预设或编造答案。
- 支持 skill 的 Codex 或 Claude Code。实时岗位研究需要网络访问；视觉排版检查需要文档渲染工具。
- **隔离审阅需要运行环境真正实施并验证每位 reviewer 的文件、网络和工具权限限制。** 独立对话或子 agent 本身不等于权限隔离。本仓库提供流程，不提供隔离运行时；如果环境无法实现，应说明限制并在采用降级审阅前征得用户同意，不能声称完整审阅通过。

## 安装

先克隆本仓库及必需依赖，再将两个 skill 目录复制到对应位置。安装前请自行检查第三方内容；如果已存在同名 skill，不要直接覆盖。下列命令假设两个仓库在当前目录，实际路径不同请调整。

```bash
git clone https://github.com/hanqingliu2000/career-application-skill.git
git clone https://github.com/mattpocock/skills.git mattpocock-skills
```

**Codex — 用户级 skill：**

```bash
mkdir -p ~/.agents/skills
cp -R career-application-skill/skills/resume-application ~/.agents/skills/
cp -R mattpocock-skills/skills/productivity/grilling ~/.agents/skills/
```

**Claude Code — 用户级 skill：**

```bash
mkdir -p ~/.claude/skills
cp -R career-application-skill/skills/resume-application ~/.claude/skills/
cp -R mattpocock-skills/skills/productivity/grilling ~/.claude/skills/
```

必要时重启会话，确认两个 skill 都可被发现。Codex 可用 `$resume-application`，Claude Code 可用 `/resume-application`；经历访谈时由本 skill 指示 agent 调用 `grilling`。云端或受管理环境的路径和加载方式可能不同，请参阅平台文档。

## 示例

- “使用求职申请 skill，整理我提供的申请材料，建立经历资料库。”
- “访谈我在这个项目中的个人贡献，并更新资料库。”
- “研究我名单里的企业，寻找与我经历相符的当前岗位。”
- “根据这份职位描述定制简历，并进行三位独立隔离审阅。”

实际投递前须获得明确授权；提供职位链接或生成简历不等于授权提交。请把个人资料和生成的申请材料保存在私有工作区，不要上传到公开仓库。

## 项目结构与平台文档

`skills/resume-application/SKILL.md` 按需指向资料库、岗位研究和简历审阅参考文件。`grilling` 在上游独立维护，本仓库不捆绑其内容。

- [Codex skills 文档](https://developers.openai.com/codex/skills)
- [Claude Code skills 文档](https://code.claude.com/docs/en/skills)
