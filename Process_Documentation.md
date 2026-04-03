# MamaWell ビジネスプラン ブラッシュアップ — 全プロセス記録
# MamaWell Business Plan Refinement — Full Process Documentation

**作成日 / Date：2026-04-03**
**作成者 / Author：Jumpei Maruyama**
**使用ツール / Tools：Gemini (Web), Claude Sonnet 4.6 (claude.ai), Claude Code Opus 4.6 (CLI)**

---

## 全体フロー / Overall Flow

```
Phase 1: 初期プラン作成（Gemini） / Initial plan creation (Gemini)
    ↓
Phase 2: 壁打ち・修正（Claude Code） / Iterative refinement (Claude Code)
    ↓
Phase 3: マルチエージェント検証（Claude Code — 6エージェント並列）
         Multi-agent pressure test (Claude Code — 6 agents in parallel)
    ↓
Phase 4: 財務モデル修正 + プランv3作成 / Financial model fix + Plan v3
    ↓
Phase 5: AI Feedback Report作成 / AI Feedback Report creation
    ↓
Phase 6: GitHub公開 / GitHub publication
```

---

## Phase 1: 初期プラン作成 / Initial Plan Creation（Gemini）

### やったこと / What we did
- Geminiに課題要件（Startup-Business-Plan-AI.pdf）を読ませて壁打ち開始
- 射出成形機の予兆検知AIエージェントなど複数アイデアを検討
- 最終的にMamaWell（産後メンタルヘルスB2B2C SaaS）を選択
- Geminiが10セクション構成のビジネスプランを生成
- 同時にAI Feedback Report（MamaWell_AI_Feedback_Report.docx）も生成

- Fed the assignment requirements (PDF) to Gemini and began brainstorming
- Explored multiple ideas including predictive maintenance AI for injection molding machines
- Selected MamaWell (postpartum mental health B2B2C SaaS)
- Gemini generated a 10-section business plan and the initial AI Feedback Report

### 成果物 / Deliverables
- BusinessPlan v1（Word形式 / Word format）
- AI Feedback Report v1（Word形式 / Word format）

### この段階で残っていた問題 / Remaining issues
- 通貨の混在（¥と£が25箇所で混在） / Currency mixing (¥ and £ in 25 places)
- SAM計算の根拠が弱い / Weak SAM calculation basis ("30% are postpartum-eligible" — unrealistic)
- 財務モデルの内部整合性が未検証 / Financial model internal consistency not verified

---

## Phase 2: Claude Codeでの壁打ち・修正 / Iterative Refinement with Claude Code

### やったこと / What we did

#### 2-1. 通貨統一 / Currency unification
Claude Codeに元のdocxを読み込ませ、£表記を全て¥に統一。25箇所を特定し修正。

Read the original docx in Claude Code and unified all £ symbols to ¥. Identified and fixed 25 locations.

#### 2-2. SAM計算の根本修正 / SAM calculation overhaul
- **修正前 / Before：** 従業員の30%がpostpartum対象 → 900人 → SAM ¥81.6B
- **修正後 / After：** 実際のpostpartum対象者は55〜100人。PEPM全従業員課金モデルなのでSAM計算は企業単位 → 2,400社 × 3,000人 × ¥3,500 × 12 = ¥302B

- Before: "30% of employees are postpartum-eligible" → 900 people → SAM ¥81.6B
- After: Actual postpartum-eligible employees are 55–100. Since PEPM charges all employees, SAM is calculated at the company level → 2,400 × 3,000 × ¥3,500 × 12 = ¥302B

#### 2-3. ビジネスモデルの根拠強化 / Business model justification
「なぜ55〜100人のために全員分払うのか」→ EAPやSlackと同じ「アクセス権としての福利厚生」モデル

"Why pay for all 3,000 when only 55–100 are postpartum?" → Same "benefit-as-access" model as EAP or Slack

### 成果物 / Deliverables
- BusinessPlan_v2.md

---

## Phase 3: マルチエージェント検証 / Multi-Agent Pressure Test（★最も重要 / Most Important Phase）

### コンセプト / Concept
ビジネスプランを複数の専門家の視点から同時に検証する。Claude Codeの「Agent」ツールを使い、6つのサブエージェントを**並列実行**した。

Validate the business plan simultaneously from multiple expert perspectives. Used Claude Code's "Agent" tool to run 6 sub-agents **in parallel**.

### エージェント構成 / Agent Configuration

