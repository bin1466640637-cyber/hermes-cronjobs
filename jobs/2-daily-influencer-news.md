# 任务2：AI大佬言论追踪

## 基本信息

| 项目 | 内容 |
|------|------|
| Job ID | `bba9d0ee2ef2` |
| 任务名 | 每日科技/AI大佬言论追踪 |
| 推送时间 | 每天 09:00 (CRON: `0 9 * * *`) |
| 推送渠道 | WeChat |
| 状态 | 永久循环 |

## 追踪人物（11位）

| 序号 | 人物 | 英文名 | 身份 |
|------|------|--------|------|
| 1 | 马斯克 | Elon Musk | 特斯拉/SpaceX/X AI CEO |
| 2 | 黄仁勋 | Jensen Huang | 英伟达 CEO |
| 3 | 纳瓦尔 | Naval Ravikant | AngelList创始人 |
| 4 | 孙宇晨 | - | Tron/HTX创始人 |
| 5 | 山姆·奥特曼 | Sam Altman | OpenAI CEO |
| 6 | 德米斯·哈萨比斯 | Demis Hassabis | Google DeepMind CEO |
| 7 | 吴恩达 | Andrew Ng | Coursera/AI Fund创始人 |
| 8 | 杰弗里·辛顿 | Geoffrey Hinton | AI教父/TensorFlow奠基人 |
| 9 | 萨提亚·纳德拉 | Satya Nadella | 微软 CEO |
| 10 | 刘小排 | - | 国内AI编程KOL |
| 11 | 段永平 | - | OPPO/VIVO/步步高创始人，价值投资者 |

## 信息来源（必须验证）

### 第1优先级：官方渠道
- 个人推特/X
- 官方博客
- 公开演讲/峰会

### 第2优先级：权威媒体
- 路透/彭博/华尔街日报
- TechCrunch/The Information

### 第3优先级：专业财经
- 巴伦周刊/福布斯/财富

### 第4优先级：中文媒体
- 36氪/虎嗅/晚点
- 极客公园/雪球

## 验证要求

1. **每条内容必须注明来源**，来源不明确的不推送
2. **同一事件多方来源交叉验证**后再推送
3. **言论需注明场合**（采访/播客/演讲/推特/访谈）
4. **引用原文关键语句**，不扭曲原意

## 去重机制

读取 `~/.hermes/scripts/influencer_tracker.json` 获取已发送内容列表。

- 只有真正新的内容才加入本次摘要
- 本次发送的所有内容更新到 sent 列表
- 保留最近 80 条，多余的删除

## GitHub Trending 模块（详细）

### 抓取流程
1. 访问 `https://github.com/trending` 获取当日 trending 仓库
2. 筛选 AI Skill/Agent 相关仓库（关键词：AI、agent、skill、tool、framework、memory、LLM）
3. 对每个候选仓库：
   - 调用 GitHub API 获取精确 star 数量和语言
   - 获取 README 第一屏内容
   - 查找安装命令（pip install / npm install 等）

### 输出格式
```
🤖 GitHub AI Skill/Agent 今日 TOP10

1. **[Owner/RepoName]**
   ⭐ 123,456 | 🐍 Python
   📝 一句话说明
   🔗 https://github.com/Owner/RepoName
   📦 安装: `pip install xxx`
   📖 详细说明：2-3句描述功能、特点和适用场景

2. ...
```

### TOP10 仓库详情（2026-06-06 示例）

#### 1. NousResearch/hermes-agent ⭐183K 🐍Python
🔗 https://github.com/NousResearch/hermes-agent
📦 安装: `pip install -e .`
📖 开源AI Agent框架，支持200+模型（Claude/GPT/Llama等），提供完整终端界面（TUI），支持多行编辑、斜杠命令自动补全、会话历史、打断重定向。内置工具：文件操作、代码执行、Web搜索、图像生成等。Windows原生支持，适合构建复杂AI工作流和多Agent协作系统。

