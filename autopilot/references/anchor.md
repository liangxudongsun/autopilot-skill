# anchor — 每轮再锚（V2.025；≤1 屏，自含）

> 每轮开头真读本文件（工具调用，非记忆检查），缺读 = deviation。全文重读仅限：会话首轮 / compact·clear 后 / 版本不符 / 拿不准。

- **轮卡**：首轮发完整开工卡（四行：任务·slug·lane·档位 ｜ 本轮调用 ｜ 分流（shield·Gate0）｜ 链·产物·第一动作；字段定义见 `SKILL.md` Round protocol）；其后每轮以一行 `卡刷新｜lane=…｜正身=…｜下一步=…` 开场；新任务、新 slug、理解转动手 → 回 Step 0 重发全卡。
- **车道一行**：A=单行直接改＋per-class 门 ｜ B=spec 嵌 ≤3 切片＋红绿＋review ｜ C=map＋票图（`effort-flow.md`）｜ D=先建反馈环再修（`bug-flow.md`）｜ E=triage 后只做 ready 票。
- **档位**：默认 full；lite 五件地板（卡/车道/一个通道产物/验证一句/日志一行）缺一 = malformed；na 仅限纯理解·误触发·STOP（`self-answer.md`）。
- **纯理解/查询轮**：不碰仓库文件；四件最小产物 = 分流行 ＋ 检索面/命中计数（含负证据口径；**不抄命中内容**）＋ 对话内检索清单（`core-triggers.md` 只读节；本 build 无日志本）。
- **收尾两件**：`Skills called:` 按调用序 ＋ 本轮 trace 三行（产物/deviation/审计；本 build 无日志本）；删标记（单轮开闭照旧记豁免行）。