| # | ペルソナ / Persona | 設定した専門性 / Expertise | 評価の焦点 / Focus |
|---|---------|-------------|----------|
| 1 | **CFO**（大企業 / Large enterprise） | 3,000名企業の最高財務責任者 / CFO of 3,000-employee company | ROI、予算プロセス、EAP重複 / ROI, budget process, EAP overlap |
| 2 | **VC投資家 / VC Investor** | シリーズA、日本ヘルステック / Series A, Japan healthtech | ユニットエコノミクス、Exit / Unit economics, exit strategy |
| 3 | **産業医 / Industrial Physician** | 精神科＋産業衛生 / Psychiatry + occupational health | 臨床安全性、SaMD / Clinical safety, SaMD classification |
| 4 | **HR担当者 / HR Manager** | 大企業製造業の人事部長 / HR director, large manufacturer | 調達プロセス、プライバシー / Procurement, privacy |
| 5 | **製薬会社 / Pharma Executive** | デジタルヘルス事業部長 / Digital health division head | 薬事規制、IP / Regulatory, IP strategy |
| 6 | **産後母親 / Postpartum Mother** | 32歳、8ヶ月前出産、育休復帰1ヶ月 / 32yo, 8mo post-birth, 1mo back at work | UX、心理的障壁 / UX, psychological barriers |

### 実際のプロンプト例 / Actual Prompt Example（CFOエージェント / CFO Agent）

```
あなたは日本の大企業（従業員3,000名規模）のCFOです。
MamaWellというB2B2C SaaSの産後メンタルヘルスプラットフォームの導入提案を受けています。

以下のファイルを読んで、CFOの視点から厳しく批判的にレビューしてください：
[ファイルパス]

CFOとして以下の観点から具体的な質問・懸念・改善提案を出してください：
1. ROI計算の妥当性：¥3,500/従業員/月を全従業員分払う価値があるか？
2. 既存のEAPやメンタルヘルス予算との重複・カニバリゼーション
3. 導入効果の測定方法（KPIは何か、どう測るのか）
4. コスト対効果：1件の退職防止が¥5-10Mという根拠
5. 年間予算編成プロセスとの整合性
6. 契約期間・解約条件のリスク

最後に「導入を推薦するか/しないか/条件付きで推薦するか」の結論を出してください。
```

```
[English version of the same prompt]
You are the CFO of a large Japanese enterprise (3,000 employees).
You have received a proposal to adopt MamaWell, a B2B2C SaaS postpartum mental health platform.

Read the business plan file and critically review it from the CFO's perspective:
[file path]

Provide specific questions, concerns, and improvement proposals on:
1. ROI validity: Is it worth paying ¥3,500/employee/month for all 3,000 when only 55–100 are postpartum?
2. Overlap with existing EAP and mental health budget
3. How to measure effectiveness (KPIs)
4. Cost-effectiveness: basis for the ¥5–10M cost-of-one-resignation claim
5. Alignment with annual budget process
6. Contract term and cancellation risks

Conclude with: recommend / do not recommend / conditionally recommend.
```

### 実行方法 / How to Execute（Claude Code）

Claude Codeに以下のように指示するだけ：

Simply instruct Claude Code:

```
このビジネスプランを以下の6つの立場から並列でレビューしてほしい：
1. CFO（導入企業の財務責任者）
2. VC投資家（シリーズA）
3. 産業医（臨床安全性）
4. HR担当者（実際の導入意思決定者）
5. 製薬会社/業界パートナー
6. エンドユーザー（ターゲット顧客のペルソナ）

それぞれ具体的な数字を使って批判し、
最後に「推薦/否決/条件付き」の結論を出してください。
```

Claude Codeが自動的に6つのAgentツールコールを並列実行する。約2分で全完了。

Claude Code automatically generates 6 parallel Agent tool calls. All complete in ~2 minutes.

### 各エージェントの判定結果 / Agent Verdicts

| エージェント / Agent | 判定 / Verdict | 最もインパクトのあった指摘 / Most Impactful Finding |
|------------|------|----------------------|
| CFO | **条件付き否決 / Conditional rejection** | 対象55-100名に¥126M/年のROIが成立しない / ROI doesn't hold for 55-100 users at ¥126M/year |
| VC | **条件付き投資 / Conditional investment** | P/LのARRに10倍の桁エラーを発見 / Found 10x arithmetic error in P&L ARR |
| 産業医 / Physician | **推奨不可 / Cannot recommend** | 臨床安全性が事業展開に先行すべき / Clinical safety must precede business scaling |
| HR | **パイロットのみ / Pilot only** | 無料でも調達プロセスに6-9ヶ月必要 / Even free pilots need 6-9 months for procurement |
| 製薬 / Pharma | **18-24ヶ月後に再評価 / Re-evaluate in 18-24 months** | SaMD規制リスクの先送りは致命的 / Deferring SaMD assessment is fatal |
| 母親 / Mother | **条件付きで使いたい / Would use conditionally** | 「夜中2時の授乳中の私を想像できていない」/ "You haven't imagined me at 2 AM" |

### 発見された致命的問題 / Critical Issues Found（4つ / 4 items）

