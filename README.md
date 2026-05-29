# Skill 仓库使用指南

本仓库包含 30+ 个 Skill，覆盖前端开发、UI 设计、动画、测试、文档、Obsidian 等多个领域。每个 Skill 都是独立的指令集，在对应场景下自动激活。

---

## 一、前端开发核心

### 1. Vue 生态

#### vue
Vue 3.5+ 核心开发指南，覆盖响应式系统、组件通信、生命周期、TypeScript 集成。

**工作流：**
- 新建组件时，使用 `<script setup lang="ts">` + `ref()` 声明状态
- 需要复用逻辑时，提取为 composable（参考 vueuse-functions）
- 父子通信用 `defineProps` + `defineEmits`，v-model 用 `defineModel()`

**触发方式：**
```
"帮我写一个 Vue 组件"
"这个 ref 为什么不响应"
"watch 和 watchEffect 有什么区别"
```

#### vue-best-practices
Vue + TypeScript 类型安全最佳实践，解决模板报错、props 提取、CSS Modules 等常见问题。

**工作流：**
- 遇到 `vue-tsc` 模板报错 → 自动应用 strict-templates 规则
- 需要包装组件继承 props → 使用 extract-component-props 模式
- 遇到 Volar 升级问题 → 查阅 volar-3-breaking-changes

**触发方式：**
```
"Vue 模板报 undefined component"
"怎么提取子组件的 props 类型"
"CSS Modules 类型报错"
```

#### pinia
Vue 官方状态管理库，支持 Setup Stores、TypeScript、SSR。

**工作流：**
- 定义 Store：`defineStore('id', () => { const count = ref(0); return { count } })`
- 组件中使用：`const store = useCounterStore()`，`storeToRefs(store)` 解构保持响应式
- 测试时用 `@pinia/testing` mock store

**触发方式：**
```
"怎么定义 Pinia store"
"store 解构后失去响应式"
"Pinia 在 SSR 中怎么用"
```

#### vueuse-functions
VueUse 组合式函数决策指南，覆盖 200+ 个常用工具函数。

**工作流：**
- 需要本地存储 → `useLocalStorage` / `useStorage`
- 需要监听元素可见性 → `useIntersectionObserver`
- 需要防抖节流 → `useDebounceFn` / `useThrottleFn`
- 需要暗黑模式 → `useDark` / `useColorMode`

**触发方式：**
```
"怎么监听元素进入视口"
"Vue 里怎么做防抖"
"实现暗黑模式切换"
```

#### vite
Vite 6.x 构建工具配置指南，覆盖开发服务器、生产构建、插件系统、SSR。

**工作流：**
- 配置别名/代理 → `vite.config.ts` 中配置 `resolve.alias` / `server.proxy`
- 环境变量 → `.env` 文件 + `import.meta.env`
- 构建库 → 使用 Library Mode 配置 `build.lib`

**触发方式：**
```
"Vite 怎么配置代理"
"环境变量不生效"
"打包优化怎么做"
```

---

### 2. 动画开发（GSAP 系列）

共 8 个 Skill，覆盖 GSAP 完整生态。按使用顺序排列：

#### gsap-core
GSAP 核心动画引擎。单元素动画、缓动函数、stagger、响应式动画。

**工作流：**
```javascript
// 基础动画
gsap.to(".box", { x: 100, duration: 1, ease: "power3.out" })

// 从隐藏状态进入
gsap.from(".item", { opacity: 0, y: 20, stagger: 0.1 })

// 响应式 + 减少动画偏好
let mm = gsap.matchMedia()
mm.add("(prefers-reduced-motion: reduce)", () => {
  gsap.set(".box", { x: 100 }) // 直接设置，无动画
})
```

**触发方式：**
```
"做个元素飞入动画"
"推荐一个 JS 动画库"
"GSAP 怎么用"
```

#### gsap-timeline
多步骤动画编排，控制时间线、label、嵌套。

**工作流：**
```javascript
const tl = gsap.timeline({ defaults: { duration: 0.5 } })
tl.to(".a", { x: 100 }, 0)           // 0秒开始
tl.to(".b", { y: 50 }, "+=0.3")      // 延迟0.3秒
tl.to(".c", { opacity: 0 }, "<0.2")  // 上一个开始后再过0.2秒
```

