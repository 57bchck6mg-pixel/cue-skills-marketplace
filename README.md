# Cue Skills Marketplace

每个目录是一个独立 Cue 搭子的 Agent Skill（`<搭子名>/SKILL.md`），可单独安装到 Claude Code / Codex CLI / Gemini CLI / Cursor 等支持 SKILL.md 标准的 AI 编码工具。

## 安装方式

### 方式 1：npx skills（推荐）

```bash
npx skills add 57bchck6mg-pixel/cue-skills-marketplace --skill <搭子目录名>
```

### 方式 2：直接 clone

```bash
git clone https://github.com/57bchck6mg-pixel/cue-skills-marketplace.git
cp -r cue-skills-marketplace/<搭子目录名> ~/.claude/skills/
```

## 已上架搭子

| 搭子 | 场景 | 说明 |
|------|------|------|
| [对公授信预尽调](./对公授信预尽调/SKILL.md) | 信贷尽调 | 授信审批视角的企业公开数据交叉尽调，覆盖主体真实性、股权穿透、关联方、司法合规、经营持续性、偿债能力 |

## 前置

- Cue API key（`~/.cue/config.json` 或 `CUE_API_KEY` env）
- `git` + `python3`
- 消耗 credits（新账号注册送 50 + 每天 10 免费积分）
