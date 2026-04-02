# AI Feedback Report: MamaWell

**Prof. Gunter J. Hitsch | Booth School of Business | March 2026**

> **統合ガイド（提出前に削除）**
> - 【元】= 元レポート（Claude Sonnet 4.6 via claude.ai で作成済み）の内容
> - 【新規】= 今回のClaude Code (Opus 4.6) マルチエージェント壁打ちで追加された内容
> - 【更新】= 元レポートの記述を今回の結果で修正・補強した内容
> - 統合時：【元】はそのまま維持、【新規】を追加、【更新】は元の記述を差し替え

---

## 1. Where Was AI Helpful?

AI contributed significantly across the following areas:

### 【元】Initial Plan Development (Claude Sonnet 4.6 via claude.ai)

1. **Market & competitive research:** Claude ran multi-source web searches (English + Japanese) to identify competitors (Lyra Health, Intellect Japan, Seven Starling, emol, Awarefy), surface market size data (IMARC: Japan mental health market USD 26.5B in 2024, CAGR 18.5% for digital), and validate VC funding trends favoring B2B2C models over D2C.

2. **Plan structure:** Starting from a concept memo, Claude restructured the full 10-section plan, maintaining consistency of assumptions across Market Opportunity, Business Model, and Financial Projections throughout iterative revisions.

3. **Strategic pivot:** When peer feedback challenged LTV, CAC, and solution reproducibility, Claude diagnosed each concern, proposed the B2B2C employer-paid model as the resolution, and rebuilt the affected sections coherently in a single session.

4. **Financial modeling:** Claude built a three-scenario P&L (optimistic / base / pessimistic) with ARR, operating profit, and break-even timing. When physician supervisor costs (¥5M/physician) were added, it recalculated all figures instantly.

5. **VC pressure-testing:** Claude simulated a skeptical investor, challenging assumptions on solution reproducibility, enterprise WTP, team diversity, and postpartum VC precedent — directly shaping the Risks and Open Questions sections.

6. **English writing & document production:** The full plan was written in professional MBA-level English from Japanese inputs, and exported as a formatted Word document (.docx) with tables, color coding, and consistent styling.

### 【新規】Multi-Agent Pressure Testing (Claude Code Opus 4.6)

7. **Cross-stakeholder validation via parallel agents:** Using Claude Code's Agent tool, we launched 6 specialized agents simultaneously — each assigned a distinct stakeholder persona (CFO, VC investor, industrial physician, HR manager, pharma executive, postpartum mother). Each agent independently read the full business plan and produced a critique from its assigned perspective. This parallel execution took approximately 2 minutes for all 6 agents, compared to the hours it would take to consult 6 actual domain experts.

8. **Financial model error detection:** The VC agent discovered a critical arithmetic inconsistency: the P&L showed Year 3 ARR of ¥840M, but the formula (50 clients × 4,000 employees × ¥3,500 × 12) yields ¥8.4B — a 10x discrepancy. It also caught that the pessimistic scenario (¥1.5B) was higher than the base case (¥840M), which is logically impossible. These errors had survived multiple rounds of human review.

9. **Assumption stress-testing with quantified alternatives:** The VC agent recalculated LTV/CAC using more conservative assumptions (churn 15% instead of 5%, CAC ¥15M instead of ¥3M), reducing the ratio from 126x to 22x — still above the VC benchmark of 3x, but far more defensible. This kind of rapid sensitivity analysis across multiple variables is where AI excels.

10. **Regulatory risk identification:** The industrial physician and pharma agents independently flagged SaMD (Software as a Medical Device) regulatory risk — a critical issue that had been deferred to "Year 3 reassessment" in the original plan. Both agents argued that EPDS screening + clinical referral functionality likely triggers PMDA classification requirements, and that delaying this assessment creates legal liability from Day 1. This cross-validation between two domain-specific agents strengthened the urgency of the finding.

11. **User experience gap analysis:** The postpartum mother agent provided insights that no business-oriented review would surface — such as the psychological resistance to receiving a "postpartum depression app" from one's employer, the impossibility of using the app during night feeds without single-hand/dark-mode/offline capability, and the need for partner support features. The insight that "the plan is optimized for investors and HR, not for the woman at 2 AM" became a key design revision driver.

---

## 2. Did You Use Agentic AI?

