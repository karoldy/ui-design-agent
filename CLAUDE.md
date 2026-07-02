# CLAUDE.md

## 仓库定位

这是 Turbo 的 UI 设计工作空间，用于管理多个项目的 UI 设计资产与交付物。当前处于初始阶段，随项目推进逐步扩展。

## 目录结构

```
.
├── projects/           # 各项目的设计资产（每个项目一个子目录）
│   └── example-app/    #   ├── spec/ wireframes/ mockups/ components/ assets/ prototypes/ README.md
├── templates/           # 项目模板 & 共享组件模板
│   └── project-template/  # 新项目快速初始化模板
├── .claude/
│   └── agents/          # 专用 Agent 定义
├── CLAUDE.md            # 本文件
└── LICENSE
```

### 项目内部约定

```
project-name/
├── spec/          # 设计规格说明、PRD 提炼的设计要点
├── wireframes/    # 线框图 / 低保真原型
├── mockups/       # 高保真视觉稿
├── components/    # 组件级设计稿 / 变体
├── prototypes/    # 交互原型（HTML/CSS 或 React）
├── assets/        # 图标、图片等静态资源
└── README.md      # 项目设计概要
```

新项目从 `templates/project-template/` 复制初始化。

## 设计工具与输出格式

- 优先使用 HTML/CSS 制作可交互原型（适合现代 Web 项目）
- 静态视觉稿可输出 PNG / PDF
- 设计规范文档用 Markdown
- 图表、流程图可用 Mermaid
- 组件库可与 Claude Design System (claude.ai/design) 同步

### 组件设计稿交互规范

组件设计稿（`components/` 目录下的 `.html` 文件）必须是**可在浏览器中独立运行的可交互页面**，而非静态截图：

- **组件间交互**：页面内嵌完整交互逻辑，点击按钮可弹出 Modal/Drawer、切换 Tab、展开 Accordion 等，所有关联组件在同一页面内协同工作
- **页面间跳转**：多页面场景下，通过 `<a>` 标签或 JS 路由实现页面间导航，每个页面是一个独立的 `.html` 文件，模拟真实应用的路由体验
- **状态覆盖**：单个页面内应展示组件的多个状态（默认、悬停、激活、禁用、加载中、空数据等），可通过页面内控件切换查看
- **自包含**：每个 HTML 文件自包含 CSS 和 JS（内联或同目录引用），不依赖外部构建工具即可在浏览器中打开

## Agent 系统

本项目定义了 4 个专用 Agent，覆盖设计工作流的各个阶段。Agent 定义文件位于 `.claude/agents/` 目录下。

| Agent | 定位 | 职责 |
|-------|------|------|
| `design-strategist` | 策略层 (Opus) | 需求分析 → 设计方向 → 项目初始化（spec/README/目录结构）。只做方向不做执行 |
| `ui-designer` | 执行层 (Sonnet) | 线框图、mockup、组件变体、图标资产。可调用 canvas-design / frontend-design / theme-factory |
| `prototype-builder` | 执行层 (Sonnet) | React + Tailwind 交互原型，用于用户测试和设计验证。可调用 web-artifacts-builder |
| `design-reviewer` | 审查层 (Opus) | 审查一致性、可用性、无障碍、状态覆盖。输出结构化反馈（问题 + 严重程度 + 建议） |

### 协作流程

```
需求输入 → design-strategist（定方向、写 spec）
                ↓
         ui-designer（出视觉稿）
                ↓
         prototype-builder（交互原型，可选）
                ↓
         design-reviewer（审查、反馈）
                ↓
         迭代细化
```

- strategist → designer → prototype-builder 为单向推进，reviewer 可随时介入
- 每个 Agent 独立调用，向它清晰描述当前阶段和期望输出
- Agent 间通过项目目录下的文件传递设计上下文（spec → wireframes → mockups → prototypes）

## 工作方式

- 讨论需求 → 确定方向 → 出方案 → 迭代细化
- 设计决策应附简要理由，方便回顾
- 每个项目需有 README 记录设计目标、约束和关键决策
- 复用优先：跨项目通用的组件/样式应提炼为共享资产
- 复杂任务优先使用专用 Agent，简单任务可直接处理

## 常用技能

| 技能 | 用途 | 主要使用者 |
|------|------|------------|
| `canvas-design` | 海报、静态视觉设计 | ui-designer |
| `frontend-design` | 前端 UI 方向与美学指导 | ui-designer |
| `theme-factory` | 主题配色与字体搭配 | ui-designer, design-strategist |
| `web-artifacts-builder` | 复杂交互原型 (React + Tailwind) | prototype-builder |
| `pdf` / `pptx` / `docx` | 文档类交付物 | 按需 |

## 工具

| 工具 | 用途 |
|------|------|
| DesignSync | 将组件库同步到 Claude Design System (claude.ai/design)，实现设计系统与代码的双向同步 |

## 注意事项

- 这是一个**设计工作空间**，不是生产代码库，容忍实验性探索
- 设计资产以可编辑、可版本管理为原则（文本格式优先于二进制）
- 对第三方品牌/设计系统，先调研再设计，保持一致性
