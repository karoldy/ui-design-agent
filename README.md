# UI Design Agent

Turbo 的 UI 设计工作空间 — 用 AI Agent 驱动设计流程，从需求分析到交互原型一站式管理。

## 快速开始

```bash
# 1. 克隆仓库
git clone <repo-url> && cd ui-design-agent

# 2. 从模板创建新项目
cp -r templates/project-template projects/my-app

# 3. 填写项目信息
# 编辑 projects/my-app/README.md，替换 {{PROJECT_NAME}} 占位符

# 4. 启动设计流程
# 在 Claude Code 中描述需求，Agent 系统会引导你完成设计
```

## 工作流

```
需求输入 → design-strategist → ui-designer → prototype-builder
                  ↑                  ↑               ↑
             design-reviewer ← ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘
                            (随时介入审查)
```

| 阶段 | Agent | 产出物 |
|------|-------|--------|
| 策略 | `design-strategist` | spec 文档、项目 README、设计约束 |
| 视觉 | `ui-designer` | 线框图、mockup、组件设计稿、图标 |
| 原型 | `prototype-builder` | React + Tailwind 交互原型 |
| 审查 | `design-reviewer` | 结构化审查报告（问题 + 建议） |

## 目录结构

```
.
├── projects/             # 各项目的设计资产
│   └── <project-name>/   #   spec/ wireframes/ mockups/ components/ prototypes/ assets/
├── templates/            # 项目模板
│   └── project-template/
├── .claude/agents/       # 专用 Agent 定义
├── CLAUDE.md             # 完整工作说明（Agent 使用指南）
└── README.md             # 本文件
```

## 设计原则

- **文本优先** — HTML/CSS/SVG/Markdown 等可编辑、可版本管理的格式优先于二进制
- **复用优先** — 跨项目通用的组件/样式提炼为共享资产
- **理由驱动** — 每个设计决策附简要理由，方便回顾与迭代
- **实验友好** — 这是设计工作空间，不是生产代码库，容许多方向探索

## 技术栈

| 类型 | 工具 |
|------|------|
| 交互原型 | HTML/CSS, React + Tailwind CSS |
| 静态视觉 | PNG, PDF（通过 `canvas-design` skill） |
| 设计规范 | Markdown |
| 流程图 | Mermaid |
| 文档交付 | PDF, DOCX, PPTX |
| 设计同步 | Claude Design System (claude.ai/design) |

## 依赖

本工作空间依赖 [Claude Code](https://claude.ai/code) 运行。核心能力通过内置 Skill 提供：

- `frontend-design` — UI 美学方向指导
- `canvas-design` — 静态视觉设计
- `theme-factory` — 主题配色与字体
- `web-artifacts-builder` — 复杂交互原型
- `pdf` / `pptx` / `docx` — 文档交付

无需安装额外包，所有工具通过 Claude Code 运行时可用。
