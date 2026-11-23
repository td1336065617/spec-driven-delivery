# 本机落地参数（不入库）

> 本文件被 `.gitignore` 排除。用途：`SKILL.md §11` 只写形状，具体值写这里。
> 换机器：复制 `local-env.example.md` 为本文件后按实际填写。

## 工作区
- 根：`<workspace>`
- 仓库：acmer_qq_group_bot / astrbot_plugin_qq_group_manager / astrbot_plugin_nickname_registry / astrbot_plugin_onebot_login_guard / menu_navigation / 来只清楚bot
- Python：`<workspace>/.venv/bin/python`（3.12，裸 `python` 不可用）

## 项目级正本（本 skill 的上游）
- `docs/插件开发规范.md`（条款 + CASE-01…CASE-20 + 回填机制）
- `docs/插件开发教训-20260927.md`（事故时间线）
- `acmer_qq_group_bot/docs/*.md`（各主题设计/实现文档）

## 打卡插件（acmer_qq_group_bot）
- 仓库：`<workspace>/acmer_qq_group_bot`
- 本地实例：`~/.venv/bin/astrbot run`（WebUI 6185），日志 `/home/<user>/astrbot-run-<version>.log`
- 线上：SSH 别名 `<alias>` → `<remote-root>`，systemd 单元 `astrbot.service`
- 运行库：`<remote-root>/data/plugin_data/acmer_qq_group_bot/acmer_store.db`
- 图片产物：`<remote-root>/data/temp/media_image_*`

## 子代理路由
- 本会话未记录 allowlist（`list_subagent_models` 无 "Authorized child routes" 段）→ 子代理继承父路由，不写 `route:` 行。