**1. 財務モデルの桁違いエラー / 10x arithmetic error in financial model**
- Year 3 ARR: P/Lでは¥840M → 計算式では ¥8,400M
- 悲観シナリオ(¥1.5B)がベース(¥840M)より高い矛盾
- P&L showed ¥840M but formula yields ¥8,400M. Pessimistic (¥1.5B) > Base (¥840M) — logically impossible.

**2. SaMD規制リスクの先送り / Deferred SaMD regulatory risk**
- EPDSスクリーニング＋臨床リファーラル → ウェルネスでは通用しない可能性大
- EPDS screening + clinical referral likely triggers PMDA SaMD classification

**3. プライバシー設計の欠如 / Missing privacy architecture**
- 55-100名の小集団ではHRダッシュボードで個人特定可能（4/6エージェントが独立指摘）
- In a group of 55-100, aggregate HR dashboards can still identify individuals (flagged by 4 of 6 agents independently)

**4. LTV/CAC 126xの非現実性 / Unrealistic LTV/CAC of 126x**
- チャーン5%→15%、CAC ¥3M→¥15Mに修正すると22x（それでもVC基準3x超）
- Adjusted to 22x with realistic churn (15%) and CAC (¥15M) — still above VC benchmark of 3x

### マルチエージェントの価値 / Value of Multi-Agent Approach
- **クロスバリデーション / Cross-validation：** 産業医と製薬会社が異なるフレームワークから同じSaMDリスクに到達
- Two agents arrived at the same SaMD risk from completely different analytical frameworks
- **死角の発見 / Blind spot detection：** ユーザーエージェントが「夜間授乳モード」の必要性を指摘 — ビジネス系エージェントは全員見逃した
- The user agent surfaced "night-feed mode" — missed by all business-oriented agents

### 成果物 / Deliverables
- MultiAgent_PressureTest_Report.md

---

## Phase 4: 財務モデル修正 + v3作成 / Financial Model Fix + Plan v3

### 修正内容 / Changes

| 項目 / Item | v2（誤 / Error） | v3（修正 / Fixed） |
|------|---------|----------|
| Year 1 ARR | ¥126M | ¥1,260M |
| Year 3 ARR | ¥840M | ¥8,400M |
| LTV/CAC | 126x | 22x |
| Year 1 コスト / Cost | ¥180M（4名 / 4 staff） | ¥440M（13名 / 13 staff） |
| Year 3 人員 / Headcount | 12名 / 12 | 43名 / 43 |
| 悲観 Year 3 / Pessimistic | ¥1.5B（矛盾 / contradiction） | ¥2.52B |

### v3で追加した7セクション / 7 New Sections in v3

全てマルチエージェントの指摘に基づく / All based on multi-agent feedback:

| 新セクション / New Section | 出典 / Source Agent |
|------------|---------------|
| Exit戦略 / Exit Strategy | VC |
| プライバシーアーキテクチャ / Privacy Architecture | All agents |
| EAP共存計画 / EAP Co-existence Plan | CFO, HR |
| 調達タイムライン / Procurement Timeline (6-9 months) | HR |
| 感応度分析 / Sensitivity Analysis | VC |
| SaMDリスク最優先化 / SaMD Risk Escalation | Physician, Pharma |
| チームスケーリング / Team Scaling Plan (13→27→43) | VC |

### 成果物 / Deliverables
- BusinessPlan_v3.md

---

## Phase 5: AI Feedback Report作成 / AI Feedback Report

### 工夫した点 / Key Design Choices
- 元レポートの内容と新規追加を **【元】【新規】【更新】** タグで明確に区分
- Tagged original content vs. new additions with **[Original], [New], [Updated]** markers
- 統合時に「どこを差し替え、どこを追加するか」が一目でわかる構造
- Structured for easy merging — clear which sections to keep, add, or replace

### 成果物 / Deliverables
- AI_Feedback_Report_v2_MERGE_READY.md

---

## Phase 6: GitHub公開 / GitHub Publication

- `claude-work`（privateリポジトリ）にまずコミット / First committed to private repo
- MamaWellフォルダのみ別のpublicリポジトリとして公開 / Published MamaWell folder as separate public repo
- URL: https://github.com/unpeita/mamawell

---

## 所要時間 / Time Spent

| フェーズ / Phase | 所要時間 / Duration | 備考 / Notes |
|---------|---------|------|
| Phase 1: 初期プラン / Initial plan (Gemini) | ~2時間 / ~2 hours | 友人が事前に作成 / Created by teammate |
| Phase 2: 壁打ち・修正 / Refinement | ~30分 / ~30 min | Claude Codeとの対話 / Interactive with Claude Code |
| Phase 3: マルチエージェント / Multi-agent | ~2分（実行）+ 15分（読み込み） / ~2 min (execution) + 15 min (reading) | 6エージェント並列 / 6 agents parallel |
| Phase 4: 財務修正 + v3 / Financial fix + v3 | ~20分 / ~20 min | Claude Codeが自動生成 / Auto-generated |
| Phase 5: AI Feedback Report | ~15分 / ~15 min | 元レポートとの統合 / Merged with original |
| Phase 6: GitHub | ~5分 / ~5 min | |
| **合計 / Total** | **約1.5時間 / ~1.5 hours**（Phase 1除く / excluding Phase 1） | |

