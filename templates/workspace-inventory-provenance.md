# 工作区清单与来源追溯记录模板

**Status:** Released for Validation  
**Purpose:** 记录工作区清单的完整性、路径映射、来源证据、责任确认与处置授权。此模板是记录工具，不会自动扫描、上传或清理文件。

## 使用说明

1. 每次采集使用唯一的 `INVENTORY_ID`，填写任务合同与收口报告引用。所有无法确认的字段写 `UNKNOWN`；不适用写 `N/A`，未执行写 `NOT RUN`，受阻写 `BLOCKED`。
2. 清单应保存在经授权、受访问控制的持久化位置；不要只留在临时目录或聊天记录。填写稳定的制品指针、SHA-256、大小和条目数，并由有权限的人员回读验证指针与哈希。不得把秘密、Token、凭据或不必要的个人数据写入清单。
3. 记录采集时的仓库、分支、HEAD、工作区状态、方法/命令、时间与时区、操作人及任务/会话/运行标识。时间同时保留 UTC 时间和原始时区/偏移。
4. 路径分组必须逐项关联直接证据。分别记录已提交版本来源、当前未提交差异来源和人员责任；提交作者不自动等于当前差异作者或责任人。无直接证据时保持 `UNKNOWN`。
5. 以下状态必须分别判定，不得相互推导：
   - `MANIFEST_EXISTS`：制品存在的证据已记录。
   - `MANIFEST_ACCESSIBLE`：授权核查者已成功读取该制品。
   - `MAPPING_VERIFIED`：分组/路径映射已依据直接证据核对。
   - `OWNER_CONFIRMED`：责任人已由有权人员明确确认，并记录确认依据。
6. 默认保护未知文件并且不处置。禁止自动清理。移动、删除、重命名、暂存、提交、推送或其他改变工作区/制品状态的动作，必须有明确的单独授权及可追溯批准记录。
7. 本记录是执行证据，不是验收裁决。按 `templates/task-closeout.md` 分别报告执行事实、独立核查和总控裁决。

---

## A. 记录身份与制品指针

| 字段 | 值 |
|---|---|
| INVENTORY_ID | |
| TASK_ID / ROUND_ID | |
| PARENT_TASK / CONTRACT_REF | |
| CLOSEOUT_REPORT_REF | |
| MANIFEST_URI（受控、稳定的持久化指针） | |
| STORAGE_OWNER / ACCESS_ROUTE | |
| SHA256 | |
| SIZE_BYTES | |
| ENTRY_COUNT（如适用） | |
| CAPTURED_AT_UTC（ISO 8601） | |
| ORIGINAL_TIMEZONE / UTC_OFFSET | |
| MANIFEST_EXISTS | UNKNOWN / YES / NO |
| MANIFEST_ACCESSIBLE | UNKNOWN / YES / NO |
| READ_BACK_VERIFIED_BY / AT | |

## B. 采集上下文

| 字段 | 值 |
|---|---|
| REPOSITORY | |
| BRANCH | |
| HEAD_COMMIT_SHA | |
| WORKTREE_STATUS（采集时） | |
| CAPTURE_METHOD / COMMANDS | |
| ENVIRONMENT / WORKSPACE_ID | |
| OPERATOR | UNKNOWN |
| SESSION_ID | UNKNOWN |
| RUN_ID | UNKNOWN |
| CAPTURED_AT_UTC | |
| ORIGINAL_TIMEZONE / UTC_OFFSET | |

## C. 路径与分组映射（每个分组/路径范围单独一行）

| GROUP_ID | PATH / PATH_RANGE | TRACKING_STATE | SOURCE_TASK / PR / COMMIT / RUN | DIRECT_EVIDENCE_REF | MAPPING_STATUS | NOTES |
|---|---|---|---|---|---|---|
| | | UNKNOWN | | | UNKNOWN | |

`MAPPING_STATUS` 可使用 `VERIFIED`、`NOT IN SOURCE`、`UNKNOWN`、`BLOCKED`。必须说明映射所依据的直接证据；不能只因文件相邻、内容相似或时间接近就建立映射。

## D. 来源与责任归属（每个关键文件/差异单独一行）

| PATH | COMMITTED_BASELINE_SHA | CURRENT_DIFF_REF / HASH（如可得） | DIFF_ORIGIN_STATUS | OWNER_STATE | OWNER | CONFIRMATION_EVIDENCE | CONFIRMED_BY / AT |
|---|---|---|---|---|---|---|---|
| | | | UNKNOWN | UNKNOWN | UNKNOWN | | |

- `DIFF_ORIGIN_STATUS` 描述当前差异来源，不等同于已提交版本来源。
- `OWNER_STATE` 只能填写 `CONFIRMED` 或 `UNKNOWN`；只有直接且足够的确认依据才可填写 `CONFIRMED`。
- Git 提交作者、文件内容、时间戳或推测不能单独证明当前未提交差异的作者/责任人。

## E. 保护与处置授权

| 字段 | 值 |
|---|---|
| PROTECTION_STATE | UNKNOWN / PROTECTED / NOT PROTECTED |
| ALLOWED_READ_ONLY_ACTIONS | |
| DISPOSITION_STATE | NO DISPOSITION AUTHORIZED |
| EXPLICIT_AUTHORIZATION_REF | N/A |
| APPROVER / APPROVED_AT_UTC | N/A |
| AUTHORIZED_SCOPE / EXPIRY（如适用） | N/A |
| BACKUP / ROLLBACK_EVIDENCE（如适用） | N/A |

未填写明确授权时，禁止任何改变文件或工作区状态的处置；不得把“未提及保护”解释为“未受保护”。

## F. 四种独立证据状态

| 状态 | 结果（YES / NO / UNKNOWN / BLOCKED） | 证据引用 | 核查者 / 时间 |
|---|---|---|---|
| MANIFEST_EXISTS | UNKNOWN | | |
| MANIFEST_ACCESSIBLE | UNKNOWN | | |
| MAPPING_VERIFIED | UNKNOWN | | |
| OWNER_CONFIRMED | UNKNOWN | | |

每个状态必须有各自的证据引用。一个状态为 YES 不得自动使其他状态变为 YES。

## G. 安全、风险与交接

- **Secrets / privacy check:** 不记录秘密或不必要个人数据；结果：
- **Unresolved gaps / risks:**
- **Recovery condition / required source:**
- **Reported vs independently reproduced:**
- **Independent verification limitation:**
- **Next action / responsible role:**
- **Controller decision required:**

## H. 最小收口核对清单

- [ ] 稳定制品指针、SHA-256、大小/条目数已记录。
- [ ] 仓库/分支/HEAD、工作区状态、采集时间及时区已记录。
- [ ] 操作人、任务/会话/运行 ID 均已记录；未知项明确标记 `UNKNOWN`。
- [ ] 路径分组与来源证据逐项对应；未证实映射保持未知。
- [ ] 已提交版本来源、当前差异来源、人员责任分别记录。
- [ ] 四种证据状态分别判断并引用证据。
- [ ] 存储位置可由授权人员读取并完成回读验证。
- [ ] 未执行自动清理；所有处置均有单独明确授权，默认不处置。
- [ ] 按 `templates/task-closeout.md` 提交事实报告；未执行检查标 `NOT RUN`，阻塞标 `BLOCKED`。
