---
name: ui-ux-design
description: UI/UX设计技能 - 包含设计系统生成、风格推荐、配色方案、字体组合和技术栈指南，用于构建专业级界面
triggers:
  keywords:
    - "UI"
    - "界面"
    - "design"
    - "设计"
    - "layout"
    - "布局"
    - "component"
    - "组件"
    - "page"
    - "页面"
    - "CSS"
    - "Tailwind"
    - "theme"
    - "主题"
    - "color"
    - "颜色"
    - "icon"
    - "图标"
    - "UX"
    - "experience"
    - "体验"
    - "React"
    - "Vue"
    - "frontend"
    - "前端"
    - "mobile"
    - "移动"
    - "app"
  file_extensions:
    - ".jsx"
    - ".tsx"
    - ".vue"
    - ".svelte"
    - ".css"
    - ".scss"
    - ".html"
  priority: medium
auto_trigger: true
---

# UI/UX Design

> 🎨 **自动触发提示**: 当检测到UI/UX设计任务、前端开发或设计相关文件时，此技能会自动应用。

## 自动触发场景

| 触发词/文件 | 应用原则 |
|-------------|----------|
| "UI", "界面", "design", "设计" | Design System: 生成设计系统 |
| ".jsx", ".tsx", ".vue", ".css" | Frontend Stack: 技术栈指南 |
| "component", "组件", "page", "页面" | UI Components: 组件设计规范 |
| "mobile", "app", "响应式" | Responsive Design: 响应式原则 |

## 快速启动

## 快速启动

### 设计工作流程

```
Step 1: 分析需求
    ├── 产品类型：SaaS、电商、作品集等
    ├── 风格关键词：minimal、professional、elegant
    ├── 行业：healthcare、fintech、gaming
    └── 技术栈：默认 html-tailwind
    ↓
Step 2: 生成设计系统（必需）
    ↓
Step 3: 补充详细搜索（按需）
    ↓
Step 4: 技术栈指南
    ↓
Step 5: 实施设计
    ↓
Step 6: 交付前检查清单
```

## 设计系统生成

### 基础命令

```bash
# 生成完整设计系统（必需第一步）
python3 skills/ui-ux-pro-max/scripts/search.py "<product> <industry> <keywords>" --design-system -p "项目名"

# 持久化设计系统
python3 skills/ui-ux-pro-max/scripts/search.py "<query>" --design-system --persist -p "项目名"

# 页面特定覆盖
python3 skills/ui-ux-pro-max/scripts/search.py "<query>" --design-system --persist -p "项目名" --page "dashboard"
```

## 搜索域参考

| 域 | 用途 | 示例关键词 |
|----|------|-----------|
| `product` | 产品类型推荐 | SaaS、e-commerce、portfolio |
| `style` | UI样式、效果 | glassmorphism、minimalism |
| `typography` | 字体配对 | elegant、professional |
| `color` | 配色方案 | saas、fintech、healthcare |
| `landing` | 页面结构 | hero、pricing、testimonial |
| `chart` | 图表类型 | trend、comparison、funnel |
| `ux` | 最佳实践 | animation、accessibility |

## 技术栈支持

| 技术栈 | 焦点 |
|--------|------|
| `html-tailwind` | Tailwind工具类、响应式、无障碍（默认） |
| `react` | 状态、hooks、性能 |
| `nextjs` | SSR、路由、图片 |
| `vue` | Composition API、Pinia |
| `svelte` | Runes、stores |
| `swiftui` | Views、State、Navigation |
| `react-native` | Components、Navigation |
| `flutter` | Widgets、State、Layout |
| `shadcn` | shadcn/ui组件、主题 |

## 专业UI常见规则

### 图标与视觉元素

| 规则 | 做 ✅ | 不做 ❌ |
|------|-------|---------|
| 不使用emoji图标 | 使用SVG（Heroicons、Lucide） | 使用emoji 🎨 🚀 |
| 稳定的悬停状态 | 颜色/透明度过渡 | 引起布局偏移的变换 |
| 正确的品牌logo | 从Simple Icons获取 | 猜测或错误路径 |

### 交互与光标

| 规则 | 做 ✅ | 不做 ❌ |
|------|-------|---------|
| Cursor pointer | 所有可点击元素 | 使用默认光标 |
| 悬停反馈 | 视觉反馈（颜色、阴影） | 无交互指示 |
| 平滑过渡 | `transition-colors duration-200` | 瞬间或太慢 |

### 明暗模式对比

| 规则 | 做 ✅ | 不做 ❌ |
|------|-------|---------|
| Glass卡片亮色 | `bg-white/80` | `bg-white/10`（太透明） |
| 亮色文本 | `#0F172A` (slate-900) | `#94A3B8` (太浅) |
| 边框可见 | `border-gray-200` | `border-white/10`（不可见） |

## 交付前检查清单

### 视觉质量
- [ ] 无emoji图标（使用SVG）
- [ ] 图标来自统一图标集
- [ ] 品牌logo准确
- [ ] 悬停状态不引起布局偏移

### 交互
- [ ] 所有可点击元素有 `cursor-pointer`
- [ ] 悬停状态有清晰视觉反馈
- [ ] 过渡平滑（150-300ms）
- [ ] Focus状态对键盘导航可见

### 明暗模式
- [ ] 亮色模式文本有足够对比度（4.5:1）
- [ ] Glass/透明元素在亮色模式可见
- [ ] 边框在两种模式都可见

### 布局
- [ ] 浮动元素与边缘有适当间距
- [ ] 内容不被固定导航栏遮挡
- [ ] 响应式（375px, 768px, 1024px, 1440px）
- [ ] 移动端无水平滚动

### 可访问性
- [ ] 所有图片有alt文本
- [ ] 表单输入有标签
- [ ] 颜色不是唯一指示器
- [ ] 尊重 `prefers-reduced-motion`
