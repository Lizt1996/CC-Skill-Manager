---
name: skill-registry
description: Use when a new skill is installed or removed — update registry.md to keep an accurate record of all globally installed skills on this machine
---

# Skill Registry

已安装 skill 的完整清单记录在同目录的 `registry.md` 中。

**每次安装或卸载 skill 后，更新 `registry.md`：**
1. 在对应来源的表格中增加或删除一行
2. 填写 skill 名称和简介
3. 在更新记录表中添加一条变更日志

---

## 查看当前清单

```bash
cat ~/.claude/skills/skill-registry/registry.md
```

## 验证本地与清单是否一致

```bash
comm -23 <(ls ~/.claude/skills/ | sort) \
         <(grep '^| `' ~/.claude/skills/skill-registry/registry.md | sed 's/^| `\([^`]*\)`.*/\1/' | sort)
```

输出的内容即为"本地有但清单未记录"的 skill。
