# AI 客服赛道竞品分析 — 网页实现 SPEC

## 技术栈

- 纯静态 HTML + CSS + JS，适合 GitHub Pages
- 图表：ECharts 5.x（CDN）
- 字体：Inter（Google Fonts CDN）
- 无框架，无构建工具

---

## 视觉风格

- 横屏优先，min-width: 1280px，不做移动端适配
- 背景色：`#0F1117`
- 主色：`#4F8EF7`（蓝）
- 强调色：`#34D399`（绿）、`#F59E0B`（黄）、`#F87171`（红）
- 卡片背景：`#1A1D27`，圆角 `12px`，边框 `1px solid #2A2D3A`
- 图表背景透明，轴线 `#2A2D3A`，文字 `#94A3B8`
- 风格参考：咨询报告风（BCG/McKinsey 数字版），简洁、克制

---

## 页面结构（8 个 Section，单页滚动）

| # | Section | 布局 |
|---|---------|------|
| 1 | Cover 封面 | 全屏居中 |
| 2 | Market Overview 赛道概览 | 左数字 + 右趋势卡片 |
| 3 | Product Cards 竞品卡片 | 横向 7 卡，可滚动 |
| 4 | Comparison Matrix 对比矩阵 | 全宽表格 |
| 5 | Charts 图表区 | 2+3 网格 |
| 6 | Key Insights 关键洞察 | 5 卡横排 |
| 7 | Recommendations 选型建议 | 4 场景卡片 |
| 8 | Sources 数据来源 | 列表 |

---

## Section 1 — Cover

```
标题：AI 客服赛道竞品分析 2025
副标题：7 大产品深度对比 · 定价 · 能力 · 市场定位
日期：2025 年 4 月
背景：深色渐变 或 细网格纹理
```

---

## Section 2 — Market Overview

**左侧大数字：**
- 2024 市场规模：**$12.06B**
- 2030 预测：**$47.82B**
- CAGR：**25.8%**

**右侧 3 个趋势卡片：**
1. Agentic AI — 从问答机器人到自主完成任务
2. 按结果计费 — Per-resolution 取代 Per-seat 成主流
3. 多渠道统一 — Chat / Email / Voice / Social 统一处理

---

## Section 3 — Product Cards

每张卡片字段：

```js
const products = [
  {
    name: "Intercom Fin",
    version: "Fin 3",
    tagline: "世界最高性能企业级 AI Agent",
    target: "Mid / Enterprise",
    pricing_model: "按解决量",
    pricing_unit: "$0.99 / resolution",
    platform_fee: "$39/seat/mo 起",
    highlights: ["10+ 渠道覆盖", "无功能分级", "Fin Vision 图像识别"],
    channels: ["Chat", "Email", "Voice", "SMS", "WhatsApp", "Instagram"],
    brand_color: "#6366F1"
  },
  {
    name: "Zendesk AI",
    version: "AI Agents + Copilot",
    tagline: "AI-first 服务平台，自主解决 + 人工辅助",
    target: "Mid / Enterprise",
    pricing_model: "按解决量",
    pricing_unit: "$1.50–$2.00 / resolution",
    platform_fee: "$55–$169/agent/mo + $50 AI 附加",
    highlights: ["收购 Forethought 引入自我改进 AI", "Copilot 提升 82% 效率", "最大集成生态"],
    channels: ["Chat", "Email", "Voice", "Social", "Messaging"],
    brand_color: "#03363D"
  },
  {
    name: "Ada CX",
    version: "",
    tagline: "AI-first 企业客服自动化，声称 80%+ 解决率",
    target: "Enterprise",
    pricing_model: "自定义合同",
    pricing_unit: "$1.00–$3.50 / interaction",
    platform_fee: "起步 ~$30K/年",
    highlights: ["多语言能力强", "无代码流程构建", "深度 CRM 集成"],
    channels: ["Chat", "Email", "Voice", "SMS", "WhatsApp"],
    brand_color: "#FF5C35"
  },
  {
    name: "Forethought",
    version: "（已被 Zendesk 收购）",
    tagline: "五 Agent 架构，覆盖全客服生命周期",
    target: "Enterprise（20K+ 工单/月）",
    pricing_model: "Outcome-based 自定义",
    pricing_unit: "自定义",
    platform_fee: "起步 ~$499/mo",
    highlights: ["Resolve/Triage/Copilot/Discover/QA 五 Agent", "自我改进 AI", "QA 自动化"],
    channels: ["Chat", "Email", "Voice", "SMS", "Web"],
    brand_color: "#7C3AED"
  },
  {
    name: "Freshdesk Freddy AI",
    version: "",
    tagline: "Freshworks 全套 AI 引擎，性价比最优",
    target: "SMB / Mid",
    pricing_model: "混合（seat + session）",
    pricing_unit: "$0.10 / 1K sessions",
    platform_fee: "$15/agent/mo 起；Copilot $29/agent/mo 附加",
    highlights: ["价格最低", "跨产品统一 AI 引擎", "适合预算有限团队"],
    channels: ["Chat", "Email", "Phone", "Social"],
    brand_color: "#00B140"
  },
  {
    name: "Salesforce Agentforce",
    version: "（原 Einstein for Service）",
    tagline: "企业级 AI Agent 平台，深度绑定 Salesforce 生态",
    target: "Enterprise",
    pricing_model: "Flex Credits（$0.10/action）或 $2/conversation",
    pricing_unit: "$0.10 / action",
    platform_fee: "Service Cloud $175+/user/mo；Agentforce 附加 $125/user/mo",
    highlights: ["CRM 数据集成最深", "跨 Sales+Service 统一", "Data Cloud 超个性化"],
    channels: ["Chat", "Email", "Voice", "Messaging"],
    brand_color: "#00A1E0"
  },
  {
    name: "Kustomer",
    version: "（Meta 旗下）",
    tagline: "CRM 驱动 AI 客服，完整客户上下文",
    target: "Mid / Enterprise（DTC 电商）",
    pricing_model: "按 seat",
    pricing_unit: "$89–$139 / seat / mo",
    platform_fee: "最低 8 seats，仅年付",
    highlights: ["客户历史数据最完整", "全渠道统一时间线", "适合高 LTV 场景"],
    channels: ["Chat", "Email", "Voice", "SMS", "WhatsApp", "Social"],
    brand_color: "#FF6B35"
  }
]
```

