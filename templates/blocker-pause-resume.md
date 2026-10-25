# 阻塞任务暂停、依赖登记与恢复记录模板

**Status:** Released for Validation  
**Purpose:** 将阻塞事实、允许继续的工作、禁止操作和恢复门槛持久化，防止重复空转或未经授权绕过依赖。此模板只记录与约束流程，不自动监控、重启或修改任何任务。

## 使用规则

1. 发现必需条件缺失时，立即暂停依赖该条件的分支，并记录本模板；不得因等待时间较长而自动恢复。
2. 分别记录可独立继续、必须暂停、禁止执行的工作。只有原任务合同明确允许的独立工作才可继续；否则请求总控裁定。
3. 同一失败动作在没有新证据、环境变化或明确诊断假设时不得重复执行。不得用猜测、Mock、虚构身份/数据或降低验收标准绕过阻塞。
4. 恢复必须同时满足：依赖/权限/环境实际可用；恢复证据可由授权人员核验；有权角色明确批准恢复。三者缺一，保持 `BLOCKED` 或 `ON HOLD`。
5. 恢复后沿用原 TASK_ID、原合同、历史证据和已接受 BASELINE，只处理未完成的阻塞项；不得重做已 PASS/CLOSED 的工作。
6. 没有新证据时不重复搜索、重跑或发布相同请求。只在预先定义的触发条件出现时复查。
7. 执行方记录事实并提出建议，不代替总控进行最终接受、关闭、风险豁免或跨任务资源裁定。

未知写 `UNKNOWN`；不适用写 `N/A`；未执行写 `NOT RUN`；缺少必需条件写 `BLOCKED`。不得将未知猜成已确认。

---

## A. 阻塞身份与影响

| 字段 | 记录 |
|---|---|
| BLOCKER_ID | |
| TASK_ID / ROUND_ID | |
| PARENT_TASK / CONTRACT_REF | |
| BASELINE_REF（已接受提交/证据） | |
| DETECTED_AT_UTC（ISO 8601） | |
| DETECTED_BY / ROLE | |
| CURRENT_STATUS | BLOCKED / ON HOLD |
| BLOCKED_ACCEPTANCE_ITEMS | |
| BLOCKER_DESCRIPTION（具体缺少什么） | |
| DIRECT_EVIDENCE_REF（日志、错误、权限/环境证据等） | |
| IMPACT_SCOPE（哪些工作/验收项受影响） | |
| RESPONSIBLE_ROLE / RESOLVER | UNKNOWN |
| WHY_REQUIRED（为什么缺少它不能安全/真实继续） | |

## B. 工作分流（每个工作项单独一行）

| WORK_ITEM | CLASSIFICATION | DEPENDENCY / REASON | CONTRACT_AUTHORITY_REF | CURRENT_ACTION | STATUS |
|---|---|---|---|---|---|
| | INDEPENDENT_CONTINUE / MUST_PAUSE / PROHIBITED | | | | |

分类规则：

- `INDEPENDENT_CONTINUE`：有合同明确授权，且不依赖该阻塞项；只做限定范围内的工作。
- `MUST_PAUSE`：正确性、权限、安全或真实验收依赖缺失条件；不得继续该分支。
- `PROHIBITED`：未经授权的高风险操作，例如擅自创建数据库/身份/数据、清理或移动未知文件、绕过权限、以 Mock 代替真实 E2E、降低验收门槛。

## C. 防止重复空转

| 字段 | 记录 |
|---|---|
| LAST_ATTEMPT / DATE | |
| ATTEMPT_ACTION | |
| ACTUAL_RESULT / ERROR_EVIDENCE | |
| SAME_ACTION_RETRY_ALLOWED | NO，除非存在下列新增依据 |
| NEW_EVIDENCE_OR_CHANGED_CONDITION | UNKNOWN |
| NEXT_DIAGNOSTIC_ACTION（如有，必须产生新证据） | |
| NO_NEW_EVIDENCE_ACTION | 保持 BLOCKED / ON HOLD；不重复相同动作 |

仅在新证据、环境/权限发生可证明的变化，或总控明确授权新的诊断步骤时，才可重新评估相同动作是否有价值。单纯经过时间不构成恢复证据。

## D. 恢复门槛（全部满足后才能恢复）

| 门槛 | 必须提供的证据 | 状态（PASS / FAIL / UNKNOWN / NOT RUN） | 核验人 / 时间 |
|---|---|---|---|
| R1. 必需依赖、权限、环境实际可用 | | | |
| R2. 恢复证据可被授权人员直接回读/复现 | | | |
| R3. 证据覆盖原阻塞原因及受影响验收项 | | | |
| R4. 有权角色明确批准恢复（附决策链接/记录） | | | |
| R5. 原任务合同、BASELINE 与剩余工作已重新对齐；无须重做已完成项 | | | |

**恢复判定：** 任何门槛为 FAIL、UNKNOWN 或 NOT RUN 时，不得恢复受阻分支。不得设置按日期、超时或重试次数自动恢复。

## E. 复查触发与恢复后的第一步

- **明确复查触发条件（例如收到指定环境可用证据、权限审批完成、原始来源记录恢复）：**
- **证据来源/应提供者：**
- **无新证据时的处理：** 保持当前状态；不重复同一搜索/失败动作，不重复发送相同请求。
- **恢复后唯一第一步：** 只核验本次阻塞项的恢复证据，再执行原合同中未完成的步骤。
- **必须保留的历史证据/状态：**
- **不重新执行的已接受 BASELINE：**

## F. 分层状态与收口

| 状态维度 | 当前状态 | 证据 / 说明 |
|---|---|---|
| 原任务整体状态 | INCOMPLETE / BLOCKED / ON HOLD / 其他有证据状态 | |
| 本阻塞分支 | BLOCKED / ON HOLD / RESUMED / RESOLVED | |
| 可独立交付项 | NOT STARTED / IN PROGRESS / IMPLEMENTED / SELF-VERIFIED / 其他 | |
| 正式验收/关闭 | PENDING，除非有权角色已裁决 | |

- **已完成且沿用的 BASELINE：**
- **本轮实际完成：**
- **未执行/受阻项及恢复条件：**
- **已知风险和责任归属未知项：**
- **执行方建议（不等于总控裁决）：**
- **总控需要决定的事项：**
- **下一步唯一明确动作 / 责任角色：**

## G. 最小收口核对清单

- [ ] 阻塞项、具体缺失条件、直接证据、影响范围和恢复条件已记录。
- [ ] 可独立继续、必须暂停、禁止执行的工作已分开列明。
- [ ] 已停止受阻分支；没有用 Mock、猜测或降低验收标准绕过。
- [ ] 无新增证据时不重复同一失败动作。
- [ ] 恢复门槛逐项核验，并有权角色明确批准；不自动恢复。
- [ ] 原任务 ID、合同、历史证据和已接受 BASELINE 得到保留。
- [ ] 整体任务、阻塞分支、独立交付项和正式裁决分别记录。
- [ ] 未执行的检查写 `NOT RUN`，未知写 `UNKNOWN`，阻塞写 `BLOCKED`。
- [ ] 通过 `templates/task-closeout.md` 提交事实报告，并由总控独立核查/裁决。
