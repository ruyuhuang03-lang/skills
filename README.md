# Skills

这里收集我为 Codex 创建的可复用 Skills。每个一级子目录都是一个独立、可安装的 Skill。

## Skills 目录

| Skill | 用途 |
| --- | --- |
| [`project-status-manager`](./project-status-manager/) | 通过 `PROJECT_STATUS.md` 维护跨对话共享的项目目标、进度、决策、风险与交接信息。 |
| [`github-open-source-evaluator`](./github-open-source-evaluator/) | 在编码前调研 GitHub 开源候选，判断维护状态、部署难度、复用价值、二开适配度，并给出技术路线与最简 MVP。 |

## 安装

先克隆本仓库：

```bash
mkdir -p ~/.codex/skill-repos ~/.codex/skills
git clone https://github.com/ruyuhuang03-lang/skills.git \
  ~/.codex/skill-repos/ruyuhuang03-skills
```

再按需把单个 Skill 链接到 Codex Skills 目录：

```bash
ln -s ~/.codex/skill-repos/ruyuhuang03-skills/project-status-manager \
  ~/.codex/skills/project-status-manager

ln -s ~/.codex/skill-repos/ruyuhuang03-skills/github-open-source-evaluator \
  ~/.codex/skills/github-open-source-evaluator
```

如果目标路径已经存在，请先保留现有目录，并改用复制或手动合并；不要直接覆盖。

## 更新

```bash
git -C ~/.codex/skill-repos/ruyuhuang03-skills pull
```

使用符号链接安装时，仓库更新后 Skills 会同步更新。

## 使用示例

```text
使用 $project-status-manager 初始化当前项目的状态跟踪。
```

```text
使用 $github-open-source-evaluator，帮我调研适合开发 XXX 的 GitHub 开源项目。
```

## 仓库结构

```text
skills/
├── README.md
├── project-status-manager/
│   ├── SKILL.md
│   └── agents/
│       └── openai.yaml
└── github-open-source-evaluator/
    ├── SKILL.md
    └── agents/
        └── openai.yaml
```

## 许可

本仓库目前未附带开源许可证。未经许可，默认版权仍由仓库所有者保留。
