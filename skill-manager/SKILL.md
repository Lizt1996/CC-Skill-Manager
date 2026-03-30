---
name: skill-manager
description: Use when setting up Claude Code skills on a new machine, syncing skills across machines, or restoring the full skill environment to avoid missing-skill disruptions during development
---

# Skill Manager

在新机器上一键恢复完整 skill 环境。当前机器的完整 skill 清单见 `skill-registry`。

---

## 新机器初始化步骤

### 第一步：读取清单并对比本地

```bash
# 查看目标清单
cat ~/.claude/skills/skill-registry/registry.md

# 找出清单中有、但本地缺失的 skill
comm -13 <(ls ~/.claude/skills/ | sort) \
         <(grep '^| `' ~/.claude/skills/skill-registry/registry.md | sed 's/^| `\([^`]*\)`.*/\1/' | sort)
```

### 第二步：安装缺失的 skill

**官方 skill（`anthropics/skills`）：**
```bash
git clone https://github.com/anthropics/skills.git /tmp/anthropic-skills
cp -r /tmp/anthropic-skills/skills/* ~/.claude/skills/
```

**方法论框架（`obra/superpowers`）：**
```bash
git clone https://github.com/obra/superpowers.git /tmp/superpowers
cp -r /tmp/superpowers/skills/* ~/.claude/skills/
```

**自建 skill：** 参考 `skill-registry` 中"本地自建"部分，手动创建或从备份复制。

### 第三步：验证

```bash
ls ~/.claude/skills/ | wc -l   # 应与 skill-registry 中数量一致
```

重新打开 Claude Code session 后生效。

---

## 网络问题处理

遇到 `schannel`、`timed out`、`unable to access` 等错误时，询问用户本地代理端口：

```bash
git -c http.proxy=http://127.0.0.1:<端口> -c http.sslVerify=false clone <url> <目标>
```

---

## 注意事项

- 全局 skill 对所有 project 可用，路径：`~/.claude/skills/`
- 项目级 skill 仅当前 project 可用，路径：`.claude/skills/`
- 同名时项目级优先于全局
- 安装或卸载 skill 后，**更新 `skill-registry`** 并重开 session
