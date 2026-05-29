# 🚀 Fleet GitOps

> **GitOps 全链路交付平台** — 代码 Push → CI 构建 → 镜像扫描 → ArgoCD 同步 → 金丝雀发布 → 自动回滚

## 状态

🔲 开发中 — Phase A of [K8s 全栈运维平台](https://github.com/290298661-pixel)

## 架构

```
GitHub Push → Actions CI (lint+test+build+scan) → ArgoCD → Argo Rollouts (Canary) → Production
                                                      ↓
                                            AnalysisTemplate
                                            ├─ NHW 节点健康检查
                                            ├─ Prometheus 指标
                                            └─ 异常自动回滚
```

## 目录

```
fleet-gitops/
├── bootstrap/          # ArgoCD App of Apps 根配置
├── apps/               # 子 Application 定义
│   ├── platform/       # 运维三部曲
│   └── monitoring/     # 可观测性组件
├── overlays/           # 多环境 Kustomize
│   ├── dev/
│   ├── staging/
│   └── production/
└── argocd/             # Rollout + AnalysisTemplate 定义
```

## 快速开始

```bash
# 安装 ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# 部署根 Application
kubectl apply -f bootstrap/root-app.yaml

# 查看同步状态
argocd app list
```
