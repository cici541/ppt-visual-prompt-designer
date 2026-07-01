# Cover Slide Example

## Input

```text
请把这页封面转成 PPT 画面提示词：

标题：AI 安全治理进入深水区
副标题：从模型能力增长到企业级风险控制
场景：网络安全发布会开场页
```

## Expected Behavior

The skill should:

- Identify the page as `封面页 / Cover`
- Extract one core message: AI capability growth requires enterprise-grade risk control
- Recommend Anheng style because this is a cybersecurity launch context
- Ask for output mode if it is missing

## Example Final Prompt Excerpt

```text
生成一张 16:9 enterprise cybersecurity presentation slide，使用安恒风格。顶部 10% 深蓝标题栏 #0F256C，左侧白色微软雅黑加粗大标题；下方 85% 纯白内容区，使用 #08287F、#084D80、#087380 构建克制的安全治理视觉。主视觉包含盾牌、数据流、AI 模型核心和企业安全边界，红色 #C7001C 仅用于风险或关键提醒。保持 generous whitespace、strict grid alignment、clear visual hierarchy，不使用杂乱科技线条或无意义复杂纹理。
```
