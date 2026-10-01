# 架构与渲染管线 ARCHITECTURE

> 青简 QingJian v14.21 · 模块化项目布局与核心渲染逻辑。

## 目录结构

```
MarkPage-fixed/
├── index.html               # 壳页面（导航 / 状态栏 / 面板骨架 + 第三方库内联引用）
├── css/
│   ├── layout.css           # 整体布局、工具栏、状态栏、面板
│   ├── content.css          # markdown-body 内容排版 + hljs 主题 + KaTeX 隔离层
│   ├── extra.css            # 增量样式（播放条 / 文件切换浮层 / PlantUML 面板 / 行号等）
│   └── print.css            # 打印 / 导出 PDF 版式
├── js/
│   ├── config.js            # 常量与配置（ZOOM_KEY / DEMO_DOC 等）
│   ├── state.js             # MP.State 全局状态（tabs / activeTab / dom 引用）
│   ├── utils.js             # 工具函数（escapeHtml / debounce / 文件读写）
│   ├── render/              # 渲染管线（见下）
│   ├── sync/scroll-sync.js  # 预览 ↔ 源码 ↔ TOC 同步
│   ├── ui/ui.js             # UI 装配：菜单 / 状态栏 / 模板插入 / 文件 IO / 快捷键
│   ├── ui/filetree.js       # 文件树 / 目录面板
│   └── app.js               # 启动组装（缩放恢复 / demo 载入 / 安卓引导）
├── demo/                    # 内置演示文档（Markdown-语法样例精讲.md）
├── assets/                  # 第三方库 + KaTeX 字体 + PlantUML 本地主题
├── build/build_standalone.py# 单文件 / 分置版构建脚本
└── dist/ dist-split/        # 构建产物
```

## 渲染管线（markdown → 预览）

```
源码文本
  → markdown-it（html / linkify / typographer + footnote/sub/sup 扩展）
      ├─ fence 规则分发：mermaid / plantuml / graphviz / abc / chart / canvas-math
      │                    / smiles / physim / chemsim / astrosim → 占位容器
      └─ 普通块 → HTML
  → 公式占位回填（data-math-block / data-math-inline → KaTeX，mhchem 化学式）
  → hljs 代码高亮（预览区所见即所得）
  → 图表异步渲染（Mermaid / PlantUML / Graphviz / 五线谱 / 扩展 Canvas 块，懒加载）
  → TOC 数据收集（块级锚点映射 buildAnchors）
  → 文本朗读句序列（reader.refreshParagraphs）
```

## 关键设计

1. **双轨源码区**：textarea（真实编辑）+ overlay（行号 + 高亮）。行号 `.ln` 与文本行
   `vertical-align: top`、padding 精确对齐（10px 原点）；高亮层禁用全局
   `pre code.hljs` 的 padding 污染（`padding:0 !important`）。
2. **三向同步**：`buildAnchors()` 为每个块级元素生成锚点 → 预览滚动时按锚点映射源码行；
   源码滚动时反向定位预览块。md / txt 用块级锚点，html / epub 回退标题级。
3. **epub**：JSZip 懒加载 → `zipFind`（大小写兜底）+ `resolveHref`（URL 解码）+
   图片 data URI 内联 → 章节列表挂目录；预览走 Shadow DOM 隔离样式。
4. **五线谱**：abcjs 仅绘图与音符时序提取（MIT）；音频由自研 `piano-synth.js`
   （WebAudio 振荡器合成，无采样版权）；播放条与谱面容器分离 + z-index 隔离。
5. **朗读引擎**：句子级分句（标点 + 换行）；卡拉 OK 高亮以引擎 `onstart` 为唯一推进点
   （onend 兜底），静默检测只提示不推进；数字按年月 / 位数习惯读法。
6. **扩展仿真**：`physim`（单摆 / 抛体 / 简谐 / 电场线 / 透镜 / 麦克斯韦 / 动力学 / 气体粒子）、
   `chemsim`（滴定 / 相图 / 轨道）、`astrosim`（开普勒轨道 / 黑体光谱 / 月相）——
   全部复用 mathjs + Canvas 自研逻辑，按需懒加载，动画可暂停 / 静态切换。
7. **构建**：`build/build_standalone.py` 将 css / js / 第三方库 / 字体 / demo 内联为
   单文件版（dist/），或外链 assets 生成分置版（dist-split/）。