**触发方式：**
```
"多个动画按顺序执行"
"怎么控制动画时间线"
```

#### gsap-scrolltrigger
滚动驱动动画，pin、scrub、batch、水平滚动。

**工作流：**
```javascript
gsap.to(".box", {
  x: 500,
  scrollTrigger: {
    trigger: ".box",
    start: "top center",
    end: "bottom center",
    scrub: true,
    pin: false
  }
})
```

**触发方式：**
```
"滚动时触发动画"
"实现视差滚动效果"
"元素固定在屏幕上"
```

#### gsap-plugins
GSAP 插件系统：Flip、Draggable、SplitText、MorphSVG、DrawSVG 等。

**工作流：**
- 布局变化动画 → `Flip.getState()` → DOM 变化 → `Flip.from()`
- 文字逐字动画 → `SplitText.create(".heading", { type: "chars" })`
- SVG 路径动画 → `DrawSVGPlugin` + `drawSVG: "0% 100%"`
- 拖拽交互 → `Draggable.create(".box", { type: "x,y", inertia: true })`

**触发方式：**
```
"文字逐个出现"
"SVG 路径绘制动画"
"拖拽元素"
```

#### gsap-react / gsap-frameworks
React/Vue/Svelte 中集成 GSAP，处理生命周期和清理。

**React 工作流：**
```javascript
import { useGSAP } from "@gsap/react"
const container = useRef(null)
useGSAP(() => {
  gsap.to(".box", { x: 100 })
}, { scope: container })
```

**Vue 工作流：**
```javascript
onMounted(() => {
  const ctx = gsap.context(() => {
    gsap.to(".box", { x: 100 })
  }, container.value)
})
onUnmounted(() => ctx?.revert())
```

**触发方式：**
```
"React 里用 GSAP"
"Vue 组件卸载后动画还在跑"
```

#### gsap-performance / gsap-utils
性能优化和工具函数。`gsap.quickTo` 高频更新，`gsap.utils.clamp/mapRange/snap` 数值处理。

---

### 3. UI 设计与实现

#### frontend-design
生产级前端界面设计，避免"AI 感"，追求独特视觉风格。

**工作流：**
1. 先确认设计上下文（目标用户、品牌调性）
2. 选择大胆的设计方向（极简/极繁/复古未来/工业风等）
3. 使用 OKLCH 色彩、独特字体搭配、不对称布局
4. 添加有意义的动效（入场动画、状态过渡）

**触发方式：**
```
"设计一个 landing page"
"这个页面太普通了，改得有设计感"
"帮我做一个产品官网"
```

#### impeccable
前端界面全面优化工具，包含 20+ 子命令。

**核心命令：**
| 命令 | 用途 |
|------|------|
| `craft [功能]` | 端到端构建功能 |
| `audit [目标]` | 技术质量检查（a11y、性能、响应式）|
| `polish [目标]` | 上线前最终打磨 |
| `animate [目标]` | 添加 purposeful 动画 |
| `colorize [目标]` | 为单色 UI 添加策略性色彩 |
| `layout [目标]` | 修复间距和视觉层次 |
| `harden [目标]` | 生产化：错误处理、i18n、边界情况 |

**工作流示例（优化现有页面）：**
```
1. 运行 audit 检查问题
2. 根据报告用 layout 修复间距
3. 用 animate 添加动效
4. 用 polish 最终检查
```

**触发方式：**
```
"/impeccable audit 首页"
"/impeccable polish 登录页"
"这个设计需要优化"
```

#### pencil-ui-design
使用 Pencil MCP 创建工业级 UI 设计稿。

**工作流：**
1. 设置设计系统变量（颜色、字体、间距）
2. 创建可复用组件（Button、Card、Input）
3. 用 `I()` 插入组件，`U()` 更新属性，`G()` 生成图片
4. 截图验证设计效果

**触发方式：**
```
"用 Pencil 设计一个 APP 界面"
"创建设计系统组件"
```

---

### 4. 测试与质量

#### frontend-testing
Dify 前端测试规范，Vitest + React Testing Library。

