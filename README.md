# Project Status Manager

一个用于 Codex 的项目状态管理 skill。它通过维护项目根目录中的 `PROJECT_STATUS.md`，让不同对话能够快速了解项目目标、进度、关键决策、风险和下一步行动。

## 功能

- 初始化结构清晰的 `PROJECT_STATUS.md`
- 读取并概括项目当前状态
- 在完成有效工作后更新进度、决策、阻塞项和后续行动
- 为跨对话协作生成简洁的交接摘要
- 在并发修改存在冲突时避免直接覆盖，并返回可供合并的 handoff

该 skill 会区分两类信息：

- `AGENTS.md`：存放 Codex 应遵循的长期工作规则
- `PROJECT_STATUS.md`：存放项目当前的事实状态

## 安装

将仓库克隆到 Codex skills 目录：

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/ruyuhuang03-lang/project-status-manager.git \
  ~/.codex/skills/project-status-manager
```

如果已经安装，可以在 skill 目录中拉取最新版本：

```bash
git -C ~/.codex/skills/project-status-manager pull
```

## 使用示例

在 Codex 中使用 `$project-status-manager`，例如：

```text
使用 $project-status-manager 初始化当前项目的状态跟踪。
```

```text
使用 $project-status-manager 总结当前项目状态，并记录这次完成的工作。
```

```text
使用 $project-status-manager 为下一个对话生成交接摘要。
```

## 工作原则

- 修改前先确认准确的项目根目录
- 保留已有的用户内容，只更新与当前任务相关的部分
- 只记录已验证的结果、明确决策、真实阻塞和具体下一步
- 不保存完整聊天记录、凭据、令牌或其他敏感信息
- 编辑前重新读取最新状态，避免覆盖其他对话的修改

## 仓库结构

```text
project-status-manager/
├── SKILL.md             # Skill 的核心指令
├── README.md            # 项目说明与安装方法
└── agents/
    └── openai.yaml      # Codex 界面元数据与默认提示词
```

## 许可

本仓库目前未附带开源许可证。未经许可，默认版权仍由仓库所有者保留。
