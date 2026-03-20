---
company: 腾讯云
company_en: Tencent Cloud
url: https://cloud.tencent.com/
location: 深圳
period: 2021/07 -- 2022/06
department: 云产品部 · 对象存储组
role: 后端开发实习生
tags: [storage, distributed-system, go, performance-optimization, object-storage]
---

# COS 对象存储服务

> 后端开发实习生

## 核心工作

### 冷热数据分层
- 参与对象存储冷热分层功能开发，实现基于访问频率的自动数据迁移
- 设计生命周期规则引擎，支持按前缀、标签、时间的灵活策略配置
- 冷数据存储成本降低 40%

### 性能优化
- 优化大文件分片上传逻辑，并发度自适应调整，上传吞吐量提升 35%
- 排查并修复 Compaction 导致的长尾延迟问题，P99 读延迟降低 60%

### 监控体系
- 构建存储集群健康度评分系统，整合 15 项指标的综合评估
- 对接 Grafana 可视化大盘，成为 SRE 团队日常巡检标准工具

## 量化成果
- 冷数据成本降低：40%
- 上传吞吐量提升：35%
- P99 读延迟降低：60%

## 技术栈
Go, C++, LevelDB, RocksDB, gRPC, Prometheus, Grafana
