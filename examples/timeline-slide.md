# Timeline Slide Example

## Input

```text
第一页：消失的叙事——Fable 5 & Mythos 5 的强制下线与合规静默

核心定位：通过梳理 72 小时内从发布到全面下线的时间线，客观呈现监管力量对顶级 AI 模型的强制干预，奠定严肃的技术与安全背景。

节点：
- 发布（6月9日）：Anthropic 正式推出 Fable 5 和 Mythos 5。
- 干预（6月12日）：BIS 介入并下达 EAR 紧急出口管制指令。
- 权限阻断：内部非美籍员工权限被剥离。
- 全面下线：全球范围暂停模型服务接入。
```

## Expected Behavior

The skill should:

- Identify the page as `时间线 / AI 安全事件开场页`
- Choose a horizontal timeline rather than a statistical chart
- Ask for output mode first
- Recommend Anheng style if the user has not selected a style

## Example Final Prompt Excerpt

```text
生成一张 16:9 蓝色科技感发布会风格 PPT 成品页，主题为“消失的叙事——Fable 5 & Mythos 5 的强制下线与合规静默”。页面中部设计一条横向 72 小时时间线，从左到右包含发布、监管介入、权限阻断、全面下线四个节点。背景使用深蓝科技渐变、低亮度数据流、网络节点和基础设施网格。关键监管节点使用少量红色或琥珀色警示高亮。整体专业、克制、冷峻、技术可信。
```
