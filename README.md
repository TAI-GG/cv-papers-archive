# CV 领域动态速览 · CV Papers Archive

> 每周自动聚合的计算机视觉（CV）论文 / 模型 / 行业动态档案库；并附「视觉目标跟踪（VOT）」中英双语论文专栏。

数据源自 [AI HOT](https://aihot.virxact.com) 中文 AI 资讯聚合平台，经关键词筛选后生成**时间线 + 卡片**式速览页面，并按周滚动存档；目标跟踪专栏另从 **arXiv / Semantic Scholar** 抓取最新论文，提供中英双语版本。

---

## 🔗 在线访问

| 页面 | 地址 | 说明 |
|------|------|------|
| 本周速览 | https://TAI-GG.github.io/cv-papers-archive/ | 最新一周 CV 动态（`index.html`） |
| 历史存档 | https://TAI-GG.github.io/cv-papers-archive/archive/2026-07-06.html | 上周快照（每周滚动新增） |
| 🎯 目标跟踪专栏 | https://TAI-GG.github.io/cv-papers-archive/tracking/index.html | 视觉目标跟踪（VOT）中英双语论文专栏 |

页面顶部 `.nav-bar` 提供导航，可在「主站·本周 / 目标跟踪 / 历史报告」之间一键切换。

---

## 📁 仓库结构

```
cv-papers-archive/
├── index.html              # 本周 CV 动态（最新一周，自动覆盖更新）
├── archive/
│   └── 2026-07-06.html     # 历史周存档（每周滚动新增，互不覆盖）
│   └── ……                  # 后续每周一个独立存档页
├── tracking/               # 🎯 目标跟踪专栏（VOT 中英双语）
│   ├── index.html          # 最新周度深度报告（含汇总表 + 主题详情 + 类别分布）
│   ├── daily/              # 每日速览（YYYY-MM-DD.html）
│   └── reports/            # 周报存档（含合并自 visual-tracking-papers 的历史报告）+ 报告索引
├── README.md               # 本说明
├── build_archive.py        # CV 主栏目构建与推送（含触发 tracking 专栏）
└── build_tracking.py       # 目标跟踪专栏独立构建脚本
```

---

## 🧠 内容筛选逻辑

### CV 主栏目（来自 AI HOT）

从 AI HOT 全量条目（约 1700+ 条 / 周）中筛选 CV 相关内容，规则如下：

1. **排除词（CV_NO）**：如 `kyber`、`eu council`、`us military`、`cursor`、`notebooklm` 等非 CV 主题，命中即丢弃；
2. **精确命中（CV_OK）**：如 `video generation`、`one-step visual`、`音乐伴舞`、`数字分身` 等，命中即收录；
3. **关键词分组（CV_KW）**：视觉 / 视频 / 图像 / 3D / 扩散 / 生成 / 分割 / 检测 / VLM / 机器人 / 自动驾驶 / 卫星 / 数字人 / 多模态 —— 跨 **≥ 2 个分组** 命中即收录。

最终按发布时间倒序排列，去重后展示。

### 🎯 目标跟踪专栏（VOT，来自 arXiv / Semantic Scholar）

独立于主栏目的「视觉目标跟踪（Visual Object Tracking）」中英双语论文专栏，由 `build_tracking.py` 生成：

- **数据来源**：arXiv API（主，`cat:cs.CV OR cat:cs.RO` ＋ tracking 检索）＋ Semantic Scholar API（best-effort，限流时自动降级为 arXiv-only）；并合并原 `TAI-GG/visual-tracking-papers` 仓库中的历史周报（共 4 期，已转为 HTML 归入 `tracking/reports/`）。
- **语言**：每篇论文提供英文原文 + 中文翻译（Google Translate，带本地缓存避免重复请求）。
- **严格相关性过滤**：标题 / 摘要须命中强信号短语（如 `object tracking`、`visual tracking`、`tracker`、`multi-object tracking`、`siamese`、`tracking benchmark`、`long-term tracking` 等），并排除 SLAM / 位姿估计 / 医学影像 / 手部·人脸·眼动跟踪 / 视频生成 / NLP 等相邻但非 VOT 的主题，避免假阳性。
- **分类**：按主题分为多目标跟踪、单目标跟踪、3D / 4D 跟踪、多模态跟踪、域自适应与鲁棒、无人机跟踪、架构（SSM / 扩散）、数据集与基准、通用跟踪。
- **产出页面**：`tracking/index.html`（本周深度报告）、`tracking/daily/`（每日速览）、`tracking/reports/`（周报存档 + 历史报告 + 报告索引）。

---

## ✨ 页面特性

**CV 主栏目**
- **时间线布局**：左侧时间轴 + 右侧内容卡片，按日期自动分组；
- **富信息卡片**：标题（外链新标签页打开原文）、类型标签（论文 / 模型 / 产品 / 技巧 / 行业）、来源徽章、相对时间、≤ 200 字摘要；
- **周次导航栏**：顶部 sticky 导航，支持历史周切换；
- **响应式设计**：移动端自适应，单列布局；
- **淡入动画**：卡片随滚动逐个渐显。

**目标跟踪专栏**
- **中英双语**：每篇论文含英文摘要与中文译文；
- **汇总表 + 主题分组详情 + 类别分布**；
- **历史报告合并**：原 `visual-tracking-papers` 周报完整保留并可访问。

---

## ⚙️ 更新机制

- **频率**：CV 主栏目每周一自动化触发；目标跟踪专栏**每日**自动化触发（与主栏目同一定时任务，`build_archive.py` 会先调用 `build_tracking.py`）。
- **流程（CV 主栏目）**：拉取最新数据 → CV 筛选 → 拆为「本周 / 上周」→ 生成 `index.html` 与 `archive/YYYY-MM-DD.html`；
- **流程（目标跟踪专栏）**：每日从 arXiv（＋ best-effort Semantic Scholar）抓取近 7 天 VOT 论文 → 严格过滤 → 中英双语渲染 → 生成 `tracking/` 下各页面；
- **推送方式**：`git clone` 现有仓库 → 覆盖生成文件 → 普通 `commit` + `push`（**不 force**，保留历史周存档与历史报告）。

---

## 🛠️ 本地构建

```bash
# 完整构建（推荐）：CV 主栏目 + 目标跟踪专栏 → 拉取 → 筛选 → 渲染 → 推送 GitHub Pages
python build_archive.py

# 仅构建目标跟踪专栏（中英双语，本地预览用，不推送）
python build_tracking.py
```

前置条件：
- Windows 凭据管理器已保存 GitHub PAT（目标 `git:https://github.com`，类型 Generic）；
- 脚本通过 `ctypes` 读取该 PAT 完成鉴权推送；
- 推送目标仓库：`TAI-GG/cv-papers-archive`；
- 网络需可经本地出口代理 `127.0.0.1:7890` 访问 GitHub / arXiv（脚本已内置代理注入）。

---

## ⚠️ 声明

- 全部内容版权归原作者 / 原发布平台所有，本仓库仅作**聚合索引**，所有链接均指向原始出处；
- 数据由自动化脚本筛选，可能存在漏判 / 误判，仅供参考；
- 部分早期周次数据因 API 缓存窗口限制无法回溯，存档自 `2026-06-30` 起完整保留。

---

<p align="center">
  Powered by <a href="https://aihot.virxact.com">AI HOT</a> · VOT column from arXiv &middot; Generated automatically
</p>
