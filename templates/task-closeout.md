# 通用任务收口与验收裁决记录模板

**Status:** Released for Validation  
**Purpose:** 将执行事实、独立核查和正式验收裁决分开记录，防止“代码完成”被误报为已验证、已推送、已集成或已接受。

> 填写规则：记录实际状态；未知写 UNKNOWN，未执行写 NOT RUN，环境阻塞写 BLOCKED。执行方的建议不能替代有权验收者的裁决。

---

# [TASK_ID]｜任务收口记录

PROJECT:
TASK_ID:
ROUND_ID:
PARENT_TASK:
CONTRACT_REF:
BASELINE_REF:
REPORT_DATE:
OVERALL_STATUS: VERIFYING

## A. 执行方事实报告

### A1. 结果

- **Implemented:** 实际完成内容：
- **Not implemented:** 未完成内容及原因：
- **Boundary:** 本任务未处理的事项：

### A2. 仓库与工作区状态

- Repository:
- Branch:
- HEAD / Commit SHA:
- Worktree status:
- Changed files:
- Diff summary:
- Commit status / SHA:
- Push status:
- Remote branch / SHA:
- Integration status:
- 其他相关环境/数据库/清理操作状态：

必须区分本地状态、远端状态和集成状态。没有实际读取证据时不得填写为已确认。

### A3. 验证证据

| 验收项 | 实际命令/步骤 | 环境 | 实际结果 | 退出码/状态 | 证据位置 |
|---|---|---|---|---|---|
| AC-01 |  |  |  |  |  |
| AC-02 |  |  |  |  |  |
| AC-03 |  |  |  |  |  |

- PASS 的验证项：
- FAIL 的验证项：
- NOT RUN 的验证项：
- BLOCKED 的验证项及缺失条件：
- 测试范围限制（mock、静态检查、单测、集成、真实后端/E2E）：

不得把测试文件存在、计划执行、模拟结果或执行方自述作为真实验证证据。

### A4. 已知问题与风险

| 问题 | 证据 | 影响 | 临时措施/恢复条件 | 是否阻塞验收 |
|---|---|---|---|---|
|  |  |  |  |  |

### A5. 执行方建议

- 建议状态：IMPLEMENTED / SELF-VERIFIED / PARTIAL / BLOCKED
- 建议下一步：
- 需要验收方决定的事项：

本节仅为执行方报告，不构成正式验收裁决。

---

## B. 独立核查记录

REVIEWER:
REVIEW_DATE:
REVIEW_STATUS: NOT STARTED
INDEPENDENCE_LIMITATION:

### B1. 实际核查范围

- 已核查：
- 未核查：
- 核查依据（仓库、提交、差异、测试证据）：

### B2. 发现

| Finding ID | 位置/证据 | 预期与实际差异 | 影响 | 最小修复/决定建议 |
|---|---|---|---|---|
|  |  |  |  |  |

### B3. 结论

逐项对照合同验收条件：
- 已通过：
- 未通过：
- 无法确认：
- 独立性限制及其影响：

若核查者修改过被核查的实现，必须明确披露；对该修改的自查不能宣称为完全独立核查。

---

## C. 有权验收者正式裁决

DECISION_OWNER:
DECISION_DATE:
FINAL_DECISION: PENDING

可选值：ACCEPTED / REJECTED / BLOCKED / ON HOLD / CANCELLED / APPROVED FOR INTEGRATION。

### C1. 裁决依据

- 对应验收条件与证据：
- 接受的风险或限制：
- 拒绝项/阻塞项：
- 是否允许集成；目标分支/环境：
- 是否允许清理、迁移或其他高风险操作（如适用）：

### C2. 正式关闭与冻结

仅在满足相应关闭条件后填写：
- Closed by:
- Closure timestamp:
- Accepted baseline / commit:
- Final status:
- 未解决事项及后续责任方：
- 需要保留的报告、审计或证据位置：

### C3. 下一步交接

- 下一任务/阶段：
- 接收角色：
- 必须沿用的 BASELINE / Contract：
- 当前阻塞与恢复条件：
- 下一步唯一明确动作：

---

## 状态解释

- IMPLEMENTED：实现完成，不表示测试通过。
- SELF-VERIFIED：执行方已完成自检并提供证据。
- INDEPENDENTLY-VERIFIED：授权核查者完成约定范围的独立核查。
- COMMITTED：提交已创建，必须记录 SHA。
- PUSHED：已推送，必须核对远端分支/提交。
- INTEGRATED：已进入约定的目标集成分支或环境。
- ACCEPTED / CLOSED：有权验收者根据证据作出正式决定。

以上状态不得相互推定。若验收证据不完整，应保持 VERIFYING、PARTIAL 或 BLOCKED，不得以流程结束为由强行关闭。
