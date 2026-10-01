# 能力清单 CAPABILITIES

> 青简 QingJian v14.21 —— 全部能力按模块列出，均离线可用。

## 1. UI 框架（index.html + css/* + js/ui/ui.js + js/ui/filetree.js）

- 顶部导航栏：logo（青简蓝圆 SVG + Favicon dataURL）、菜单（新建 / 打开 / 打开文件夹 / 导出 / 撤销 / 重做 / 目录面板显隐 / 插入模板 / 播放条）
- 多标签页（不关闭当前页新建 / 打开；激活文档以颜色区分）
- 状态栏：类型胶囊（兼文档切换）、编码、大小、字符统计、渲染耗时、就绪态、行号开关、朗读条（🔊 / ⚙️ / ▾，最小态不跨行）
- 左侧目录 / 文件树面板（一个按钮控制整栏显隐；页签内部分别承载文档 TOC 与系统文件树）
- 欢迎首页（品牌化：新建 / 打开 / 功能卡片 / 最近打开）
- 移动端自适应：横屏引导（源码模式可竖屏）、按钮等比缩放、窄屏状态栏保留朗读条

## 2. 渲染管线（js/render/*）

| 模块 | 输入 | 输出 |
| --- | --- | --- |
| markdown.js | .md / .txt | HTML（markdown-it + 扩展插件）→ 公式回填 → hljs 高亮 → 图表懒加载 → TOC 数据 |
| math.js | $…$ / $$…$$ / mhchem | KaTeX 渲染（行内 / 块级 / 矩阵 / cases / align / \tag） |
| diagrams.js | ```mermaid / plantuml / dot``` | Mermaid 全 24 种图表、PlantUML 本地降级、Graphviz |
| extra.js | ```chart / canvas-math / smiles / physim / chemsim / astrosim``` | Canvas 数学曲线、SMILES 分子、交互式仿真（滑块 / 动画 / 暂停重置） |
| piano-synth.js | ABC 音符时序 | 纯 MIT 自研 WebAudio 钢琴合成（无采样版权风险） |
| abcplayer.js | ```abc``` 五线谱 | 谱面 + 播放条（播放 / 暂停 / 重置 / 倍速 / 音量 / 卡拉OK音符高亮），z-index 隔离不与复制按钮重叠 |
| epub.js | .epub | JSZip 解包 → 章节 XHTML → 图片 data URI 内联 → 章节目录 → 默认 100% 预览 |
| reader.js | 预览文本 | 句子级分句朗读、卡拉 OK 跟读高亮、语速 / 语言 / 音源（system / local / azure）、朗读起点选择 |
| radio.js | ```radio``` / 频道面板 | HLS.js 懒加载音频流 / m3u8 直播，localStorage 频道管理，.m3u 批量导入，JSON 导入导出 |

## 3. 编辑能力（源码区）

- textarea + 高亮 overlay 双轨：行号逐行对齐（光标原点 10px 一致）、代码高亮、自动补全、成对闭合
- 每标签页独立撤销 / 重做；>256KB 自动降级纯 textarea
- 行号开关（可关闭）；html 源码同享编辑区并支持预览
- 代码块：预览区所见即所得高亮 + 一键复制；源码区完整行号

## 4. 同步联动

- 目录 / 预览 / 源码三向：TOC 点击 → 预览定位（块级锚点映射）；预览滚动 ↔ 源码滚动双向同步
- 打开文件后 TOC 自动展开；文件树页签切换内容（md 显示 TOC、文件夹显示系统树、epub 显示内部结构）
- 图片加载：打开文件 / 打开文件夹 / epub 三种路径均自动解析并统计成功数 / 总数

## 5. 导出

- PDF（A4 幅面、单图不跨页、字体字号出版级美化）、HTML（内嵌样式独立运行）、Word（.doc 兼容）
- 悬浮菜单导出均可选本地保存路径；导出 HTML 含完整渲染结果（公式 / 图表 / 谱面）

## 6. 文件与数据

- 打开：.md / .txt / .html（源码 + 预览）/ .epub / .doc（提示另存）/ 图片 / 音视频 / 文件夹
- 最近打开（同名仅保留最近一次）、草稿自动保存、localStorage 偏好

## 7. 安全与合规

- 用户数学表达式执行保留沙箱隔离；epub 内容在 Shadow DOM 中渲染（样式隔离）
- radio 播放器不内置任何直播源（免责声明）；频道数据仅存 localStorage
- 图标 / 字体 / 音频全部 MIT 兼容，无需要商用授权的素材（详见 COMPLIANCE.md）