---

## Section 4 — Comparison Matrix

**列定义（8 维度，1–5 分）：**

| 维度 | 说明 |
|------|------|
| AI 自动化深度 | 能否端到端自主解决复杂问题 |
| 多渠道覆盖 | 渠道数量与质量 |
| Agent Copilot | 人工辅助能力 |
| 集成生态 | 与 CRM/电商/工单系统集成深度 |
| 定价透明度 | 是否有公开定价 |
| 部署简易度 | 上线周期与技术门槛（5=最简单） |
| 适合规模 | 文字标注 |
| 差异化优势 | 一句话 |

**评分数据：**

```js
const scores = [
  { name: "Intercom Fin",        automation: 5, multichannel: 5, copilot: 4, integration: 4, pricing_transparency: 5, deploy_ease: 4, scale: "Mid/Enterprise" },
  { name: "Zendesk AI",          automation: 4, multichannel: 5, copilot: 5, integration: 5, pricing_transparency: 3, deploy_ease: 3, scale: "Mid/Enterprise" },
  { name: "Ada CX",              automation: 4, multichannel: 4, copilot: 3, integration: 4, pricing_transparency: 2, deploy_ease: 3, scale: "Enterprise" },
  { name: "Forethought",         automation: 5, multichannel: 4, copilot: 5, integration: 4, pricing_transparency: 2, deploy_ease: 2, scale: "Enterprise" },
  { name: "Freshdesk Freddy",    automation: 3, multichannel: 4, copilot: 3, integration: 3, pricing_transparency: 4, deploy_ease: 4, scale: "SMB/Mid" },
  { name: "Salesforce Agentforce", automation: 4, multichannel: 4, copilot: 4, integration: 5, pricing_transparency: 1, deploy_ease: 1, scale: "Enterprise" },
  { name: "Kustomer",            automation: 3, multichannel: 5, copilot: 3, integration: 4, pricing_transparency: 3, deploy_ease: 3, scale: "Mid/Enterprise" },
]
```

**颜色规则：**
- 4–5 分：`#34D399`（绿）
- 3 分：`#F59E0B`（黄）
- 1–2 分：`#F87171`（红）

---

## Section 5 — Charts（5 张，ECharts）

### Chart 1：雷达图 — 多维能力对比
- 6 个维度：AI 自动化 / 多渠道 / Copilot / 集成 / 定价透明 / 部署简易
- 7 条 series，每产品一条线
- 建议只默认显示 3 条（Fin / Zendesk / Freshdesk），其余可点击图例切换

