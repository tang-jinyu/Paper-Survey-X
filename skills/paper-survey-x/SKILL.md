---
name: paper-survey-x
description: "Systematic tech/paper survey: layered retrieval of papers and open-source projects, per-item verification of links/venues/dates, and delivery of a nine-column Excel workbook with a reading guide, itemized methods/architectures/key ideas, warm light-pink styling, separate Chinese and Latin fonts, enlarged sheet titles, paper/project-specific link labels and all available figures embedded. Includes original figures from open-access PDFs, self-drawn diagrams, a landscape summary and a doubtful-citation list. Use for surveys, literature reviews, related work, technical research tables or open-source comparisons. Triggers: survey, literature review, related work, 调研, 文献综述, 调研表格."
---

# Paper Survey X（论文调研助手X）

Turn "survey topic X" into a quality-gated pipeline: layered retrieval → per-item verification → Excel table → figures → landscape summary.

## Confirm inputs first

Ask once (in a single message) if missing:

1. **Topic & scope**: direction, time range (default: foundational classics → current), exclusions;
2. **Purpose**: competition design / thesis proposal / tech selection — determines the "reuse points" column;
3. **Existing survey list**: titles already collected (for deduplication). Skip on a first-round survey.

## Workflow

### 0. Apply the delivery design standard

Before generating any workbook, diagram or document, read [references/design.md](references/design.md) and enforce it: reading guide, warm light-pink palette, three-level type hierarchy, separate Chinese/Latin fonts, named links, embedded figures, content-aware row heights, orthogonal diagram connectors and the final delivery checklist. Render the result for visual inspection; code-level checks alone are insufficient.

### 1. Layered retrieval

Search in multiple rounds, one per method-spectrum lead (adapt to the topic): classic methods, ML/RL methods, fuzzing/mutation methods, formal/semi-formal methods, latest LLM/Agent methods, surveys. Use both Chinese and English keywords; search open-source projects in a dedicated round (official releases first).

### 2. Per-item verification (red line)

Before any record enters the table:

- The paper really exists and the link is reachable (arXiv / IEEE Xplore / ACM DL / USENIX / DOI);
- Venue and year are cross-checked (when arXiv date ≠ publication date, note both);
- Open-source entries include repo link, LICENSE and maintenance status; repos without a license must be marked "no LICENSE — do not copy code".

**Rather collect less than fabricate.** Unverifiable records never enter the table; they go to a "doubtful citations" list with the checking process described. A wrong link/venue/year is worse than a missing entry — this is the skill's highest discipline.

### 3. Build the Excel workbook

Default sheet order: 「阅读指南」「论文」「开源项目」「图形类」; add landscape/conclusions, sources and doubtful-citation sheets as needed. The two main sheets use nine columns; see [references/schema.md](references/schema.md):

`论文题目 | 中文名称 | 链接 | 发表会议/期刊 | 发表时间 | 主要方法 | 架构 | 核心思想 | 对本工程可借鉴点`

- **「主要方法」「架构」「核心思想」 must be itemized** (3–6 bullets each in-cell; 2–4 for 核心思想) — one-sentence summaries are forbidden;
- "Reuse points" must land on a concrete module/problem of the user's project — no filler;
- The reading guide contains counts, clickable navigation, a recommended reading order and usage cautions;
- Data sheets use an independent 14pt title in row 1, scope note in row 2, 11pt column headers in row 3 and 10pt body text from row 4; freeze `A4`;
- Apply warm light-pink styling. Use SimSun for Chinese and Times New Roman for English/numbers; for mixed cells, set fonts separately with rich-text runs (`CellRichText + TextBlock + InlineFont` in openpyxl);
- Link labels must be the specific paper/project name, never generic labels such as “官方页面”, “代码仓库” or “查看链接”. After inserting title rows, rebind hyperlinks from the original records and compare every label, target URL and source item;
- Use a human-readable Chinese filename and save to the workspace output directory;
- Run spreadsheet validation when available, then render the reading guide, a main-table page and a figure page to check clipping, overflow and page breaks.

### 4. Figures (per paper)

See [references/figures.md](references/figures.md):

1. **Original architecture figure**: extract only from open-access PDFs (arXiv / author page / open repo). No full-text access → mark "not extracted (no full-text access)". Never fabricate an "original" figure;
2. **Self-drawn diagram**: after reading the method, redraw the pipeline in plain, beginner-friendly language (matplotlib), fully annotated;
3. **Key result figures**: extract the final result figure/table and the related-work comparison figure/table (if any); mark "no comparison in paper" when absent.

Save full-resolution images to `<survey-name>_figures/` and add the 「图形类」 sheet (paper | figure type | file path/not-extracted note | one-line note | embedded image). **Every available image must be embedded in the workbook, not merely linked by path.** Preserve aspect ratio, fit row height to the complete image, and verify that source-image count equals embedded-image count after saving. The figures directory remains the high-resolution companion.

### 5. Summary (in the delivery reply)

- Landscape: method tiers, current strongest route;
- 3–5 findings most relevant to the user's project, with reasons;
- Overlap warning: new works closest to the user's narrative that need differentiation;
- Doubtful-citation list: process and verdicts;
- Dedup note: titles excluded as duplicates.

## Iteration

For "deep-dive these N papers" follow-ups, reuse the verified links and output structure the user specifies; afterwards correct the table links to the final verified versions and add check marks, keeping the table the single source of verified truth.