### 【元】Emergent Agentic Behavior (Claude Sonnet 4.6)

In the initial plan development phase, we did not configure a formal agentic workflow, but multi-step autonomous sequences emerged naturally. Three examples: (1) given a single prompt to research competitors, Claude searched, filtered, synthesized, and generated a positioning map and comparison table unprompted; (2) asked to build a TAM/SAM/SOM section, it searched multiple sources, cross-validated figures, and fed results directly into the financial model; (3) given raw peer feedback in Japanese, it parsed the concerns, proposed the B2B2C pivot, and rebuilt relevant sections — all in one continuous workflow. Agentic behavior was most effective when full context (original plan + feedback) was provided upfront with a clear directive.

### 【新規】Deliberate Multi-Agent Workflow (Claude Code Opus 4.6)

In the refinement phase, we designed and executed a formal agentic workflow using Claude Code's Agent tool:

**Setup:**
- Tool: Claude Code (CLI), powered by Claude Opus 4.6 with 1M context window
- Method: 6 sub-agents launched in parallel via the Agent tool, each with a distinct system prompt defining their persona, expertise, and evaluation criteria
- Input: Each agent received the full business plan (BusinessPlan_v2.md) and a structured review prompt

**Agent Configuration:**

| Agent | Persona | Key Review Focus |
|-------|---------|-----------------|
| Agent 1 | CFO of a 3,000-employee Japanese enterprise | ROI justification, budget process, EAP overlap |
| Agent 2 | Series A VC investor (Japan healthtech) | Unit economics, team scalability, exit strategy |
| Agent 3 | Industrial physician (psychiatry + occupational health) | Clinical safety, SaMD classification, liability |
| Agent 4 | HR manager (large Japanese manufacturer) | Procurement reality, privacy concerns, employee fairness |
| Agent 5 | Pharma digital health executive (DTx/SaMD experience) | Regulatory pathway, IP strategy, partnership potential |
| Agent 6 | Postpartum mother (8 months post-birth, just returned to work) | UX feasibility, psychological barriers, real-world usability |

**Prompt example (Agent 1 — CFO):**
> "You are the CFO of a large Japanese enterprise with 3,000 employees. You have received a proposal to adopt MamaWell. Read the business plan and critically review it from the following perspectives: (1) ROI calculation validity — is it worth paying ¥3,500/employee/month for all 3,000 employees when only 55–100 are postpartum-eligible? (2) Overlap with existing EAP... [7 specific review criteria]. Conclude with: recommend / do not recommend / conditionally recommend."

**Results:**
- All 6 agents completed their reviews in ~2 minutes (parallel execution)
- Each produced 1,500–3,000 word structured critiques with specific numerical analysis
- 4 critical issues were identified that had survived all prior human and single-AI review rounds
- All 6 agents independently reached "conditional" verdicts — none gave unconditional approval, but none rejected the core business idea
- The integrated report identified 17 specific issues, prioritized into Must Fix (4), Should Fix (8), and Nice to Have (5)

**Key agentic advantage:** The value was not in any single agent's output, but in the **cross-validation pattern** — when 4 out of 6 agents independently flagged the same privacy concern, or when the pharma agent and industrial physician agent converged on the same SaMD regulatory risk from completely different analytical frameworks, the finding carried far more weight than a single review.

---

## 3. Where Was AI Not Helpful?

### 【元】Original Limitations (unchanged — these remain valid)

The most important limitation: AI cannot originate the emotional foundation of the idea. The conviction that postpartum mothers are silently suffering — that the system is designed around the baby while the mother disappears — came from lived experience and personal motivation, not from a prompt. Investors evaluate founders as much as plans; the answer to "why you?" cannot be generated by AI.

Two further limitations: (1) market figures required independent verification — some estimates (e.g. the ¥1.2T productivity loss anchor) were plausible but not directly citable; (2) Japan-specific nuances (ringi approval process, industrial physician influence, Kenkou Keiei mechanics) were surface-level and required team judgment to sharpen.

### 【新規】Additional Limitations Discovered Through Multi-Agent Testing

3. **AI produces high-quality QA, not competitive advantage.** The multi-agent pressure test dramatically improved plan quality — catching arithmetic errors, identifying regulatory gaps, strengthening assumptions. However, every team in this class has access to the same AI tools. The same prompt structure could generate the same caliber of critique for any business plan. **AI is a quality equalizer, not a differentiator.** The competitive advantage of a startup still comes from human insight, domain expertise, and founder conviction — none of which AI can generate.

