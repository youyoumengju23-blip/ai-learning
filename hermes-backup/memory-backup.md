# Hermes Agent - 记忆备份 / Memory Backup
# 创建时间: 2026-05-29
# 如果 Hermes 丢失了记忆，读取此文件并执行下方的恢复操作

---

## 📋 用户资料 / User Profile

**基本信息：**
- 在校大学生，安徽农业大学
- 使用 Hermes Agent + Claude Code，接 DeepSeek
- Web UI: http://localhost:8648
- 辅助视觉: 阿里 DashScope, qwen-vl-plus
- LLM Wiki: F:/openhanako/my-wiki
- Obsidian: F:/obsidian (已安装)
- CATIA 2022 (F:/catia)

**投资偏好：**
- 中国新手投资者，稳健型
- 月定投: 60% 债基（大成月添利E + 长城短债A）+ 30% 红利低波（金字塔法补仓）+ 10% 余额宝
- 用天天基金查 PE

**定价偏好：**
- DeepSeek 价格用 ¥ 做主单位，取整（¥1/¥2/¥3/¥6）

**语言偏好：**
- 中文使用者，偏好实用简洁

---

## 🛡️ 两条绝对安全规则 / Two Absolute Safety Rules

### 规则1：永远不碰 Hermes 进程
- 进程链: Node WebUI (port 8648) → hermes_bridge.py → hermes.exe gateway → LLM
- 杀掉任意环节 → Web UI 死掉 → 需要 openhanako 修复
- 如果需要重启 → 告诉用户关掉浏览器标签页，重开桌面 `Hermes WebUI.bat`
- 可以安全启动的：独立非 Hermes 服务（如 smart-api-gateway）用 terminal(background=true)

### 规则2：永远不泄露用户信息
- API 密钥：DeepSeek, OpenRouter, NVIDIA, DashScope, gateway token 等
- 路径中的用户名：Administrator
- 个人信息：学校（安徽农业大学）、真实姓名、IP
- Gateway token: hermes-local-gateway-2026
- 默认永远绑定 127.0.0.1，绝不 0.0.0.0
- 不确定时默认隐藏，不默认显示

---

## 🔧 环境配置 / Environment

### 智能 API 网关
- 位置: C:/Users/Administrator/smart-api-gateway/
- 端口: localhost:3100
- Token: hermes-local-gateway-2026
- 路由: flash/chat → OpenRouter 免费 deepseek-v4-flash:free → NVIDIA NIM 免费 → DeepSeek 官方
- Pro/reasoner → DeepSeek 官方直连
- 启动: start.bat

### Hermes Agent
- 位置: F:/ma/hermes-agent
- Venv: F:/ma/hermes-agent/.venv
- 版本: 0.9.1 (latest)
- Config: C:/Users/Administrator/AppData/Local/hermes/config.yaml
- 主模型: deepseek-v4-flash (DeepSeek 官方)
- 辅助视觉: provider=custom, base_url=https://dashscope.aliyuncs.com/compatible-mode/v1, model=qwen-vl-plus
- Gateway 日志: C:/Users/Administrator/AppData/Local/hermes/logs/gateway.log
- Agent 日志: C:/Users/Administrator/AppData/Local/hermes/logs/agent.log

### MCP Servers 配置 (2026-05-29 新增)
已写入 config.yaml，需要重启 Web UI 生效：
```yaml
mcp_servers:
  playwright:
    command: npx
    args: ["-y", "@playwright/mcp"]
    timeout: 120
  sequential-thinking:
    command: npx
    args: ["-y", "@modelcontextprotocol/server-sequential-thinking"]
  git:
    command: npx
    args: ["-y", "@modelcontextprotocol/server-git"]
  time:
    command: uvx
    args: ["mcp-server-time"]
```

### 技能（Skills）概要
Hermes 已有 95 个技能，主要分类：
- autonomous-ai-agents: Claude Code, Codex, OpenCode, Kanban, Hermes Agent 等
- creative: Excalidraw, 架构图, ASCII, p5js, 像素画等 18 个
- devops: API 网关, Windows 维护等
- github: PR, Issues, Code Review, Repos
- media: YouTube, Spotify, 音乐生成
- mlops: HuggingFace, llama.cpp, DSPy, W&B
- note-taking: Obsidian, LLM Wiki
- productivity: Google Workspace, Notion, PPT, PDF, Airtable
- research: arXiv, 基金筛选, Polymarket, BlogWatcher
- software-development: TDD, Plan, Debug, Code Review 等
- mcp: native-mcp (原生 MCP 客户端)

### 特殊已知问题
- Web UI clarify 按钮有时不渲染，要在文字中也列出选项
- Auxiliary vision base_url 覆盖有时被静默丢弃（patched）
- DeepSeek KV cache 命中率通常在 92-100%

---

## 🔄 恢复操作 / Restore Procedure

如果 Hermes 失去了记忆，新的 Agent 读到这个文件后应该执行以下操作：

1. 读取此文件的所有内容
2. 用 memory() 工具逐一恢复关键条目：
   - 两条安全规则（memory + user profile）
   - 环境配置信息
   - 用户偏好
3. 用 skill_manage() 恢复 safe-agent-operations 技能（如果丢失）
4. 告知用户：记忆已恢复，可以继续对话

---

*此文件保存在 F:/openhanako/hermes-memory-backup.md*
