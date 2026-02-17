---
name: collect-news
description: 基于AI四层框架（变革层/创业层/使用层/奇迹层）收集和分类AI新闻。从多个来源聚合新闻，智能分类到四个层次，并输出结构化JSON文件。当用户说"搜索AI新闻"、"收集AI新闻"、"按框架收集新闻"、"四层新闻"时触发。
---

# Collect News - AI新闻四层框架收集器

## 概述

本技能从多个权威来源收集AI新闻，并按照AI四层框架进行分类：
- **E. 变革层 (Evolution Layer)**: 技术突破、模型发布、研究论文、开源项目
- **S. 创业层 (Startup Layer)**: 融资轮次、产品发布、并购、商业模式
- **U. 使用层 (Usage Layer)**: AI工具、生产力应用、提示词工程、使用案例
- **M. 奇迹层 (Miracle Layer)**: AGI/ASI讨论、AI安全、伦理、长期预测

技能会将所有收集和分类的新闻输出为结构化JSON文件，保存到当前工作目录。

## 何时使用本技能

当用户请求以下内容时触发本技能：
- "搜索AI新闻" / "收集AI新闻" / "按框架收集新闻"
- "collect ai news" / "gather ai news"
- "四层新闻" / "4-layer news"
- "按照ESMU框架收集新闻"

## 核心工作流程

### 阶段1：分层信息收集（并行执行）

对四个层次分别执行并行收集：

#### 1. 变革层 (E层) 收集
**主要新闻源：**
- MIT Technology Review AI: https://www.technologyreview.com/topic/artificial-intelligence/
- AI News: https://artificialintelligence-news.com/
- arXiv最新论文: https://arxiv.org/list/cs.AI/recent
- 机器之心: https://www.jiqizhixin.com/
- 量子位: https://www.qbitai.com/

**公司博客：**
- OpenAI Blog: https://openai.com/blog
- Google AI Blog: https://blog.google/technology/ai/
- DeepMind Blog: https://deepmind.google/discover/blog/
- Anthropic News: https://www.anthropic.com/news
- Meta AI Blog: https://ai.meta.com/blog/

**研究源：**
- Hugging Face Blog: https://huggingface.co/blog
- Papers with Code: https://paperswithcode.com/

**搜索关键词：**
```
"AI模型发布" after:[DATE]
"大模型" "发布" after:[DATE]
"开源模型" after:[DATE]
"AI技术突破" after:[DATE]
"人工智能研究" after:[DATE]
"AI model release" after:[DATE]
"AI research breakthrough" after:[DATE]
```

#### 2. 创业层 (S层) 收集
**主要新闻源：**
- TechCrunch AI: https://techcrunch.com/category/artificial-intelligence/
- VentureBeat AI: https://venturebeat.com/category/ai/
- 36氪: https://36kr.com/
- 投资界: https://www.pedaily.cn/

**补充来源：**
- Microsoft AI Blog: https://blogs.microsoft.com/ai/ (企业应用)
- Synced Review: https://syncedreview.com/ (中国AI生态)
- 创业邦: https://www.cyzone.cn/
- 钛媒体: https://www.tmtpost.com/

**搜索关键词：**
```
"AI公司" "融资" after:[DATE]
"人工智能" "投资" after:[DATE]
"AI创业" after:[DATE]
"大模型" "融资" after:[DATE]
"AI产品发布" after:[DATE]
"AI startup funding" after:[DATE]
"AI acquisition" after:[DATE]
```

#### 3. 使用层 (U层) 收集
**主要新闻源：**
- The Verge AI: https://www.theverge.com/ai-artificial-intelligence
- AI Hub Today: https://ai.hubtoday.app/
- 少数派: https://sspai.com/
- InfoQ AI: https://www.infoq.cn/ai

**教程与工具源：**
- KDnuggets: https://www.kdnuggets.com/
- Towards Data Science: https://towardsdatascience.com/

**搜索关键词：**
```
"AI工具" after:[DATE]
"提示词" after:[DATE]
"AI应用" after:[DATE]
"AI效率" after:[DATE]
"ChatGPT使用" after:[DATE]
"AI productivity tools" after:[DATE]
"prompt engineering" after:[DATE]
```