4. **Simulated personas are useful but not real.** The "postpartum mother" agent produced remarkably empathetic and specific feedback (night-feed mode, dark UI, partner support). But it was drawing from training data about postpartum experiences, not from lived experience. Its suggestions were directionally correct but lacked the raw, unfiltered truth that comes from actual user interviews. For example, the agent suggested "softer language" — a real mother might say something far more specific and unexpected about what language actually triggers shame.

5. **AI agents agree too much with each other.** All 6 agents reached "conditional" verdicts. None said "this is a terrible idea, don't do it." While the plan may genuinely have merit, there is a risk that AI agents are structurally biased toward diplomatic hedging. A real CFO might simply say "no" without conditions. A real VC might not return the call. AI lacks the brutal selectivity of real market feedback.

6. **Numerical validation still requires human judgment.** The VC agent caught the 10x ARR error — but it also produced its own questionable numbers without flagging uncertainty. For instance, it stated "Japanese HRtech churn is 15–25%" without citing a source. AI is good at checking internal consistency but can introduce new unverified assumptions in the process of correcting old ones.

---

## 4. Which AI(s) Did You Use?

### 【更新】（元の記述を拡張）

| Phase | Tool | Model | Usage |
|-------|------|-------|-------|
| Plan development (Phase 1) | Claude.ai (web) | Claude Sonnet 4.6 | All research, writing, financial modeling, document production. Single extended session (~4–5 hours). |
| Plan refinement (Phase 2) | Gemini (web) | Gemini | SAM assumption chain validation, defensible postpartum user estimate (55–100 per company), currency inconsistency review (¥/£ mixed). |
| Multi-agent pressure test (Phase 3) | Claude Code (CLI) | Claude Opus 4.6 (1M context) | 6 parallel sub-agents for stakeholder simulation. Financial model correction. Plan v3 creation with all feedback integrated. |

**Workflow across tools:**
- Phase 1 (Claude.ai): Generated the initial business plan from concept to structured 10-section document
- Phase 2 (Gemini): Challenged key assumptions; produced the "defensible assumption chain" that corrected the SAM user count from 900 to 55–100 per company; identified ¥/£ currency mixing across 25 locations
- Phase 3 (Claude Code): Executed the formal multi-agent agentic workflow; corrected the 10x financial model error; integrated all stakeholder feedback into Plan v3 with 7 new sections (Exit strategy, Privacy architecture, EAP co-existence, Procurement timeline, Sensitivity analysis, SaMD risk escalation, Team scaling plan)

**Key insight on multi-tool workflow:** Each AI tool had distinct strengths. Claude.ai excelled at long-form document creation; Gemini was effective at challenging assumptions with concrete counter-evidence; Claude Code's Agent tool enabled the parallel multi-stakeholder simulation that no single-threaded AI conversation could replicate. The combination was more powerful than any single tool alone.

---

> **統合作業メモ（提出前に削除）**
>
> ### 元レポートからの変更点サマリー
>
> | セクション | 元レポート | 変更内容 |
> |-----------|----------|---------|
> | 1. Where Helpful | 6項目 | +5項目追加（#7-11: マルチエージェント関連） |
> | 2. Agentic AI | 「正式なワークフローは未実施」 | 新規セクション追加：6エージェント並列実行の詳細 |
> | 3. Not Helpful | 3つの限界 | +4つ追加（#3-6: AI品質均等化、ペルソナ限界、合意バイアス、数値検証） |
> | 4. Which AIs | Claude Sonnet 4.6のみ | Gemini + Claude Code Opus 4.6 を追加。3フェーズのワークフロー図 |
>
> ### 統合時の注意
> - 【元】セクションは元のdocxの文章をそのまま使う（英語表現を変えない）
> - 【新規】セクションはこのファイルの内容をそのまま追加
> - 【更新】セクションはこのファイルの内容で元の記述を置き換え
> - Section 1の#4（Financial modeling）で言及されている「LTV/CAC ~126x」は、Section 2の新規部分で「22xに修正」と記載済みなので矛盾しない（v1で126xを計算→v3で22xに修正、という時系列）
