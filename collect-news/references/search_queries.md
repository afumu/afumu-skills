# AI新闻搜索查询模板

本文档定义了针对四层AI框架的搜索查询模板，全部使用中文关键词。

## 日期过滤器

使用动态日期过滤器确保新闻时效性：

- **最近24小时**: `after:YYYY-MM-DD` (昨天的日期)
- **最近3天**: `after:YYYY-MM-DD` (3天前的日期)
- **最近一周**: `after:YYYY-MM-DD` (7天前的日期)

## E. 变革层 (Evolution Layer) 搜索查询

### 核心查询（必须执行）

```
1. "AI模型发布" after:[DATE]
2. "大模型" "发布" after:[DATE]
3. "开源模型" after:[DATE]
4. "AI技术突破" after:[DATE]
5. "人工智能研究" after:[DATE]
```

### 扩展查询（深度模式）

```
6. "Transformer" "架构" after:[DATE]
7. "多模态" "模型" after:[DATE]
8. "AI训练" "方法" after:[DATE]
9. "机器学习" "论文" after:[DATE]
10. "深度学习" "突破" after:[DATE]
11. "神经网络" "创新" after:[DATE]
12. "算力" "GPU" after:[DATE]
```

### 公司特定查询

```
13. "OpenAI" "模型" after:[DATE]
14. "Anthropic" "Claude" after:[DATE]
15. "Google" "Gemini" after:[DATE]
16. "Meta" "LLaMA" after:[DATE]
17. "DeepSeek" after:[DATE]
18. "月之暗面" after:[DATE]
19. "智谱AI" after:[DATE]
```

## S. 创业层 (Startup Layer) 搜索查询

### 核心查询（必须执行）

```
1. "AI公司" "融资" after:[DATE]
2. "人工智能" "投资" after:[DATE]
3. "AI创业" after:[DATE]
4. "大模型" "融资" after:[DATE]
5. "AI产品发布" after:[DATE]
```

### 扩展查询（深度模式）

```
6. "A轮融资" "AI" after:[DATE]
7. "B轮融资" "人工智能" after:[DATE]
8. "AI公司" "估值" after:[DATE]
9. "AI" "收购" after:[DATE]
10. "AI" "并购" after:[DATE]
11. "AI" "IPO" after:[DATE]
12. "AI商业模式" after:[DATE]
```

### 地区特定查询

```
13. "中国AI" "融资" after:[DATE]
14. "硅谷" "AI创业" after:[DATE]
15. "AI独角兽" after:[DATE]
```

## U. 使用层 (Usage Layer) 搜索查询

### 核心查询（必须执行）

```
1. "AI工具" after:[DATE]
2. "提示词" after:[DATE]
3. "AI应用" after:[DATE]
4. "AI效率" after:[DATE]
5. "ChatGPT使用" after:[DATE]
```

### 扩展查询（深度模式）

```
6. "AI助手" after:[DATE]
7. "AI编程" after:[DATE]
8. "AI写作" after:[DATE]
9. "AI设计" after:[DATE]
10. "prompt工程" after:[DATE]
11. "AI工作流" after:[DATE]
12. "AI生产力" after:[DATE]
13. "AI教程" after:[DATE]
```

### 场景特定查询

```
14. "企业" "AI应用" after:[DATE]
15. "AI" "案例" after:[DATE]
16. "AI" "最佳实践" after:[DATE]
17. "AI插件" after:[DATE]
```

## M. 奇迹层 (Miracle Layer) 搜索查询

### 核心查询（必须执行）

```
1. "AGI" after:[DATE]
2. "通用人工智能" after:[DATE]
3. "AI安全" after:[DATE]
4. "AI伦理" after:[DATE]
5. "AI监管" after:[DATE]
```

### 扩展查询（深度模式）

```
6. "超级智能" after:[DATE]
7. "AI风险" after:[DATE]
8. "AI治理" after:[DATE]
9. "AI政策" after:[DATE]
10. "AI法规" after:[DATE]
11. "AI意识" after:[DATE]
12. "AI未来" after:[DATE]
```

### 专家观点查询

```
13. "AI预测" after:[DATE]
14. "AI威胁" after:[DATE]
15. "AI对齐" after:[DATE]
```

## 查询执行策略

### 标准模式（Standard）
- 每层执行 **5个核心查询**
- 总计：20个查询
- 预计时间：30-45秒

### 深度模式（Deep）
- 每层执行 **核心查询 + 扩展查询**
- E层：13个查询
- S层：12个查询
- U层：13个查询
- M层：12个查询
- 总计：50个查询
- 预计时间：60-90秒

### 快速模式（Brief）
- 每层执行 **3个核心查询**
- 总计：12个查询
- 预计时间：15-20秒

## 查询优化技巧

### 1. 组合关键词
使用多个关键词提高精确度：
```
"AI模型" "发布" "开源"
"融资" "大模型" "亿元"
```

### 2. 排除无关内容
使用 `-` 排除不相关结果：
```
"AI" -"游戏" -"电影"
```

### 3. 精确匹配
使用引号进行精确匹配：
```
"GPT-5"
"Claude 4"
```

### 4. 站点限定
限定特定网站：
```
site:36kr.com "AI融资"
site:jiqizhixin.com "模型发布"
```

## 中文新闻源推荐

### 综合科技媒体
- 36氪 (36kr.com)
- 机器之心 (jiqizhixin.com)
- 量子位 (qbitai.com)
- 新智元 (aiust.com)
- AI科技评论 (leiphone.com/category/ai)

### 专业AI媒体
- 智东西 (zhidx.com)
- 雷峰网AI (leiphone.com)
- InfoQ AI (infoq.cn/ai)

### 财经媒体（创业层）
- 投资界 (pedaily.cn)
- 创业邦 (cyzone.cn)
- 钛媒体 (tmtpost.com)

## 搜索结果处理

### 结果数量
- 每个查询获取 **前10-15个结果**
- 去重后保留最相关的内容

### 时间范围验证
- 确认文章发布日期在指定范围内
- 过滤掉过时内容

### 来源可信度
优先级排序：
1. 官方博客和公告
2. 主流科技媒体
3. 专业AI媒体
4. 财经媒体
5. 其他来源

## 多语言处理

虽然主要使用中文查询，但也会遇到英文内容：

### 英文内容处理
1. 保留原标题（英文）
2. 生成中文摘要
3. 关键点翻译为中文
4. URL保持原样

### 混合内容
- 标题：优先使用中文，英文作为副标题
- 摘要：全部中文
- 关键词：中英文混合标注