#### 4. 奇迹层 (M层) 收集
**主要新闻源：**
- MIT Technology Review AI (深度分析): https://www.technologyreview.com/topic/artificial-intelligence/
- AI Ethics Newsletter: https://aiethicsnewsletter.com/
- 机器之心 (伦理话题): https://www.jiqizhixin.com/

**搜索关键词：**
```
"AGI" after:[DATE]
"通用人工智能" after:[DATE]
"AI安全" after:[DATE]
"AI伦理" after:[DATE]
"AI监管" after:[DATE]
"artificial general intelligence" after:[DATE]
"AI safety" after:[DATE]
```

### 阶段2：智能分类与评分

对每篇收集到的文章：

1. **主要层次分配**：基于以下因素确定主要层次
   - 关键词匹配（参见 `references/classification_rules.md`）
   - 内容语义分析
   - 来源类型（研究 vs 商业 vs 教程）

2. **次要层次标注**（可选）：某些文章可能跨越多个层次
   - 示例：关于AGI公司的融资新闻（S层）也涉及奇迹层（M层）
   - 标注主要/次要层次

3. **相关性评分** (0.0 - 1.0)：
   - 0.9-1.0: 高度相关，重大新闻
   - 0.7-0.89: 相关，重要更新
   - 0.5-0.69: 中等相关
   - 低于0.5: 过滤掉

4. **重要性评估**：
   - `high`: 重大公告、突破、大额融资
   - `medium`: 值得关注的更新、有趣的发展
   - `low`: 次要新闻、常规更新

### 阶段3：去重与排序

1. **跨层去重**：
   - 比较URL（精确匹配）
   - 比较标题（相似度 > 85%）
   - 保留相关性评分最高的版本
   - 优先选择权威来源

2. **层内排序**：
   - 按重要性排序：high > medium > low
   - 然后按相关性评分排序（降序）
   - 最后按发布日期排序（最新优先）

3. **限制结果数量**：
   - 默认：每层保留前15-20篇文章
   - 可通过用户请求配置

### 阶段4：生成JSON输出

生成以下结构的JSON文件（完整schema见 `references/output_schema.json`）：

```json
{
  "metadata": {
    "generated_at": "2026-02-17T10:30:00Z",
    "date_range": "2026-02-16 to 2026-02-17",
    "total_articles": 68,
    "sources_count": 15,
    "layers_distribution": {
      "evolution": 20,
      "startup": 18,
      "usage": 22,
      "miracle": 8
    }
  },
  "layers": {
    "evolution": {
      "name": "变革层 (Evolution Layer)",
      "description": "底层技术研究、模型发布、开源项目、技术突破",
      "count": 20,
      "articles": [
        {
          "title": "OpenAI发布GPT-5，推理能力提升10倍",
          "summary": "OpenAI今日宣布推出GPT-5...",
          "key_points": ["推理任务性能提升10倍", "..."],
          "impact": "这是大语言模型推理能力的重大突破...",
          "source": "OpenAI Blog",
          "url": "https://openai.com/blog/gpt-5-announcement",
          "published_date": "2026-02-17",
          "relevance_score": 0.98,
          "importance": "high",
          "secondary_layers": ["startup"]
        }
      ]
    },
    "startup": { /* ... */ },
    "usage": { /* ... */ },
    "miracle": { /* ... */ }
  },
  "key_insights": [
    "变革层：OpenAI和Anthropic本周发布重大模型更新",
    "创业层：AI基础设施公司本周融资总额达23亿美元",
    "使用层：企业级提示词工程工具快速普及",
    "奇迹层：多位AI领袖调整AGI时间线预测至2027-2028年"
  ]
}
```

**输出位置**：当前工作目录
**文件名格式**：`ai_news_4layer_YYYY-MM-DD.json`

## 自定义选项

用户可以通过以下参数自定义收集：

### 时间范围
- 默认：最近24小时
- 选项："最近3天"、"最近一周"、"自定义范围"
- 示例："收集最近3天的AI新闻"

