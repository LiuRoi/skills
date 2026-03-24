# Skills 使用索引

> 这是我的个人 skill 收藏，针对我的工作流程和编码习惯优化。

---

## 目录

- [Superpowers 系列](#superpowers-系列-核心工作流)
- [TDD / 测试系列](#tdd--测试系列)
- [Impeccable 设计系列](#impeccable-设计系列)
- [前端框架系列](#前端框架系列)
- [代码质量系列](#代码质量系列)
- [文档工具系列](#文档工具系列)
- [开发工具系列](#开发工具系列)
- [设计工具系列](#设计工具系列)
- [Design System 系列](#design-system-系列)

---

## Superpowers 系列（核心工作流）

这一系列是我的**主力工作流**，从想法到上线全覆盖。

| Skill | 用途 |
|-------|------|
| **using-superpowers** | 每次对话开始时调用，确立 skill 调用规范 |
| **brainstorming** | 任何创意工作之前必须使用，探索意图、需求、设计 |
| **writing-plans** | 将设计转化为可执行的任务清单 |
| **subagent-driven-development** | 子 agent 驱动开发，每任务配 spec+code 两阶段审查 |
| **executing-plans** | 批量执行计划，有检查点，适合跨 session |
| **finishing-a-development-branch** | 完成开发后的分支处理：merge、PR 或清理 |
| **verification-before-completion** | 完成前必须验证，证据优于断言 |
| **requesting-code-review** | 请求代码审查 |
| **receiving-code-review** | 接收审查反馈，验证后实施，不盲从 |
| **dispatching-parallel-agents** | 并行分发独立任务 |
| **using-git-worktrees** | 创建隔离的工作空间 |

**典型工作流**：

```
brainstorming → writing-plans → subagent-driven-development
                                              ↓
                              using-git-worktrees (隔离环境)
                                              ↓
                              verification-before-completion
                                              ↓
                              requesting-code-review / receiving-code-review
                                              ↓
                              finishing-a-development-branch
```

---

## TDD / 测试系列

| Skill | 用途 |
|-------|------|
| **test-driven-development** | 测试优先，写测试再看它失败，再写代码通过 |
| **tdd-workflow** | 中文版 TDD 工作流，80%+ 覆盖率要求 |
| **systematic-debugging** | 系统调试，发现 bug 先找根因再修 |
| **frontend-testing** | 前端测试，Vitest + React Testing Library |

**规则**：`NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST`

---

## Impeccable 设计系列

这一系列确保我的设计**从一开始就正确**。

| Skill | 用途 |
|-------|------|
| **teach-impeccable** | 一次性建立项目设计上下文，持久化到配置文件 |
| **frontend-design** | 创建独特、生产级的前端界面 |
| **overdrive** | 超越常规限制，技术上雄心勃勃的实现 |
| **polish** | 最终质量打磨，修复间距、对齐、细节问题 |
| **frontend-slides** | 创建动画丰富的 HTML 演示文稿 |
| **web-design-guidelines** | Web 界面合规性审查 |

**Design System 系列**：

| Skill | 用途 |
|-------|------|
| **adapt** | 适配不同屏幕、设备、平台 |
| **arrange** | 改进布局、间距、视觉节奏 |
| **bolder** | 放大安全或无聊的设计 |
| **colorize** | 添加战略性色彩 |
| **critique** | 从 UX 角度评估设计效果 |
| **delight** | 添加惊喜、人格化元素 |
| **distill** | 精简设计到核心本质 |
| **normalize** | 规范化设计以匹配设计系统 |
| **quieter** | 降低过于激进的设计强度 |
| **typeset** | 改进字体、层级、大小 |

**使用顺序**：teach-impeccable → frontend-design → polish / overdrive

---

## 前端框架系列

| Skill | 用途 |
|-------|------|
| **vue** | Vue 3 + Composition API 最佳实践 |
| **vue-best-practices** | Vue 3 + TypeScript + Volar 类型检查 |
| **vueuse-functions** | VueUse 组合式函数应用 |
| **pinia** | Pinia 状态管理 |
| **vite** | Vite 构建工具配置 |

---

## 代码质量系列

| Skill | 用途 |
|-------|------|
| **code-review-excellence** | 全面的代码审查指导 |
| **code-documentation-doc-generate** | API 文档、架构图、用户指南生成 |
| **update-docs** | 代码变更后更新文档 |
| **changelog-generator** | 从 git commits 自动生成用户友好的变更日志 |

---

## 文档工具系列

| Skill | 用途 |
|-------|------|
| **docx** | Word 文档 (.docx) 的创建、编辑、转换 |
| **readme-generation** | README 文件生成 |

---

## 开发工具系列

| Skill | 用途 |
|-------|------|
| **chrome-devtools** | 浏览器调试、性能分析、网络请求 |
| **jira-workflow-creator** | 企业级 Jira 工作流创建 |

---

## Obsidian 系列

| Skill | 用途 |
|-------|------|
| **obsidian-sdk-patterns** | Obsidian 插件 TypeScript 模式 |

---

## Skill 编写系列

| Skill | 用途 |
|-------|------|
| **writing-skills** | 创建、编辑、验证 skill |

---

## 使用提示

1. **每次对话开始**：先调用 `using-superpowers`，它会告诉你哪些 skill 适用于当前任务

2. **创意工作**：先 `brainstorming`，不跳过

3. **实现功能**：`teach-impeccable`（如果是 UI）→ `frontend-design` → `polish`

4. **调试问题**：`systematic-debugging`，先找根因

5. **写测试**：`test-driven-development`，测试优先

6. **提交代码**：`verification-before-completion` 确保验证通过后再声称完成
