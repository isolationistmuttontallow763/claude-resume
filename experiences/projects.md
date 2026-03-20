---
tags: [RAG, LLM, agent, kubernetes, operator, open-source, python, go]
---

# QueryBase — 企业知识库问答系统

> 个人开源项目 | github.com/zhiyuanlin/querybase | **200+ Stars**

- 基于 LlamaIndex + FastAPI 构建的 RAG 知识库问答系统，支持 PDF/Markdown/Notion 多源接入
- 实现混合检索策略（向量检索 + BM25），召回率较纯向量方案提升 18%
- 设计多轮对话上下文管理，自动摘要历史对话避免 token 溢出
- Docker Compose 一键部署，支持 Ollama 本地模型和 OpenAI API 两种后端

技术栈: Python, LlamaIndex, FastAPI, PostgreSQL + pgvector, Docker

---

# KubeWatch — K8s 集群巡检 Operator

> 个人开源项目 | github.com/zhiyuanlin/kubewatch

- 基于 Kubebuilder 构建的 Kubernetes Operator，定时巡检集群健康状态
- 设计 CRD 声明式配置巡检规则，支持资源水位、证书过期、镜像漏洞等 12 类检查
- 实现 Webhook 告警通知（飞书/钉钉/Slack），异常自动生成修复建议

技术栈: Go, Kubernetes, Kubebuilder, CRD, Helm Charts