#### 2. affaan-m/ECC ⭐208K 🐍JavaScript
🔗 https://github.com/affaan-m/ECC
📦 安装: `npm install`（支持pnpm/yarn/bun）
📖 通用Agent性能优化系统，支持Claude Code/Codex/Cursor/OpenCode/Gemini等主流AI编程工具。提供Skills/Instincts/Memory/Security模块，跨Harness的Agent工作流编排。

#### 3. PaddlePaddle/PaddleOCR ⭐80K 🐍Python
🔗 https://github.com/PaddlePaddle/PaddleOCR
📦 安装: `pip install paddleocr`
📖 百度飞桨OCR工具包，支持文本/表格/印章识别，将PDF/图片转结构化数据，填补LLM无法直接读取扫描件的Gap。

#### 4. MemPalace/mempalace ⭐53K 🐍Python
🔗 https://github.com/MemPalace/mempalace
📦 安装: `pip install mempalace`
📖 本地优先AI记忆系统，LongMemEval上达到96.6% R@5，无需API调用。兼容MCP协议，解决Agent长期记忆丢失问题。

#### 5. CopilotKit/CopilotKit ⭐32K 🐍TypeScript
🔗 https://github.com/CopilotKit/CopilotKit
📦 安装: `npx copilotkit@latest create -f <framework>`
📖 AI Agents前端技术栈，发起AG-UI Protocol。提供生成式UI、共享状态、人在回路工作流，React/Angular/Vue/React Native全覆盖。

#### 6. mvanhorn/last30days-skill ⭐28K 🐍Python
🔗 https://github.com/mvanhorn/last30days-skill
📦 安装: `/plugin install mvanhorn/last30days-skill`
📖 AI Agent Skill，自动综合研究Reddit/HN/Polymarket/X/YouTube等平台话题，输出有据可查的结构化摘要。

#### 7. lfnovo/open-notebook ⭐26K 🐍TypeScript
🔗 https://github.com/lfnovo/open-notebook
📦 参考: docs/1-INSTALLATION/index.md
📖 开源版Google Notebook LM，支持多格式导入、语音转文字、AI问答，可自托管，数据完全私有。

#### 8. Panniantong/Agent-Reach ⭐21K 🐍Python
🔗 https://github.com/Panniantong/Agent-Reach
📦 安装: `pip install agent-reach`
📖 让AI Agent"看见"整个互联网——Twitter/Reddit/YouTube/GitHub/小红书/B站，一个CLI搞定，零API费用。

#### 9. chopratejas/headroom ⭐14K 🐍Python
🔗 https://github.com/chopratejas/headroom
📦 安装: `pip install "headroom-ai[all]"`
📖 LLM输入压缩器，压缩tool outputs/logs/RAG chunks 60-95%，同时保持输出质量。兼容主流Agent。

#### 10. NVIDIA/cosmos ⭐9K 🐍Jupyter
🔗 https://github.com/NVIDIA/cosmos
📦 安装: `pip install --torch-backend=auto`
📖 NVIDIA开源世界模型平台，面向机器人/自动驾驶/智能基础设施的Physical AI开发者。

## AI圈重要新闻模块

搜索当日最重要的 AI 新闻：
- 大模型进展（GPT-5、Claude 4、Gemini 2等）
- AI 产品发布
- AI 公司重大战略
- AI 监管政策

信息来源：官方公告 + 权威科技媒体

## 输出格式

```
🗣️ 今日科技/AI大佬言论追踪

🚀 马斯克
• [言论标题]（来源，场合）- 核心观点 + 原文引用

🔥 黄仁勋
• ...

...

💰 段永平
• ...

---
已发送 {N} 条新内容

🤖 GitHub AI Skill/Agent 今日 TOP10
[详细仓库列表]

---
📰 AI圈今日重要新闻
• [新闻标题]（来源）- 核心要点
```

## 推送标准

### 应推送的内容 ✅
- 有深度的观点：AI发展、创业建议、财富观念、技术趋势、投资逻辑
- 重大 announcements
- 管理层重要讲话

### 不推送的内容 ❌
- 无关痛痒的日常推文
- 照片分享
- 来源不明的传闻

## 任务状态

- 创建时间：2026-06-06
- 上次执行：2026-06-06 09:04 (状态: OK)
- 下次执行：2026-06-07 09:00
