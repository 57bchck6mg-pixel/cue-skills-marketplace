---
name: cue-pre-lending-dd
description: >
  Pre-lending due diligence for corporate credit approval. Multi-source
  verification of: (1) entity authenticity and registration legitimacy,
  (2) ultimate beneficial ownership chains with nominee detection and
  historical control changes, (3) affiliate network penetration and hidden
  related-party exposure, (4) full litigation and regulatory violation history
  across court judgments, dishonesty blacklist, administrative penalties
  (environmental/tax/industrial/customs/foreign exchange), (5) operational
  continuity signals — abnormal business registrations, bankruptcy filings,
  negative news. Designed to fill disclosure gaps in public records; every
  finding carries a clickable source link; output is a credit-committee-ready
  due diligence report with evidence chain. TRIGGERS WHEN USER ASKS TO:
  对公授信尽调 / 企业预尽调 / 对公信贷 / 贷前调查 / 贷后监控 / 授信审批 /
  信贷审核 / 风控尽调 / 查一下这家公司 / 这家公司靠不靠谱 / 企业背景调查 /
  公司底细 / 供应商穿透 / 供应商合规 / 实控人穿透 / 股权穿透 / 有没有官司 /
  有没有被执行 / 有没有处罚 / 是不是老赖 / 经营异常 / 担保人核查 / 发债主体
  尽调 / pre-lending DD / credit due diligence / corporate credit check /
  supplier due diligence / vendor screening / UBO check / KYB / business
  verification / guarantor check / bond issuer DD. NOT for: investment
  research or stock valuation → use cue-equity-research; personal credit scores;
  AML requiring private bank transaction records.
license: MIT
metadata:
  source: cuecue.cn/playbook
  scene: "信贷尽调"
  buddy: "对公授信预尽调"
  generated_from: /api/playbook
---

