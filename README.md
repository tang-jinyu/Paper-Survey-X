# Paper Survey X · 论文调研助手X

> 让 AI 帮你调研论文，但它**绝不许编造引用**。
> 一个平台无关的 Agent Skill：分层检索 → 逐条核实 → 九列 Excel 调研表 → 论文图表 → 领域版图总结。
> 当前功能基线：**v1.2.1**（与 Kimi 插件「论文调研助手X」v1.2.1 同步）。

## 为什么做这个

2026 年的第三方审计显示，主流 AI 深度研究工具的学术引用错误率在 37%～94% 之间——你拿到一份漂亮的调研报告，里面三分之一的文献可能根本不存在。本技能把"防编造"写成了最高纪律：

- 每条文献入表前必须核实存在性、链接可达、会议与年份交叉验证；
- 查无实据的一律进「存疑清单」，**宁可少收，不可编造**；
- 表格是"已验证真相"的单一来源，持续迭代。

## 功能

- 📚 **分层检索**：经典方法 / ML-RL / fuzzing / 形式化 / LLM-Agent 全谱系，中英文双语关键词；
- ✅ **逐条核实**：链接、会议、年份三重验证，开源项目附 LICENSE 状态；
- 📊 **九列 Excel 调研表**：题目、中文名、链接、会议期刊、时间、主要方法、架构、核心思想、可借鉴点——方法/架构/思想**分点详述**（3～6 要点），拒绝一句话概括；
- 🧭 **阅读指南**：数量概览、可点击工作表导航、建议阅读顺序和使用纪律；
- 🎀 **统一暖色排版**：浅粉暖色、中文宋体、英文和数字 Times New Roman，首行标题 14pt、正文 10pt；
- 🔗 **具名链接**：直接显示论文／工程具体名称，并在插入标题行后逐行核对链接目标；
- 🖼️ **论文图表全嵌入**：截取原文架构图/结果图/对比图（开放获取 PDF），用通俗中文自绘架构图/流程图，所有已产出图片嵌入「图形类」sheet 并适配行高；
- 🗺️ **领域版图总结**：方法梯队、最强路线、与你工作的重叠预警；
- 🧹 **去重**：支持与已有调研清单去重，适合增量调研。

## 安装

本技能遵循 [Agent Skills](https://agentskills.io/specification) 开放格式（一个文件夹 + `SKILL.md`），可用于任何实现该格式的 agent。

### Claude Code

```bash
# 个人级
cp -r skills/paper-survey-x ~/.claude/skills/
# 或项目级
cp -r skills/paper-survey-x .claude/skills/
```

### Codex / 其他 agent

将 `skills/paper-survey-x/` 整个文件夹复制到对应 agent 的技能目录（如 `.codex/` 技能路径），或把 `SKILL.md` 全文粘贴进自定义指令 / system prompt。没有任何平台专属 API 依赖。

### Kimi

本技能的官方 Kimi 封装（插件「论文调研助手X」）见 Releases 中的 `.kplugin` 文件，下载后按自定义插件方式安装。

## 使用

安装后直接用自然语言触发，例如：

```
调研数字IC验证领域提高功能覆盖率的方法，生成表格
调研 ECDSA P-521 硬件实现相关论文，用于芯片设计选题
调研 LLM agent 方向的论文和开源项目（此前已调研过 A、B、C，去重）
```

输出：带「阅读指南」「论文」「开源项目」「图形类」的 `XX方向调研_论文与开源项目.xlsx` + `XX方向调研_figures/` 高清图集 + 领域版图总结 + 存疑清单。Excel 自含全部已产出图片，并通过链接、图片数量、字体与实际渲染检查。

## 仓库结构

```
paper-survey-x/
├── skills/paper-survey-x/
│   ├── SKILL.md              # 触发条件 + 工作流程 + 质量红线
│   └── references/
│       ├── design.md         # 阅读指南、暖色、字体、具名链接、图片嵌入与终检规范
│       ├── schema.md         # 九列表格定义与样式约定
│       └── figures.md        # 图表截取、自绘、嵌入与数量核验规范
├── README.md
└── LICENSE                   # MIT
```

## 效果示例
1. 描述简洁
<img width="2416" height="1449" alt="image" src="https://github.com/user-attachments/assets/974c15ba-8d30-429c-b5ff-e66e4f984230" />
2. 生成物
<img width="2359" height="1257" alt="image" src="https://github.com/user-attachments/assets/2b86acf7-e376-483f-9f0e-5d53b8afc197" />
<img width="1255" height="599" alt="image" src="https://github.com/user-attachments/assets/f1d48611-b7cc-4e77-a788-fc7b20b3520c" />
<img width="1070" height="610" alt="image" src="https://github.com/user-attachments/assets/2e2d0591-a4e3-43a6-b7f2-70071be42e0e" />
<img width="1822" height="1176" alt="image" src="https://github.com/user-attachments/assets/ea79898a-e93d-4781-bac2-e56a800ed5ef" />
<img width="1590" height="1188" alt="image" src="https://github.com/user-attachments/assets/fe534068-176f-42fb-9551-a8ebea1d0034" />
<img width="947" height="639" alt="image" src="https://github.com/user-attachments/assets/0a0b6d77-414e-4c51-bdb7-eef9897356b9" />




## 贡献与协议

- 欢迎 Issue / PR：新的检索线索、更好的核实方法、效果截图；
- 代码与文档均采用 [MIT License](LICENSE)；
- 安全提示：skill 会以 agent 权限运行，安装第三方 skill 前请先阅读其 SKILL.md 全文。

## Star History

如果这个项目帮到了你，欢迎点一个 ⭐