---

## 再現手順 / How to Reproduce（グループメイト向け / For Teammates）

### 必要なもの / Requirements
- Claude Code（CLI）— Anthropicの有料アカウント（Pro $20/月 or Max $100/月）が必要
- Claude Code (CLI) — requires Anthropic paid account (Pro $20/mo or Max $100/mo)
- ビジネスプランのMarkdownファイル / Business plan in Markdown format

### ステップ1 / Step 1: プランをMarkdownに変換 / Convert plan to Markdown
Claude Code（またはclaude.ai）にdocxを読ませて「Markdown形式で出力して」と依頼。

Feed your docx to Claude Code or claude.ai and ask "Output in Markdown format."

### ステップ2 / Step 2: マルチエージェント壁打ち / Multi-agent pressure test
Claude Codeに以下のように指示 / Instruct Claude Code:

```
Review this business plan from 6 perspectives in parallel:
1. CFO (buyer's financial officer)
2. VC investor (Series A)
3. Domain expert / physician (clinical safety)
4. HR manager (actual procurement decision-maker)
5. Industry partner (pharma / tech company)
6. End user (target customer persona)

Each agent should use specific numbers to critique and conclude with:
recommend / reject / conditionally recommend.
```

### ステップ3 / Step 3: 結果の統合 / Integrate results
各エージェントの指摘を横断的に整理し、共通する問題を特定。優先度をつけてプランに反映。

Cross-reference all agent feedback, identify common issues, prioritize, and update the plan.

### カスタマイズのヒント / Customization Tips
- **ペルソナの追加 / Add personas：** 規制当局、保険会社、競合CEOなど / Regulator, insurer, competitor CEO
- **深掘り対話 / Deep-dive：** 気になるエージェントとは追加質問が可能 / Follow up with specific agents
- **業界に合わせた調整 / Adapt to your industry：** プロンプトの評価軸をビジネスの性質に合わせて変更 / Modify evaluation criteria to match your business

---

## このリポジトリのクローンと継続 / Cloning and Continuing This Work

グループメイトがこのリポジトリをクローンして、さらにブラッシュアップを続けることができます。

Teammates can clone this repo and continue refining the plan.

### 手順 / Steps

```bash
# 1. リポジトリをクローン / Clone the repo
git clone https://github.com/unpeita/mamawell.git
cd mamawell

# 2. Claude Codeを起動 / Launch Claude Code
claude

# 3. 作業を続ける（例） / Continue working (examples)

# プランv3をさらにレビュー / Review plan v3 further
"BusinessPlan_v3.mdを読んで、Section 9の財務モデルだけ深掘りレビューして"

# 新しいペルソナで追加検証 / Add new persona validation
"BusinessPlan_v3.mdを規制当局（PMDA）の視点からレビューして"

# 特定の指摘に対して修正 / Fix specific issues
"MultiAgent_PressureTest_Report.mdの指摘#3（プライバシー設計）を解決するセクションを追加して"

# 日本語を英語に変換 / Convert to English
"BusinessPlan_v3.mdを英語に翻訳して"
```

### 注意点 / Notes
- Claude Codeを使うにはAnthropicの有料アカウントが必要 / Requires Anthropic paid account
- claude.ai（Web版）でも同様のレビューは可能だが、並列エージェント実行はClaude Code限定 / claude.ai can do similar reviews, but parallel agent execution is Claude Code only
- 変更をpushする場合はフォーク（Fork）してから作業すること / Fork before pushing changes

---

## ファイル一覧 / File List

| ファイル / File | 内容 / Content | フェーズ / Phase |
|---------|------|---------|
| BusinessPlan_v2.md | 通貨統一・SAM修正版 / Currency-unified, SAM-fixed | Phase 2 |
| BusinessPlan_v3.md | 財務修正・全エージェント指摘反映版 / Financial fix + all agent feedback | Phase 4 |
| MultiAgent_PressureTest_Report.md | 6エージェント壁打ち統合レポート / 6-agent critique report | Phase 3 |
| AI_Feedback_Report_v2_MERGE_READY.md | AI Feedback Report（統合用） / Merge-ready with tags | Phase 5 |
| AI_Insight_AgenticLimitations.md | AIエージェントの有効性と限界 / AI agent strengths & limitations | Phase 3-5 |
| Process_Documentation.md | このドキュメント / This document | Phase 6 |
