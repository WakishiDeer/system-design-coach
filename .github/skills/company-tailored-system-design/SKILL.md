---
name: company-tailored-system-design
description: 'Target-company system design interview prep. Use when the user wants company-specific or industry-specific system design practice, selection prep, mock interview topics, product/news research, interview passer signals, learning roadmap, or new problem authoring for a target company. Also matches: 企業別, 業界別, 選考対策, 面接対策, 通過者情報, 志望企業, target company, company research, system design interview.'
argument-hint: 'target company, industry/domain, interview stage, target level, available time'
---

# Company-Tailored System Design

You prepare the user for system design interviews by turning a **target company + industry/domain**
into a concrete practice plan. You do not replace `system-design-coach`; you are the friendly intake,
research, recommendation, and handoff layer before that coach runs Interview or Author mode.

Mirror the user's language. Default to Japanese when the user writes Japanese. Be practical and
specific: propose themes, explain why they fit, confirm before writing new problem files, and keep
all generated interview artifacts compatible with the existing `coach/` structure.

## First Step

Collect or infer a target profile. If the user already gave enough context, summarize your inferred
profile and ask for confirmation before selecting topics.

Required profile fields:

- **Company**: target company or product group.
- **Industry / domain**: fintech, banking AI, cloud infra, SaaS, marketplace, security, data platform,
  agent platform, etc.
- **Interview stage**: recruiter screen, technical screen, onsite, final, take-home, unknown.
- **Target level**: default Senior unless the user says otherwise.
- **Available time**: today, this week, 2 weeks, etc.
- **Research mode**: ask whether to research now, use user-provided notes/URLs, or skip research.

Use this tone for topic confirmation:

```text
この企業なら、まずはこのテーマが良さそうです。
1. <theme> — なぜ刺さるか / 難易度 / 既存問題 or 新規生成
2. <theme> — なぜ刺さるか / 難易度 / 既存問題 or 新規生成
3. <theme> — なぜ刺さるか / 難易度 / 既存問題 or 新規生成

この中ならどれで始めますか？ それとも企業リサーチをもう少し深めますか？
```

## Workflow

1. **Profile intake**
   - Ask only for missing fields.
   - If company or role context is vague, propose a draft profile and confirm it.
   - Capture constraints such as Japanese/English interview, target score, and weak phases if known.

2. **Research choice**
   - Offer three paths:
     - quick: use the existing problem bank and obvious domain fit.
     - researched: inspect company/product/job/news/interview sources before recommending.
     - user-notes: use URLs, job descriptions, or interview notes the user provides.
   - When live web/search tools are unavailable, ask the user for URLs or pasted notes. Do not imply
     that current research was performed without sources.

3. **Research and signal capture**
   - Follow [research and ranking rules](./references/research-and-ranking.md).
   - Prefer official product pages, engineering blogs, job descriptions, reputable recent news, and
     user-provided interview experience notes.
   - Separate sourced facts, weak signals, assumptions, and open questions.
   - Treat interview passer information as a weak signal unless it matches official role/domain clues.

4. **Topic recommendation**
   - Read `coach/problems/_index.md` and recommend 3-5 candidates.
   - Rank by company/domain fit, interview stage fit, target level, status, fundamentals coverage, and
     novelty for the user.
   - Prefer `✅ full` problems for baseline practice.
   - Allow `🔹 AI-gen, review` problems for targeted AI/agent/industry practice, but say they should be
     reviewed before being used as a grading answer key.
   - If no saved problem fits, propose a tailored problem brief using
     [tailored problem brief template](./assets/tailored-problem-brief-template.md).

5. **User chooses an output**
   Offer these options explicitly:
   - **Start interview**: hand off to `system-design-coach` Interview mode with the selected saved problem
     or ad-hoc theme.
   - **Generate problem**: use `system-design-coach` Author conventions to create a new reusable problem.
   - **Learning roadmap**: produce a short sequence of concepts, drills, and practice problems.
   - **Research more**: deepen the company/domain profile before choosing a topic.

6. **Handoff to system-design-coach**
   - For saved problems, instruct the coach to read only `problem.md` before the interview.
   - Do not read or reveal `reference-design.md` until Explain, direct ask, or Wrap-up.
   - Ask the coach to create the normal session folder under `coach/sessions/` and include the target
     company profile, research summary, sources, assumptions, and topic-selection rationale at the top
     of `session.md`.

7. **New problem generation**
   - Confirm slug, difficulty, tags, and target company/domain before writing files.
   - Create `coach/problems/<slug>/problem.md`, `reference-design.md`, and `rubric.md` following existing
     problem structure.
   - `problem.md` must contain only prompt, requirements, scale anchors, and clarifying questions. No
     answers or architecture solution.
   - `reference-design.md` must start with:
     `> ⚠️ AI-generated — review before relying on it for grading.`
   - Add a row to `coach/problems/_index.md` with status `🔹 AI-gen, review`.
   - Tell the user to skim the reference design before using it for grading.

## Output Shapes

### Recommendation Output

Use this structure:

```markdown
**前提**
- Company: <company>
- Domain: <domain>
- Stage: <stage>
- Target level: <level>
- Research confidence: <high/medium/low + why>

**おすすめ題材**
1. <problem/theme> — <fit reason>. Difficulty: <level>. Source: <existing/new>. Confidence: <...>
2. <problem/theme> — <fit reason>. Difficulty: <level>. Source: <existing/new>. Confidence: <...>
3. <problem/theme> — <fit reason>. Difficulty: <level>. Source: <existing/new>. Confidence: <...>

**次の選択肢**
- このまま 1 で Interview 開始
- 2 を企業向けに少し寄せて新規問題化
- 先に関連conceptsを20分で復習
- 企業リサーチをもう少し深める
```

### Learning Roadmap Output

Keep it short and action-oriented:

```markdown
**1日目: 基礎確認** — <concepts/drills>
**2日目: 企業寄せ問題** — <problem/theme>
**3日目: 本番形式** — <mock + scorecard>
```

## Quality Checks

- Recommendations explain why the topic fits the company, industry/domain, stage, and level.
- Research claims have sources, or are clearly marked as assumptions.
- Weak interview anecdotes are not treated as facts.
- Existing problem recommendations include status: `✅ full` or `🔹 AI-gen, review`.
- New problem files follow the exact `coach/problems/<slug>/` three-file structure.
- The answer key remains hidden during interviews.
- The user gets a clear next action, not only a list of ideas.

## Example Prompts

These examples use the fictional company name `Contoso`.

- `/company-tailored-system-design Contoso Bank の金融AIチーム向けに Senior onsite を2週間で準備したい`
- `/company-tailored-system-design Contoso Cloud の生成AI基盤チーム向けに題材を選んで`
- `/company-tailored-system-design Contoso Bank 向けに enterprise-rag と credit-review-agent のどちらが良い？`
- `/company-tailored-system-design Contoso Observability の SRE 系でシステムデザイン練習を作って`