**工作流：**
1. 分析组件复杂度：`pnpm analyze-component <路径>`
2. 按复杂度排序：工具函数 → Hooks → 简单组件 → 复杂组件
3. 逐个编写测试，每个文件覆盖：渲染、Props、交互、边界情况
4. 运行测试：`pnpm test <文件>.spec.tsx`
5. 目标覆盖率：函数/语句 100%，分支/行 >95%

**触发方式：**
```
"给这个组件写测试"
"测试覆盖率不够"
"Vitest 怎么用"
```

#### tdd-workflow
测试驱动开发工作流，强制先写测试再实现。

**工作流：**
1. 编写用户故事
2. 生成测试用例（正常路径 + 边界情况 + 错误路径）
3. 运行测试（应该失败）
4. 实现代码使测试通过
5. 重构，保持测试通过
6. 验证覆盖率 >80%

**触发方式：**
```
"用 TDD 开发这个功能"
"先写测试"
```

#### code-review-excellence
代码审查最佳实践，支持 React/Vue/Rust/TypeScript/Python/Java/C/C++。

**工作流：**
1. 上下文收集：PR 描述、改动范围、CI 状态
2. 高层审查：架构设计、性能、测试策略
3. 逐行审查：逻辑正确性、安全、可维护性
4. 总结反馈：标记阻塞/重要/建议级别

**触发方式：**
```
"帮我 review 这段代码"
"这个 PR 有什么问题"
```

---

## 二、内容创作与文档

### 1. 演示与文档

#### frontend-slides
零依赖 HTML 演示文稿，支持 PPT 转换。

**工作流：**
1. 确定模式：新建 / PPT 转换 / 优化现有
2. 内容发现：确认用途（路演/教学/会议）、页数、内容就绪度
3. 风格探索：生成 3 个预览文件供选择
4. 生成完整演示文稿（每页必须适配视口，无滚动）
5. 键盘/触摸/滚轮导航

**触发方式：**
```
"做一个 pitch deck"
"把 PPT 转成网页版"
"生成技术分享幻灯片"
```

#### docx
Word 文档创建与编辑。

**工作流：**
- 新建文档 → 使用 `docx-js` 库，设置页面尺寸（US Letter: 12240x15840 DXA）
- 编辑现有文档 → 解压 → 编辑 XML → 打包
- 关键规则：表格需双宽度（columnWidths + cell width）、使用 DXA 单位、避免 unicode 项目符号

**触发方式：**
```
"生成一个 Word 文档"
"编辑这个 docx 文件"
```

#### readme-generation
README 最佳实践。

**工作流：**
1. 标题 + 一句话描述
2. 徽章（CI、版本、许可证）
3. 安装步骤（含前置条件）
4. 使用示例（从简单到复杂）
5. 配置变量表格
6. 贡献指南 + 许可证

**触发方式：**
```
"帮我写 README"
"优化项目文档"
```

#### code-documentation-doc-generate
从代码自动生成文档。

**工作流：**
1. 识别文档类型（API/架构/用户指南）
2. 从代码、配置、注释中提取信息
3. 生成一致术语和结构的文档
4. 添加自动化验证

**触发方式：**
```
"给这个项目生成文档"
"自动生成 API 文档"
```

#### update-docs
Next.js 文档更新工作流。

**工作流：**
1. `git diff canary...HEAD --stat` 查看改动
2. 映射源码改动到文档路径
3. 按模板更新或新建文档
4. `pnpm lint` 验证格式

**触发方式：**
```
"这些改动需要更新文档吗"
"同步代码和文档"
```

#### changelog-generator
从 Git 提交生成用户友好的更新日志。

**工作流：**
1. 扫描指定时间范围的 Git 历史
2. 分类：新功能、改进、修复、破坏性变更
3. 将技术提交翻译为用户语言
4. 过滤内部提交（重构、测试等）

**触发方式：**
```
"生成本周更新日志"
"写版本发布说明"
```

---

## 三、Obsidian 生态

### 1. 笔记与内容

#### obsidian-markdown
Obsidian 专属 Markdown 语法。

**核心语法：**
```markdown
[[笔记名]]                    # 内部链接
[[笔记名|显示文本]]            # 自定义显示
![[图片.png|300]]             # 嵌入内容
> [!note] 标题               # Callout
%%隐藏内容%%                 # 注释
==高亮文本==                 # 高亮
```

**触发方式：**
```
"创建 Obsidian 笔记"
"wikilink 怎么用"
```

