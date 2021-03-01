## GTB 代码质量评分细则说明

GTB 使用 Sonarqube 工具分析学员提交的作业、评估代码，根据分析结果对代码质量做出评分，并计入每次作业、评估的成绩。

每次作业、评估的代码库的代码质量评分总分为 20 分，根据 Sonarqube 分析结果中的 5 个指标构成，分别是

- 认知复杂度 *Cognitive Complexity*
- 重复代码占比 *Duplicated Lines Density*
- 可维护性评级 *Maintainability Rating*
- 可靠性评级 *Reliability Rating*
- 坏味道 *Code Smells*

本文以下详细定义各项指标的评分标准。 其中 *本次作业/评估失败* 是指存在某些严重的错误，导致当前代码库的评分以 0 计，而不再考虑其他指标项的得分情况。

### 认知复杂度

[认知复杂度](https://en.wikipedia.org/wiki/Cognitive_complexity)
是描述代码被阅读和理解时的复杂程度的度量，其定义和计算方法请查阅 SonarSource S.A. 发表的
[白皮书](https://www.sonarsource.com/docs/CognitiveComplexity.pdf)
和
[简介](https://blog.sonarsource.com/cognitive-complexity-because-testability-understandability)
。 GTB 给定了每个代码库的**参考复杂度**，在 GTB Dashboard 上可以查阅。

GTB 使用 **Sonarqube 分析得出的代码认知复杂度** 与 **参考复杂度** 之比（CCR）来确定一份代码认知复杂度得分，具体规则是：

- 若 CCR ≥ 2: 本次作业/评估失败
- 若 1.5 ≤ CCR < 2: 计 0 分
- 若 1.2 ≤ CCR < 1.5: 计 1 分
- 若 CCR < 1.2: 计 3 分

### 重复代码占比

GTB 使用 **Sonarqube 分析得出的代码重复率（DLP）** 来确定重复代码占比得分，具体规则是

- 若 DLP ≥ 3.5: 计 0 分
- 若 1.5 ≤ CCR < 3.5: 计 1 分
- 若 0.5 ≤ CCR < 1.5: 计 2 分
- 若 CCR < 0.5: 计 3 分

### 可维护性评级

GTB 使用 **Sonarqube 分析得出的可维护性评级（MR）** 来确定可维护性评级得分，具体规则是

- MR 为 `C` `D` `E`：本次作业/评估失败
- MR 为 `B`：计 0 分
- MR 为 `A`：计 2 分

### 可靠性评级

GTB 使用 **Sonarqube 分析得出的可靠性评级（RR）** 来确定可靠性评级得分，具体规则是

- RR 为 `C` `D` `E`：本次作业/评估失败
- RR 为 `B`：计 0 分
- RR 为 `A`：计 2 分

### 坏味道

GTB 使用 **Sonarqube 分析得出的坏味道（CS）的严重度和数量** 来确定坏味道得分，具体规则是

- 没有 Code Smell: 10 分
- 出现 `INFO` 级的 Code Smell: 10 分（不影响得分）
- 出现 `MINOR` 级的 Code Smell: 每出现一个，扣除 2 分，总共扣完 10 分后不再累计
- 出现 `MAJOR` `CRITICAL` `BLOCKER` 级的 Code Smell: 本次作业/评估失败
