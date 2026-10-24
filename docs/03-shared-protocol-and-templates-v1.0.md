# AI 协同开发共享协议与模板 V1.0

**Status:** Released for Validation  
**Version:** 1.0  
**Purpose:** 供总控规范与中间层规范共同引用，统一术语、状态和交接字段，避免各角色重复记忆或定义冲突。

## 1. 角色与权力边界

| 角色 | 主要责任 | 不得擅自决定 |
|---|---|---|
| Controller / 总控 | 项目目标、授权、优先级、跨组协调、最终验收与集成决定 | 不得把最终决策责任默认为下放 |
| Middle Layer / 中间层工作组 | 任务拆解、编程工具协调、独立核查、集中纠错、交接 | 不得改变目标、验收标准、共享 Contract 或跨组资源决定 |
| Coding Tool / 编程工具 | 按执行合同实现并自检，提交证据与报告 | 不得扩大范围、绕过授权或自行宣称最终接受 |

架构为三个责任层级，不增加第四层。具体项目可使用 A/B/C 等并行工作组名称，但名称不改变权限边界。

## 2. 标识规则

- `TASK_ID`：任务的稳定身份。
- `ROUND_ID`：同一任务的一次执行/纠错轮次，例如 `TASK-042-R01`、`TASK-042-R02`。
- `PARENT_TASK`：上级授权任务；没有时写 `N/A`。
- `BASELINE`：已被正式接受且可作为后续工作的前序状态/提交/证据。
- `CONTRACT`：任务目标、范围、交付物、验收标准及权限边界的明确约定。

项目已有正式编号规则时必须沿用，不得为套用示例而重写历史标识。若项目按每轮递增任务号管理，应保留其既有约定，并另设关联字段追踪父任务与轮次。

## 3. 状态词汇

| 状态 | 含义 |
|---|---|
| PLANNED | 已规划，尚未开始实施 |
| IN PROGRESS | 正在实施 |
| IMPLEMENTED | 实现已完成，但尚不表示测试通过 |
| SELF-VERIFIED | 实施方已执行自检并提供证据 |
| INDEPENDENTLY-VERIFIED | 授权的独立核查者完成约定范围核查 |
| COMMITTED | 已在本地/目标仓库创建提交；需记录 SHA |
| PUSHED | 已推送到指定远端分支；需核对远端状态 |
| INTEGRATED | 已按约定进入目标集成分支/环境 |
| PASS / CLOSED | 指定验收方已根据证据正式接受并关闭 |
| PARTIAL | 部分完成，仍有明确剩余事项 |
| VERIFYING | 验证正在进行，尚无最终结论 |
| BLOCKED | 缺少必需条件，当前无法安全或真实地继续 |
| ON HOLD | 经有权角色决定暂缓 |
| CANCELLED | 经有权角色决定取消 |
| REJECTED | 验收方根据证据拒绝接受 |

状态不能自动推导：IMPLEMENTED ≠ SELF-VERIFIED；SELF-VERIFIED ≠ INDEPENDENTLY-VERIFIED；COMMITTED ≠ PUSHED；PUSHED ≠ INTEGRATED；上述任一状态都不自动等于 PASS/CLOSED。

## 4. 任务执行合同模板

复制以下模板并填写；不适用字段写 N/A，不要留有影响执行的模糊项。

```markdown
# [TASK_ID]｜任务名称

PROJECT:
TASK_ID:
ROUND_ID:
PARENT_TASK:
AUTHORIZED_BY:
EXECUTION_OWNER:
STATUS: PLANNED

## 1. Objective
唯一核心目标：

## 2. Confirmed Baseline / Contracts
已接受基线、Contract 文件、提交 SHA、已知事实：

## 3. In Scope
允许修改/调查的文件、模块、环境：

## 4. Out of Scope
明确禁止或暂不处理的内容：

## 5. Dependencies / Preflight
必需权限、凭据、数据库、服务、数据、前置任务及开工检查：

## 6. Implementation Requirements
具体要求；避免让执行方猜测关键业务规则：

## 7. Deliverables
必须交付的代码、文档、报告、证据：

## 8. Acceptance Criteria
可客观判断的通过条件：

## 9. Verification Plan
命令/步骤、环境、预期结果、必须提供的实际输出：

## 10. Stop Conditions / Safe Partial Work
何时停止；阻塞时允许继续的只读或非依赖工作：

## 11. Risk / Authorization
禁止操作、高风险操作授权及回滚要求：

## 12. Handoff
报告接收者、必须记录的状态、证据路径和下一决策点：
```

## 5. 编程工具完工报告模板

```markdown
# [TASK_ID]｜完工报告

TASK_ID:
ROUND_ID:
STATUS: IMPLEMENTED / SELF-VERIFIED / PARTIAL / BLOCKED

## Implemented
实际完成内容：

## Files Changed
文件路径及变更摘要：

## Verification
- 命令/步骤：
- 环境：
- 实际结果/退出状态：
- 失败、跳过或未执行项：

## Repository State
- Branch:
- Commit SHA:
- Remote branch / SHA:
- Push status:
- Integration status:

## Known Issues
已知问题、风险和未验证事项：

## Boundary
本轮未处理内容及原因：

## Next
建议下一步；不得替总控宣称最终接受：
```

## 6. 中间层独立核查模板

```markdown
# [TASK_ID]｜独立核查报告

TASK_ID:
ROUND_ID:
REVIEWER:
STATUS: PASS / PARTIAL / BLOCKED / REJECTED

## Scope Checked
实际核查范围与未核查范围：

## Evidence
仓库/分支/提交、文件差异、测试命令与实际结果：

## Findings
每项问题包含位置、证据、影响和最小修复建议：

## Independence Limitations
核查者是否修改过被核查内容；若有，说明独立性限制：

## Conclusion
逐项对照验收标准给出结论：

## Handoff
需要总控决定的事项及建议下一步：
```

## 7. 总控任务台账模板

| 字段 | 记录内容 |
|---|---|
| TASK_ID / ROUND_ID | 稳定任务身份与当前轮次 |
| Objective / Scope | 目标、允许范围、排除项 |
| Owner / Dependencies | 执行组、依赖和共享资源 |
| Baseline / Contract | 已接受基线及正式 Contract 位置 |
| Status | 当前真实状态 |
| Evidence | 测试、审查、远端状态和报告位置 |
| Completed / Remaining | 已完成与剩余工作 |
| Blocker / Recovery | 阻塞原因和恢复条件 |
| Controller Decision | 接受、拒绝、继续、挂起、取消或集成决定 |
| Next Action | 唯一明确的下一动作及责任方 |

## 8. 轮次与纠错原则

目标是尽量在 3–5 轮交互内收口。若未能收口，应基于证据重新规划、合并纠错或升级总控，不得以轮数为由降低质量。每轮必须有明确输入、产出和状态变化；无新增证据或决策的重复循环应停止。

## 9. 证据最低要求

- 计划执行不等于实际执行。
- 测试文件存在不等于测试通过。
- mock、静态分析或局部单测不能冒充真实后端/业务 E2E。
- 本地提交不能证明远端已更新。
- 推送不能证明已集成。
- 自检不能冒充独立核查。
- 无实际证据时使用 NOT RUN、UNKNOWN 或 BLOCKED，不得猜测 PASS。

## 10. 变更控制与验证记录

修订本协议时记录版本、修改原因、影响规范、兼容性和验证证据。两份角色规范不得自行定义与本协议冲突的状态含义。当前全部文件均为 Released for Validation；真实试用前不得宣称已经正式验证。
