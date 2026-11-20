# Web3 CEX 业务测试 Skills

面向现货撮合、合约交易和资金账务的需求分析与业务测试设计。执行沿用已有测试平台；这里维护业务分析方法、任务 Prompt 和可复查样例。

当前已交付 **7 个业务 Skill、10 份 Prompt**。每个 Skill 自包含，可直接消费原始资料，也可复用上一阶段产物，不要求安装整套规划能力。

| 阶段 | Skill | 配套 Prompt |
|---|---|---|
| 需求分析与补全 | [cex-requirement-review](cex-requirement-review/SKILL.md) | [P01 需求分析](prompts/P01-requirement-analysis.md)、[P02 需求评审](prompts/P02-requirement-review.md) |
| 业务建模 | [cex-business-modeling](cex-business-modeling/SKILL.md) | [P03 业务链路](prompts/P03-business-flow-modeling.md)、[P04 规则与状态](prompts/P04-rule-state-modeling.md) |
| 测试点设计与补充 | [cex-testpoint-design](cex-testpoint-design/SKILL.md) | [P05 核心测试点](prompts/P05-core-testpoint-design.md)、[P06 增量补充](prompts/P06-testpoint-supplement.md) |
| 测试点评审 | [cex-testpoint-review](cex-testpoint-review/SKILL.md) | [P07 评审与修订](prompts/P07-testpoint-review.md) |
| 现货与撮合专项 | [cex-spot-matching](cex-spot-matching/SKILL.md) | [P10 现货专项](prompts/P10-spot-matching.md) |
| 合约与风险专项 | [cex-futures-risk](cex-futures-risk/SKILL.md) | [P11 合约专项](prompts/P11-futures-risk.md) |
| 资金与对账专项 | [cex-funds-reconciliation](cex-funds-reconciliation/SKILL.md) | [P12 资金专项](prompts/P12-funds-reconciliation.md) |

## 第一批

交付需求分析、评审与补全 Skill 和 P01/P02。评估保留了首轮发现的一处只减仓判据遗漏及其修订，详见 [第一批修订与复核](evals/results/revision-01-review.md)。新一轮应用分别检验“不增仓”和“不反向”，并检查了多头、空头同方向增仓的反例。

## 第二批

新增业务建模、测试点设计、测试点评审三个 Skill，以及 P03—P07 五份 Prompt。重点处理：

- 订单、仓位、资金和展示的独立状态与收敛关系。
- 原量、累计成交、活动剩余、取消量及冻结资金的口径。
- 从来源和不变量推导有具体条件、预期与核对方法的测试点。
- 区分规则未定与执行准备不足，未知策略不写成固定答案。
- 增量补漏、错误预期修订、真正重复与不同竞争顺序的区分，保留 ID 和变更映射。

验证材料位于 `evals/batch-02/`，先读 [第二批评估与修订](evals/batch-02/results/batch-02-evaluation.md)。记录保留了阶段金额判据和真实重复资金效果的修订，原样试跑不是全部通过的标准答案。全部合成输入和文本试跑只检查设计与评审能力，不是实际交易、撮合、账务或平台自动化运行证据。

## 第三批

新增现货与撮合、合约交易与风险、资金账务与一致性三个专项 Skill，以及 P10—P12。重点将具体产品规则转换成可计算、可核对的业务场景：

- 现货先区分撮合资格、同价生效顺序、成交价格与订单类型，再核对撤改单、资金和行情代际。
- 合约先固定产品/账户画像，再分析委托、仓位、保证金、估值、费用资金费、结算与支持的风险处置。
- 资金先定义资产与科目、资金腿及阶段，再核对在途、费用、真实重复效果和链上事件身份。

样例与记录在 `evals/batch-03/`，先读 [第三批评估与修订](evals/batch-03/results/batch-03-evaluation.md)。它们是合成资料的文本应用，不是实际交易或平台执行证明。

P08/P09 与 P13/P14 属于最后一批，当前编号按原任务目录保留，并非漏存文件。

## 使用与交接

可按“需求分析 → 业务模型 → 测试点 → 评审修订”使用，也可只选一个阶段。Prompt 的双花括号是有意保留的输入变量，替换为实际资料或附件引用即可。

```text
使用 $cex-business-modeling，依据这些需求和现有分析梳理相关业务链路、状态和资金关系。
使用 $cex-testpoint-design，基于上述模型生成核心测试点，分开记录确定预期和待确认分支。
使用 $cex-testpoint-review，依据原始资料评审清单，只修订受影响条目并保留已有编号。
```

这是源码交付，不表示已安装到全局技能目录。使用单个 Skill 时复制相应整个目录，保持内部参考文件路径。本次没有自动运行上述示例指令或注册平台配置。

## 平台边界

Prompt 可独立作为任务指令。接入 N-Tester 等平台时，需要核对阶段、字段和输出格式；普通 Markdown 报告不能冒充接口场景 JSON 或已写入的测试资产。本系列不另建接口/UI/性能执行框架，不执行交易或压测。

后续剩余详细用例设计评审、变更影响与回归两个 Skill 及四份 Prompt，仍按最后一批计划交付；当前阶段不依赖尚未创建的能力。
