---
name: ppt-viz
description: "Transform PPT slide content into structured, presentation-ready AI visual prompts using design heuristics. Use when the user says ppt-viz or PPT设计, asks to turn PPT page content into visual prompts, asks whether a page needs a chart or structure, asks for PPT visual design judgment, or asks for a full deck / slide deck / presentation deck with consistent style, visual consistency, batch slide prompts, deck visual system, 整套PPT, 一套PPT, 统一视觉风格, 批量生成PPT页面, or 整套PPT风格一致性模式."
metadata:
  version: 1.2.0
---

# ppt-viz

## Purpose

Use this skill to transform PPT slide or full-deck content into structured, presentation-ready visual generation prompts. The skill does not create slides, images, or PPTX files. It analyzes the user's content, applies design heuristics, clarifies missing design intent through a short multi-turn dialogue, chooses justified chart or visual structures, loads style presets, and outputs copy-ready visual prompts.

## Trigger

Use this skill whenever the user asks to:

- use PPT设计 or ppt-viz
- turn PPT page content into a visual prompt
- design a slide image prompt
- generate PPT画面提示词
- decide whether a page needs a chart
- convert slide copy, page briefs, outlines, data summaries, or timeline content into AI image prompts
- create prompts for PowerPoint, Keynote, Figma, AI PPT tools, Midjourney, GPT Image, or similar visual generation tools
- create prompts for a full deck, slide deck, presentation deck, or multiple slides
- keep several pages in a consistent style, unified visual language, or deck visual system
- generate prompts for 整套PPT, 一套PPT, 整套方案, 整套发布会PPT, 整套汇报材料, 商业计划书, 融资计划书, 产品发布会, 解决方案PPT, 批量生成PPT页面, or 统一视觉风格
- apply PPT visual design judgment, design heuristics, readability rules, color semantics, chart selection rules, page-type matching, or style-fit advice

## Workflow Modes

Route the request before generating prompts.

```yaml
- mode: single-slide
  name: 单页 PPT 视觉提示词模式
- mode: deck-consistency
  name: 整套 PPT 风格一致性模式
```

Use `deck-consistency` when the user asks for a full deck, slide deck, presentation deck, consistent style, visual consistency, generate prompts for multiple slides, batch slide prompts, deck visual system, 帮我做一整套 PPT, 帮我生成一套 PPT 提示词, 这几页保持同一风格, 帮我为 10 页 PPT 生成统一风格 prompt, 整套方案保持一致, 批量生成 PPT 页面, 帮我规划整套 deck, 统一视觉风格, 整套发布会 PPT, 整套汇报材料, or 一套商业计划书 / 融资计划书 / 产品发布会 / 解决方案 PPT.

In `deck-consistency`, do not directly generate isolated page prompts. First establish the Deck Visual System, then plan page structures, then generate per-slide prompts under that unified system.

## Design Heuristics / 设计经验规则库

Before generating final prompts in any workflow mode, read and apply `references/design-heuristics.md`.

Use the heuristics to decide:

- whether the current style fits the scene
- whether color semantics are correct
- whether content density is too high
- whether the page needs a chart, structure diagram, cards, or a visual metaphor
- whether brand/style rules are violated
- whether finished-image text is appropriate
- whether content should be split into more slides
- whether a full deck remains visually consistent

If heuristics reveal a conflict, proactively tell the user and provide a better option. Examples: recommend white consulting style for dense text instead of dark launch style, recommend background-only prompts for Chinese-heavy finished images, split overloaded content into multiple slides, or avoid statistical charts when there is no real data relationship.

## Output Language

Output language follows user language.

- Use Chinese section titles for Chinese conversations.
- Use English section titles only when the user writes in English.

## Default Assumptions

Use these defaults only when the user asks to directly generate or does not provide enough detail:

