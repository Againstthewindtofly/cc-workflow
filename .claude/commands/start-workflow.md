---
name: start-workflow
description: 启动Claude Code工作流，开始从需求分析到项目交付的完整流程
allowed-tools: Read, Write, Edit, Grep, Glob
---

# 启动Claude Code工作流

这个命令将帮助你启动完整的Claude Code SubAgents工作流，从用户初始想法开始，逐步推进到项目交付。

## 使用方法

```bash
/start-workflow "你的项目想法描述"
```

## 工作流程说明

### 自动执行流程

1. **初始化项目结构**
   - 创建必需的目录结构
   - 初始化工作流状态文件
   - 设置代理配置

2. **启动需求分析**
   - 调用 `requirement-analyst` 代理
   - 与用户进行需求讨论
   - 生成需求文档

3. **技术调研**
   - 调用 `knowledge-researcher` 代理
   - 进行技术栈调研
   - 收集参考资料

4. **架构设计**
   - 调用 `project-architect` 代理
   - 设计系统架构
   - 制定开发计划

5. **开发协调**
   - 调用 `development-coordinator` 代理
   - 任务分配和进度管理
   - 协调开发工作

## 执行步骤

当用户运行 `/start-workflow` 命令时，系统将：

### 第一步：环境检查
```bash
# 检查目录结构
if [ ! -d ".claude" ]; then
    echo "初始化Claude Code工作流环境..."
    mkdir -p .claude/agents
    mkdir -p docs
    mkdir -p context/{research,drafts,external}
    mkdir -p development/{tasks,progress,reviews}
fi

# 检查代理配置
if [ ! -f ".claude/workflow.json" ]; then
    echo "创建初始工作流状态..."
    cat > .claude/workflow.json << 'EOF'
{
  "workflow": {
    "version": "1.0",
    "current_stage": "requirement-analyst",
    "current_task": "项目初始化和需求分析",
    "status": "starting",
    "progress": {}
  }
}
EOF
fi
```

### 第二步：启动需求分析
```bash
echo "🚀 启动Claude Code工作流..."
echo "📋 第一阶段：需求分析"
echo "正在调用 requirement-analyst 代理..."
```

### 第三步：调用第一个代理
现在调用 requirement-analyst 代理开始工作：

```
> 使用 requirement-analyst 代理开始需求分析
> 用户想法：{用户输入的项目想法}
> 请开始与用户进行详细的需求讨论
```

## 用户交互指南

### 需求分析阶段
当 requirement-analyst 代理启动后，它会：
1. 询问你的项目想法和目标
2. 通过提问帮助你完善需求
3. 讨论功能需求和技术偏好
4. 最终生成完整的需求文档

### 如何配合工作流
1. **详细描述你的想法** - 越具体越好
2. **积极回答代理的问题** - 帮助完善需求
3. **提供反馈** - 对代理的建议给出意见
4. **确认需求文档** - 确保准确反映你的想法

## 工作流监控

### 检查进度
使用以下命令随时检查工作流进度：
```bash
claude "请检查当前项目的工作流状态"
```

### 恢复中断的工作
如果工作流被中断：
```bash
claude "我需要继续之前的项目，请帮我恢复工作状态"
```

### 查看具体阶段状态
```bash
claude "显示 {代理名称} 的工作状态和输出"
```

## 预期输出

工作流启动后，你将看到：

### 1. 目录结构创建
```
project-root/
├── .claude/
│   ├── agents/           # 代理配置文件
│   └── workflow.json     # 工作流状态
├── docs/                 # 正式文档输出
├── context/              # 背景资料
└── development/          # 开发相关
```

### 2. 需求文档生成
`docs/requirements.md` - 详细的项目需求文档

### 3. 工作流状态更新
`.claude/workflow.json` - 实时的工作流状态

## 常见问题

### Q: 如何重新开始工作流？
A: 删除 `.claude/workflow.json` 文件，然后重新运行 `/start-workflow`

### Q: 可以跳过某个阶段吗？
A: 可以手动调用特定代理，但要确保前置条件满足

### Q: 如何查看已完成的工作？
A: 查看 `docs/` 目录下的文档和 `development/progress/` 下的进度报告

### Q: 工作流中断了怎么办？
A: 使用 workflow-manager 代理帮助恢复状态

## 最佳实践

1. **充分参与需求讨论** - 这是整个项目的基础
2. **及时提供反馈** - 确保每个阶段的输出符合预期
3. **定期检查进度** - 使用 workflow-manager 监控状态
4. **保存重要决策** - 在文档中记录关键决策和理由

## 示例用法

```bash
# 启动一个电商网站项目
/start-workflow "我想开发一个简单的电商网站，支持用户注册登录、商品浏览、购物车和订单功能"

# 启动一个博客系统项目
/start-workflow "我想创建一个个人博客系统，支持文章发布、评论、标签分类和用户管理"

# 启动一个任务管理应用
/start-workflow "开发一个团队任务管理应用，支持项目创建、任务分配、进度跟踪和团队协作"
```

## 注意事项

1. **确保有足够的上下文** - 工作流需要充分的对话上下文
2. **耐心配合** - 每个阶段都需要时间进行充分的分析和设计
3. **备份重要文件** - 定期备份 `docs/` 和 `.claude/` 目录
4. **遵循代理指引** - 每个代理都会提供具体的下一步指引

---

准备好了吗？运行 `/start-workflow "你的项目想法"` 开始你的项目开发之旅！