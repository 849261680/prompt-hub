本指南为 Claude 4 模型（Opus 4.1、Opus 4 和 Sonnet 4）提供具体的提示工程技术，帮助您在应用中取得最佳效果。这些模型经过训练，能够比 Claude 模型的以往版本更精确地遵循指令。

明确你的指令

Claude 4 模型对清晰、明确的指令反应良好。具体说明你期望的输出结果可以帮助提升效果。那些希望获得之前 Claude 模型“超越预期”行为的客户可能需要更明确地请求这些行为配合 Claude 4。

示例：创建分析仪表盘

**效果较差：**

复制

```text
Create an analytics dashboard
```

**更有效：**

复制

```text
Create an analytics dashboard. Include as many relevant features and interactions as possible. Go beyond the basics to create a fully-featured implementation.
```


添加上下文以提升性能

提供背景信息或动机，例如向 Claude 解释为什么这种行为很重要，可以帮助 Claude 4 模型更好地理解你的目标并给出更有针对性的回复。

示例：格式偏好

**效果较差：**

复制

```text
NEVER use ellipses
```

**更有效：**

复制

```text
Your response will be read aloud by a text-to-speech engine, so never use ellipses since the text-to-speech engine will not know how to pronounce them.
```

Claude 足够智能，能够从解释中泛化。



对示例和细节保持警惕

Claude 4 模型在遵循指令时会关注细节和示例。确保你的示例与你想鼓励的行为一致，并尽量减少你想避免的行为。


针对特定情况的指导

### 

[​

](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices#control-the-format-of-responses)

控制响应格式

我们发现有几种方法特别有效地引导 Claude 4 模型的输出格式：

1. **告诉 Claude 该做什么，而不是不该做什么**
    
    - 而不是：“不要在你的回复中使用 markdown”
    - 尝试：“你的回复应该由流畅的段落组成。”
2. **使用 XML 格式指示符**
    
    - 尝试：“将你的回应的散文部分写在 <smoothly_flowing_prose_paragraphs> 标签中。”
3. **使你的提示风格与期望的输出相匹配**
    
    你提示中使用的格式风格可能会影响 Claude 的回应风格。如果你在输出格式方面仍然遇到可引导性问题，我们建议尽可能使你的提示风格与期望的输出风格相匹配。例如，从你的提示中移除 Markdown 可以减少输出中的 Markdown 数量。
    

### 

[​

](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices#leverage-thinking-%26-interleaved-thinking-capabilities)

利用思考与交错思考能力

Claude 4 提供思考能力，这在涉及工具使用后的反思或复杂多步推理的任务中尤其有帮助。你可以引导其初始或交互式思考，以获得更好的结果。

示例提示

复制

```text
After receiving tool results, carefully reflect on their quality and determine optimal next steps before proceeding. Use your thinking to plan and iterate based on this new information, and then take the best next action.
```

关于思考能力的更多信息，请参见 [扩展思考](https://docs.anthropic.com/en/docs/build-with-claude/extended-thinking) 。

### 

[​

](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices#optimize-parallel-tool-calling)

优化并行工具调用

Claude 4 模型擅长并行工具执行。它们在没有提示的情况下使用并行工具调用时成功率很高，但一些轻微的提示可以提升这一行为至接近 100%的并行工具使用成功率。我们发现以下提示最为有效：

代理的示例提示

复制

```text
For maximum efficiency, whenever you need to perform multiple independent operations, invoke all relevant tools simultaneously rather than sequentially.
```

### 

[​

](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices#reduce-file-creation-in-agentic-coding)

在代理式编程中减少文件创建

Claude 4 模型有时会为测试和迭代目的创建新文件，尤其是在处理代码时。这种方法允许 Claude 将文件（尤其是 Python 脚本）用作“临时草稿板”，在保存最终输出之前使用。使用临时文件可以改善结果，特别是在代理式编程用例中。

如果您希望尽量减少净新增文件创建，可以指示 Claude 自行清理：

示例提示

复制

```text
If you create any temporary new files, scripts, or helper files for iteration, clean up these files by removing them at the end of the task.
```

### 

[​

](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices#enhance-visual-and-frontend-code-generation)

增强视觉和前端代码生成

对于前端代码生成，你可以通过提供明确的鼓励来引导 Claude 4 模型创建复杂、详细和交互式的设计：

示例提示

复制

```text
Don't hold back. Give it your all.
```

您还可以通过提供额外的修饰符和详细信息来提升 Claude 前端在特定领域的性能，说明需要关注的内容：

- “尽可能包含相关的功能和交互”
- “添加精心设计的细节，如悬停状态、过渡效果和微交互”
- “创建一个展示网页开发能力的令人印象深刻的表现”
- “应用设计原则：层级、对比、平衡和动感”

### 

[​

](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices#avoid-focusing-on-passing-tests-and-hard-coding)

避免专注于通过测试和硬编码

前沿语言模型有时会过度关注让测试通过，而牺牲更通用的解决方案。为防止这种行为并确保稳健、可推广的解决方案：

示例提示

复制

```text
Please write a high quality, general purpose solution. Implement a solution that works correctly for all valid inputs, not just the test cases. Do not hard-code values or create solutions that only work for specific test inputs. Instead, implement the actual logic that solves the problem generally.

Focus on understanding the problem requirements and implementing the correct algorithm. Tests are there to verify correctness, not to define the solution. Provide a principled implementation that follows best practices and software design principles.

If the task is unreasonable or infeasible, or if any of the tests are incorrect, please tell me. The solution should be robust, maintainable, and extendable.
```

## 

[​

](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices#migration-considerations)

迁移考虑事项

从 Sonnet 3.7 迁移到 Claude 4 时：

1. **明确期望的行为** ：考虑详细描述你希望在输出中看到的内容。
    
2. **用修饰语来构建你的指令** ：添加鼓励 Claude 提高输出质量和细节的修饰语，有助于更好地塑造 Claude 的表现。例如，不要用“创建一个分析仪表板”，而应该用“创建一个分析仪表板。尽可能多地包含相关的功能和交互。超越基础，创建一个功能完备的实现。”
    
3. **明确请求特定功能** ：当需要动画和交互元素时，应明确提出请求。