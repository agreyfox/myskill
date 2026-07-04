# My AI Agent Skills Library 🛠️

这是一个专为 AI 编码/智能代理（如 Antigravity, Claude Code, Cursor 等）设计的全局 Skill (技能) 库。  
通过在代理的自定义路径中挂载此目录，可以让所有的开发 Agent 共享并自动装载这些经过优化的高价值技能。

## 📂 技能列表

当前库中收录了以下 **12** 个高价值 Skill：

| 技能名称 (Dir) | 简介 | 核心职责 |
|---|---|---|
| 📂 [debugger](./debugger) | 调试与报错解决专家 | 当程序报错、测试失败或发生异常行为时，指导 Agent 进行系统化排查与修复。 |
| 📂 [deep-research](./deep-research) | 深度网络调研与研究 | 提供系统的网页检索、内容收集、并行研究并最终汇集成高标准报告的指南。 |
| 📂 [frontend-design](./frontend-design) | 前端设计与像素级还原 | 还原 UI 设计稿、确保高水准审美与优秀交互设计的视觉工程指南。 |
| 📂 [flutter-expert](./flutter-expert) | Flutter/Dart 开发专家 | 针对跨平台移动端开发的 Flutter & Dart 最佳实践和组件化架构设计。 |
| 📂 [golang-pro](./golang-pro) | Go 语言高级开发专家 | 编写高性能、并发安全且架构清晰的 Go 语言代码规范。 |
| 📂 [bazi-skill](./bazi-skill) | 传统八字命理分析 | 结合易经八字理论，分析个人运势和性格特征的趣味分析技能。 |
| 📂 [legal-advisor](./legal-advisor) | 法律分析与合同审查 | 针对法律文本的系统性结构分析、合同漏洞扫描与合规性审查建议。 |
| 📂 [brainstorming](./brainstorming) | 头脑风暴与思维发散 | 指导 Agent 进行多维度、打破常规的创意激发与方案构思。 |
| 📂 [grilling](./grilling) | 深度痛点挖掘与苏格拉底提问 | 类似于 Matt Pocock 提倡的 "Grilling" 模式，通过尖锐且有深度的问题挖掘核心需求。 |
| 📂 [imagen](./imagen) | Imagen 图像生成控制 | 精细化控制图像生成 Prompt 和参数，生成符合高要求视觉规范的图片资源。 |
| 📂 [obsidian](./obsidian) | Obsidian 知识库管理 | 处理和同步本地或云端的 Markdown 笔记，实现自动化双链管理。 |
| 📂 [obsidian-project-executor](./obsidian-project-executor) | Obsidian 项目执行工作流 | 用 Obsidian Project Plan、功能/Gap note、实施 leaf log 和测试门禁推进软件项目。 |

---

## ⚙️ 如何在 Agent 中使用？

### 1. 全局挂载到 Antigravity / Gemini CLI
在全局配置文件中将此路径添加到您的自定义技能加载路径（或克隆到您的自定义 roots 目录下）。

### 2. 在其他工作区（如 Claude Code / OpenClaw）中链接
可在目标项目工作区的 `.agents/skills/` 下，或者通过环境变量加载此技能库。
