# AI 资讯速览 · AI News Archive

> 每日自动聚合的 AI / 计算机视觉资讯档案库：论文、模型、产品、技巧与行业动态，按周滚动存档。

数据源自 [AI HOT](https://aihot.virxact.com) 中文 AI 资讯聚合平台，经关键词筛选后生成**时间线 + 卡片**式速览页面。

> **说明**：原站内「视觉目标跟踪（VOT）」专栏已拆分为独立项目
> [TAI-GG/vot-papers-archive](https://TAI-GG.github.io/vot-papers-archive/)，
> 本仓库 `/tracking/` 路径保留自动跳转页，旧链接不会失效。

---

## 🔗 在线访问

| 页面 | 地址 | 说明 |
|------|------|------|
| 本周速览 | https://TAI-GG.github.io/cv-papers-archive/ | 最新一周动态（`index.html`） |
| 上周存档 | https://TAI-GG.github.io/cv-papers-archive/archive/last-week.html | 上一周内容 |
| 历史周快照 | 上周页底部列表 | 更早的每周存档，互不覆盖 |
| 🎯 VOT 专栏（独立站点） | https://TAI-GG.github.io/vot-papers-archive/ | 视觉目标跟踪中英双语论文专栏 |

页面顶部 `.nav-bar` 提供导航，可在「本周 / 上周 / VOT 目标跟踪专栏」之间切换。

---

## 📁 仓库结构

```
cv-papers-archive/
├── index.html              # 本周动态（自动覆盖更新）
├── archive/
│   ├── last-week.html      # 上周存档
│   └── YYYY-MM-DD.html     # 历史周快照（每周滚动新增，互不覆盖）
├── tracking/
│   └── index.html          # 跳转页：VOT 专栏已迁至独立站点
├── README.md               # 本说明
└── build_archive.py        # 构建与推送脚本
```

---

## 🧠 内容筛选逻辑

从 AI HOT 全量条目（约 2000+ 条 / 周）中筛选视觉与多模态相关内容，规则如下：

1. **排除词（CV_NO）**：如 `kyber`、`eu council`、`us military`、`cursor`、`notebooklm` 等非相关主题，命中即丢弃；
2. **精确命中（CV_OK）**：如 `video generation`、`one-step visual`、`音乐伴舞`、`数字分身` 等，命中即收录；
3. **关键词分组（CV_KW）**：视觉 / 视频 / 图像 / 3D / 扩散 / 生成 / 分割 / 检测 / VLM / 机器人 / 自动驾驶 / 卫星 / 数字人 / 多模态 —— 跨 **≥ 2 个分组** 命中即收录。

最终按发布时间倒序排列，去重后展示。

---

## ✨ 页面特性

- **时间线布局**：左侧时间轴 + 右侧内容卡片，按日期自动分组；
- **富信息卡片**：标题（外链新标签页打开原文）、类型标签（论文 / 模型 / 产品 / 技巧 / 行业）、来源徽章、相对时间、≤ 200 字摘要；
- **周次导航栏**：顶部 sticky 导航，支持历史周切换；
- **响应式设计**：移动端自适应，单列布局；
- **淡入动画**：卡片随滚动逐个渐显。

---

## ⚙️ 更新机制

- **频率**：每日自动构建与推送；
- **流程**：拉取最新数据 → 筛选 → 按真实日期切分为「近 7 天 / 7–14 天」→ 生成 `index.html` 与 `archive/last-week.html` → 写入 `/tracking/` 跳转页 → 推送；
- **推送方式**：`git fetch` + `reset --hard` 同步现有仓库 → 覆盖生成文件 → 普通 `commit` + `push`（**不 force**，保留全部历史存档）。

---

## 🛠️ 本地构建

```bash
python build_archive.py
```

前置条件：
- Windows 凭据管理器已保存 GitHub PAT（目标 `git:https://github.com`，类型 Generic，需 `repo` 权限）；
- 脚本通过 `ctypes` 读取该 PAT 完成鉴权推送（凭据不落盘、不打印）；
- 推送目标仓库：`TAI-GG/cv-papers-archive`；
- 网络需可经本地出口代理访问 GitHub（脚本已内置代理注入）。

---

## ⚠️ 声明

- 全部内容版权归原作者 / 原发布平台所有，本仓库仅作**聚合索引**，所有链接均指向原始出处；
- 数据由自动化脚本筛选，可能存在漏判 / 误判，仅供参考；
- 早期周次数据因 API 缓存窗口限制无法回溯，存档自 `2026-06-30` 起完整保留。
