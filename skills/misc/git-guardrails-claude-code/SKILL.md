---
name: git-guardrails-claude-code
description: 配置 Claude Code 钩子，在执行前拦截危险的 git 命令（push、reset --hard、clean、branch -D 等）。当用户希望阻止破坏性 git 操作、添加 git 安全钩子或拦截 git push/reset 时使用。
---

# 设置 Git 防护栏

配置一个 PreToolUse 钩子，用于拦截并阻止危险的 git 命令，避免 Claude 执行它们。

## 哪些操作会被拦截

- `git push`（包括 `--force` 在内的所有变体）
- `git reset --hard`
- `git clean -f` / `git clean -fd`
- `git branch -D`
- `git checkout .` / `git restore .`

被拦截时，Claude 会收到一条提示，告知其无权执行这些命令。

## 操作步骤

### 1. 询问作用范围

询问用户：仅针对**当前项目**（`.claude/settings.json`）安装，还是针对**所有项目**（`~/.claude/settings.json`）全局安装？

### 2. 复制钩子脚本

随附脚本位于：[scripts/block-dangerous-git.sh](scripts/block-dangerous-git.sh)

根据作用范围复制到目标位置：

- **项目级**：`.claude/hooks/block-dangerous-git.sh`
- **全局**：`~/.claude/hooks/block-dangerous-git.sh`

使用 `chmod +x` 赋予其可执行权限。

### 3. 将钩子添加到设置

添加到对应的设置文件中：

**项目级**（`.claude/settings.json`）：

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "\"$CLAUDE_PROJECT_DIR\"/.claude/hooks/block-dangerous-git.sh"
          }
        ]
      }
    ]
  }
}
```

**全局**（`~/.claude/settings.json`）：

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "~/.claude/hooks/block-dangerous-git.sh"
          }
        ]
      }
    ]
  }
}
```

如果设置文件已存在，请将钩子合并到现有的 `hooks.PreToolUse` 数组中，不要覆盖其他设置。

### 4. 询问是否需要自定义

询问用户是否希望在拦截列表中增加或移除某些模式，并据此编辑已复制的脚本。

### 5. 验证

运行一个快速测试：

```bash
echo '{"tool_input":{"command":"git push origin main"}}' | <path-to-script>
```

应返回退出码 2，并向 stderr 输出一条 BLOCKED 消息。
