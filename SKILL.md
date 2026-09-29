---
name: smooth-plan-switcher
description: 制作"超丝滑"的方案切换组件（分段控制器 / 滑块胶囊 / 套餐·定价·月付年付切换 / 标签页切换 / segmented control / pricing toggle / plan switcher）的前端 skill。只要用户提到方案切换、套餐切换、定价切换、tab 切换、滑动胶囊、丝滑切换动画、分段选择器，或想给网页加带滑动指示器与内容淡入淡出的切换 UI，即使没有明确说"组件"，也务必使用本 skill。输出单文件 HTML/CSS（可选少量 JS），带弹性滑块、内容交叉淡入、键盘无障碍、深浅色主题与减弱动画支持。
---

# 丝滑方案切换组件

生成一个"滑块胶囊 + 内容平滑切换"的方案切换组件。核心体验：点击选项时，高亮胶囊像有弹性一样滑到目标位置，同时下方内容淡入淡出且**不发生布局跳动**。

> 来源说明：本 skill 依据视频《教你做一个超丝滑的方案切换组件》（B站 UP 主：原子软糖At）的主题整理，
> 技术做法为通用的前端实现思路，并非视频逐帧复刻。

## 何时使用

- 月付 / 年付、个人 / 团队 / 企业等套餐切换
- 任意 2–5 个互斥选项的分段控制器（segmented control）
- 需要"滑动指示器"而不是简单高亮切换的 tab

## 工作流程

1. **确认需求**：选项数量与文案、是否等宽、是否需要下方内容面板、主题色。用户没说就用默认：3 个选项、等宽、带面板、跟随系统深浅色。
2. **选择实现**：
   - 选项**等宽** → 纯 CSS 方案（默认，见 `assets/plan-switcher.html`）
   - 选项**不等宽**（文字长度不同） → 读 `references/variants.md` 的 JS 测量方案
3. **以 `assets/plan-switcher.html` 为起点**改文案、颜色、选项数，交付单文件 HTML。
4. 按下方"质量清单"自检后再交付。

## 核心技巧（必须保留）

| 目标 | 做法 |
|---|---|
| 滑块丝滑 | 只动画 `transform`，不要动画 `left/width`；用 `--i`（当前索引）驱动 `translateX(calc(var(--i) * 100%))` |
| 弹性手感 | `transition: transform .5s cubic-bezier(.34, 1.4, .64, 1)`（轻微过冲） |
| 状态来源 | 用原生 `<input type="radio">` + `:has(:checked)`，无需 JS 即可切换，天然支持键盘方向键 |
| 内容不跳动 | 所有面板叠放在同一个 grid 单元格（`grid-area: 1/1`），只切 `opacity` / `transform`，容器高度取最高面板 |
| 交叉淡入 | 未选中面板 `opacity:0; transform: translateY(8px); pointer-events:none; visibility:hidden`，选中面板延迟 60–80ms 进入，避免两层重叠 |
| 文字颜色 | 文字色过渡与滑块同步（`transition: color .3s`），选中态文字在胶囊上保持对比度 |
| 主题 | 颜色全部放 CSS 变量，`prefers-color-scheme: dark` 里重定义 |
| 无障碍 | `role="radiogroup"` + `aria-label`；保留 `:focus-visible` 焦点环；`prefers-reduced-motion` 下关闭动画 |

## 选项数量变化

纯 CSS 版本用 `--n`（选项数）控制宽度：`.thumb { width: calc(100% / var(--n)); }`，
新增选项时需同步：① 增加 radio + label ② 修改 `--n` ③ 增加对应 `:has(#pN:checked)` 规则 ④ 增加面板。

## 质量清单（交付前自检）

- [ ] 点击、键盘方向键、Tab 聚焦都能切换，焦点环可见
- [ ] 快速连点不会出现滑块卡顿或面板重叠
- [ ] 切换面板时页面高度不抖动
- [ ] 深色 / 浅色模式都清晰可读
- [ ] 开启"减少动画"时无位移动画
- [ ] 手机宽度（≤ 380px）下不溢出
- [ ] 单文件、无外部依赖（不引用 CDN 图片/字体）

## 文件

- `assets/plan-switcher.html` — 可直接打开的完整示例（纯 CSS，3 选项 + 面板）
- `references/variants.md` — 不等宽选项的 JS 测量方案、竖向切换、增加图标/角标的写法
