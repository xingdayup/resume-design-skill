---
name: resume-design
description: AI Agent, LLM application, RAG, intelligent customer service, and backend-oriented technical resume design, critique, rewriting, and JD-targeted tailoring. Use when Codex needs to read a resume or resume draft, diagnose weak bullets, rewrite project experience, optimize skills sections, align keywords to a target JD, or create truthful quantified descriptions for AI Agent/LLM/RAG roles in Chinese or English.
---

# Resume Design

## Core Standard

Optimize resumes for AI Agent / LLM application / RAG roles by making each claim:

- **True**: do not fabricate experience, customer names, scale, or metrics.
- **Specific**: name the owned module, scenario, technical choice, and collaboration boundary.
- **Quantified**: prefer before/after metrics, offline evaluation, pressure test numbers, scale, cost, latency, accuracy, stability, or verified qualitative evidence.
- **Interview-expandable**: every important bullet should support an 8-10 minute interview explanation covering background, solution, tradeoff, metric source, and retrospective.
- **JD-aligned**: move target JD keywords forward when they match real experience.

For detailed templates and example phrases, read `references/ai-agent-resume-guide.md` only when needed.

## Workflow

1. **Read inputs**
   - If given a resume file, extract existing structure, projects, skills, education, work history, and metrics.
   - If given a target JD, identify required keywords, seniority signals, and role priorities.
   - If no JD is given, default to AI Agent / LLM application / RAG engineering roles.

2. **Diagnose first**
   - Lead with concrete issues: vague ownership, unquantified results, name-only tech stacks, overlong paragraphs, leakage risk, irrelevant CRUD content, or claims that cannot survive interview follow-up.
   - Do not rewrite by inflating claims. Mark missing data as placeholders or ask for exact numbers when the output depends on them.

3. **Rewrite using compressed STAR**
   - Compress Situation, Task, Action, Result into 1-3 resume sentences.
   - Use this pattern when useful: `在 [场景与规模] 下，为 [目标指标]，采用 [方案 + 技术]，[本人动作]，最终实现 [量化结果/明确对比]。`
   - Prefer active verbs such as `设计并实现`, `主导`, `落地`, `优化`, `推动上线`, `排查并修复`, `建立`.

4. **Shape sections**
   - Skills: group by language/runtime, backend/API, Agent/model, retrieval/data, async/task, observability/deployment.
   - Projects: include project name, context, tech stack, role boundary, core responsibilities, technical highlights, and results.
   - Summary: 1-3 lines that state years/background, target direction, strongest ownership, and strongest metric.

5. **Validate**
   - Check that numbers have a source or honest label such as `自建 200 条评测集`, `本地压测`, `人工抽检`, or `日志采样`.
   - Check that team outcomes are not written as sole ownership unless the user truly owned them.
   - Check that sensitive company/customer/data names are anonymized.
   - Check that every bullet contains an action and a reason/result, not only technology nouns.

## Role Emphasis

- **Student / beginner**: emphasize 1-2 deep projects, reproducible code, evaluation set, experiment records, and honest offline metrics.
- **1-3 years experience**: emphasize ownership, production results, collaboration boundary, incident/cost/latency/evaluation work, and technical tradeoffs.
- **Career switcher**: translate prior experience into stability, performance, API contracts, ETL, data quality, evaluation, requirement decomposition, and metric thinking; compress unrelated legacy work.

## Output Rules

- Write in the resume's language unless the user requests otherwise.
- Keep bullets concise and scannable; avoid marketing tone, emojis, and casual wording.
- Use placeholders like `X`, `Y`, `Z`, `XX%`, or `[需补充]` only when the user has not supplied verifiable data.
- When critiquing, provide fix examples directly after the issue.
- When rewriting, preserve factual boundaries and explicitly label assumptions.
