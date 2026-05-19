# Resume Design Skill 使用手册

> 面向 AI Agent / LLM 应用 / RAG / 智能客服岗位的简历诊断、改写与 JD 定制 skill。

## 目录

- [功能简介](#功能简介)
- [适用场景](#适用场景)
- [目录结构](#目录结构)
- [在 Codex 中使用](#在-codex-中使用)
- [在 Claude Code 中安装](#在-claude-code-中安装)
- [在 Claude.ai 中安装](#在-claudeai-中安装)
- [常用提示词](#常用提示词)
- [输出规范](#输出规范)
- [常见问题](#常见问题)
- [参考资料](#参考资料)

## 功能简介

`resume-design` 是一个简历设计 skill，用于帮助 AI 助手按技术招聘视角处理简历：

- 诊断简历中「描述笼统、没有量化、只堆技术栈、职责边界不清」等问题。
- 将项目经历压缩成适合简历的 STAR bullet。
- 针对 AI Agent、LLM 应用、RAG、智能客服、模型网关等岗位优化关键词。
- 按 Python / Java / Go 技术路线整理技能栏与项目模板。
- 保持真实边界，不虚构数据、客户名、线上规模或团队贡献。

## 适用场景

适合在以下任务中使用：

- 「帮我改一版 AI Agent 岗位简历」
- 「按这个 JD 优化我的项目经历」
- 「把我的 RAG 项目写进简历」
- 「诊断这份简历哪里不像技术岗」
- 「把项目 bullet 写得更有结果和指标」
- 「我没有线上数据，怎么诚实地写评测结果」

不适合用于：

- 编造工作经历、客户名称或业务指标。
- 生成无法在面试中自洽解释的夸张描述。
- 替代真实的求职材料核验。

## 目录结构

当前 skill 目录结构：

```text
resume-design/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    └── ai-agent-resume-guide.md
```

核心文件说明：

- `SKILL.md`：触发条件、工作流程和输出约束。
- `references/ai-agent-resume-guide.md`：详细模板、模块句式、项目写法和常见问题对照。
- `agents/openai.yaml`：Codex UI 展示信息。

## 在 Codex 中使用

将 `resume-design` 目录复制到：

```text
~/.codex/skills/resume-design
```

在 Codex 中直接提出相关任务即可自动触发，例如：

```text
使用 resume-design，帮我诊断这份简历并按 AI Agent 岗位改写。
```

或：

```text
请按目标 JD 优化我的 RAG 项目经历，保留真实边界，没有数据的地方用 [需补充] 标记。
```

## 在 Claude Code 中安装

Claude Code 支持个人级和项目级 skills。

### 方式一：安装为个人 skill

个人 skill 对所有 Claude Code 项目生效。

Windows PowerShell：

```powershell
$target = "$env:USERPROFILE\.claude\skills\resume-design"
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.claude\skills" | Out-Null
Copy-Item -Recurse -Force ".\resume-design" $target
```

macOS / Linux：

```bash
mkdir -p ~/.claude/skills
cp -R ./resume-design ~/.claude/skills/resume-design
```

启动 Claude Code 后测试：

```bash
claude
```

在 Claude Code 中输入：

```text
/resume-design 帮我诊断这份 AI Agent 简历
```

也可以自然语言触发：

```text
帮我把这份简历改成更适合 RAG 工程师岗位的版本。
```

### 方式二：安装为项目级 skill

项目级 skill 只在当前仓库生效，适合团队共享。

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force -Path ".claude\skills" | Out-Null
Copy-Item -Recurse -Force ".\resume-design" ".claude\skills\resume-design"
```

macOS / Linux：

```bash
mkdir -p .claude/skills
cp -R ./resume-design .claude/skills/resume-design
```

项目结构应类似：

```text
your-project/
└── .claude/
    └── skills/
        └── resume-design/
            ├── SKILL.md
            └── references/
                └── ai-agent-resume-guide.md
```

### 安装后验证

在 Claude Code 中执行：

```text
/resume-design
```

如果命令可见并能响应，说明安装成功。若刚创建了 `.claude/skills` 顶层目录但 Claude Code 没识别，重启 Claude Code 后再试。

## 在 Claude.ai 中安装

Claude.ai 的自定义 skill 通常需要上传 zip 包。打包时必须让 zip 内部包含 skill 目录本身，而不是把 `SKILL.md` 直接放在 zip 根目录。

正确结构：

```text
resume-design.zip
└── resume-design/
    ├── SKILL.md
    └── references/
        └── ai-agent-resume-guide.md
```

Windows PowerShell 打包：

```powershell
Compress-Archive -Path ".\resume-design" -DestinationPath ".\resume-design.zip" -Force
```

macOS / Linux 打包：

```bash
zip -r resume-design.zip resume-design
```

上传后可用类似提示词测试：

```text
使用 resume-design skill，帮我把这份简历改成 AI Agent / RAG 岗位导向，并标出需要补充真实数据的位置。
```

## 常用提示词

### 简历诊断

```text
使用 resume-design，按技术面试官视角诊断这份简历。请优先指出会影响通过率的问题，并给出修改示例。
```

### JD 定制

```text
使用 resume-design，根据下面 JD 优化我的简历。要求：
1. 只对齐真实经历，不编造；
2. 把 JD 关键词自然前置；
3. 没有数据的位置用 [需补充] 标记。
```

### 项目经历改写

```text
使用 resume-design，把下面 RAG 项目改写成 4 条简历 bullet。每条包含场景、动作、技术方案和结果；没有指标时给出可替换的指标口径。
```

### 技能栏整理

```text
使用 resume-design，按 AI Agent / LLM 应用岗位重写技能栏。按语言、后端、Agent、RAG、数据、可观测、部署分组。
```

### 应届生项目包装

```text
使用 resume-design，我是应届生，没有线上数据。请把我的个人 RAG 项目写得专业但诚实，突出评测集、实验记录和可复现代码。
```

## 输出规范

推荐输出结构：

```text
## 主要问题
- ...

## 修改建议
- ...

## 改写版本
- ...

## 需要补充的数据
- ...
```

改写原则：

- 优先写「负责模块 + 技术动作 + 指标结果」。
- 少写「参与、熟悉、了解」，多写可验证动作。
- 没有线上数据时，使用离线评测、压测、人工抽检、日志采样等诚实口径。
- 涉及客户、公司、内部数据时做脱敏。
- 不把团队成果全部写成个人独立成果。

## 常见问题

### Claude Code 找不到 `/resume-design`

检查目录是否正确：

```text
~/.claude/skills/resume-design/SKILL.md
```

或项目级：

```text
.claude/skills/resume-design/SKILL.md
```

如果是在 Claude Code 运行后才新建了 `.claude/skills` 顶层目录，重启 Claude Code。

### Claude 没有自动触发 skill

可以直接输入：

```text
/resume-design
```

或在提示词中明确写：

```text
使用 resume-design skill ...
```

### 能不能把 Codex skill 直接给 Claude 用

可以。这个 skill 的核心是标准 `SKILL.md` + `references/` 结构，Claude Code 与 Claude.ai 都能识别类似结构。Claude Code 更推荐放在 `.claude/skills/<skill-name>/SKILL.md` 或 `~/.claude/skills/<skill-name>/SKILL.md`。

## 参考资料

- [Claude Code Skills 官方文档](https://code.claude.com/docs/en/skills)
- [Claude.ai 创建自定义 Skills 文档](https://claude.com/docs/skills/how-to)
- [Claude Code Plugins 文档](https://code.claude.com/docs/en/plugins)
