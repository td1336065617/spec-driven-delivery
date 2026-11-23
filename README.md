# spec-driven-delivery

一套给 AI 编码代理（也给人）用的**开发流程规范**：把"文档即规格、先量后画、真实样本回归、独立审计、部署≠生效"这些用事故换来的规则，写成带出口门槛（DoD）和可执行命令的分阶段流程。

它不是通用模板，是从真实线上事故里反推出来的——每条规则背后都能指到一个具体的失效案例。

## 内容

| 文件 | 作用 |
|---|---|
| `SKILL.md` | 流程主干：8 个阶段 + 每阶段出口门槛 + 防错清单 + 门禁命令 + 反模式表 + 理论映射 |
| `references/failure-catalog.md` | 91 条真实失败案例，13 个类别，每条含「症状 → 根因 → 防线 → 证据」 |
| `references/local-env.example.md` | 本机参数样例（仓库路径、部署别名、数据位置）——复制为 `local-env.md` 后按实际填写，该文件不入库 |

## 安装

作为 **DeepSeek Harness / Claude Code 的技能**使用，克隆到用户级技能目录即可对**所有项目、所有会话**生效：

```bash
git clone https://github.com/<you>/spec-driven-delivery.git ~/.agents/skills/spec-driven-delivery
cp ~/.agents/skills/spec-driven-delivery/references/local-env.example.md \
   ~/.agents/skills/spec-driven-delivery/references/local-env.md
# 然后按实际填写 local-env.md
```

项目级安装（只对某个仓库生效）则克隆到 `<repo>/.agents/skills/spec-driven-delivery`。

加载方式：会话里说"按 spec-driven-delivery 来"，或由代理按 `description` 自动匹配（动手改代码之前）。

## 三个不可违背的原则

1. **文档即规格，但文档本身要经验证**——文档写错按文档 bug 处理；测试全绿不是正确性的证明。
2. **先量后画**——尺寸/高度/容量必须来自实际跑一遍，禁止把另一条管线的估算值拿来用。
3. **部署 ≠ 生效**——必须验日志版本号、进程启动时间、真实输入复现的实物。

## 三个最贵的案例（详见案例库）

- **身份字段双值**：一个字段同时是适配器名与 ID，ACL 严格比对 → 93.4% 数据 44 天不可召回，**零报错**。
- **重启清空进程内平台态**：13/17 个群收不到提醒，而"版本号 + 启动时间 + 真实输入"三件套**全部通过**——重启本身才是故障源。
- **卡高用错来源**：复用另一条渲染管线的估算值 → 底部信息压住页脚；第一版修了表象（折行），第二版才修来源。

## 适用性

规范本身与语言/框架无关；示例命令以 Python + systemd 为主（`pytest`、`rsync/tar`、`systemctl`）。在 Node/Go/Java 项目里沿用同一套阶段与门槛，只需替换 §8 的门禁命令。

## 许可

MIT
