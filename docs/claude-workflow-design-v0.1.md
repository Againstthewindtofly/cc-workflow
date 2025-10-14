# Claude Code SubAgents 工作流设计方案 v0.1

## 概述

本文档描述了一套基于Claude Code SubAgents的完整工作流设计方案，旨在通过专业化代理协作的方式，从用户初始想法到最终项目交付的全流程自动化管理。

## 代理架构

### 代理列表（6个核心代理）

1. **requirement-analyst** (需求分析师)
2. **knowledge-researcher** (知识研究员)
3. **project-architect** (项目架构师)
4. **development-coordinator** (开发协调器)
5. **frontend-developer** (前端开发)
6. **backend-developer** (后端开发，按需使用)
7. **code-reviewer** (代码审查员)

### 工作流程图

```
用户初始想法
    ↓
【requirement-analyst】需求分析
    ↓
【knowledge-researcher】背景研究
    ↓
【project-architect】架构规划
    ↓
【development-coordinator】开发协调
    ↓
    ├──【frontend-developer】前端开发
    └──【backend-developer】后端开发（如需要）
    ↓
【code-reviewer】代码审查
    ↓
项目交付
```

## 目录结构规范

```
project-root/
├── .claude/
│   ├── agents/                 # 项目级代理配置
│   └── workflow.json          # 工作流状态文件
├── docs/                      # 正式文档输出
│   ├── requirements.md        # 需求文档
│   ├── architecture.md        # 架构设计文档
│   ├── development-plan.md    # 开发计划
│   └── progress-report.md     # 进度报告
├── context/                   # 背景资料和参考
│   ├── research/             # 研究资料
│   │   ├── tech-stack.md     # 技术栈调研
│   │   ├── references.md     # 参考资料
│   │   └── examples/         # 示例代码
│   ├── drafts/               # 草稿和临时文档
│   └── external/             # 外部资料
└── development/              # 开发相关
    ├── tasks/               # 任务分解
    ├── progress/            # 开发进度
    └── reviews/             # 代码审查
```

## 工作流状态管理

### workflow.json 结构

```json
{
  "workflow": {
    "version": "1.0",
    "current_stage": "development-coordinator",
    "current_task": "frontend-ui-development",
    "status": "in_progress",
    "progress": {
      "requirement-analyst": {
        "status": "completed",
        "output_file": "docs/requirements.md",
        "next_agent": "knowledge-researcher"
      },
      "knowledge-researcher": {
        "status": "completed",
        "output_file": "context/research/tech-stack.md",
        "next_agent": "project-architect"
      },
      "project-architect": {
        "status": "completed",
        "output_file": "docs/architecture.md",
        "next_agent": "development-coordinator"
      },
      "development-coordinator": {
        "status": "in_progress",
        "current_task": "分配前端开发任务",
        "output_file": "docs/development-plan.md",
        "next_agent": "frontend-developer"
      },
      "frontend-developer": {
        "status": "pending",
        "depends_on": ["development-coordinator"]
      },
      "backend-developer": {
        "status": "pending",
        "depends_on": ["development-coordinator"]
      },
      "code-reviewer": {
        "status": "pending",
        "depends_on": ["frontend-developer", "backend-developer"]
      }
    }
  }
}
```

## 代理详细工作流程

### 1. requirement-analyst (需求分析师)

**触发条件**：用户提供模糊的项目想法

**工作流程**：
1. 初始对话了解项目想法
2. 引导式功能讨论
3. 技术偏好探索
4. 输出结构化需求文档

**输出文件**：`docs/requirements.md`

**传递给**：`knowledge-researcher`

### 2. knowledge-researcher (知识研究员)

**触发条件**：收到结构化需求文档

**工作流程**：
1. 技术栈分析和推荐
2. 竞品分析
3. 实现方案调研
4. 技术难点识别

**输出文件**：
- `context/research/tech-stack.md`
- `context/research/references.md`

**传递给**：`project-architect`

### 3. project-architect (项目架构师)

**触发条件**：收到需求文档 + 背景知识报告

**工作流程**：
1. 确定最终技术栈
2. 设计系统架构
3. 分解开发任务
4. 风险评估

**输出文件**：`docs/architecture.md`

**传递给**：`development-coordinator`

### 4. development-coordinator (开发协调器)

**触发条件**：收到完整的项目规划

**工作流程**：
1. 版本规划（v1.0可行性验证）
2. 任务分配给开发代理
3. 进度跟踪和协调
4. 质量控制

**输出文件**：
- `docs/development-plan.md`
- `development/tasks/task-breakdown.md`
- 更新 `.claude/workflow.json`

**传递给**：`frontend-developer` / `backend-developer`

### 5. frontend-developer / backend-developer (开发代理)

**触发条件**：收到具体的开发任务

**工作流程**：
1. 任务分析和技术方案
2. 编码实现和调试
3. 自测验证
4. 进度汇报

**输出文件**：
- 完成的功能代码
- 单元测试
- 开发进度报告

### 6. code-reviewer (代码审查员)

**触发条件**：有代码需要审查

**工作流程**：
1. 代码质量检查
2. 安全性和规范验证
3. 问题分类和反馈
4. 修复建议

**输出文件**：
- 代码审查报告
- 问题修复建议

## 状态管理规范

### 状态类型
- **pending**: 待开始
- **in_progress**: 进行中
- **completed**: 已完成
- **blocked**: 阻塞

### 进度表示
- 使用百分比：0%-100%
- 状态图标：✅ 完成 / 🔄 进行中 / ⏳ 待开始 / ❌ 阻塞

### 任务中断恢复机制

1. **状态检查命令**：
   ```bash
   claude "根据 .claude/workflow.json 和相关文档，告诉我项目当前进度"
   claude "我需要继续之前的项目，请检查当前状态并告诉我该怎么做"
   ```

2. **自动状态恢复**：
   - 每个代理开始工作前读取 workflow.json
   - 检查前置依赖是否完成
   - 确认当前任务状态
   - 更新工作流状态

3. **进度可视化**：
   - 定期生成 `docs/progress-report.md`
   - 提供整体进度概览
   - 显示当前任务和阻塞问题

## 文档模板规范

### 统一的文档结构
每个输出文档都包含：
- 基本信息（项目名称、代理、状态、依赖）
- 核心内容（根据代理职责）
- 下一步行动
- 相关文件引用

### 状态同步机制
- 每个代理完成任务后更新 workflow.json
- 文档间通过文件路径建立引用关系
- 支持从任意断点恢复工作

## 协作机制

### 顺序执行
- 严格按照工作流顺序进行
- 每个代理完成后再传递给下一个
- 确保信息完整传递

### 反馈循环
- 后续代理发现问题可反馈给前置代理
- 支持迭代优化和重新处理

### 并行开发
- 前后端代理可并行工作
- 由开发协调器负责同步和集成

## 设计原则

1. **专业化**：每个代理专注特定领域
2. **状态可追溯**：完整的进度跟踪和历史记录
3. **中断恢复**：支持从任意断点恢复工作
4. **文档驱动**：所有重要信息都以文档形式保存
5. **灵活扩展**：可根据项目需要调整代理组合

## 版本信息

- **版本**: v0.1
- **创建时间**: 2024-01-15
- **状态**: 设计方案完成，待实现验证

## 后续计划

1. 创建具体的代理配置文件
2. 实现工作流管理工具
3. 测试工作流的实际效果
4. 根据测试结果优化设计