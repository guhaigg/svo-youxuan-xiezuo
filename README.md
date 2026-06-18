# Spec Verify Optimize

一个面向 AI 协作的中文方法论、可移植协议和 Codex Skill。

SVO = Spec -> Verify -> Optimize。

它解决的问题不是“怎么写更长的提示词”，而是：如何避免 AI 在还没有理解真实目标、成功标准、关键假设和验证方法之前，就自信地产出代码、文档、方案或设计。

## 它适合什么

- 项目开局
- MVP 范围定义
- 产品或功能方案
- 技术路线选择
- 文档或规范写作
- 多轮复杂任务
- 需要跨 AI、跨电脑接续的协作

## 它不适合什么

- 简单问答
- 明确的小改动
- 命令输出
- 格式转换
- 用户已经给出清晰验收标准的机械任务

## 核心思想

```text
目标函数 -> 关键变量 -> 最值得验证的小桶 -> Spec -> Verifier -> 执行 -> 检查点 -> 收缩搜索空间
```

SVO 把 Karpathy 式的 Spec / Verifier 思路，与华罗庚优选法中的“用较少试验逼近更优解”结合起来。

每一轮协作不是为了多做一点，而是为了更快确认：

- 什么假设成立
- 什么选项应该排除
- 哪个变量仍然最不确定
- 下一步做什么最划算

## 五个核心理念

1. **按假设拆分，而不是按任务拆分**  
   小桶不是“做登录页”，而是“验证用户是否需要先体验核心价值再注册”。

2. **定义反目标**  
   目标函数说明优化什么，反目标说明不能为了优化它而牺牲什么。

3. **区分证据等级**  
   真实用户和真实数据优先，自动化验证其次，人工检查再次，AI 自评只能辅助。

4. **检查点必须收缩搜索空间**  
   检查点不是“完成了”，而是“我们确认了什么、排除了什么、下一步应该验证什么”。

5. **达到足够好就停止优化**  
   SVO 不是无限打磨。达到验收标准，或继续优化收益小于成本，就交付或切换模式。

## 仓库结构

```text
spec-verify-optimize/
  README.md
  LICENSE
  CHANGELOG.md
  skill/
    SKILL.md
    agents/
      openai.yaml
    references/
      SVO.md
      examples.md
  portable/
    SVO.md
    SVO-examples.md
```

## 在 Codex 中使用

把 `skill/` 目录复制到你的 Codex skills 目录，例如：

```text
~/.codex/skills/spec-verify-optimize
```

Windows 示例：

```text
C:\Users\<你的用户名>\.codex\skills\spec-verify-optimize
```

然后在 Codex 中可以这样说：

```text
使用 spec-verify-optimize / SVO / 优选小桶模式。
先不要写代码，先帮我明确项目目标、目标函数、关键假设和第一桶。
```

## 在其他 AI 中使用

如果你使用 Claude、Gemini、ChatGPT、Cursor 或其他 AI：

1. 打开 `portable/SVO.md`
2. 复制内容到对话开头，或放进项目规则文件
3. 如需示例，继续附上 `portable/SVO-examples.md`

常见项目规则文件：

```text
AGENTS.md
CLAUDE.md
GEMINI.md
.cursorrules
```

## 快速启动词

```text
使用 SVO 优选协作协议。

在开始写代码、文档、方案或设计之前，请先明确：
1. 这个项目真正要改善什么
2. 目标函数是什么
3. 反目标是什么
4. 当前最关键的不确定性是什么
5. 第一桶应该验证哪个假设
6. 这个小桶的 Spec 和 Verifier 是什么

每完成一个小桶后，请给出验证证据、已确认判断、已排除选项、剩余不确定性和下一桶建议，并暂停等我确认。
```

## 版本状态

当前版本：`v0.1.0`

这是一个 public draft，已经适合真实使用，但仍欢迎继续补充更多案例、反模式和不同场景下的 verifier 模板。

## License

MIT