### Chart 2：气泡图 — 定价 vs 自动化 vs 规模
- X 轴：定价透明度（1–5）
- Y 轴：AI 自动化深度（1–5）
- 气泡大小：SMB=20 / Mid=35 / Enterprise=50
- 每个气泡标注产品名
- 结论：Fin 在"高自动化 + 高透明"象限；Salesforce 在"高自动化 + 低透明"象限

### Chart 3：柱状图 — 每次解决成本对比

```js
const costData = [
  { name: "Intercom Fin",     cost: 0.99,  note: "per resolution" },
  { name: "Zendesk AI",       cost: 1.75,  note: "per resolution（均值）" },
  { name: "Ada CX",           cost: 2.25,  note: "per interaction（均值）" },
  { name: "Salesforce",       cost: 2.00,  note: "per conversation（旧模式）" },
  { name: "Freshdesk",        cost: 0.10,  note: "per session（≠resolution）", different_unit: true },
  { name: "Gorgias",          cost: 0.93,  note: "per resolution（均值）" },
]
```

- Freshdesk 用不同颜色 + 注释标注（计费单位不同）
- X 轴：产品名；Y 轴：美元

### Chart 4：热力图 — 功能覆盖矩阵

```js
// 0 = 不支持，1 = 部分支持，2 = 完整支持
const features = ["知识库", "工单", "Agent Copilot", "自动动作", "多渠道", "语音", "自我改进AI", "QA自动化"]
const featureMatrix = [
  { name: "Intercom Fin",        values: [2, 2, 2, 2, 2, 2, 1, 0] },
  { name: "Zendesk AI",          values: [2, 2, 2, 2, 2, 2, 2, 1] },
  { name: "Ada CX",              values: [2, 2, 1, 2, 2, 2, 0, 0] },
  { name: "Forethought",         values: [2, 2, 2, 2, 2, 1, 2, 2] },
  { name: "Freshdesk Freddy",    values: [2, 2, 2, 1, 2, 1, 0, 0] },
  { name: "Salesforce Agentforce", values: [2, 2, 2, 2, 2, 2, 1, 0] },
  { name: "Kustomer",            values: [2, 2, 2, 2, 2, 2, 0, 0] },
]
```

- 颜色：0=`#1E2030`（深灰）/ 1=`#F59E0B`（黄）/ 2=`#34D399`（绿）

### Chart 5：定位散点图 — 企业规模 vs 定价门槛

```js
// x: 1=SMB, 2=Mid, 3=Enterprise
// y: 1=低门槛, 5=高门槛
const positioning = [
  { name: "Intercom Fin",        x: 2.5, y: 2.5 },
  { name: "Zendesk AI",          x: 2.5, y: 3.5 },
  { name: "Ada CX",              x: 3,   y: 4   },
  { name: "Forethought",         x: 3,   y: 4.5 },
  { name: "Freshdesk Freddy",    x: 1.5, y: 1.5 },
  { name: "Salesforce Agentforce", x: 3, y: 5   },
  { name: "Kustomer",            x: 2.5, y: 3   },
]
```

- X 轴标签：SMB / Mid-market / Enterprise
- Y 轴标签：低门槛 → 高门槛

---

## Section 6 — Key Insights（5 条）

```js
const insights = [
  {
    icon: "💰",
    title: "按结果计费成为主流",
    body: "Intercom Fin（$0.99）、Zendesk（$1.50–$2.00）均采用 per-resolution 模式，买家只为成功解决付费，ROI 更易量化。"
  },
  {
    icon: "🔀",
    title: "Zendesk 收购 Forethought，整合自我改进 AI",
    body: "2026 年 3 月完成收购，Forethought 的五 Agent 架构和自我改进能力将并入 Zendesk，格局重塑。"
  },
  {
    icon: "🏗️",
    title: "Salesforce 定价最复杂，生态锁定最深",
    body: "三种计费模式并存，实施成本 $50K–$150K+，适合已深度使用 Salesforce 的大企业，其他场景性价比低。"
  },
  {
    icon: "💡",
    title: "Freshdesk 是 SMB 性价比最优解",
    body: "平台费最低，AI 附加模块化，适合预算有限、工单量中等的中小团队，但 AI 深度不及头部产品。"
  },
  {
    icon: "🤖",
    title: "Agentic AI 成为 2025 核心战场",
    body: "Gartner 预测 2028 年 80% 客服交互由 Agentic AI 处理；Cisco 调研显示 68% 企业 3 年内将主要依赖 Agentic AI。"
  },
]
```

