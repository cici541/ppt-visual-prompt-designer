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

## Case 6: Government-enterprise cybersecurity history timeline

**Prompt**

```text
请你用这个技能，帮我做一页中国近20年网络安全发展史的PPT。输出成品图，我想要用政企风格。
```

**Expected**

- Uses Chinese fields.
- Classifies the page as a timeline or industry history slide.
- Defines the core message as China's cybersecurity evolution from compliance construction toward data security, critical infrastructure protection, AI security, and digital infrastructure security governance.
- Chooses a horizontal timeline or staged roadmap instead of a statistical chart.
- Uses a professional government-enterprise cybersecurity style with blue-white palette, restrained technology visuals, strict alignment, and readable finished-image text.
- Groups the timeline into clear stages such as system start, national strategy, legal system formation, data and critical infrastructure protection, and AI/digital infrastructure security.

## Case 7: Blue Gold Tech digital transformation roadmap

**Prompt**

```text
不用问，直接生成。使用蓝金科技风，把这一页转成 PPT 画面提示词：标题是“企业数字化转型从能力建设走向价值创造”。内容包括数据治理、流程在线、AI智能运营、组织协同、业务增长飞轮，想表达数字化不是系统上线，而是持续创造业务价值。输出成品图。
```

**Expected**

- Uses `presets/blue-gold-tech.yaml`.
- Outputs all required Chinese final sections.
- Classifies the page as a roadmap, capability model, process, or transformation path slide.
- Uses blue for digital capability, systems, process, and intelligent operations.
- Uses gold for business value, outcomes, growth, and final conclusions.
- Includes Blue Gold Tech mandatory prompt phrases such as `16:9 professional enterprise consulting presentation slide`, `clean white or very light blue-gray background`, `technology blue palette with gold value accents`, `hexagonal modules where appropriate`, and `blue represents digital capability and process`.
- Avoids dark cyberpunk background, messy decorative lines, overly complex patterns, and saturated neon colors.

## Case 8: Digital transformation style recommendation

**Prompt**

```text
帮我把这一页转成 PPT 画面提示词：标题是“智能运营能力体系建设路线图”。内容包括数据底座、流程重构、AI Copilot、运营指标、价值闭环。还没想好风格。
```

**Expected**

- Recognizes the digital transformation / intelligent operations / capability system context.
- Recommends Blue Gold Tech style first when asking about visual style.
- Still asks only one follow-up question per turn.

## Case 9: Black Gold Launch financing proposal direct generation

**Prompt**

```text
不用问，直接生成。使用黑金发布会，把这一页转成 PPT 画面提示词：标题是“新一代智能制造平台融资计划书”。内容包括项目背景、市场空间、商业模式、核心团队、融资用途、三年财务预测，想表达项目具备高成长性和资本价值。输出成品图。
```

**Expected**

- Uses `presets/black-gold-launch.yaml`.
- Outputs all required Chinese final sections.
- Classifies the page as a financing proposal, investor roadshow, business plan, or premium business presentation slide.
- Uses a dark black or deep gray-black background with warm gold or champagne-gold accents.
- Uses gold for capital value, key numbers, core conclusions, icons, nodes, and important highlights.
- Includes Black Gold Launch mandatory prompt phrases such as `16:9 high-end black and gold business presentation slide`, `dark premium background with subtle black gradient`, `black-gold financing proposal aesthetic`, `premium pitch deck / investor presentation tone`, and `professional, high-end, capital-oriented visual tone`.
- Avoids blue consulting report look, messy decorative patterns, colorful palette, cheap bright gold, and cyberpunk neon effects.

## Case 10: Capital roadshow style recommendation

**Prompt**

```text
帮我把这一页转成 PPT 画面提示词：标题是“商业计划书核心投资亮点”。内容包括市场规模、增长逻辑、团队优势、商业模式、融资计划和退出路径。还没想好风格。
```

**Expected**

- Recognizes the financing / investor roadshow / business plan context.
- Recommends Black Gold Launch style first when asking about visual style.
- Still asks only one follow-up question per turn.
