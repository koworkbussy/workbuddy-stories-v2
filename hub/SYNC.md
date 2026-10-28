# 跨端同步协议 · SYNC.md

> 适用：所有登录同一账号（eef38531-9dc0-46a0-9f3e-d7643add7bb2）的终端 —— 电脑端、手机端、平板。
> 目标：任何终端都能在同一页面看到最新状态，且换设备不丢上下文。

## 一、唯一共享通道

| 内容 | 位置 | 读取方式 |
|---|---|---|
| 总控台页面 | `https://koworkbussy.github.io/workbuddy-stories-v2/hub/` | 浏览器直接打开，任何设备 |
| 设备状态文件 | `hub/sync/state.json` | 页面自动读取，每 45 秒刷新 |
| 项目看板 | `PROJECTS.md`（电脑端 Claw 目录） | 手动同步到本仓库 |
| 日报文件 | 电脑端桌面 `Email_Daily_YYYYMMDD.html` | 待上云（见"四"） |

仓库：`koworkbussy/workbuddy-stories-v2`（公开，分支 main）
Token：`~/.workbuddy/github-token`（电脑端已配置）

## 二、state.json 字段约定

```json
{
  "updatedAt": "ISO 时间",
  "updatedBy": "设备名 · 主机",
  "devices": [
    { "name": "手机端", "status": "working|online|idle", "lastSeen": "ISO 时间", "task": "当前在做什么" }
  ],
  "projects": [ { "name": "项目名", "state": "进行中|待部署|已完成|暂停", "next": "下一步" } ],
  "reports": { "latest": "文件名", "location": "存放位置", "pending": "待办" }
}
```

规则：
1. 只改自己那条 `devices` 记录 + `updatedAt` / `updatedBy`，不要动别人的记录
2. 每次会话结束前更新一次；任务变化时也更新
3. **读取无需权限**（公开仓库），**写入需要 token**——没有 token 的终端，把内容发给有 token 的终端代写

## 三、各终端操作口令

**电脑端（有 token）：**
> "更新同步状态：任务=xxx" → 改写 `Claw/hub/sync/state.json` 并 push 到 `hub/sync/state.json`

**手机端（无 token）：**
- 看：直接打开总控台链接
- 写：把要在页面上显示的任务内容发到电脑端（或微信转发），由电脑端写入
- 产出：手机端部署的页面链接，加进总控台的对应项目卡片

## 四、待打通（按优先级）

1. **日报上云**：生成 `Email_Daily_*.html` 后自动推送到 `reports/`，手机可看历史日报
2. **看板上云**：PROJECTS.md 推送为 `PROJECTS.md`，页面直接渲染
3. **记忆同步**：会话开始拉取、结束推送 MEMORY.md（需注意隐私，公开仓库只放项目信息）

## 五、不要放进来的内容

公开仓库禁止写入：邮箱内容、账号密码、个人财务信息、浏览器登录态、其他隐私数据。
`state.json` 只写"在做什么"，不写"具体内容"。
