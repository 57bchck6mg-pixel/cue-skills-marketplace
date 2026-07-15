# Cue Skills Marketplace

每个 Cue 搭子独立打包为一个 Agent Skill，可单独安装到 Claude Code / Codex CLI / Gemini CLI / Cursor 等支持 SKILL.md 标准的 AI 编码工具。

## 目录结构

```
cue-skills-marketplace/
├── zh/    # 国内中文版 — 面向 A 股/港股/中资企业场景
├── en/    # 海外英文版 — 面向全球市场场景（出海推广）
```

部分搭子双目录都有一份（中英双语），部分仅在一侧。

## 安装

```bash
# 方式 1：npx skills
npx skills add 57bchck6mg-pixel/cue-skills-marketplace --skill zh/<搭子名>

# 方式 2：直接 clone + 复制
git clone https://github.com/57bchck6mg-pixel/cue-skills-marketplace.git
cp -r cue-skills-marketplace/zh/<搭子名> ~/.claude/skills/
```

## 国内版（zh/）

| 搭子 | 场景 | 说明 |
|------|------|------|
| [对公授信预尽调](./zh/对公授信预尽调/SKILL.md) | 信贷尽调 | 授信审批视角的企业公开数据交叉尽调，覆盖主体真实性、股权穿透、关联方、司法合规、经营持续性、偿债能力 |

## 海外版（en/）

| 搭子 | 场景 | 说明 |
|------|------|------|
| — | — | 待上架 |

## 前置

- Cue API key（`~/.cue/config.json` 或 `CUE_API_KEY` env）
- `git` + `python3`
- 消耗 credits（新账号注册送 50 + 每天 10 免费积分）
