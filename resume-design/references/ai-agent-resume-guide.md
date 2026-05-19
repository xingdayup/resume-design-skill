# AI Agent / LLM / RAG Resume Reference

## Quick Rewrite Pattern

Use compressed STAR in 1-3 sentences:

```text
在 [场景与规模] 下，为 [目标指标]，采用 [方案 A + 关键技术名]，[你本人主导的动作]，最终实现 [量化结果 / 明确对比]。
```

Bad:

```text
负责 RAG 模块，使用了向量数据库。
```

Better:

```text
在日均 1 万+ 问答请求的内部知识库场景下，为降低幻觉与尾延迟，采用混合检索（向量 + BM25）+ Cross-Encoder 重排，并落地 Redis 热点缓存与批量向量化配置，将 P95 端到端延迟从 800ms 降至 320ms，人工抽检回答准确率从 72% 提升至 86%。
```

## Quantification Menu

- Performance: QPS/RPS, P95/P99 latency, TTFT, single-request cost.
- Quality: accuracy, recall, F1, MRR, nDCG, user rating, bad-case ratio.
- Scale: documents, vectors, tenants, shards, DAU, conversation turns, tool calls.
- Efficiency/cost: token reduction, GPU usage, human time saved, iteration cycle.
- Stability: availability, error rate, circuit-breaker events, incident reduction.

If there is no production metric, use honest alternatives:

```text
在自建 200 条问答集上，F1 从 0.61 提升至 0.79。
压测单机 X req/s 时 P95 Y ms（环境：...）。
```

## Skills Section Templates

Python:

```text
语言与运行时：Python 3.11+（类型注解 / asyncio）
Web 与 API：FastAPI、Uvicorn、Pydantic v2
Agent 与编排：LangChain、LangGraph（或 AutoGen、自研状态机）
模型与网关：OpenAI 兼容 API、vLLM / Ollama、提示词与工具 Schema 治理
检索与向量：Milvus / Qdrant / Weaviate、Elasticsearch（BM25）、混合检索、重排模型
数据与缓存：PostgreSQL、Redis（会话 / 缓存 / 限流计数）
可观测：OpenTelemetry、LangSmith / Langfuse、结构化日志
部署与工程：Docker、Kubernetes、GitHub Actions / GitLab CI
```

Java:

```text
语言：Java 17+
框架：Spring Boot 3、Spring WebFlux 或 Spring MVC
集成与韧性：OpenFeign、Resilience4j（熔断 / 限流 / 重试）
检索：Elasticsearch Java API、Milvus/Qdrant 客户端或 HTTP 向量服务
数据：Spring Data JPA / MyBatis、PostgreSQL、Redis
可观测：Micrometer、Prometheus、Grafana
构建与部署：Maven / Gradle、Docker、Kubernetes
```

Go:

```text
语言：Go 1.22+
Web 与 RPC：Gin / Fiber / Echo、gRPC、protobuf
Agent 相关：高性能 LLM 代理、流式 chunk 转发、工具执行器、连接池与背压
检索与存储：Redis、PostgreSQL、Elasticsearch
可观测：OpenTelemetry Go、Prometheus、Grafana、zap / slog
部署：Docker、Kubernetes、健康检查与优雅退出
```

## Project Templates

Python Agent platform:

```text
项目名称：企业级 AI Agent 智能助手平台
项目描述：基于大模型的企业级智能客服与知识助手系统，支持多轮对话、知识库检索、工具调用与人工兜底；面向内部员工或外部客户，对接企业文档与工单系统，满足合规与审计要求。
技术栈：Python, FastAPI, LangChain, LangGraph, Milvus, Redis, PostgreSQL
核心职责：
1. 设计并实现 Agent 多步编排与状态持久化，支持工具失败重试与人工介入节点，日均稳定处理 X 万轮对话。
2. 搭建 RAG 流水线：文档解析、分块、向量化与增量更新，并实现混合检索 + 重排序，将 Top-5 命中率从 X% 提升至 Y%。
3. 落地会话级记忆与业务记忆分层策略，结合 Redis TTL 与 PostgreSQL 归档，将长会话上下文成本降低约 Z%。
4. 与模型网关联调流式输出与限流熔断，将端到端 P95 延迟控制在 X ms 内。
```

Java LLM service:

```text
项目名称：企业级智能问答与 Agent 编排服务平台
技术栈：Java 17, Spring Boot 3, Spring WebFlux, OpenFeign, Resilience4j, Elasticsearch, Redis, PostgreSQL
核心职责：
1. 设计并实现模型网关调用层：流式 SSE、超时重试、熔断与配额，保障核心链路可用性达 X%。
2. 封装工具执行与权限校验，与内部 CRM/工单 API 集成；工具失败时降级为纯 RAG 回答。
3. 主导检索策略编排：查询改写、结果合并与重排结果融合，将业务相关问题 Top-3 命中率提升 X%。
4. 使用 Micrometer + Prometheus 搭建核心指标大盘，缩短平均故障定位时间。
```

