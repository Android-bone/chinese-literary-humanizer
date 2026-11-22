# chinese-literary-humanizer

**中文文学化去 AI 编辑 Skill**

[![Version 0.1.0](https://img.shields.io/badge/version-0.1.0-8A3B32)](VERSION)
[![Language: Chinese](https://img.shields.io/badge/language-%E4%B8%AD%E6%96%87-C93C3C)](SKILL.md)
[![Agent Skill](https://img.shields.io/badge/type-Agent%20Skill-3A6B5D)](SKILL.md)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue)](LICENSE)

把“信息正确，但像模型组装出来的中文”，改成事实站得住、句子说得顺、背后有人在思考的文章。

这个 Skill 面向中文长文的改写、润色和审阅。它会清理通用 AI 痕迹、翻译腔和机械结构，同时保护数据、来源、因果边界与原有格式；当文章需要作者声线时，再按需加入第一作者视角、克制幽默、结构判断和文学余味。

**当前状态：** `0.1.0` 包含 3 种处理模式、6 个按需加载的参考模块、24 类常见 AI 写作模式、一套第一作者写作规则，以及 50 分基础复核和长文附加自评。首版已完成 frontmatter、相对引用、目录完整性和示例边界检查。

[主要能力](#主要能力) · [处理模式](#处理模式) · [改写示例](#改写示例) · [快速安装](#快速安装) · [使用方式](#使用方式) · [工作流与目录](#工作流与目录) · [验证与边界](#验证与边界) · [参与贡献](#参与贡献)

## 主要能力

| 能力 | 具体处理 |
| --- | --- |
| 去除 AI 痕迹 | 清理宣传腔、意义拔高、模糊归因、否定式排比、强凑三项、列表膨胀、口号结尾和协作话术 |
| 中文母语化 | 修复英文句法直译、主语缺失、长定语、系动词回避、同义词轮换、连环冒号和术语混乱 |
| 结构改写 | 找到文章真正的问题，合并重复段落，补足因果与反例，打破“定义—分点—总结”的机械推进 |
| 作者视角 | 处理公众号开篇、观点承担、过渡衔接、共情与互动，同时防止虚构“我亲测”“朋友告诉我” |
| 文学评论 | 从具体异常进入现实机制，使用克制幽默、有效比喻和跨领域知识锚点，在结尾完成情绪降落 |
| 事实与格式保护 | 保留数据、时间、法规、专有名词、因果强度、HTML、Markdown、脚注、链接和图片位置 |
| 交付复核 | 使用快速检查、50 分基础评分、长文附加自评和事实硬检查决定继续修订还是交付 |

这个项目不是违禁词替换器。某个词、三项列举或破折号只要承担真实功能，就可以保留；真正需要修正的是它是否在替代事实、逻辑和作者判断。

## 处理模式

| 模式 | 适用文本 | 改写力度 |
| --- | --- | --- |
| 清理模式 | 公告、报告、技术说明、短文 | 删除 AI 痕迹，修正中文句法和术语，尽量保留结构，不强加文学性 |
| 深度改写模式 | 博客、产品分析、行业文章、普通公众号稿 | 重排弱段落，合并重复观点，修复因果和主线，按需加入作者视角 |
| 文学评论模式 | 社会观察、商业评论、科技文化、职场与经济议题 | 在深度改写基础上加入生活切口、结构分析、克制幽默、比喻和具象收束 |

技术说明和监管材料不会被硬改成散文。第一人称也不是默认装饰：只有原稿、用户材料或作者能够真实承担相应经历时，才使用“我亲测”“我踩过坑”等表述。

## 改写示例

### 改写前

> TACH 是坦桑尼亚支付生态中的关键基础设施，充分彰显了该国在数字金融领域的持续进步。2025 年，该系统实现了 99.98% 的高可用率，并以 T+0 的强大能力处理 2,262 万笔 EFT。这不仅提升了支付效率，也为金融普惠注入了新动能。

### 改写后

> 坦桑尼亚央行 2025 年国家支付系统年报显示，TACH 当年可用率为 99.98%，并为批量交易提供同日结算。这里的“同日”不等于实时到账：文件要赶上截止时间，通过格式校验和批次处理，银行净头寸也要完成结算。
>
> 2025 年经 TACH 处理的银行间 EFT 为 2,262 万笔。相比“关键基础设施”这类判断，这组数据和处理条件更能说明 TACH 在做什么。

改写删除了没有机制支撑的意义宣告，保留来源、数字和术语边界，并把“T+0”可能引起的误读说明白。更多完整案例见 [`references/full-examples.md`](references/full-examples.md)。

## 快速安装

### 使用 Skills CLI

仓库根目录本身就是技能目录，可以直接安装：

```powershell
# 安装到当前项目
npx skills add Android-bone/chinese-literary-humanizer

# 安装为个人全局 Skill
npx skills add Android-bone/chinese-literary-humanizer -g
```

### 手动安装

Codex：

```powershell
git clone https://github.com/Android-bone/chinese-literary-humanizer.git `
  "$env:USERPROFILE\.codex\skills\chinese-literary-humanizer"
```

Claude Code：

```powershell
git clone https://github.com/Android-bone/chinese-literary-humanizer.git `
  "$env:USERPROFILE\.claude\skills\chinese-literary-humanizer"
```

也可以把下载后的整个目录复制到代理使用的 skills 根目录。不要只复制 `SKILL.md`：深度改写、作者视角和交付复核依赖 `references/` 中的按需参考文件。

## 使用方式

### 改写文章

```text
请用 $chinese-literary-humanizer 深度改写 article.md。
保留数据、链接和图片位置，删除翻译腔和机械结构，另存为新文件。
```

### 第一作者公众号

```text
把这篇公众号文章改成可信的第一作者视角。
作者可以承担资料整理和专业判断，但不要虚构朋友对话或亲身经历。
```

### 文学评论

```text
用文学评论模式改写这篇科技文化文章。
从具体异常切入，增加结构分析和克制幽默，结尾不要喊口号。
```

### 只做审阅

```text
先不要改稿。请检查这篇文章的事实边界、AI 痕迹、中文语感和结构问题，列出最重要的修改建议。
```

不同代理的显式调用方式可能不同。无法使用 `$skill-name` 时，直接描述“去 AI 味、中文母语化、深度改写或第一作者公众号”等目标即可触发相同工作流。

## 工作流与目录

运行入口是 [`SKILL.md`](SKILL.md)。它先判断文本类型与改写力度，再只读取当前任务需要的参考模块，避免每次加载全部规则。

```text
chinese-literary-humanizer/
├── SKILL.md                         技能入口、模式路由、事实与输出约束
├── references/
│   ├── diagnostics.md               去 AI、结构和中文母语化诊断顺序
│   ├── humanizer-patterns.md        24 类常见模式及改写前后示例
│   ├── author-voice.md              第一作者、过渡、共情和互动规则
│   ├── commentary-craft.md          原创中文文学评论写法
│   ├── full-examples.md             六类完整改写案例
│   └── final-review.md              快速检查、评分和硬性退回条件
├── VERSION                          当前版本
├── CHANGELOG.md                     版本变更记录
├── THIRD_PARTY_NOTICES.md           上游项目与许可说明
└── LICENSE                          MIT License
```

典型执行顺序：

1. 核对事实、数字、来源、专业术语和交付格式。
2. 判断使用清理、深度改写还是文学评论模式。
3. 先修主线、重复、跳跃和因果，再处理句子。
4. 只加载与当前文本有关的诊断、作者视角或评论模块。
5. 交付前执行快速检查和评分；事实错误不能被风格分数抵消。

## 验证与边界

**`0.1.0` 首版检查：**

- `SKILL.md` frontmatter 的名称和描述完整。
- 六个参考文件均可由相对路径访问，没有孤立模块。
- 24 类 AI 写作模式均配有中文解释或前后对照。
- 第一作者模块区分真实亲历、资料整理、公开案例和作者推断。
- 完整示例覆盖产品稿、普通长文、支付制度科普、文学评论、技术清单和第一作者公众号。
- 交付前复核包含事实、结构、中文母语感、AI 痕迹、作者视角和文学评论检查。

当前版本是指令型 Skill，没有联网服务、后台进程或遥测，也不会自动上传用户文本。实际效果仍取决于所用模型、原稿质量、材料完整度和用户提供的事实。

它的目标是提高中文写作质量，不是帮助文本绕过 AI 检测器。AI 检测结果本身也不应当被当作作者身份的确定证据。

## 后续计划

- [ ] 增加零依赖的 frontmatter、相对链接和目录结构检查脚本。
- [ ] 增加覆盖公告、技术文档、公众号和监管科普的行为评测样例。
- [ ] 增加英文 README，方便非中文用户理解安装与能力边界。
- [ ] 根据真实改稿反馈继续精简重复规则，避免 Skill 本身变成新的模板。

## 参与贡献

欢迎通过 [Issues](https://github.com/Android-bone/chinese-literary-humanizer/issues) 提交误判、遗漏模式和改写案例，也欢迎发起 [Pull Request](https://github.com/Android-bone/chinese-literary-humanizer/pulls)。

反馈规则问题时，建议同时提供：

- 原句及其上下文。
- 当前输出为什么不自然或不准确。
- 希望保留的事实、语气和格式。
- 一个能够说明方向的修改版本。

请不要提交未经授权的私人对话、付费文章全文或带有敏感信息的真实材料。新增规则应解决可重复出现的问题，不要把某一篇文章的个人偏好升级成全局禁令。

## 致谢与许可

本项目在重新设计工作流和中文示例的过程中，吸收并改写了以下 MIT 项目的部分方法：

- [`op7418/Humanizer-zh`](https://github.com/op7418/Humanizer-zh)：通用 AI 写作痕迹、快速检查和评分思路。
- [`ai-zixun/humanizer-zh`](https://github.com/ai-zixun/humanizer-zh)：中文翻译腔、结构腔、排版和长文母语化处理。

它们进一步受到 [`blader/humanizer`](https://github.com/blader/humanizer)、[`hardikpandya/stop-slop`](https://github.com/hardikpandya/stop-slop) 和 Wikipedia “Signs of AI writing”等资料启发。详细版权与许可声明见 [`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md)。

本仓库采用 [MIT License](LICENSE)。保留上游项目的版权与许可声明，是再发布和衍生使用的一部分。

