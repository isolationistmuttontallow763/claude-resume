---
company: 字节跳动
company_en: ByteDance
url: https://www.bytedance.com/
location: 北京
period: 2024/03 -- 至今
department: 基础架构部 · 云原生团队
role: 高级后端开发工程师
tags: [kubernetes, operator, cloud-native, go, architecture, microservice, service-mesh, AI-driven-dev]
---

# 项目一：KubeFlow 智能调度平台

> 2024.06 - 至今 | 技术负责人

## 项目背景

为字节内部 AI 训练集群构建智能资源调度平台，管理 5000+ GPU 节点的训练任务调度，解决资源碎片化、排队时间长、利用率低等问题。

## 核心工作

### 调度引擎设计
- 主导调度引擎架构设计，基于 Kubernetes Scheduler Framework 扩展自定义调度插件
- 实现 Gang Scheduling、Topology-Aware Scheduling 等高级调度策略
- 设计资源预测模型，基于历史数据预测任务资源需求，提升 bin-packing 效率

### 多租户资源管理
- 设计并实现 Quota 管理系统，支持层级配额、弹性借用、抢占优先级
- 构建资源画像系统，实时追踪 2000+ 团队的资源使用模式

### AI 辅助运维
- 基于 Claude Code + TDD 构建 K8s Operator，自动化处理节点故障迁移
- 开发智能告警聚合系统，将告警噪音降低 70%

## 量化成果
- GPU 集群利用率：62% → 85%
- 训练任务排队时间：平均 4h → 45min
- 管理 GPU 节点：5000+
- 告警噪音降低：70%

## 技术栈
Go, Kubernetes, Scheduler Framework, Prometheus, gRPC, etcd, Claude Code, TDD

---

# 项目二：服务网格控制面

> 2024.03 - 2024.06 | 核心开发

## 项目背景

参与字节内部服务网格（Service Mesh）控制面研发，支撑百万级 Pod 的流量治理。

## 核心工作

- 实现基于 xDS 协议的配置分发引擎，支撑 100 万+ Pod 的流量规则下发
- 优化控制面性能，配置推送延迟从 P99 800ms 降至 200ms
- 设计灰度发布策略引擎，支持按流量比例、用户标签、地域等多维度灰度

## 量化成果
- 配置推送延迟 P99：800ms → 200ms
- 支撑 Pod 规模：100 万+

## 技术栈
Go, Envoy, xDS, gRPC, Kubernetes, Istio
