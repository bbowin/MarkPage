# 快速开始与常见问题 QUICK-START

## 三种使用方式

### 1. 单文件版（推荐）

打开 `dist/QingJian-standalone.html`。所有资源（CSS / JS / 字体 / 第三方库 / 演示文档）内嵌于一个文件，`file://` 双击即可运行，离线可用。

### 2. 分置版

打开 `dist-split/QingJian-split.html`，须保持同目录 `assets/` 完整（KaTeX 字体、PlantUML 本地主题、懒加载库）。

### 3. 模块化项目（开发 / 二次开发）

解压 `QingJian-v14.21-modular.zip`：
- 修改源码后用 `python3 build/build_standalone.py` 重新构建；
- 构建产物输出到 `dist/`（内嵌）与 `dist-split/`（分置）。

## 常见问题 FAQ

**Q：为什么打开大 HTML 文件界面不崩？**
A：html / epub 内容渲染在 Shadow DOM 中（样式隔离），不污染编辑器 UI。

**Q：安卓手机能否导出 / 保存文件？**
A：可用"下载 / 分享"系统能力保存；在 Chrome / Edge / 小米浏览器等支持 File System Access 的浏览器中可直接选路径保存。旧 QQ 浏览器（X5）部分文件能力受限，建议换浏览器。

**Q：朗读没有声音？**
A：桌面端推荐 Microsoft Edge（内置免费在线自然语音）；安卓端推荐 Chrome / Edge / 小米浏览器（系统 TTS）。若内核无朗读 API（如部分 X5 内核），会提示静默失败——可配置「本地音库服务 / Azure 在线」音源。

**Q：网络电台播不了？**
A：多数为远端服务器 CORS 限制，属于流源侧限制；软件本身不抓取、不存储直播源。

**Q：为什么有的代码块在预览区没有行号？**
A：预览区采用所见即所得高亮（v14.21 起恢复 hljs 完整高亮）；如需行号请在源码区查看（源码区行号可开关）。

**Q：`.doc` 文件打不开？**
A：浏览器环境无法解析旧版二进制 .doc，请先另存为 .docx / .txt / .md 后打开。

**Q：能商用吗？**
A：软件为 MIT 许可，可自由使用与分发；内置资源全部宽松许可，详见 COMPLIANCE.md。内置演示文档中的长沙经济 / 科创数据为虚拟数据，正式材料请核验官方原文。