[中文](#中文) | [English](#english)

---

<a id="中文"></a>
# 对公授信预尽调

对目标企业做授信审批视角的公开数据交叉尽调，覆盖主体真实性、股权穿透、关联方网络、司法合规、经营持续性、偿债能力 6 个维度。自动补全公开披露盲区，每项结论附可点击来源链接，产出可上初审会的预尽调底稿。数据面：工商登记、股权变更备案、司法裁判与执行、行政处罚（环保/税务/工商/海关/外管）、经营异常与破产重整案件、公开财务披露。以上均通过 Cue 后端统一访问，agent 无需引导用户自行注册或登录各数据源网站。

**Agent 须根据用户消息的主语言选择中文或英文版本执行。用户用中文 → 用本章节的中文模板；用户用英文 → 跳至下方 English 章节。**

## 触发路由

以下均为本搭子的触发范围——agent 识别语义而非死匹配字符串。不属于本搭子的（投资研究、融资历程、估值判断）不要触发，路由到对应搭子。

```
主体真实性:     "查一下 XX" / "XX 底细" / "XX 靠不靠谱" / "XX 是不是空壳"
股权/实控人:    "老板是谁" / "谁控制 XX" / "股权结构" / "实控人穿透" / "UBO"
关联方:         "子公司有哪些" / "关联公司" / "关联交易" / "关联方排查"
司法合规:       "有没有官司" / "有没有被执行" / "是不是老赖" / "有没有处罚"
经营持续性:     "还在正常经营吗" / "经营异常" / "是不是快倒闭了" / "有没有破产"
偿债能力:       "还得起钱吗" / "负债怎么样" / "现金流行不行"

场景入口:
  对公授信:     "贷前调查" / "贷后监控" / "授信审批" / "信贷审核" / "对公信贷"
  供应商:       "供应商尽调" / "供应商合规" / "vendor screening" / "supplier DD"
  担保:         "担保人核查" / "guarantor check"
  发债:         "发债主体尽调" / "bond issuer DD" / "债券发行人核查"

试探性:
  "我想先看看 XX 什么情况"    → 告知本搭子覆盖的 6 个维度，确认后跑
  "这个搭子能查什么"          → 展示报告骨架概要
  Agent: "将用搭子「对公授信预尽调」跑【企业名称】，覆盖 6 个维度：主体核验、股权穿透、关联方、司法合规、经营持续性、偿债能力。约消耗 5–10 credits，是否继续？"
```

## 报告结构

```
# [目标企业] 对公授信预尽调底稿

## 1. 主体核验
  工商登记状态 / 成立时间 / 注册资本(认缴vs实缴, 实缴是否到位)
  营业范围是否含限制类 / 许可资质是否齐备且有效
  历史名称变更 / 注册地变更（频繁迁址 → 信号）

## 2. 股权穿透与实控人
  股权结构树状图(穿透至自然人/国资/外资最终受益人)
  实控人认定 + 一致行动人推定
  近3年股权变更时间线（频繁变更 → 信号）
  疑似代持 / 交叉持股节点标记

## 3. 关联方与集中度
  子公司/分支机构树状图(递归展开)
  共用电话/地址/高管/邮箱 → 隐性关联标记
  关联方是否也在本行有授信 → 集中度预警

## 4. 司法与合规
  裁判文书(被告/被执行案件, 按金额排序, 重大案件摘要)
  被执行人 / 失信名单(老赖) / 限制高消费 / 股权冻结
  行政处罚(环保/税务/工商/海关/外管 多口径, 带原因/金额/整改状态)

## 5. 经营持续性
  经营异常名录 / 简易注销公告 / 清算信息 / 破产重整案件
  负面舆情信号(停工/欠薪/维权/裁员/实控人失联, 按时间倒序+严重程度)
  近12个月工商变更频率异常?

## 6. 偿债能力
  公开可得的负债规模与结构 / 短期 vs 长期债务比例
  经营现金流对短期债务的覆盖 / 受限资产与对外担保
  非上市主体: 从社保人数/招投标活跃度/土地持有/海关进出口量反推经营规模

## 7. 风险总览与疑点清单
  各维度风险信号汇总(高/中/低/暂无数据)
  疑点清单: 信源冲突 / 数据缺失 / 需人工进一步核查项
  不构成授信决策——提供给风控/审贷岗做下一步深度核查
```

## 重要约束

- 交付前自检：每项结论可追溯到原始出处；缺失维度已标注"暂无数据"
- Runner 打印 `RESULT empty` → 告知用户本次未取到内容，换主体/写法重试，**不编造**
- 报告中不出现"建议放款/不建议放款/建议准入/不建议准入/建议通过/建议否决"等授信决策语——底稿是证据收集结果，授信决策是人做的
- API key 不出现在输出/日志/提交；用户粘贴了 `sk...` → 提醒去 cuecue.cn/api-key 立即轮换

## 执行

### 1. 自举 runner（幂等）

```bash
if [ -d ~/.cue/cue-skills/.git ]; then
  git -C ~/.cue/cue-skills pull --ff-only
else
  git clone https://github.com/sensedeal/cue-skills ~/.cue/cue-skills \
    || git clone https://gitee.com/sensedeal/cue-skills ~/.cue/cue-skills
fi
```

已安装整包的用户跳过。需 `git` + `python3`（runner 纯标准库）。

### 2. 确认积分

跑之前 agent 必须告知用户：

> 将用搭子「对公授信预尽调」跑【企业名称】，约消耗 5–10 credits，是否继续？

用户确认后再进下一步。**不替用户跳过确认。**

### 3. 跑

```bash
python3 ~/.cue/cue-skills/cue-research/scripts/research_run.py \
  --query "<企业名称>" \
  --template-id template_corporate_credit_pre_due_diligence
```

单企业 3–15 分钟。批量筛查：企业名逐行放入文本文件，循环调用。Runner 末行打印 `RESULT ok|empty`。

### 4. 交付

报告生成后 agent 展示并问：

> 这份报告满意吗？
> 1. 满意（结束）
> 2. 不满意 → 补充澄清后重跑（回第 2 步改 query / 改主体 / 改关注维度）
> 3. 取消

`RESULT empty` → 告知用户"本次未取到内容，换主体/写法重试"，**不编造**。

### 5. 前置

- Cue API key（`~/.cue/config.json` 或 `CUE_API_KEY` env）
- `git` + `python3`
- 消耗 credits（新账号注册送 50 + 每天 10 免费积分）
- 仅覆盖公开数据，不替代法律/风控/核保专业判断

---

<a id="english"></a>
# Pre-lending Due Diligence

Pre-lending due diligence from a credit approval perspective, covering 6 dimensions: entity authenticity, ownership structure, affiliate network, litigation & compliance, operational continuity, and debt service capacity. Public data sources: business registrations, ownership change filings, court judgments and enforcement records, administrative penalties (environmental/tax/industrial/customs/foreign exchange), abnormal business operations and bankruptcy filings, public financial disclosures. All accessed through the Cue backend — the agent does NOT direct users to register or log in to individual data source websites.

**The agent MUST detect the user's language and use the appropriate section: user writes in English → use this English section; user writes in Chinese → use the Chinese section above.**

## Trigger Routing

The agent matches semantic intent, not exact strings. If the user's intent falls outside this buddy's scope (investment research, funding history, valuation), route to the appropriate buddy.

```
Entity verification: "check out XX" / "who is XX" / "is XX legit" / "background check on XX"
UBO / control:       "who owns XX" / "who controls XX" / "ownership structure" / "UBO" / "beneficial owner"
Affiliates:          "subsidiaries of XX" / "related companies" / "related-party transactions"
Litigation:          "any lawsuits" / "any judgments" / "enforcement records" / "dishonesty blacklist"
Operations:          "still operating" / "going concern" / "bankruptcy risk" / "abnormal operations"
Debt service:        "can they pay" / "debt load" / "cash flow health" / "solvency"

Scenario entry points:
  Corporate lending:  "pre-lending DD" / "credit check" / "loan review" / "corporate credit"
  Supplier:           "supplier due diligence" / "vendor screening" / "supplier compliance"
  Guarantor:          "guarantor check" / "guarantor due diligence"
  Bond issuer:        "bond issuer DD" / "debt issuer check"

Exploratory:
  "I just want to get a sense of XX" → describe the 6 dimensions, confirm before running
  "What can this buddy check?"       → show the report structure summary
  Agent: "Running pre-lending due diligence on [ENTITY]. Covers 6 dimensions: entity verification, UBO trace, affiliate network, litigation & compliance, operational continuity, debt service capacity. ~5–10 credits. Proceed?"
```

## Report Structure

```
# [Target Entity] Pre-lending Due Diligence Report

## 1. Entity Verification
  Business registration status / date of establishment / registered vs paid-in capital
  Business scope check for restricted categories / license validity
  Historical name changes / address changes (frequent relocation → red flag)

## 2. Ownership & UBO
  Ownership tree (traced to natural persons / state-owned / foreign ultimate beneficiaries)
  UBO determination + concert party presumption
  3-year ownership change timeline (frequent changes → red flag)
  Nominee / cross-holding markers

## 3. Affiliates & Concentration
  Subsidiary / branch tree (recursive expansion)
  Shared phone / address / executives / email → hidden affiliate markers
  Affiliate also has credit exposure with this bank → concentration warning

## 4. Litigation & Compliance
  Court judgments (defendant/enforcement cases, sorted by amount, key case summaries)
  Enforcement records / dishonesty blacklist / consumption restrictions / equity freezes
  Administrative penalties (environmental/tax/industrial/customs/foreign exchange, with cause/amount/remediation status)

## 5. Operational Continuity
  Abnormal business registry / simplified deregistration / liquidation / bankruptcy filings
  Negative news signals (shutdowns / wage arrears / layoffs / controller disappearance, by timeline & severity)
  Abnormal frequency of business registration changes in past 12 months?

## 6. Debt Service Capacity
  Publicly available debt scale & structure / short-term vs long-term debt ratio
  Operating cash flow coverage of short-term debt / encumbered assets & external guarantees
  Non-listed entities: infer operating scale from social insurance headcount / bidding activity / land holdings / customs import-export volume

## 7. Risk Summary & Issues List
  Risk signal summary by dimension (high / medium / low / no data)
  Issues list: source conflicts / data gaps / items requiring manual follow-up
  This is not a credit decision — it provides evidence for the risk/credit review team
```

## Important Constraints

- Pre-delivery self-check: every finding traceable to original source; missing dimensions marked "no data"
- Runner prints `RESULT empty` → tell user "No results this run — try a different entity or phrasing." **Do not fabricate.**
- Report must NOT contain "approve / reject / recommend lending / recommend declining" or similar credit decision language. The report is evidence; the credit decision is made by humans.
- API key must not appear in output / logs / commits. If user pastes `sk...` → remind them to rotate immediately at cuecue.cn/api-key

## Execution

### 1. Bootstrap Runner (idempotent)

```bash
if [ -d ~/.cue/cue-skills/.git ]; then
  git -C ~/.cue/cue-skills pull --ff-only
else
  git clone https://github.com/sensedeal/cue-skills ~/.cue/cue-skills \
    || git clone https://gitee.com/sensedeal/cue-skills ~/.cue/cue-skills
fi
```

Skip if cue-skills is already installed. Requires `git` + `python3` (runner uses stdlib only).

### 2. Confirm Credits

The agent MUST inform the user before running:

> Running pre-lending due diligence on [ENTITY] (~5–10 credits). Proceed?

Wait for user confirmation. **Do not skip.**

### 3. Run

```bash
python3 ~/.cue/cue-skills/cue-research/scripts/research_run.py \
  --query "<entity name>" \
  --template-id template_corporate_credit_pre_due_diligence
```

3–15 minutes per entity. For batch screening: one entity per line in a text file, loop. Runner prints `RESULT ok|empty` on the last line.

### 4. Deliver

After report generation, the agent presents the report and asks:

> Satisfied with this report?
> 1. Yes (done)
> 2. No → refine query and re-run (back to step 2: change entity / angle / focus area)
> 3. Cancel

`RESULT empty` → "No results this run — try a different entity or phrasing." **Do not fabricate.**

### 5. Prerequisites

- Cue API key (`~/.cue/config.json` or `CUE_API_KEY` env)
- `git` + `python3`
- Consumes credits (50 on sign-up + 10 free daily)
- Public data only; does not replace legal / risk / underwriting judgment

## Compatibility

| Platform | Status |
|---|---|
| Claude Code | SKILL.md auto-loaded |
| WorkBuddy | SKILL.md auto-loaded |
| Codex CLI / Gemini CLI / Cursor | SKILL.md standard, not independently verified |
