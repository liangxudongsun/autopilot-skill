# invocation — 调用面：tool / inline / missing（V2.030）

> 为什么要有这一页：有的 harness 会严格遵守子 skill 的 `disable-model-invocation: true`（DSH 就是），把 Skill 工具调用直接拒掉。这不是「没装」，也不是「skill 坏了」，是**调用面**问题。规则不认这条路，driver 就只能在「违规 inline」和「空转补调」之间二选一（真实现场：ask-matt 被拒后先干活、收尾才补 T0；档案里另有 5 条开工卡把 automatt 冒名成 T0）。

## 三种调用面（每个 skill 只判一次，判完缓存在本轮 trace）

| 面 | 判定 | 合法动作 | 痕迹 |
|---|---|---|---|
| `tool` | Skill 工具返回正文 | 按正文执行 | `Skills called:` 写名字 |
| `inline` | 工具返回 `is not available for model invocation`；或 `unknown or no longer available` 但已安装目录里有正文 | 读已安装的 `SKILL.md` 正文（优先装目录 `.dsh/skills/`、`.codex/skills/`；读到仓内同内容副本也合法，但开工卡 `调用面:` 必须写**实际读到的那个路径**，V2.040），按正文 inline 执行 | `Skills called:` 写 `name(inline)` ＋ `调用面:` 行 ＋ 正文 `file:line` |
| `missing` | 工具拒绝/未知，**且** `<skills-root>/<name>/SKILL.md` 确实不存在（用 `test -f` 复核，别凭印象） | 用 `references/` 的 bundled fallback，记 deviation | `deviation:` 逐项 |

**拒绝串识别（原样匹配，别猜）**：

- `skill "<name>" is not available for model invocation` → `inline`（harness 遵守了 flag）
- `skill "<name>" is unknown or no longer available` → 先查已安装目录：有正文 = `inline`，无 = `missing`
- 没有 Skill 工具 / 工具整体不可用 → 按 `inline` / `missing` 处理，判据不变

**被拒 ≠ missing（V2.037 现场：把 harness 过滤掉的 skill 记成 missing，于是走了 bundled fallback 而不是 inline 读）**：判 missing 前必须 `test -f <skills-root>/<name>/SKILL.md`；文件存在就是 inline，文件不存在才是 missing。

**最多探一次**：同一个 skill 在同一会话最多试一次工具；被拒后直接用缓存的面，后续轮次不再试。已知 harness 会拒绝（如 DSH）时可以直接读正文、连探都不探；探过再探 = 空转，记 deviation。**已安装但被拒 ≠ `missing`**：目录里有正文就必须 inline 读，**不得用 bundled fallback 代替**（V2.034 现场：ask-matt 被拒后误记 bundled-fallback）；bundled 只在目录里确实没有正文时使用。

**读安装副本正文的路径（V2.052，别自己拼）**：用**安装目录路径原样读** —— `~/.dsh/skills/<name>/SKILL.md`（或 `~/.codex/skills/<name>/SKILL.md`）。这两个是 junction，**不要自己去解析它的目标再拼路径**（现场：某轮读了 junction 目标后**把路径少拼了一层仓根** —— 拼到家目录底下去 → 文件不存在 → 一行红字；真身（自用库里的那本）一直是好的）。**读不到就换另一条已验证路径再试一次**（先换同名的另一个 harness 目录，再换自用库路径），别停在报错上 —— 那不是 skill 坏了。
**用哪个工具读（V2.053）**：`read` 能穿过 junction 读到安装副本；`ops_inspect_local_file` 对同一路径会报 `PATH_RESTRICTED`（那是沙箱读策略，**不是文件不存在**）⇒ 读安装副本一律用 `read`，别拿 `PATH_RESTRICTED` 当「没装」。

## 痕迹格式（机器可查）

开工卡/卡刷新加一行（只列本轮要用的 skill，别列 27 个）：

```
调用面: ask-matt=inline(read <skills-root>/ask-matt/SKILL.md:1-40)｜to-spec=inline(...)｜tdd=tool
```

`Skills called:` 行同步标注：`ask-matt(inline), to-spec(inline), tdd, code-review`。审计与 `grep` 都按这个格式对账；出现在 `调用面:` 里却没有 `(inline)` 标注、或标了 `(inline)` 却没有正文 `file:line` 的，按未加载正身记。

**inline 的合法证据**（缺一 = malformed）：①文件真实路径 + 行号；②正文里的一句引用（能看出本轮用的条款）；③`substitution: inline(harness-flag)` 注记。只写「我读了」不算。

## T0 特别条款

T0 只能是 `ask-matt`（`tool` 或 `inline`）——**加载 automatt 本身不是 T0**。T0 必须是本轮**第一个 skill 动作**（加载 driver 与 Step 0 侦察/必读集不算），且在任何 lane skill、任何改文件之前；被拒或已知会被拒时直接 inline 读 `ask-matt/SKILL.md`，不许先干活再补。inline 读属于「把正文当路由表读」，不是「调用 user-invoked skill」，不违反编排铁律。

## 与既有条款的关系

- `core-triggers.md`「子 skill 只回文档：inline 执行并注记」：那是**工具成功但只回文档**；本页是**工具被 harness 拒绝**。两者都要求 inline 执行，但痕迹不同（前者写 `substitution`，后者写 `(inline)` + `调用面:`）。
- `core-triggers.md`「正身优先：fallback 只留给未安装」：加一条——**拒绝 ≠ 未安装**，拒绝走 inline 读，未安装才走 bundled fallback。
- 本页对所有带 `disable-model-invocation: true` 的子 skill 生效（27 个里 16 个；8 个核心里 5 个），不限于 T0。