- Aspect ratio: 16:9
- Output mode: 底图模式 unless the user explicitly asks for a complete image with rendered text
- General style: consulting preset
- Capital roadshow style: Black Gold Launch preset when content is about financing, roadshows, business plans, project background, strategy planning, financial forecasts, fundraising plans, market analysis, commercial value, capital expression, company introduction, or premium business launches
- Enterprise security style: Anheng preset when content is about cybersecurity, government-enterprise reporting, security launch events, enterprise security solutions, SOC, attack-defense, data security, AI security, code audit security, or digital infrastructure
- Digital transformation style: Blue Gold Tech preset when content is about digital transformation, strategy planning, consulting reports, growth flywheels, capability systems, value creation, intelligent operations, enterprise upgrades, or business transformation
- If content matches capital roadshow themes and another domain theme, recommend Black Gold Launch first unless the user explicitly asks for another preset
- If content matches both enterprise security and digital transformation themes, recommend Anheng first unless the user explicitly asks for Blue Gold Tech or blue-gold value style

## Single-Page Workflow

### Phase 1: Content Analysis

Identify the slide type:

- Cover
- Agenda
- Data
- Process
- Comparison
- Summary
- Timeline
- Architecture
- Relationship
- Problem
- Insight
- Capability
- Case Study
- Closing

Extract the page into three levels:

- 主要层级 / Primary: the single message the audience must remember
- 次要层级 / Secondary: the main proof, structure, stages, modules, or metrics
- 三级层级 / Tertiary: details, context, qualifiers, examples, and notes

State the core message in one sentence.

### Phase 2: Chart Decision

Choose charts only when the content contains a real data or structural relationship.

- Quantity comparison: column chart, bar chart, lollipop chart, ranked bar chart
- Time trend: line chart, area chart, slope chart
- Composition/share: pie chart, donut chart, treemap, 100% stacked bar
- Process/sequence: flowchart, step diagram, funnel, swimlane, journey map
- Relationship/influence: relationship map, network diagram, matrix, cause-effect diagram
- System structure: architecture diagram, layered architecture, hub-and-spoke diagram, modular system map
- Before/after or option comparison: comparison table, two-column contrast, quadrant, side-by-side cards
- No real data relationship: do not force a chart; use a visual metaphor, structured cards, annotated scene, or editorial composition

### Phase 2.5: Design Heuristics Check

Apply `references/design-heuristics.md` before confirming style or generating the final prompt.

Check style fit, color semantics, content density, page-type match, chart choice, text-in-image policy, brand consistency, readability, design restraint, and information compression.

If the requested direction conflicts with the heuristics, briefly explain the conflict and recommend a better option before producing the final prompt. Do not silently follow a visually weak choice.

### Phase 3: Style Confirmation

Ask at most one question per assistant turn and no more than four follow-up questions total.

Confirm in this order:

1. Output mode
2. Style preset
3. Color direction
4. Aspect ratio

Output mode choices:

- 底图模式: visual background only; no readable title, body text, chart labels, logos, annotations, or page numbers
- 成品模式: full finished image; includes title, subtitles, body text, chart text, and annotations when provided or approved

If output mode is missing, ask:

```text
输出模式选无文字底图，还是带标题和正文的成品图？
```

If style is missing and the content belongs to financing, roadshows, business plans, project background, strategy planning, financial forecasts, fundraising plans, market analysis, commercial value, capital expression, company introduction, or premium business launches, recommend Black Gold Launch first:

```text
这页属于融资/路演/高端商务发布会场景，我建议优先用黑金发布会风格。是否采用？
```

If style is missing and the content belongs to cybersecurity, government-enterprise reporting, security launch events, enterprise security solutions, SOC, attack-defense, data security, AI security, code audit security, or digital infrastructure, recommend Anheng first:

```text
这页属于网络安全/政企方案场景，我建议优先用安恒风格。是否采用？
```

If style is missing and the content belongs to digital transformation, strategy planning, consulting reports, growth flywheels, capability systems, value creation, intelligent operations, enterprise upgrades, or business transformation, recommend Blue Gold Tech first:

