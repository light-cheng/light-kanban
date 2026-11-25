# kanban-worker（Light-Kanban 官方内置 Worker Skill）

> English summary: `skills/kanban-worker/` is the authoritative first-party
> `kanban-worker` Skill maintained directly in `light-cheng/light-kanban` and
> verified on every commit by `make check` (`make check-skill`).

## 这是什么

`skills/kanban-worker/` 是 Light-Kanban 官方第一方 Worker Skill，直接由本仓库（`light-cheng/light-kanban`）作为唯一行为权威维护与发布：定时唤醒的自主 Agent 安装一次即可每次认领/续做至多一张看板任务，并在完成后交回人类确认或上报具体阻碍。

## 安装方式

### 方式一（推荐）：通过 `npx skills` 直接从本仓库安装

```bash
npx skills add light-cheng/light-kanban \
  --skill kanban-worker \
  --yes \
  --copy \
  --agent '*'
```

### 方式二：手动复制目录（离线 / 无 `npx`）

把整个包目录（包含 `SKILL.md`、`agents/openai.yaml`、`references/api.md`）复制到你的 Agent Host 识别的 skills 目录，例如：

```bash
mkdir -p ~/.agents/skills
cp -R skills/kanban-worker ~/.agents/skills/kanban-worker
```

然后刷新或重启 Agent Host，确认技能列表中已发现 `kanban-worker`。

## 校验与测试

本技能自带零第三方依赖的契约与行为测试套件（覆盖正向契约与 6 类对抗性负例变体），已接入 `make check` 与 GitHub Actions CI：

```bash
make check-skill
# 等价于：
python3 -m unittest discover -s skills/kanban-worker/tests -p "test_*.py"
```
