# smooth-plan-switcher

一个用于生成"丝滑方案切换组件"（滑块胶囊分段控制器 + 内容平滑切换）的 Claude Skill。

- 纯 CSS 实现（`radio` + `:has()`），弹性滑块、面板交叉淡入、无布局跳动
- 支持键盘操作、深浅色主题、`prefers-reduced-motion`
- 附带不等宽选项的 JS 测量方案

## 目录

```
smooth-plan-switcher/
├── SKILL.md                    # 技能说明（Claude 读取）
├── assets/plan-switcher.html   # 可直接打开预览的完整示例
└── references/variants.md      # 变体与常见坑
```

## 使用

- **Claude.ai / Claude Code**：将 `smooth-plan-switcher` 文件夹放入 skills 目录（或在设置中上传），
  然后对 Claude 说"帮我做一个丝滑的套餐切换组件"即可触发。
- **直接预览**：双击打开 `assets/plan-switcher.html`。

## 说明

灵感来自 B站视频《教你做一个超丝滑的方案切换组件》（UP 主：原子软糖At）。
本仓库是基于该主题的通用实现，非视频源码；如需引用请注明原视频。

## License

MIT