```text
这页属于数字化转型/战略咨询/价值创造场景，我建议优先用蓝金科技风。是否采用？
```

Otherwise ask:

```text
这页更希望偏商务咨询风、蓝色科技感风、安恒风格、蓝金科技风，还是黑金发布会？
```

### Phase 4: Style Loading

Load the matching preset before generating the final prompt:

- `presets/anheng.yaml` for 安恒风格 / Anheng style
- `presets/consulting.yaml` for 商务咨询风 / consulting style
- `presets/tech-blue.yaml` for 蓝色科技感风 / blue technology style
- `presets/blue-gold-tech.yaml` for 蓝金科技风 / Blue Gold Tech style
- `presets/black-gold-launch.yaml` for 黑金发布会 / Black Gold Launch style

Style loading rules:

- If the user explicitly selects a preset, use it.
- If the user says "直接生成" or "不用问" and the content is capital-roadshow-related, use `presets/black-gold-launch.yaml`.
- If the user says "直接生成" or "不用问" and the content is enterprise-security-related, use `presets/anheng.yaml`.
- If the user says "直接生成" or "不用问" and the content is digital-transformation-related, use `presets/blue-gold-tech.yaml`.
- If the content is neither capital-roadshow-related, enterprise-security-related, nor digital-transformation-related and no style is specified, use `presets/consulting.yaml`.
- If the user asks for a blue technology look, use `presets/tech-blue.yaml`.
- If the user asks for 蓝金科技风, blue-gold, enterprise digital transformation style, value-creation consulting style, or a blue-and-gold consulting technology look, use `presets/blue-gold-tech.yaml`.
- If the user asks for 黑金发布会, black-gold launch, black-gold pitch deck, financing proposal style, investor roadshow style, premium business launch style, or capital-oriented visual tone, use `presets/black-gold-launch.yaml`.
- Preset rules override generic defaults.

### Phase 5: Prompt Generation

When enough information is available, output this structure for Chinese conversations:

```markdown
## 页面类型

## 核心信息

## 视觉层级
- 主要层级:
- 次要层级:
- 三级层级:

## 图表决策
- 决策:
- 理由:
- 图表/结构类型:

## 设计经验检查
- 结论:
- 建议:

## 版式规划

## 风格定义
- 风格预设:
- 字体规范:
- 品牌色:
- 视觉风格:
- 画幅与密度:

## 输出模式

## 最终画面提示词
```

For English conversations, use:

```markdown
## Slide Type

## Core Message

## Visual Hierarchy
- Primary:
- Secondary:
- Tertiary:

## Chart Decision
- Decision:
- Rationale:
- Chart/Structure Type:

## Design Heuristics Check
- Finding:
- Recommendation:

## Layout Plan

## Style Definition

## Output Mode

## Final Visual Prompt
```

## Deck-Consistency Workflow

Use this mode for a whole deck, multiple slides, or style-consistency review.

### Mode Definition

```yaml
mode: deck-consistency
name: 整套 PPT 风格一致性模式
```

### Goal

Build a unified visual system before generating any slide prompt.

Correct sequence:

```text
User provides deck topic / outline / multi-page content
↓
Identify deck type
↓
Apply Design Heuristics
↓
Confirm or recommend one style preset
↓
Build Deck Visual System
↓
Plan page structures
↓
Generate per-slide prompts
↓
Output consistency checklist
```

The value of this mode is to keep the deck visually unified while allowing page-level variation. Consistency does not mean copying the same layout; it means using one visual system across different page types.

### Deck Visual System

When entering `deck-consistency`, output or internally determine this object before per-slide prompts:

```yaml
deck_visual_system:
  deck_type:
  style_preset:
  aspect_ratio:
  background_system:
  color_palette:
  typography_system:
  title_system:
  page_grid:
  visual_motifs:
  icon_style:
  chart_style:
  card_style:
  section_divider_style:
  content_page_style:
  data_page_style:
  closing_page_style:
  text_policy:
  image_policy:
```

