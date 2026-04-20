# GitNexus 项目分析报告

## 项目概述

**GitNexus** 是一个零服务器的代码智能引擎，通过知识图谱构建代码库的深度架构认知，为 AI 编码助手提供 MCP（Model Context Protocol）集成支持。

## 核心特性

- **客户端知识图谱构建** — 完全运行在浏览器或 CLI 工具中
- **输入方式** — 支持 GitHub 仓库或 ZIP 文件导入
- **输出** — 交互式知识图谱 + 内置 Graph RAG Agent 用于代码探索

## 项目统计

| 指标 | 数值 |
|------|------|
| Stars | 28.2k |
| Forks | 3.2k |
| Releases | 66 |
| 最新版本 | v1.6.2 |

## 技术栈

### CLI 层
- Node.js (原生)
- Tree-sitter 原生绑定
- LadybugDB 原生
- HuggingFace transformers.js (GPU/CPU)
- MCP (stdio)

### Web 层
- 浏览器 (WASM)
- Tree-sitter WASM
- LadybugDB WASM
- transformers.js (WebGPU/WASM)
- LangChain ReAct agent
- Sigma.js + Graphology (WebGL)
- React 18 + TypeScript + Vite + Tailwind v4
- Web Workers + Comlink

## 支持语言

TypeScript, JavaScript, Python, Java, Kotlin, C#, Go, Rust, PHP, Ruby, Swift, C, C++, Dart

## 核心功能

1. **知识图谱构建** — 多阶段流水线：文件树映射、AST 解析（Tree-sitter）、导入/调用解析、社区聚类、执行流追踪、混合搜索索引
2. **MCP 集成** — 暴露 16 个工具（11 个 per-repo + 5 个 group-level），包括影响分析、按进程分组搜索、上下文查询、重命名和 Cypher 访问
3. **Claude Code Hooks** — PreToolUse/PostToolUse hooks 增强搜索并在提交后自动重新索引
4. **Wiki 生成** — 由 LLM 从知识图谱结构生成文档
5. **多仓库支持** — 从单个 MCP 服务器提供多个已索引仓库
6. **Docker 部署** — Cosign 签名镜像，支持供应链保护和 Kubernetes Sigstore policy-controller 集成

## 目录结构

```
gitnexus/
├── gitnexus/                    # 核心 CLI 包
├── gitnexus-shared/             # 共享库
├── gitnexus-web/                # Web UI 应用
├── gitnexus-claude-plugin/      # Claude 集成
├── gitnexus-cursor-integration/ # Cursor 集成
├── gitnexus-test-setup/         # 测试设置
├── deploy/kubernetes/           # K8s 清单
├── docs/                        # 文档
├── eval/                        # 评估工具
├── .claude-plugin/
├── AGENTS.md, ARCHITECTURE.md, CLAUDE.md
├── CONTRIBUTING.md, GUARDRAILS.md, TESTING.md
├── RUNBOOK.md, MIGRATION.md, CHANGELOG.md
├── Dockerfile.web, Dockerfile.cli
├── docker-compose.yaml
└── eslint.config.mjs, prettierrc, .cursorrules
```

## 主要模块

| 模块 | 说明 |
|------|------|
| gitnexus | CLI 索引、MCP 服务器、仓库分析 |
| gitnexus-shared | CLI 和 Web 的公共工具库 |
| gitnexus-web | 基于浏览器的图谱浏览和 AI 聊天界面 |
| gitnexus-claude-plugin | Claude Code 集成（hooks） |

## 许可证

PolyForm Noncommercial
