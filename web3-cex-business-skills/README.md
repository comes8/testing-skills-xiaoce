# Web3 CEX 业务测试 Skills

面向现货撮合、合约交易和资金账务的需求分析与业务测试设计。执行沿用已有测试平台；这里维护业务分析方法、任务 Prompt 和可复查样例。

## 第一批

- **1 个 Skill**：`cex-requirement-review`，需求分析、评审与补全。
- **2 份 Prompt**：P01 需求解读与业务分析、P02 需求评审与缺口补充。
- **验证材料**：三个合成输入、验收检查口径和独立评估记录。它们不是任何真实交易所的规则或真实交易执行证据。

评估保留了首轮发现的一处只减仓判据遗漏及其修订，详见 [修订与复核记录](evals/results/revision-01-review.md)。新一轮应用已分别检验“不增仓”和“不反向”，并检查了多头、空头同方向增仓的反例。

```text
web3-cex-business-skills/
├── cex-requirement-review/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/
├── prompts/
│   ├── P01-requirement-analysis.md
│   └── P02-requirement-review.md
└── evals/
    ├── cases/
    ├── acceptance.md
    └── results/
```

先阅读 [Skill 入口](cex-requirement-review/SKILL.md)，或复制 [P01](prompts/P01-requirement-analysis.md) / [P02](prompts/P02-requirement-review.md) 的正文，附上实际资料。Prompt 中的双花括号是有意保留的输入变量，可直接用附件或资料路径替代。

在 Codex 中注册该 Skill 后，可这样发起任务：

```text
使用 $cex-requirement-review，从业务、研发和测开视角分析这些需求与技术资料。
梳理相关流程、规则和状态，找出缺口和冲突，给出有来源的验收依据。
本次先完成需求分析与评审，不展开完整测试用例。
```

本目录是源码交付，不表示已经安装到全局技能目录。仅使用 Skill 时复制 `cex-requirement-review` 整个目录，保持内部参考文件路径。它不依赖其他八个尚未交付的规划 Skill，也不要求连接某个具体平台。

## 平台使用边界

P01/P02 可以作为独立任务提示词。接入 N-Tester 的需求分析、Writer/Reviewer 等阶段时，需要核对调用链和输出字段；本批不修改平台、不注册配置、不把普通报告冒充接口场景 JSON，也不执行交易或压测。

本批聚焦需求准备程度。后续业务建模、测试点、专项和回归能力按分批计划补齐；当前不会因为引用未来能力而阻塞独立使用。
