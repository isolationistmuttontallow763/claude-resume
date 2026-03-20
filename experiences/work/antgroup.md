---
company: 蚂蚁集团
company_en: Ant Group
url: https://www.antgroup.com/
location: 杭州
period: 2022/07 -- 2024/02
department: 技术风险部 · 容灾架构组
role: 后端开发工程师
tags: [distributed-system, high-availability, disaster-recovery, java, multi-cloud, database, middleware]
---

# 多活容灾平台

> 核心开发 | 保障支付宝核心链路高可用

## 项目背景

负责蚂蚁集团多活容灾平台的研发，确保支付宝核心链路在机房级故障下的秒级切换能力。平台覆盖 3 个数据中心、2000+ 核心应用。

## 核心工作

### 流量调度引擎
- 设计并实现基于 DNS + SDK 的多层流量调度方案
- 实现机房级故障的 30 秒自动切换，RPO=0
- 构建流量染色体系，支持单元化路由和灰度验证

### 数据一致性保障
- 主导跨机房数据同步方案设计，基于 binlog 实现准实时数据复制
- 设计冲突检测与自动修复机制，数据一致性达 99.999%
- 优化同步延迟，跨城同步 P99 从 3s 降至 500ms

### 容灾演练平台
- 从零构建自动化容灾演练平台，支持一键发起机房级故障模拟
- 实现演练编排引擎，支持串行/并行/条件分支等复杂演练场景
- 年度完成 200+ 次自动化演练，发现并修复 35 个潜在容灾缺陷

### 稳定性治理
- 负责核心链路强弱依赖梳理，推动 500+ 弱依赖降级改造
- 设计实现全链路压测染色方案，支撑双十一全链路压测

## 量化成果
- 故障切换时间：30 秒（RPO=0）
- 跨城同步延迟 P99：3s → 500ms
- 年度自动化演练：200+ 次
- 弱依赖降级改造：500+
- 覆盖核心应用：2000+

## 技术栈
Java (SpringBoot), MySQL, OceanBase, ZooKeeper, RocketMQ, Diamond, SOFA Stack