---

## Section 7 — Recommendations（4 场景）

```js
const recommendations = [
  {
    scenario: "SMB（<50 人客服团队）",
    pick: "Freshdesk Freddy AI",
    reason: "价格最低，上手快，AI 能力够用，不需要复杂实施。"
  },
  {
    scenario: "Mid-market（50–200 人，重视 AI 自动化）",
    pick: "Intercom Fin",
    reason: "定价透明，功能无分级，多渠道覆盖最全，Fin 3 支持复杂推理。"
  },
  {
    scenario: "Enterprise（已用 Zendesk Suite）",
    pick: "Zendesk AI Agents + Copilot",
    reason: "无迁移成本，Copilot 成熟，收购 Forethought 后 AI 能力持续增强。"
  },
  {
    scenario: "Enterprise（已用 Salesforce 生态）",
    pick: "Salesforce Agentforce",
    reason: "CRM 数据集成无可替代，跨 Sales+Service 统一，但需接受高实施成本。"
  },
]
```

---

## Section 8 — Sources

```
1. Intercom Fin 官方文档 — https://www.intercom.com/help/en/articles/7120684-fin-ai-agent-explained
2. Intercom Fin 3 发布博客 — https://www.intercom.com/blog/whats-new-with-fin-3/
3. Zendesk Copilot 官网 — https://www.zendesk.com/service/ai/copilot/
4. Zendesk outcome-based 定价公告 — https://www.thehindubusinessline.com/info-tech/zendesk-launches-outcome-based-pricing-for-ai-agents/article68634373.ece
5. Zendesk 收购 Forethought — https://techcrunch.com/2026/03/11/zendesk-acquires-agentic-customer-service-startup-forethought/
6. Forethought 官方定价 — https://forethought.ai/pricing
7. Salesforce 定价更新官方公告 — https://www.salesforce.com/news/stories/pricing-update/
8. Salesforce Agentforce 定价演变 — https://redresscompliance.com/salesforce-agentforce-pricing-evolution-2026.html
9. Freshworks 官方定价 — https://www.freshworks.com/freshdesk/pricing/
10. Kustomer 官方 AI 定价 — https://www.kustomer.com/ai-pricing/
11. AI CS 定价横向对比 — https://fin.ai/learn/ai-customer-service-agent-pricing-comparison
12. 市场规模数据 — MarketsandMarkets via https://paymentib.marketsandmarkets.com/Market-Reports/ai-for-customer-service-market-244430169.html
13. GlobeNewsWire 市场报告 — https://www.globenewswire.com/news-release/2025/03/07/3038782/0/en/AI-in-Customer-Service-Market-Report-2025-2030
调研日期：2025 年 4 月 20 日
```

---

## 给 Codex 的执行说明

### 任务

生成一个单文件 `index.html`，实现上述 AI 客服竞品分析横屏报告，可直接部署到 GitHub Pages。

### 文件结构

```
index.html          ← 唯一文件，所有 CSS/JS 内联
```

### 实现要求

1. **数据内联**：将 `products`、`scores`、`costData`、`featureMatrix`、`positioning`、`insights`、`recommendations` 全部写成 JS 常量，放在 `<script>` 块中
2. **ECharts CDN**：`https://cdn.jsdelivr.net/npm/echarts@5/dist/echarts.min.js`
3. **Inter 字体**：Google Fonts CDN
4. **导航**：顶部固定 nav，点击跳转各 Section（`scroll-behavior: smooth`）
5. **图表响应**：窗口 resize 时调用 `chart.resize()`
6. **Section 间距**：每个 Section `min-height: 100vh`，`padding: 60px 80px`
7. **卡片悬停**：`transform: translateY(-4px)`，`transition: 0.2s`
8. **矩阵表格**：固定表头（`position: sticky; top: 0`），横向可滚动
9. **评分圆点**：用 `<span>` 实现，颜色按分值规则渲染
10. **不需要**：响应式、移动端、暗/亮模式切换、外部 API 调用

### 交付标准

- 在 Chrome 1440px 宽度下无横向滚动（除矩阵表格区域）
- 5 张 ECharts 图表全部正常渲染
- 所有数据与本 SPEC 一致
- 文件大小 < 500KB（不含 CDN 资源）
