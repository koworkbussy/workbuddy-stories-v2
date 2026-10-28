# 项目看板 · PROJECTS.md

> ⚠️ 本文件已降级为「执行侧备注」。
> **项目清单 / 链接 / 状态的唯一真相源是 `hub/data/resources.json`**（托管在 GitHub，所有终端共用）。
> 两者冲突时，以 resources.json 为准；本文件只记录电脑端的执行细节。

> 每次会话结束前由 WorkBuddy 更新状态。约定状态标签：`进行中` / `待部署` / `已完成` / `暂停`。
> 创建：2026-10-27 ｜ 最近更新：2026-10-28

## 🔴 进行中 / 待部署（需要收尾）

| 项目 | 状态 | 下一步 | 挂起自 |
|---|---|---|---|
| 儿童故事 V2（元宝版） | 进行中 | 第 2 集《魔法充电》部署；第 3–5 集开发 | 2026-07-27 |
| 老王和沃克巴迪 V3（9 集） | 待部署 | deploy-1~9 部署到 CloudStudio，分发链接 | 2026-07-31 |
| AI 重点资讯总结 | 暂停 | 决定：恢复运行或删除 | 2026-07 |

## 🟢 已完成（维护即可）

| 项目 | 完成时间 | 备注 |
|---|---|---|
| 沃克巴迪儿童故事集 V1（5 篇+序曲+主题曲） | 2026-07-26 | 部署链接见 Claw/MEMORY.md |
| 老李和沃克巴迪 · 老年人互动故事（8 篇） | 2026-07-26 | 合集+8 链接已归档 |
| 丑小鸭蜕变记（V1 手机端 + V2 电脑端） | 2026-07-29 | 双版本并存 |
| 老王系列 V1（8 集，AgentOS） | 2026-07-30 | 已上线 |
| MSN 邮箱日报自动化 | 2026-07-28 | 持续运行中，详见下方"日常机制" |
| WorkBuddy 升级 5.3.11 → 5.6.2 | 2026-09-24 | 备份：workbuddy-backup-5.3.11-20260924 |

## ⚙️ 日常机制（2026-10-27 建立｜2026-10-28 全部上云）

**跨端总控台（任何设备可访问）：** https://koworkbussy.github.io/workbuddy-stories-v2/hub/
本地源文件：`C:/Users/koralo/WorkBuddy/Claw/hub/index.html`

**云端数据（唯一口径，所有终端只读同一份）：**

| 文件 | 内容 | 地址 |
|---|---|---|
| `hub/data/resources.json` | 项目 / 链接 / 状态（SSOT） | raw.githubusercontent.com/…/hub/data/resources.json |
| `hub/data/progress.json` | 进展时间线 | …/hub/data/progress.json |
| `hub/sync/state.json` | 设备状态 + 任务信箱 | …/hub/sync/state.json |
| `reports/index.json` | 日报归档索引（26 期） | …/reports/index.json |
| `hub/data/PROJECTS.md` | 本看板云端副本 | …/hub/data/PROJECTS.md |

**唯一写入口：** `C:/Users/koralo/WorkBuddy/2026-07-28-08-50-34/cloudsync.py`
```
python cloudsync.py reports            # 日报上云 + 重建索引（日报脚本已自动调用）
python cloudsync.py projects           # 推送本看板
python cloudsync.py progress "内容" --tag 标签   # 追加进展时间线
python cloudsync.py push <远端路径> <本地文件> --msg 说明
```

| 时间 | 任务 | 说明 |
|---|---|---|
| 每天 09:30 | 晨间站会 | 读云端数据：任务信箱 + 昨日待办 + 项目待办 + 今日建议 |
| 每天 10:00 | MSN 邮箱日报 | 生成 Email_Daily_YYYYMMDD.html 并**自动上云** |
| 每天 21:00 | 日报看门狗 | 本地与云端双查，缺失则补跑/补推 |
| 每周日 20:00 | 项目周报 | 云端口径：产出 + 挂起 + 自动化健康度 |

## 📌 工作规范（沿用既有原则）

- 所有版本保留，不删除任何产出；重要项目立即写入本看板
- 项目统一放在 `C:/Users/koralo/WorkBuddy/Claw/`，部署链接记录在 Claw/MEMORY.md
- GitHub 备份：koworkbussy 账号；部署：CloudStudio
- 每次会话结束：更新本看板状态
