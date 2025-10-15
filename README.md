# Claude Code SubAgents 工作流系统

[![Version](https://img.shields.io/badge/version-v0.1-blue.svg)](docs/claude-workflow-design-v0.1.md)
[![Status](https://img.shields.io/badge/status-设计中-green.svg)]()

一套基于Claude Code SubAgents的完整工作流设计方案，通过专业化代理协作实现从用户初始想法到最终项目交付的全流程自动化管理。

## 🎯 项目概述

本项目旨在构建一个智能化的软件开发工作流系统，通过多个专业化的AI代理协作，自动化处理软件开发的各个环节，包括需求分析、技术调研、架构设计、开发协调、代码实现和质量审查。

## 🏗️ 系统架构

### 核心代理

| 代理 | 职责 | 输出 |
|------|------|------|
| **requirement-analyst** | 需求分析师 | 结构化需求文档 |
| **knowledge-researcher** | 知识研究员 | 技术栈调研报告 |
| **project-architect** | 项目架构师 | 系统架构设计 |
| **development-coordinator** | 开发协调器 | 开发计划和任务分配 |
| **frontend-developer** | 前端开发 | 前端代码实现 |
| **backend-developer** | 后端开发 | 后端代码实现 |
| **code-reviewer** | 代码审查员 | 代码质量报告 |

### 工作流程

```
用户初始想法 → 需求分析 → 背景研究 → 架构规划 → 开发协调 → 代码实现 → 代码审查 → 项目交付
```

## 📁 项目结构

```
cc-workflow/
├── .claude/                   # 工作流配置
│   ├── agents/               # 代理配置文件
│   ├── commands/             # 工作流命令
│   └── workflow.json         # 工作流状态文件
├── docs/                     # 正式文档输出
│   ├── requirements.md       # 需求文档
│   ├── architecture.md       # 架构设计文档
│   ├── development-plan.md   # 开发计划
│   └── progress-report.md    # 进度报告
├── context/                  # 背景资料和参考
│   ├── research/            # 研究资料
│   ├── drafts/              # 草稿和临时文档
│   └── external/            # 外部资料
└── development/             # 开发相关
    ├── tasks/               # 任务分解
    ├── progress/            # 开发进度
    └── reviews/             # 代码审查
```

## 🚀 快速开始

### 状态检查

检查当前工作流状态：
```bash
claude "根据 .claude/workflow.json 和相关文档，告诉我项目当前进度"
```

### 恢复工作

从中断点继续工作：
```bash
claude "我需要继续之前的项目，请检查当前状态并告诉我该怎么做"
```

## 📊 状态管理

### 状态类型

- ✅ **completed**: 已完成
- 🔄 **in_progress**: 进行中  
- ⏳ **pending**: 待开始
- ❌ **blocked**: 阻塞

### 工作流状态文件

工作流状态通过 `.claude/workflow.json` 文件进行管理，包含：
- 当前阶段和任务
- 各代理的完成状态
- 依赖关系和输出文件
- 进度百分比

## 🔧 核心特性

### 🎯 专业化分工
每个代理专注特定领域，确保专业性和效率

### 📈 状态可追溯
完整的进度跟踪和历史记录，支持任意时点的状态查询

### 🔄 中断恢复
支持从任意断点恢复工作，保证工作连续性

### 📝 文档驱动
所有重要信息都以文档形式保存，确保信息完整传递

### 🔧 灵活扩展
可根据项目需要调整代理组合和工作流程

## 📋 使用场景

- **新项目启动**: 从模糊想法到完整项目规划
- **技术调研**: 自动化技术栈分析和方案对比
- **架构设计**: 系统化的架构规划和风险评估
- **开发协调**: 任务分解和进度管理
- **代码审查**: 自动化代码质量检查

## 🛠️ 开发状态

- **当前版本**: v0.1
- **状态**: 设计方案完成，待实现验证
- **创建时间**: 2025-10-14

## 📈 后续计划

1. ✅ 创建具体的代理配置文件
2. ⏳ 实现工作流管理工具
3. ⏳ 测试工作流的实际效果
4. ⏳ 根据测试结果优化设计

## 📖 文档

- [设计方案详细文档](docs/claude-workflow-design-v0.1.md)
- [代理配置说明](.claude/agents/)
- [工作流命令参考](.claude/commands/)

## 📄 许可证

本项目采用 MIT 许可证。

---

**注意**: 这是一个实验性的工作流设计方案，目前处于设计和验证阶段。