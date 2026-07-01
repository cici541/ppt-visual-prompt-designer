---
name: ppt-visual-prompt-designer
version: 1.0.0
author: Jay
description: Multi-turn Claude skill for generating high-quality PPT visual prompts
tags:
  - ppt
  - presentation
  - visual-design
  - prompt-engineering
---

# ppt-visual-prompt-designer

## Purpose

Use this skill to transform PPT slide content into structured, presentation-ready visual generation prompts. The skill does not create slides, images, or PPTX files. It analyzes the user's content, clarifies missing design intent through a short multi-turn dialogue, chooses a justified chart or visual structure, loads a style preset, and outputs a copy-ready final visual prompt.

## Trigger

Use this skill whenever the user asks to:

- turn PPT page content into a visual prompt
- design a slide image prompt
- generate PPT画面提示词
- decide whether a page needs a chart
- convert slide copy, page briefs, outlines, data summaries, or timeline content into AI image prompts
- create prompts for PowerPoint, Keynote, Figma, AI PPT tools, Midjourney, GPT Image, or similar visual generation tools

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

## Workflow

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

## Layout Plan

## Style Definition

## Output Mode

## Final Visual Prompt
```

## Quality Rules

- Do not generate the final prompt before content analysis and chart decision.
- Do not ask bundled questions.
- Stop asking once information is sufficient.
- Keep text editable in PPT for bottom-image mode.
- For finished-image mode, warn briefly that generated text may still require manual correction.
- Do not ask the image model to invent precise data, labels, logos, QR codes, or source text.
- Long text should be converted into grouped cards, short bullets, emphasis strips, or colored background boxes.
- Visual elements must support the slide message.
