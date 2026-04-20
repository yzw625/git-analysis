Optimizing tool selection...

Read [](file:///Users/yezhiwen/Desktop/Codebase/GitNexus/README.md#1-1), lines 1 to 100

Read [](file:///Users/yezhiwen/Desktop/Codebase/GitNexus/ARCHITECTURE.md#1-1), lines 1 to 80

## GitNexus 项目概览

**GitNexus** 是一个**代码智能分析平台**，为 AI 代理（如 Cursor、Claude Code 等）构建"代码库神经系统"。核心目标是帮助 AI 理解整个代码库的依赖关系、调用链和执行流。

---

### 🎯 核心功能

1. **代码知识图谱** — 将任何代码库索引成知识图谱，记录：
   - 所有依赖关系
   - 函数/方法调用链
   - 代码簇（功能区域）
   - 执行流

2. **智能工具集** — 通过 MCP（Model Context Protocol）暴露给 AI：
   - `query` — 混合搜索（BM25 + 向量搜索）
   - `impact` — **撞击半径分析**（修改代码会破坏什么）
   - `context` — 查看一个符号的完整上下文（调用者/被调用者）
   - `rename` — 安全的跨文件重命名
   - `detect_changes` — 检测代码变更影响范围

3. **两种使用方式**：
   - **CLI + MCP**（推荐）：本地索引，所有数据在本机，直接集成开发工具
   - **Web UI**：可视化图形浏览器 + AI 聊天，无需安装

---

### 📦 项目结构

| 模块 | 作用 |
|------|------|
| gitnexus | CLI + MCP 服务器、索引管道、知识图谱存储 |
| gitnexus-web | React + Vite 前端，通过 HTTP 调用后端 |
| gitnexus-shared | 共享类型定义 |
| eval | Python 评估框架（基准测试） |

---

### 🔄 工作流程

```
代码库 → 索引分析 → 知识图谱（LadybugDB） → MCP 工具 → AI 代理
```

1. **分析** — 12 阶段流水线解析代码、提取符号、构建图谱
2. **存储** — 保存到 `.gitnexus/` 目录（LadybugDB 格式）
3. **查询** — 通过 MCP 工具、HTTP API 或 CLI 查询
4. **应用** — Cursor、Claude Code 等 AI 工具获得深度上下文

---

### 💡 关键优势

- **全局可见性** — AI 不会遗漏依赖或破坏调用链
- **本地隐私** — 所有数据离线处理，无需上传
- **多语言** — 支持 TypeScript、Python、Java、Go 等（通过 Tree-sitter）
- **多仓库** — 可跨仓库分析（企业功能）

---

### 📄 主要文档

- ARCHITECTURE.md — 架构和代码组织
- AGENTS.md — AI 代理集成规则
- CONTRIBUTING.md — 开发指南