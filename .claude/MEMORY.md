# Keep 项目记忆

## 项目路径
`/Users/fadewalk/Documents/mycode/keep`

## 分支策略

### Remote 仓库
- **origin** - GitHub 个人仓库 (https://github.com/fadewalk/keep)
- **gitee** - Gitee 个人仓库 (https://gitee.com/wyule/keep)
- **upstream** - 官方仓库 (https://github.com/keephq/keep)

### 分支
- **main** - 官方主分支（只同步，不推送）
- **feat/i18n-zh-CN** - 中文翻译分支
- **develop** - 本地开发分支（推送到自己 GitHub 和 Gitee，不推送上游）

### 工作流
1. 从 upstream/main 拉取官方更新到本地 main
2. 从 upstream/feat/i18n-zh-CN 拉取翻译更新
3. 本地 develop 分支开发，同步推送到 GitHub 和 Gitee
4. **不推送 PR 到上游**，保持私有开发

## 已完成的工作

### 1. OPENAI_BASE_URL 私有 LLM 支持
修改了 5 个文件支持私有 LLM（GLM-5/Kimi-2.5/MiniMax-2.5 等 OpenAI 兼容接口）：
- `keep/api/consts.py` - 新增 OPENAI_BASE_URL 常量
- `keep/api/bl/ai_suggestion_bl.py` - AI 告警聚类支持 base_url
- `keep/api/bl/incident_reports.py` - 事件报告支持 base_url
- `keep-ui/app/api/copilotkit/route.ts` - CopilotKit 前端支持 base_url
- `docker-compose.common.yml` - 环境变量透传

### 2. 中文文档翻译
- 翻译了 370 个文档文件到 `docs/zh-Hans/`
- 独立出 `docs-zh/` 目录，包含完整的中文文档结构
- 本地预览：`mintlify dev --port 3003`（目录 docs-zh）

### 3. Mintlify i18n 限制
- 本地 CLI v4.2.446 不支持 `languages` 配置
- 多语言切换功能是 Mintlify Cloud-only 功能
- 本地预览需要在 URL 前加 `/zh-Hans/` 手动访问

## 环境变量（私有 LLM）
```bash
OPENAI_API_KEY=your-private-llm-api-key
OPENAI_BASE_URL=http://your-private-llm-endpoint/v1
OPENAI_MODEL_NAME=glm-5  # 或 kimi-2.5、minimax-2.5 等
```

## 本地开发注意事项
- `.playwright-mcp/` 已加入 .gitignore
- `.claude/` 已加入 git 追踪（设置同步）
- `.cursor/rules/` 已迁移到 `.claude/rules/`
- 开发分支推送地址：origin (GitHub) + gitee (Gitee)

## 常用命令

### 同步上游官方更新
```bash
# 切换到 main，拉取上游更新
git checkout main
git fetch upstream
git merge upstream/main

# 同步到 feat/i18n-zh-CN
git checkout feat/i18n-zh-CN
git merge upstream/feat/i18n-zh-CN

# 推送到自己的远程
git push origin main
git push origin feat/i18n-zh-CN
```

### 开发分支同步
```bash
git checkout develop
git push origin develop  # GitHub
git push gitee develop   # Gitee
```

## 相关文档
- Obsidian 笔记目录：`/Users/fadewalk/Documents/mycode/obsidian/03-work/Keep/`
