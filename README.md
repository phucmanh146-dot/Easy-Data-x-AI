# Easy Data × AI

> 我的「Easy Data × AI」课程学习笔记仓库
>
> 课程：[datawhalechina/easy-data-x-ai](https://github.com/datawhalechina/easy-data-x-ai) · [在线阅读](https://datawhalechina.github.io/easy-data-x-ai/)
> 主办：Datawhale 开源社区 · 课程协议：CC BY-NC-SA 4.0

这个仓库只放我自己的学习产出：每个 Task 一篇笔记，包含知识点重述、我的理解、踩坑记录和自检清单。**不复制教程原文**，引用处均标注出处。

---

## 学习进度

| 任务 | 范围 | 状态 | 笔记 |
| --- | --- | --- | --- |
| Task01 | 环境准备与课前导读（F0 / F1 / F2） | ✅ 已完成 | [Task01-环境准备与课前导读](notes/Task01-环境准备与课前导读.md) |
| Task02 | 场景识别与 API 工程化（P1 + D1） | ✅ 已完成 | [Task02-场景识别与API工程化](notes/Task02-场景识别与API工程化.md) · [思维导图](notes/Task02-思维导图.md) |
| Task03 | Agentic RAG 与 AI 应用数据层（P2 + D2） | ✅ 已完成 | [Task03-AgenticRAG与数据层](notes/Task03-AgenticRAG与数据层.md) · [思维导图](notes/Task03-思维导图.md) |

> 后续 Task 按群公告节奏补充。

---

## 目录结构

```text
Easy-Data-x-AI/
├── README.md                              # 本文件：仓库说明与进度
└── notes/
    ├── Task01-环境准备与课前导读.md          # 环境准备 + F0/F1/F2 学习笔记
    ├── Task02-场景识别与API工程化.md         # P1 场景识别 + D1 API 工程化（含分节心得 / 结构速览）
    ├── Task02-思维导图.md                    # Task02 复盘思维导图（Mermaid + 纯文本）
    ├── Task03-AgenticRAG与数据层.md          # P2 Agentic RAG + D2 数据层
    └── Task03-思维导图.md                    # Task03 复盘思维导图（Mermaid + 纯文本）
```

---

## Task01 一句话结论

这门课反复讲的是同一件事：**AI 产品的上限由数据决定，模型只是放大器**。

- F0（OpenClaw）示范：Agent「越用越好用」不是因为模型变强，而是因为每次交互的经验被写回了 workspace 里的 md 数据。
- F1 给出公式：`AI 产品能力上限 = 数据质量 × 模型能力`，幻觉/知识截止/个性化盲区是同一个根因——缺数据。
- F2 扩展为：`Agent 能力上限 = 模型能力 × 数据质量 + 流程编排`，RAG / MCP / Skill / Memory 本质都是「什么数据、在什么时机进入上下文」。

---

## Task02 一句话结论

做 Agent 之前先问一句「数据在哪」，**Tool Use 是模型从「只能说」变成「能做事」的分界线**。

- P1 给了判断尺子：数据可得性（最重要）、任务可定义性、流程编排（先 Workflow 再 Agent）。90% 的 AI 功能失败不是模型不行，而是立项时没人问数据在哪。
- D1 把工程讲透：对话本质是消息列表，模型没有记忆；流式输出首 Token 延迟比总生成时间重要；Tool Use 中模型只负责声明调用，真正执行和拿数据的是你的代码。
- 道与术呼应：代码连接的是管道，数据才是水。管道再精良，没水也白搭。

---

## Task03 一句话结论

**RAG 的 R 是 Retrieval，不是 Vector**；「AI 答得不好」是症状不是诊断，绝大多数问题在数据层。

- P2 先破除误解：向量搜索只是 Retrieval 的一路，全文、过滤、图谱、API 都算 R。传统 RAG 和 Agentic RAG 的差别不是复杂度，而是有没有环（DAG vs 闭环）。
- P2 给出可操作的归因框架：数据层（检索不到 / 检索到错的）、模型层（幻觉）、业务层（合规与风格），配合四步决策树；实践中 60%~80% 的问题在数据层，真正是幻觉的只有 10%~20%。
- D2 把判断落成工程：切分四策略（固定 overlap / 语义分块 / 动态 overlap / 父子 chunk）、Embedding 选型的四个维度，以及最关键的混合搜索——向量管语义、全文管精确、关系过滤管范围。
- 对比实验说明这不是「好一点」：纯向量把 E-4013 排在 E-4012 前面，混合搜索才把正确答案顶到第一，错误码搞错就是「对和错」。

---

## 本地环境（我的实际配置）

| 项 | 版本 / 状态 | 说明 |
| --- | --- | --- |
| OS | Windows | 教程对 Windows 单独给了 PowerShell 命令 |
| Python | 系统为 3.13.11，建了 3.11 虚拟环境 | 教程 CI 固定 3.11，`pyseekdb` 要求 3.11+ |
| Node | v24.16.0 | 仅文档站（VitePress）需要，跑示例代码不需要 |
| Docker | 未安装 | D2 起需要 seekdb Server 模式；Windows 不能用 Embedded |

复现命令（仓库根目录，PowerShell）：

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r code/requirements-test.txt
python -m pip check
$env:PYTHONPATH = "code/D3;code"
python code/D3/d3_5_evaluate.py     # 零 Key、零数据库的自检入口
```

---

## 引用与版权

- 课程内容版权归 Datawhale 及课程作者所有，采用 [CC BY-NC-SA 4.0](http://creativecommons.org/licenses/by-nc-sa/4.0/) 协议。
- 本仓库笔记为个人学习总结，非官方材料；标注「教程原话」处引用自课程，其余为个人理解。
- 若引用有误或表述不当，欢迎提 Issue 指正。