#### obsidian-cli
通过命令行操作 Obsidian 仓库。

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

**触发方式：**
```
"用 CLI 创建 Obsidian 笔记"
"调试 Obsidian 插件"
```

### 2. 数据与可视化

#### obsidian-bases
数据库视图（.base 文件），类似 Notion 数据库。

**工作流：**
1. 创建 `.base` 文件，定义 YAML 结构
2. 设置 `filters` 筛选笔记（按标签、文件夹、属性）
3. 定义 `formulas` 计算字段
4. 配置 `views`：table / cards / list / map

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

**触发方式：**
```
"创建一个任务追踪 base"
"Obsidian 数据库怎么用"
```

#### json-canvas
可视化画布（.canvas 文件），思维导图、流程图。

**工作流：**
1. 创建 `.canvas` 文件：`{"nodes": [], "edges": []}`
2. 添加节点（text/file/link/group），生成 16 位 hex ID
3. 添加边连接节点（`fromNode` → `toNode`）
4. 验证：ID 唯一、边引用有效

**触发方式：**
```
"创建思维导图"
"做一个流程图"
```

### 3. 插件开发

#### obsidian-sdk-patterns
Obsidian 插件开发模式（TypeScript）。

**核心模式：**
- Settings Pattern：类型安全的配置管理
- Service Layer：Vault 操作封装
- Event Manager：事件注册与自动清理
- Command Builder：流式命令注册
- Async Queue：批量操作防竞态

**触发方式：**
```
"Obsidian 插件最佳实践"
"怎么管理插件配置"
```

---

## 四、工具与调试

#### chrome-devtools
浏览器调试、性能分析、自动化。

**工作流：**
- 元素定位 → `take_snapshot` 获取 uid → `click(uid)` / `fill(uid)`
- 错误排查 → `list_console_messages` + `list_network_requests`
- 性能分析 → `performance_start_trace` → `performance_analyze_insight`

**触发方式：**
```
"调试这个页面"
"分析页面加载性能"
"截图看看效果"
```

#### defuddle
从网页提取干净内容（去广告、去导航）。

**使用：**
```bash
defuddle parse <url> --md           # Markdown 输出
defuddle parse <url> --md -o out.md # 保存文件
defuddle parse <url> -p title       # 提取标题
```

**触发方式：**
```
"提取这个网页内容"
"把文章转成 Markdown"
```

#### web-design-guidelines
检查 UI 是否符合 Web Interface Guidelines。

**工作流：**
1. 从 GitHub 获取最新指南
2. 读取指定文件
3. 逐条检查规则
4. 输出 `file:line` 格式的问题列表

**触发方式：**
```
"检查这个页面的可访问性"
"review 我的 UI"
```

---

## 五、企业工作流

#### jira-workflow-creator
Jira 工作流创建辅助。

**触发方式：**
```
"创建 Jira 工作流"
"jira workflow creator"
```

---

## 快速参考：按场景选 Skill

| 你想做什么 | 使用 Skill |
|-----------|-----------|
| 写 Vue 组件 | vue + vue-best-practices |
| 管理 Vue 状态 | pinia |
| 需要 Vue 工具函数 | vueuse-functions |
| 配置构建工具 | vite |
| 做网页动画 | gsap-core → gsap-timeline → gsap-scrolltrigger |
| React 里用动画 | gsap-react |
| Vue 里用动画 | gsap-frameworks |
| 设计产品界面 | frontend-design / impeccable |
| 用 Pencil 画设计稿 | pencil-ui-design |
| 写前端测试 | frontend-testing / tdd-workflow |
| 代码审查 | code-review-excellence |
| 做演示文稿 | frontend-slides |
| 写 README | readme-generation |
| 生成更新日志 | changelog-generator |
| 操作 Obsidian | obsidian-cli / obsidian-markdown |
| Obsidian 数据库 | obsidian-bases |
| Obsidian 画布 | json-canvas |
| 开发 Obsidian 插件 | obsidian-sdk-patterns |
| 调试网页 | chrome-devtools |
| 提取网页内容 | defuddle |
| 检查 UI 规范 | web-design-guidelines |
| 创建 Word 文档 | docx |
| 更新 Next.js 文档 | update-docs |
