# Skill 仓库使用指南

本仓库包含 **38 个 Skill**，覆盖前端开发、UI 设计、动画、测试、文档、Obsidian、工作流等多个领域。每个 Skill 都是独立的指令集，在对应场景下自动激活。

---

## 目录

- [一、前端开发核心](#一前端开发核心)
- [二、UI 设计与实现](#二ui-设计与实现)
- [三、测试与质量](#三测试与质量)
- [四、内容创作与文档](#四内容创作与文档)
- [五、Obsidian 生态](#五obsidian-生态)
- [六、工具与调试](#六工具与调试)
- [七、开发工作流](#七开发工作流)
- [快速参考](#快速参考按场景选-skill)

---

## 一、前端开发核心

### 1. Vue 生态

#### vue
**Vue 3.5+ 核心开发指南**，覆盖响应式系统、组件通信、生命周期、TypeScript 集成。

**核心能力：**
- 响应式系统：`ref()`、`reactive()`、`computed()`、`watch()`/`watchEffect()`
- 组件通信：`defineProps` + `defineEmits`、`defineModel()`、provide/inject
- 生命周期：`onMounted`、`onUnmounted`、`onBeforeUpdate` 等
- TypeScript 集成：类型推导、泛型组件、类型安全 props

**工作流：**
```
新建组件 → <script setup lang="ts"> + ref() 声明状态
复用逻辑 → 提取为 composable（参考 vueuse-functions）
父子通信 → defineProps + defineEmits，v-model 用 defineModel()
```

**相关 Skill：** `vue-best-practices` | `vueuse-functions` | `pinia`

---

#### vue-best-practices
**Vue + TypeScript 类型安全最佳实践**，解决模板报错、props 提取、CSS Modules 等。

**核心规则：**
| 规则 | 说明 |
|------|------|
| `extract-component-props` | 从 .vue 组件提取类型 |
| `vue-tsc-strict-templates` | 捕获模板中的未定义组件 |
| `fallthrough-attributes` | 类型检查透传属性 |
| `strict-css-modules` | 捕获 CSS 类名拼写错误 |
| `volar-3-breaking-changes` | 修复 Volar 3.0 升级问题 |

---

#### pinia
**Vue 官方状态管理库**，支持 Setup Stores、TypeScript、SSR。

**工作流：**
```
定义 Store → defineStore('id', () => { ... })
组件中使用 → const store = useCounterStore()
解构保持响应式 → storeToRefs(store)
测试时 mock → @pinia/testing
```

---

#### vueuse-functions
**VueUse 组合式函数决策指南**，覆盖 200+ 个常用工具函数。

**常用函数：**
| 类别 | 函数 |
|------|------|
| 状态 | `useLocalStorage`, `useStorage` |
| 元素 | `useIntersectionObserver` |
| 事件 | `useDebounceFn`, `useThrottleFn` |
| 主题 | `useDark`, `useColorMode` |

---

### 2. 动画开发（GSAP 系列）

共 **8 个 Skill**，按使用顺序排列：

```
gsap-core (核心引擎) → gsap-timeline (时间线) → gsap-scrolltrigger (滚动)
         ↓
gsap-plugins (插件) | gsap-react/frameworks (框架集成) | gsap-performance/utils (优化)
```

#### gsap-core
**GSAP 核心动画引擎**。单元素动画、缓动函数、stagger、响应式动画。

**核心方法：** `gsap.to()` | `gsap.from()` | `gsap.fromTo()` | `gsap.set()`

```javascript
gsap.to(".box", { x: 100, duration: 1, ease: "power3.out" })
gsap.from(".item", { opacity: 0, y: 20, stagger: 0.1 })

// 响应式 + 减少动画偏好
let mm = gsap.matchMedia()
mm.add("(prefers-reduced-motion: reduce)", () => {
  gsap.set(".box", { x: 100 })
})
```

---

#### gsap-timeline
**多步骤动画编排**，控制时间线、label、嵌套。

```javascript
const tl = gsap.timeline({ defaults: { duration: 0.5 } })
tl.to(".a", { x: 100 }, 0)           // 0秒开始
tl.to(".b", { y: 50 }, "+=0.3")      // 延迟0.3秒
tl.to(".c", { opacity: 0 }, "<0.2")  // 相对上一个
```

---

#### gsap-scrolltrigger
**滚动驱动动画**，pin、scrub、batch。

```javascript
gsap.to(".box", {
  scrollTrigger: {
    trigger: ".box",
    start: "top center",
    scrub: true,
    pin: true
  }
})
```

---

#### gsap-plugins
**GSAP 插件系统**：Flip、Draggable、SplitText、MorphSVG、DrawSVG。

| 插件 | 功能 |
|------|------|
| Flip | 布局变化动画 |
| SplitText | 文字逐字动画 |
| DrawSVG | SVG 路径绘制 |
| Draggable | 拖拽交互 |

---

#### gsap-react / gsap-frameworks
**React/Vue/Svelte 中集成 GSAP**。

**React：**
```javascript
import { useGSAP } from "@gsap/react"
useGSAP(() => { gsap.to(".box", { x: 100 }) }, { scope: container })
```

**Vue：**
```javascript
onMounted(() => {
  const ctx = gsap.context(() => { gsap.to(".box", { x: 100 }) }, container.value)
})
onUnmounted(() => ctx?.revert())
```

---

### 3. 构建工具

#### vite
**Vite 6.x 构建工具配置指南**。

**核心能力：** 开发服务器、生产构建、插件系统、环境变量、Library Mode


---

## 二、UI 设计与实现

### 1. frontend-design 设计系统

**生产级前端界面设计**，避免"AI 感"，追求独特视觉风格。

**设计原则：** OKLCH 色彩系统 | 独特字体搭配 | 不对称布局 | 有意义的动效

---

### 2. impeccable 全栈优化系列

**前端界面全面优化工具**，包含 **23 个子命令**，覆盖设计、构建、评估、优化全流程。

#### 架构设计

impeccable 分为两个核心 **Register（寄存器）**：

| Register | 适用场景 | 设计目标 |
|----------|----------|----------|
| **brand.md** | 品牌站、落地页、营销页面 | 设计即产品，追求独特性 |
| **product.md** | 应用 UI、管理后台、工具界面 | 设计服务于产品，追求熟悉感 |

---

#### 命令分类

##### Build（构建类）

| 命令 | 功能 | 典型用法 |
|------|------|----------|
| `craft [功能]` | 端到端构建功能 | 从设计到实现完整流程 |
| `shape [功能]` | 设计规划 | 在写代码前规划 UX/UI |
| `init` | 项目初始化 | 设置 PRODUCT.md、DESIGN.md |
| `document` | 文档生成 | 从现有代码生成 DESIGN.md |
| `extract [目标]` | 设计系统提取 | 提取可复用的 tokens 和组件 |

##### Evaluate（评估类）

| 命令 | 功能 | 评分维度 |
|------|------|----------|
| `critique [目标]` | UX 设计审查 | 启发式评分、可用性问题 |
| `audit [目标]` | 技术质量检查 | 可访问性、性能、响应式、主题、反模式 |

**audit 评分维度（0-20分）：**

| 维度 | 检查内容 |
|------|----------|
| 可访问性 (A11y) | 对比度、ARIA、键盘导航、语义 HTML |
| 性能 | 布局抖动、动画优化、资源加载 |
| 主题 | 设计 Token、暗色模式、硬编码颜色 |
| 响应式 | 固定宽度、触摸目标、水平滚动 |
| 反模式 | AI 感、渐变文字、玻璃拟态 |

**评级标准：**
- 18-20：Excellent
- 14-17：Good
- 10-13：Acceptable
- 6-9：Poor
- 0-5：Critical

##### Refine（精炼类）

| 命令 | 功能 | 适用场景 |
|------|------|----------|
| `polish [目标]` | 上线前最终打磨 | 综合检查、细节优化 |
| `bolder [目标]` | 放大设计 | 平淡设计需要冲击力 |
| `quieter [目标]` | 降低设计强度 | 激进设计需要克制 |
| `distill [目标]` | 提炼核心 | 移除复杂性 |
| `harden [目标]` | 生产化 | 错误处理、国际化、边界情况 |
| `onboard [目标]` | 引导设计 | 首次使用流程、空状态 |

##### Enhance（增强类）

| 命令 | 功能 |
|------|------|
| `animate [目标]` | 添加有目的的动画 |
| `colorize [目标]` | 为单色 UI 添加策略性色彩 |
| `typeset [目标]` | 排版优化 |
| `layout [目标]` | 修复间距和视觉层次 |
| `delight [目标]` | 添加个性和难忘细节 |
| `overdrive [目标]` | 突破常规限制 |

##### Fix（修复类）

| 命令 | 功能 |
|------|------|
| `clarify [目标]` | UX 文案、标签、错误信息优化 |
| `adapt [目标]` | 不同设备和屏幕尺寸适配 |
| `optimize [目标]` | UI 性能诊断和修复 |

##### Iterate（迭代类）

| 命令 | 功能 |
|------|------|
| `live` | 可视化变体模式，浏览器中选择元素生成替代方案 |

---

#### 典型工作流

**新建项目：**
```
/impeccable init          # 设置项目上下文
/impeccable shape 首页    # 规划设计
/impeccable craft 首页    # 端到端构建
/impeccable audit 首页    # 检查质量
/impeccable polish 首页   # 最终打磨
```

**优化现有页面：**
```
/impeccable audit 首页    # 发现问题
/impeccable layout 首页   # 修复间距
/impeccable animate 首页  # 添加动效
/impeccable polish 首页   # 最终检查
```

---

#### 设计禁令（Absolute Bans）

impeccable 强制禁止以下 AI 常见反模式：

- ❌ 侧边框装饰：`border-left/right > 1px` 作为卡片装饰
- ❌ 渐变文字：`background-clip: text` + 渐变背景
- ❌ 玻璃拟态滥用：作为默认装饰
- ❌ Hero-metric 模板：大数字 + 小标签 + 渐变
- ❌ 相同卡片网格：无限重复的卡片
- ❌ 每节上方的小写标签：01/02/03 或 ABOUT/PROCESS
- ❌ 文字溢出容器：标题在不同断点溢出


---

### 3. pencil-ui-design 工业设计

**使用 Pencil MCP 创建工业级 UI 设计稿**。

**核心能力：**
- 设计系统变量：颜色、字体、间距、圆角、阴影
- 可复用组件：Button、Card、Input、Avatar、Badge
- 图标系统：Material Symbols Rounded（不是 Lucide！）
- 图片处理：AI 生成 + Stock 图片

**工作流：**
```
1. 设置设计系统变量 → mcp_pencil_set_variables
2. 创建可复用组件 → reusable: true
3. 用 I() 插入组件，U() 更新属性，G() 生成图片
4. 截图验证 → mcp_pencil_get_screenshot
```

---

## 三、测试与质量

### frontend-testing
**Dify 前端测试规范**，Vitest + React Testing Library。

**技术栈：** Vitest 4.0.16 | React Testing Library 16.0 | jsdom | nock

**工作流：**
```
1. 分析复杂度 → pnpm analyze-component <路径>
2. 按复杂度排序 → 工具函数 → Hooks → 简单组件 → 复杂组件
3. 逐个编写测试 → 渲染、Props、交互、边界情况
4. 目标覆盖率 → 函数/语句 100%，分支/行 >95%
```

**测试原则：**
- AAA 模式：Arrange → Act → Assert
- 黑盒测试：测试可观察行为
- 单一行为：每个测试验证一个用户行为

---

### tdd-workflow
**测试驱动开发工作流**，强制先写测试再实现。

**核心原则：**
- 测试优先于代码
- 最低 80% 覆盖率（单元 + 集成 + E2E）
- 覆盖所有边缘情况和错误场景

**TDD 步骤：**
```
1. 编写用户旅程
2. 生成测试用例（正常 + 边界 + 错误）
3. 运行测试（应该失败）
4. 实现代码使测试通过
5. 重构，保持测试通过
6. 验证覆盖率 >80%
```

---

### code-review-excellence
**代码审查最佳实践**，支持 React/Vue/Rust/TypeScript/Python/Java/C/C++。

**工作流：**
```
1. 上下文收集 → PR 描述、改动范围、CI 状态
2. 高层审查 → 架构设计、性能、测试策略
3. 逐行审查 → 逻辑正确性、安全、可维护性
4. 总结反馈 → 标记阻塞/重要/建议级别
```

---

## 四、内容创作与文档

### frontend-slides
**零依赖 HTML 演示文稿**，支持 PPT 转换。

**工作流：**
```
1. 确定模式 → 新建 / PPT 转换 / 优化现有
2. 内容发现 → 用途、页数、内容就绪度
3. 风格探索 → 生成 3 个预览文件
4. 生成完整演示文稿 → 每页适配视口，无滚动
5. 导航支持 → 键盘/触摸/滚轮
```

---

### guizang-ppt
**杂志风网页 PPT 生成**，单 HTML 文件，含 WebGL 背景。

**两种风格：**
| 风格 | 特点 | 适用场景 |
|------|------|----------|
| **A · 电子杂志风** | WebGL 流体背景、衬线标题、暖色调 | 人文分享、行业观察、商业发布 |
| **B · 瑞士国际主义** | 网格点阵背景、无衬线、高对比功能色 | 科技产品、数据汇报、技术分享 |

**核心能力：**
- 横向翻页（键盘 ← →、滚轮、触屏、ESC 索引）
- WebGL 背景（流体/等高线/色散/网格点阵）
- 5 套预设主题色（墨水经典/靛蓝瓷/森林墨/牛皮纸/沙丘）
- Lucide 图标、Motion One 入场动效

**工作流：**
```
1. 需求澄清 → 风格选择、受众、时长、素材
2. 拷贝模板 → assets/template.html 或 template-swiss.html
3. 选定主题色 → 从 5 套预设中选择
4. 填充内容 → 按 layouts.md 版式填充
5. 添加图片 → images/ 文件夹，命名规范 {页号}-{语义}.{ext}
```

**触发方式：**
```
"做一份杂志风 PPT"
"瑞士国际主义风格的演示文稿"
"横向翻页的网页 PPT"
```

---

### html-ppt
**HTML PPT Studio**，36 个主题、31 种布局、15 个完整模板。

**核心能力：**
- **36 个主题**：minimal-white, editorial-serif, tokyo-night, dracula, catppuccin-latte/mocha, xiaohongshu-white, neo-brutalism, swiss-grid, terminal-green 等
- **15 个完整模板**：pitch-deck, product-launch, tech-sharing, weekly-report, xhs-post, presenter-mode-reveal 等
- **31 种布局**：标题页、图文混排、数据展示、对比页等
- **27 个 CSS 动画** + **20 个 Canvas FX 动画**
- **演讲者模式**：按 S 键打开，显示当前/下一页预览、逐字稿、计时器

**演讲者模式特性：**
- CURRENT/NEXT 预览：像素级精确的 iframe 预览
- SPEAKER SCRIPT：大字体逐字稿（可滚动）
- TIMER：计时器 + 页码 + 前后/重置按钮
- 卡片可拖拽、可调整大小，位置持久化

**工作流：**
```
1. 确认内容 → 主题、页数、受众
2. 选择风格 → 从 36 个主题中选
3. 选择模板 → 从 15 个完整模板中选择
4. 填充内容 → 替换 demo 数据
5. 添加动画 → data-anim 属性
```

**触发方式：**
```
"做一份技术分享 PPT"
"产品发布会演示文稿"
"小红书风格的图文"
"带演讲者模式的 PPT"
```

---

### docx
**Word 文档创建与编辑**。

**工作流：**
```
新建文档 → 使用 docx-js 库，设置页面尺寸
编辑文档 → 解压 → 编辑 XML → 打包
```

**关键规则：** 表格双宽度、DXA 单位、避免 unicode 项目符号

---

### readme-generation
**README 最佳实践**。

**结构：** 标题 + 描述 → 徽章 → 安装 → 使用示例 → 配置 → 贡献指南

---

### code-documentation-doc-generate
**从代码自动生成文档**。

**工作流：** 识别类型 → 提取信息 → 生成文档 → 添加验证

---

### update-docs
**Next.js 文档更新工作流**。

**工作流：** git diff → 映射改动 → 更新文档 → pnpm lint

---

### changelog-generator
**从 Git 提交生成更新日志**。

**工作流：** 扫描历史 → 分类 → 翻译为用户语言 → 过滤内部提交


---

## 五、Obsidian 生态

### 1. 笔记与内容

#### obsidian-markdown
**Obsidian 专属 Markdown 语法**。

**核心语法：**
```markdown
[[笔记名]]                    # 内部链接
[[笔记名|显示文本]]            # 自定义显示
![[图片.png|300]]             # 嵌入内容
> [!note] 标题               # Callout
%%隐藏内容%%                 # 注释
==高亮文本==                 # 高亮
```

---

#### obsidian-cli
**通过命令行操作 Obsidian 仓库**。

**常用命令：**
```bash
obsidian read file="笔记名"
obsidian create name="新笔记" content="# 标题"
obsidian append file="笔记名" content="追加内容"
obsidian search query="关键词" limit=10
obsidian daily:append content="- [ ] 任务"
obsidian property:set name="status" value="done"
```

**开发调试：**
```bash
obsidian plugin:reload id=my-plugin
obsidian dev:errors
obsidian dev:screenshot path=screenshot.png
```

---

### 2. 数据与可视化

#### obsidian-bases
**数据库视图（.base 文件）**，类似 Notion 数据库。

**工作流：**
```
1. 创建 .base 文件，定义 YAML 结构
2. 设置 filters 筛选笔记
3. 定义 formulas 计算字段
4. 配置 views（table/cards/list/map）
```

**示例：**
```yaml
filters:
  and:
    - file.hasTag("task")
formulas:
  days_until_due: 'if(due, (date(due) - today()).days, "")'
views:
  - type: table
    name: "待办任务"
    order: [file.name, status, formula.days_until_due]
```

---

#### json-canvas
**可视化画布（.canvas 文件）**，思维导图、流程图。

**工作流：**
```
1. 创建 .canvas 文件 → {"nodes": [], "edges": []}
2. 添加节点 → text/file/link/group
3. 添加边 → fromNode → toNode
4. 验证 → ID 唯一、边引用有效
```

**节点类型：**
| 类型 | 必需字段 |
|------|----------|
| text | `text` |
| file | `file` |
| link | `url` |
| group | `label` |

---

### 3. 插件开发

#### obsidian-sdk-patterns
**Obsidian 插件开发模式（TypeScript）**。

**核心模式：**
| 模式 | 用途 |
|------|------|
| Settings Pattern | 类型安全的配置管理 |
| Service Layer | Vault 操作封装 |
| Event Manager | 事件注册与自动清理 |
| Command Builder | 流式命令注册 |
| Async Queue | 批量操作防竞态 |


---

## 六、工具与调试

### chrome-devtools
**浏览器调试、性能分析、自动化**。

**工作流：**
```
元素定位 → take_snapshot 获取 uid → click(uid) / fill(uid)
错误排查 → list_console_messages + list_network_requests
性能分析 → performance_start_trace → performance_analyze_insight
```

---

### defuddle
**从网页提取干净内容**（去广告、去导航）。

**使用：**
```bash
defuddle parse <url> --md           # Markdown 输出
defuddle parse <url> --md -o out.md # 保存文件
defuddle parse <url> -p title       # 提取标题
```

---

### web-design-guidelines
**检查 UI 是否符合 Web Interface Guidelines**。

**工作流：**
```
1. 从 GitHub 获取最新指南
2. 读取指定文件
3. 逐条检查规则
4. 输出 file:line 格式的问题列表
```

---

## 七、开发工作流

本仓库包含一系列通用开发工作流 Skill，作为开发实践的最佳实践指南：

| 文件 | 用途 |
|------|------|
| `test-driven-development` | TDD 测试驱动开发流程 |
| `brainstorming` | 头脑风暴和创意生成 |
| `systematic-debugging` | 系统化调试方法 |
| `writing-plans` | 编写开发计划 |
| `executing-plans` | 执行开发计划 |
| `verification-before-completion` | 完成前验证清单 |
| `receiving-code-review` | 接收代码审查反馈 |
| `requesting-code-review` | 请求代码审查 |
| `finishing-a-development-branch` | 完成开发分支 |
| `using-git-worktrees` | 使用 Git Worktrees |
| `dispatching-parallel-agents` | 并行 Agent 调度 |
| `subagent-driven-development` | 子 Agent 驱动开发 |
| `using-superpowers` | 使用高级能力 |
| `writing-skills` | 编写自定义 Skill |

**这些工作流文件是通用指南，不需要特定触发词，可在相应场景下参考使用。**


---

## 快速参考：按场景选 Skill

| 你想做什么 | 使用 Skill |
|-----------|-----------|
| **Vue 开发** | |
| 写 Vue 组件 | `vue` + `vue-best-practices` |
| 管理 Vue 状态 | `pinia` |
| 需要 Vue 工具函数 | `vueuse-functions` |
| 配置构建工具 | `vite` |
| **动画开发** | |
| 做网页动画 | `gsap-core` → `gsap-timeline` → `gsap-scrolltrigger` |
| React 里用动画 | `gsap-react` |
| Vue 里用动画 | `gsap-frameworks` |
| 使用 GSAP 插件 | `gsap-plugins` |
| **UI 设计** | |
| 设计产品界面 | `frontend-design` / `impeccable` |
| 端到端构建功能 | `/impeccable craft [功能]` |
| 技术质量检查 | `/impeccable audit [目标]` |
| 设计优化 | `/impeccable polish [目标]` |
| 用 Pencil 画设计稿 | `pencil-ui-design` |
| **测试与质量** | |
| 写前端测试 | `frontend-testing` / `tdd-workflow` |
| 代码审查 | `code-review-excellence` |
| **文档创作** | |
| 做演示文稿 | `frontend-slides` / `guizang-ppt` / `html-ppt` |
| PPT 演示文稿（杂志风） | `guizang-ppt` |
| PPT 演示文稿（多主题） | `html-ppt` |
| 写 README | `readme-generation` |
| 生成更新日志 | `changelog-generator` |
| 创建 Word 文档 | `docx` |
| **Obsidian** | |
| 操作 Obsidian | `obsidian-cli` / `obsidian-markdown` |
| Obsidian 数据库 | `obsidian-bases` |
| Obsidian 画布 | `json-canvas` |
| 开发 Obsidian 插件 | `obsidian-sdk-patterns` |
| **工具调试** | |
| 调试网页 | `chrome-devtools` |
| 提取网页内容 | `defuddle` |
| 检查 UI 规范 | `web-design-guidelines` |
| **企业工作流** | |
| 创建 Jira 工作流 | `jira-workflow-creator` |

---

## Skill 协作关系

### Vue 开发完整链路
```
vue (组件开发)
  ├── vue-best-practices (TypeScript 类型问题)
  ├── vueuse-functions (组合式函数)
  ├── pinia (状态管理)
  └── vite (构建配置)
```

### GSAP 动画开发链路
```
gsap-core (基础动画)
  → gsap-timeline (多步骤编排)
  → gsap-scrolltrigger (滚动驱动)
  → gsap-plugins (高级效果)
  
gsap-react / gsap-frameworks (框架集成)
gsap-performance / gsap-utils (性能优化)
```

### impeccable 优化链路
```
评估 → audit / critique
  ↓
优化 → layout / animate / colorize / typeset
  ↓
精炼 → polish / bolder / quieter / distill
  ↓
生产 → harden / onboard
```

### 测试工作流
```
tdd-workflow (TDD 流程)
  → frontend-testing (具体测试实现)
  → code-review-excellence (代码审查)
```

---

## 贡献指南

### 添加新 Skill

1. 在仓库根目录创建文件夹：`skill-name/`
2. 创建 `SKILL.md` 文件，包含：
   - `name`：Skill 名称
   - `description`：描述和触发条件
   - 详细说明和使用示例
3. 如有参考文档，放在 `reference/` 子目录
4. 更新本 README 的快速参考表

### Skill 模板

```markdown
---
name: skill-name
description: "描述和触发条件"
---

# Skill 标题

## 何时使用

## 工作流

## 示例

## 参考
```

---

## 许可证

各 Skill 遵循其各自的许可证声明。未特别说明的遵循 Apache 2.0 许可证。