Field rules:

- `deck_type`: classify the deck, such as 产品发布会, 企业解决方案, 商业计划书, 融资计划书, 数字化转型汇报, 网络安全方案, 战略规划汇报, 培训课件, 行业洞察报告, or 咨询方案.
- `style_preset`: choose from 安恒风格, 蓝金科技风, 深蓝色科技感发布会 / 科技蓝风格, 黑金发布会, 高端咨询风, or 用户自定义风格. If unspecified, recommend the best preset and explain why.
- `aspect_ratio`: default to 16:9.
- `background_system`: define one deck-wide background logic. Cover and section dividers may be more dramatic; content and data pages must be calmer and readable; closing page should echo the cover.
- `color_palette`: define primary, secondary, and accent colors with semantic meaning, not only color values. Example: blue = technology capability, gold = business value, red = risk warning.
- `typography_system`: define title, chapter title, module title, body, note, and optional English microcopy hierarchy.
- `title_system`: define title position, alignment, size relationship, English subtitle behavior, page number or presentation label rules.
- `page_grid`: define reusable grid patterns such as left-right split, three-card grid, central visual plus side notes, top title / middle content / bottom conclusion, timeline, or roadmap.
- `visual_motifs`: define repeated motifs such as halo, glass cards, hexagons, gold flow lines, security shields, blue arrows, data streams, orbit lines, or circular nodes.
- `icon_style`: define one icon language, such as line icons, glowing icons, flat icons, glass-like icons, gold circular icons, or security shield icons.
- `chart_style`: define chart colors, line weights, gridline strength, axis style, data label style, and risk/warning colors.
- `card_style`: define card radius, border, transparency, shadow, header strip, and icon placement.
- `section_divider_style`: define PART ONE / PART TWO treatment, Chinese chapter title placement, background intensity, and motif reuse.
- `content_page_style`: define ordinary content-page layout rules.
- `data_page_style`: define data-page rules with readability first.
- `closing_page_style`: define an ending style that echoes the cover and leaves a memorable final impression.
- `text_policy`: define output as background-only, final-with-text, or both.
- `image_policy`: define whether people, product images, icons, abstract shapes, real photos, screenshots, or generated scenes are allowed.

Apply the Design Heuristics when defining every Deck Visual System field. For example, choose deep-blue technology launch for product launches, Blue Gold Tech for digital transformation consulting, Anheng for cybersecurity government-enterprise reports, and Black Gold Launch for financing roadshows unless the user's brand rules override that choice.

### Deck Questions

Ask at most one question per assistant turn and no more than five follow-up questions total. Stop once information is sufficient. If the user says "直接生成", use reasonable defaults.

Confirm missing information in this order:

1. Purpose / scene of the deck.
2. Page count or outline.
3. Style preset.
4. Text policy.
5. Brand rules, logo, or corporate colors.

Do not ask for information already provided.

For text policy, ask exactly:

```text
这套 PPT 你希望输出哪种形式？
A. 只生成无文字底图，文字后期在 PPT 中排版
B. 直接生成带完整文字的成品图
C. 同时输出无文字底图 prompt 和带文字成品图 prompt
```

If the user does not choose, recommend and default to C.

### Deck Input Types

- Topic only: ask for page count or outline first. If the user does not provide one or asks to directly generate, default to a 10-page structure.
- Outline provided: build the Deck Visual System and generate prompts based on the outline.
- Per-page content provided: analyze each page type, keep one Deck Visual System, and generate per-slide prompts.
- Existing prompts for review: enter style-consistency evaluation. Infer or use the Deck Visual System, list inconsistencies, and suggest revisions. Do not generate a new deck unless asked.

### Default 10-Page Structure

When only a topic is provided and no page count or outline is available, use:

1. Cover
2. Agenda
3. Background / Trend
4. Pain Points / Challenges
5. Solution Overview
6. Core Capabilities
7. Application Scenarios
8. Value / Benefits
9. Implementation Path / Future Roadmap
10. Closing

