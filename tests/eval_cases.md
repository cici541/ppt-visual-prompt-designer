# Evaluation Cases

## Case 1: Multi-turn process page

**Prompt**

```text
帮我把这一页转成画面提示词：标题是“AI代码审计从发现问题走向闭环整改”。内容包括代码接入、漏洞识别、影响路径分析、整改建议、报告归档。这页想表达 AI 代码审计不是只扫漏洞，而是帮助研发团队完成整改闭环。
```

**Expected**

- Uses Chinese fields.
- Analyzes page type, core message, 主要层级, 次要层级, 三级层级.
- Chooses process or architecture visualization rather than a statistical chart.
- Asks exactly one follow-up question.
- Prioritizes output mode if it is missing.

## Case 2: Direct generation for data comparison

**Prompt**

```text
不用问，直接生成。页面内容：2024年三个渠道收入分别是直销1200万、代理800万、线上450万，想表达直销仍是核心收入来源。
```

**Expected**

- Outputs all required Chinese final sections.
- Chooses bar chart or column chart.
- Defaults to bottom-image mode.
- Keeps exact labels and numbers editable in PPT.

## Case 3: English architecture prompt

**Prompt**

```text
Please turn this slide content into a visual generation prompt. Slide: Our platform has three layers: data ingestion, AI analysis engine, and remediation workflow. The point is that the product connects code, risk, and remediation in one system. Ask me if you need design choices.
```

**Expected**

- Responds in English.
- Uses English field names.
- Classifies the page as architecture or system structure.
- Does not force a statistical chart.
- Asks no more than one follow-up question.

## Case 4: Anheng style direct generation

**Prompt**

```text
不用问，直接生成。使用安恒风格，把这一页转成 PPT 画面提示词：标题是“AI 安全能力从检测走向运营闭环”。内容包括资产接入、风险识别、攻击路径分析、处置编排、SOC 运营看板。输出无文字底图。
```

**Expected**

- Uses Anheng style.
- Uses strict top 10% #0F256C title bar and lower 85% pure white content area.
- Uses #08287F as dominant blue and #C7001C only for emphasis or alerts.
- Forbids readable title, body text, chart labels, annotations, logos, watermarks, and fake UI text.
- Includes mandatory Anheng prompt phrases.

## Case 5: Security context without explicit style

**Prompt**

```text
帮我把这一页转成 PPT 画面提示词：标题是“安全运营从告警处置走向闭环治理”。内容包括资产接入、风险识别、攻击路径分析、处置编排、SOC 运营看板。还没想好风格。
```

**Expected**

- Recognizes the cybersecurity/SOC context.
- Recommends Anheng style first when asking about visual style.
- If the user requests direct generation, defaults to Anheng style.
