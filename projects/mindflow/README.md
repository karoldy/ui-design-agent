# MindFlow — 设计项目概览

> **让记录像 Apple Notes 一样轻量快速，让知识沉淀像 Obsidian 一样结构化。**

MindFlow 是一款 Offline-First 的知识管理型笔记产品，面向知识工作者、研究员、产品经理、设计师、创业者与学生。产品围绕 **快速记录**、**双向链接**、**知识图谱** 三大差异化能力展开，追求「低门槛启动、高上限积累」的体验。

---

## 设计目标

1. **零摩擦启动** — 用户可在 < 2 秒内进入编辑状态，任何感知层面的等待都是设计失败。
2. **知识可视化** — 通过双向链接 [[ 和力导向图，将隐性的思维联系变为显性的可探索网络。
3. **渐进复杂性** — 新手看到的是一个干净的笔记应用；高级用户发现的是链接、标签、图谱构成的系统。
4. **跨平台一致性** — Web（React/TypeScript）、iOS（SwiftUI）、Android（Kotlin/Jetpack Compose）三端视觉风格统一，交互适应该平台惯用范式。

---

## 关键设计决策

| 决策 | 选择 | 理由 |
|------|------|------|
| 编辑器范式 | Markdown 块级编辑器 | 兼容 Obsidian 用户迁移路径，块级结构利于后续块引用和拖拽排序 |
| 导航结构 | 侧边栏主导 + 顶部搜索常驻 | 最大化正文阅读/编辑区域，符合桌面端笔记应用惯例 |
| 视觉风格 | 极简 + 微妙低饱和色 | 响应「干净、专注」定位，降低视觉认知负荷 |
| 字体选择 | 系统字体栈（正文）+ Inter / 等宽字体（代码） | 系统字体保证各平台渲染性能，Inter 提供跨平台一致的 UI 标签 |
| 图标库 | Material Design Icons (MDI) | 跨平台许可证友好，图标覆盖面广，与本项目图标规范一致 |
| 搜索 | 常驻搜索条 + FTS5 本地引擎 | 搜索是知识检索的核心入口，需始终可见且毫秒级响应 |
| 离线优先 | 本地 SQLite + 云端同步（LWW） | 核心卖点之一，所有核心功能在无网状态下完整可用 |

---

## 目录结构

```
mindflow/
├── spec/              # 设计规格说明（从 PRD 提炼的设计要点与约束）
├── wireframes/        # 线框图 / 低保真原型（Lofi 页面布局和流程）
├── mockups/           # 高保真视觉稿（按平台分类）
│   ├── web/           #   Web 桌面端（亮色 6 + 暗色 3）
│   ├── mobile/        #   移动端 Web（3 页面）
│   ├── ios/           #   iOS App 原生（4 页面）
│   └── android/       #   Android App 原生（4 页面）
├── components/        # 组件级设计稿/变体（可交互的组件展示页）
├── assets/            # 图标、图片等静态资源
└── README.md          # 本文件
```

---

## 设计阶段与进度

### Phase 1 — Web MVP（已完成）
- [x] 项目初始化 & 设计策略
- [x] 设计规格确认（spec/design-spec.md）
- [x] 信息架构 & 页面线框图（wireframes/ ×6）
- [x] 核心组件设计稿（components/ ×24：基础13 + 复合10 + 入口1）
- [x] 高保真 mockup（mockups/ ×6：核心3 + 辅助3）
- [ ] 设计审查 & 迭代（当前阶段）

> 交互原型（React + Tailwind）属于开发实现阶段，不在 UI 设计工作空间范围内。

### Phase 2 — Web Full Launch (W13-W24, GA)
- [ ] 知识图谱完整交互设计
- [ ] 双向链接完整交互设计
- [ ] 高级搜索操作符 UI
- [ ] 版本历史 UI
- [ ] 数据导入导出流程 UI

### Phase 3 — Mobile (GA 后)
- [ ] iOS 设计规范
- [ ] Android 设计规范
- [ ] 移动端组件库

---

## 设计约束

- **平台优先**：Web (React/TypeScript) 为首发平台，移动端保持视觉一致但适配各自设计语言
- **可访问性**：WCAG 2.1 AA 为目标，关注对比度、焦点指示、屏幕朗读
- **性能预算**：冷启动渲染 < 2s，输入延迟 < 50ms，搜索 < 500ms（5000条笔记）
- **离线优先**：所有 UI 状态需考虑无网络场景，包括占位展示和同步状态指示
- **图标**: 统一使用 Material Design Icons (MDI)

---

## 参考资源

- [Obsidian Design Guide](https://help.obsidian.md/) — 竞品设计模式参考
- [Apple Notes Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/notes) — 快速笔记范式参考
- [Material Design Icons](https://materialdesignicons.com/) — 本项目图标库
- [WCAG 2.1 AA Checklist](https://www.w3.org/TR/WCAG21/) — 可访问性标准