Adjust by deck type:

- Financing proposal: include project background, market analysis, competitive landscape, business model, team, financing plan, and financial forecast.
- Product launch: include cover, product overview, core capabilities, product architecture, scenarios, R&D timeline, trend analysis, and future outlook.
- Cybersecurity solution: include security background, threat challenges, solution architecture, core capabilities, deployment path, and customer value.

### Page-Type Variation Rules

- Cover: strongest visual impact and largest title.
- Agenda: emphasize structure and navigation.
- Section divider: stronger background, minimal text, transitional role.
- Content page: prioritize information carrying capacity and readability.
- Data page: chart readability first.
- Architecture page: make module relationships clear.
- Summary page: emphasize conclusions.
- Closing page: echo the cover and stay simple and memorable.

### Per-Slide Prompt Rules

Every slide prompt must reference the global Deck Visual System. Do not generate isolated prompts.

Each slide prompt must include:

- unified style name
- unified background system
- unified color rules
- unified typography rules
- page type
- core message
- slide-specific layout
- slide-specific key visual elements
- elements that keep it consistent with other pages
- forbidden items

Use phrasing such as:

```text
Create a 16:9 presentation slide in the same {style_preset} visual system as the full deck...
```

or:

```text
生成一张 16:9 PPT 页面，延续整套“{style_preset}”风格...
```

### Deck Final Output

For Chinese conversations, final output must use:

````markdown
# 整套 PPT 视觉系统

## 1. Deck 类型
{deck_type}

## 2. 推荐风格
{style_preset}
选择理由：{reason}

## 2.5 设计经验检查
- 场景适配：
- 色彩语义：
- 内容密度：
- 可读性：
- 调整建议：

## 3. 全局视觉规范
- 画幅：
- 背景系统：
- 色彩语义：
- 字体系统：
- 标题系统：
- 页面网格：
- 视觉母题：
- 图标风格：
- 图表风格：
- 卡片风格：
- 文字策略：

## 4. 页面结构规划
| 页码 | 页面类型 | 核心信息 | 推荐布局 | 关键视觉元素 |
|---|---|---|---|---|

## 5. 逐页画面提示词

### Slide 01：{page_title}
页面类型：
核心信息：
布局规划：
视觉一致性要求：
最终 Prompt：
```text
{prompt}
```

### Slide 02：{page_title}
页面类型：
核心信息：
布局规划：
视觉一致性要求：
最终 Prompt：
```text
{prompt}
```

## 6. 一致性检查清单
- [ ] 是否使用同一风格 preset
- [ ] 是否使用统一标题系统
- [ ] 是否使用统一配色语义
- [ ] 是否复用统一视觉母题
- [ ] 是否保持图标风格一致
- [ ] 是否保持卡片 / 图表风格一致
- [ ] 是否区分封面、章节页、内容页和结束页
- [ ] 是否避免每页像不同模板
````

For English conversations, translate the section titles naturally while preserving the same structure.

## Quality Rules

- Do not generate the final prompt before content analysis and chart decision.
- Do not ask bundled questions.
- Stop asking once information is sufficient.
- In `deck-consistency`, do not generate per-slide prompts before establishing the Deck Visual System.
- Keep text editable in PPT for bottom-image mode.
- For finished-image mode, warn briefly that generated text may still require manual correction.
- Do not ask the image model to invent precise data, labels, logos, QR codes, or source text.
- Long text should be converted into grouped cards, short bullets, emphasis strips, or colored background boxes.
- Visual elements must support the slide message.
- For full decks, keep a unified visual language, title system, color semantics, icon style, chart style, card style, and repeated motifs across pages.
- If visual effect conflicts with readability, prioritize readability.
- If the user requests a style that does not fit the scene, explain the mismatch and recommend the better style.
- If the content is too dense for one slide or for finished-image text, recommend splitting pages, compressing into bullets, or using background-only prompts.