Go LLM gateway:

```text
项目名称：高并发 LLM 网关与 Agent 执行引擎
技术栈：Go, Gin/Fiber, gRPC, Redis, PostgreSQL, OpenTelemetry, Prometheus, Kubernetes
核心职责：
1. 实现高性能流式代理：chunk 转发、连接复用、优雅关闭，单机压测支撑 X k QPS（写明环境）。
2. 设计工具执行沙箱与超时控制，隔离用户输入与下游 HTTP 调用，降低 SSRF 与资源耗尽风险。
3. 基于 Redis 的令牌桶与滑动窗口限流，按租户与模型维度配额，保障核心客户 SLA。
4. 全链路 Trace ID 贯通网关、工具与向量检索，可观测数据在 P95 X ms 内完成上报。
```

## Module Phrases

Agent orchestration:

- 基于 LangGraph / 自研有向图将业务拆成「意图识别 -> 规划 -> 工具调用 -> 反思 -> 最终回复」多节点流程，状态持久化至 Redis/DB，支持断点续跑与人工接管。
- 配置最大步数、最大工具调用次数、重复调用检测，将异常会话占比从 X% 降至 Y%。
- 对敏感操作设计确认节点与二次校验，满足业务风控要求。

RAG retrieval:

- 搭建解析 -> 清洗 -> 分块 -> 向量化 -> 索引全链路，支持 PDF/Word/HTML/表格等格式，全量索引 X 万篇、增量更新延迟 < X 分钟。
- 采用稠密向量检索 + BM25 混合召回，并用 Cross-Encoder / 轻量重排模型精排，Recall@5 从 X 提升至 Y（Z 条标注集）。
- 针对短问句、指代、多跳问题引入查询改写 / HyDE / 子查询分解，「检索为空」类 bad case 下降 X%。

Memory:

- 设计会话级短期记忆（Redis）+ 用户级长期偏好（PostgreSQL）分层存储，关键字段满足审计与追溯。
- 采用摘要压缩 + 滑动窗口策略，平均每轮 token 消耗降低 X%，多轮主题连贯性经人工抽检达标。

Tools:

- 基于 OpenAPI / JSON Schema 统一工具描述与入参校验，对接内部 HTTP API、只读 SQL、检索服务。
- 为工具调用增加鉴权、租户隔离、超时、重试与幂等键，失败时自动降级为纯模型回答或固定话术，工具成功率从 X% 提升至 Y%。

Routing and reliability:

- 实现主备模型与多供应商路由，按成本 / 延迟 / 能力配置策略，故障时自动切换，核心链路可用性 X%。
- 对 429、5xx、超时实施指数退避 + 熔断 + 舱壁隔离，并结合热点问答缓存削减峰值依赖。

Observability:

- 接入 OpenTelemetry，为请求生成 Trace ID，贯通网关、Agent、检索、工具、模型调用。
- 定义核心 SLI（P95 延迟、错误率、工具失败率）与 SLO，接入告警与值班流程。

## Common Fixes

Vague:

```text
修改前：负责公司 AI 项目开发。
修改后：负责企业知识库问答子系统：基于 FastAPI + Milvus 实现混合检索与重排，覆盖 X 个业务线、Y 万份文档，日均 Z 万次查询。
```

No metric:

```text
修改前：显著降低了延迟。
修改后：将检索链路 P95 延迟从 650ms 降至 280ms（含 Redis 缓存与批量向量优化）。
```

Tech stack only:

```text
修改前：使用 Python、LangChain、向量数据库、Redis。
修改后：使用 Python + LangChain 搭建 Agent；向量检索采用 Milvus HNSW 索引，Redis 缓存热点 query 的检索结果，命中后延迟 < 50ms。
```

Document-like project description:

```text
修改前：本系统是一个基于大模型的智能问答系统，用户输入问题，系统检索知识库并返回答案。
修改后：面向一线客服场景，打通多轮对话与工单检索；本人负责检索与重排，通过混合检索 + Cross-Encoder 将 Top-1 准确率从 52% 提升至 71%，P95 延迟满足 SLA 400ms。
```

## Final Self-Check

1. Can this experience be explained for 8-10 minutes in an interview?
2. Are all numbers traceable to a source, sampling method, environment, or honest offline evaluation?
3. Are keywords aligned to the target JD without fabricating experience?