### 每层文章数量
- 默认：15-20篇文章
- 选项："前10篇"、"前30篇"、"所有相关"
- 示例："每层收集30篇新闻"

### 重点层次
- 默认：全部4层
- 选项：指定1-3个重点层次
- 示例："只收集变革层和创业层的新闻"

### 深度级别
- `brief`（快速）：快速扫描，仅主要来源
- `standard`（标准）：全面覆盖（默认）
- `deep`（深度）：包含Tier 3-4来源，更多搜索查询

## 质量标准

确保所有收集的新闻符合以下标准：

1. **时效性**：在指定时间范围内发布
2. **相关性**：相关性评分 ≥ 0.5
3. **可访问性**：所有URL有效且可访问
4. **无重复**：每篇文章只出现一次
5. **准确分类**：文章正确分配到各层
6. **完整元数据**：所有必填字段已填充
7. **中文输出**：所有标题、摘要、关键点均为中文

## 使用示例

**用户请求1：**
```
搜索AI新闻
```

**执行动作：**
- 收集最近24小时的新闻
- 全部4层，标准深度
- 每层15-20篇文章
- 输出：`ai_news_4layer_2026-02-17.json`

**用户请求2：**
```
收集最近3天的AI新闻，重点关注创业层和使用层
```

**执行动作：**
- 收集最近3天的新闻
- 重点关注创业层和使用层
- 标准深度
- 输出：`ai_news_4layer_2026-02-17.json`（S/U层文章更多）

**用户请求3：**
```
按四层框架收集AI新闻，每层30篇，深度模式
```

**执行动作：**
- 收集最近24小时的新闻
- 全部4层，深度模式
- 每层30篇文章
- 包含Tier 3-4来源
- 输出：`ai_news_4layer_2026-02-17.json`

## 资源文件

### references/ 目录
加载到上下文中的参考文档，用于指导收集和分类过程：

- **framework.md**：四层AI框架的详细解释和示例
- **news_sources.md**：新闻源到四层的完整映射
- **search_queries.md**：每层的搜索查询模板（中英文）
- **classification_rules.md**：分类决策树和相关性评分算法
- **output_schema.json**：完整的JSON输出schema和字段定义

### examples/ 目录
展示预期JSON结构的示例输出：

- **example_output.json**：包含所有四层的示例JSON输出

## 使用的工具

本技能使用以下MCP工具：

1. **mcp__web_reader__webReader**：从新闻网站获取内容
   - 参数：`return_format: markdown`, `timeout: 20s`
   - 用于网站抓取和完整文章检索

2. **WebSearch**：执行带日期过滤的搜索查询
   - 动态日期过滤器（例如：`after:2026-02-16`）
   - 每层2-4个查询
   - 每个查询返回前10-15个结果

## 实现说明

### 并行执行策略
- 启动4个并行收集任务（每层一个）
- 每个任务独立从其分配的来源获取
- 所有任务完成后聚合结果
- 总执行时间：标准深度约30-60秒

### 错误处理
- 如果某个来源无法访问，跳过并继续其他来源
- 在元数据中记录失败的来源
- 确保每层至少有10篇文章（如果可用）

### 速率限制
- 尊重网站速率限制
- 对同一域名的请求之间添加1-2秒延迟
- 使用WebSearch进行批量发现，然后获取单篇文章

### 日期处理
- 所有日期使用ISO 8601格式（YYYY-MM-DD）
- 时区：UTC
- "最近24小时" = 当前时间 - 24小时

### 多语言处理
- 英文文章自动翻译为中文
- 标题、摘要、关键点全部中文化
- 保留原文URL和来源信息
- 可选保留原始英文标题

## 成功标准

成功的收集应该：
1. ✅ 在当前目录生成有效的JSON文件
2. ✅ 包含所有4层的文章（除非用户指定重点）
3. ✅ 各层之间无重复文章
4. ✅ 所有URL有效且可访问
5. ✅ 相关性评分准确反映文章重要性
6. ✅ 分类符合四层框架
7. ✅ 元数据完整准确
8. ✅ 所有内容为中文（标题、摘要、关键点）
