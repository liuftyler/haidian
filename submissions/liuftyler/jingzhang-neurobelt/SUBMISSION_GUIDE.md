# 提交指引 / Submission Guide

## 方案包已完成内容

本方案包"京张智脉"（Jingzhang NeuroBelt）已包含以下全部文件：

### 核心文件 (9个JSON)
- `manifest.json` — 方案清单（需运行 finalize 更新状态和哈希）
- `agent.json` — Agent 信息
- `metrics.json` — 指标（3项核心视觉指标均为 known）
- `assumptions.json` — 10项关键假设
- `sources.json` — 12条资料来源
- `self_check.json` — 自检状态（需运行脚本完成正式自检）
- `compliance_matrix.json` — 合规矩阵（6项agent任务 + 11项公告任务）
- `standard_matrix.json` — 标准矩阵（5项强制 + 4项非强制标准）
- `design_depth_matrix.json` — 设计深度矩阵（14项全部 complete）

### 方案文本 (双语)
- `proposal.md` — 中文方案（约31KB，覆盖全部章节和agent.1-6任务）
- `proposal.en.md` — 英文等义翻译（约40KB）

### 几何文件 (9个GeoJSON)
- `geometry/site_boundary.geojson` — 总体设计范围临时边界
- `geometry/key_areas.geojson` — 三处重点区域
- `geometry/land_use.geojson` — 15个用地分区多边形（无gap/overlap）
- `geometry/buildings.geojson` — 12个概念建筑基底
- `geometry/roads.geojson` — 10条道路中心线
- `geometry/green_space.geojson` — 8个绿地多边形
- `geometry/public_space.geojson` — 9个公共空间要素
- `geometry/constraints.geojson` — 6个约束要素
- `geometry/phasing.geojson` — 3个分期多边形

### 图件 (5张PNG)
- `assets/figures/site-overview.png`
- `assets/figures/land-use-structure.png`
- `assets/figures/key-areas.png`
- `assets/figures/mobility-bluegreen.png`
- `assets/figures/metrics-evidence.png`

### 渲染和可视化
- `report/proposal.html` — 方案离线渲染版
- `report/copyright_statement.md` — 版权声明
- `visual/index.html` — 离线可视化展板
- `drawings/a3-booklet.pdf` — A3图册（最小PDF，需替换为正式版）
- `drawings/a0-boards.pdf` — A0展板（最小PDF，需替换为正式版）
- `changelog.md` — 变更记录

---

## 提交步骤

### 第1步：安装环境

```bash
# 安装 Python 3.10+ (https://python.org)
# 安装 Git (https://git-scm.com)
# 安装 GitHub CLI (https://cli.github.com)

# 验证安装
python3 --version
git --version
gh --version

# 登录 GitHub
gh auth login
```

### 第2步：Fork 仓库并创建工作区

```bash
# Fork 仓库
gh repo fork open-city-ai/haidian --clone=false

# 下载引导脚本
curl -fsSLo /tmp/bootstrap_participant_workspace.py https://raw.githubusercontent.com/open-city-ai/haidian/main/scripts/bootstrap_participant_workspace.py

# 创建工作区（将 trae-agent 替换为你的 GitHub 登录名）
python3 /tmp/bootstrap_participant_workspace.py --proposal-slug jingzhang-neurobelt --target haidian --github-login <你的GitHub登录名> --fork-owner <你的GitHub登录名>

cd haidian
```

### 第3步：复制方案包

将本目录下的所有文件复制到工作区的 `submissions/<你的GitHub登录名>/jingzhang-neurobelt/` 目录：

```bash
# 将本方案包内容复制到工作区
cp -r /path/to/jingzhang-neurobelt/* submissions/<你的GitHub登录名>/jingzhang-neurobelt/
```

**重要**：将所有文件中的 `trae-agent` 替换为你的实际 GitHub 登录名。

### 第4步：安装依赖并运行脚本

```bash
# 安装参赛 skill
python3 scripts/install_submission_skill.py

# 安装审核依赖
python3 -m pip install -r requirements-review.txt

# 渲染 proposal.html（从 proposal.md 重新生成）
python3 scripts/render_proposal_html.py submissions/<你的GitHub登录名>/jingzhang-neurobelt

# 终化方案包（设置 package_state=ready_for_review，写入哈希）
python3 scripts/finalize_submission.py submissions/<你的GitHub登录名>/jingzhang-neurobelt

# 运行自检
python3 scripts/self_check_submission.py submissions/<你的GitHub登录名>/jingzhang-neurobelt --pr-author <你的GitHub登录名> --mark-self-checked --json

# 运行推送前检查
python3 scripts/participant_preflight.py submissions/<你的GitHub登录名>/jingzhang-neurobelt --pr-author <你的GitHub登录名> --check-push
```

### 第5步：修复问题

自检可能会发现以下问题，按提示修复：
- **package_state=scaffold**：运行 finalize_submission.py
- **PDF 页数为零**：用浏览器打印正式 A3/A0 PDF 替换最小占位 PDF
- **proposal.html 未更新**：运行 render_proposal_html.py
- **SHA-256 哈希缺失**：运行 finalize_submission.py
- **图件质量问题**：确保5张PNG为展示级城市设计图

反复运行自检直到所有检查通过（PASS）。

### 第6步：提交 Pull Request

```bash
# 提交代码
git add submissions/<你的GitHub登录名>/jingzhang-neurobelt/
git commit -m "Add Jingzhang NeuroBelt urban design proposal"

# 推送到你的 fork
git push origin main

# 创建 Pull Request
gh pr create --repo open-city-ai/haidian \
  --title "Add Jingzhang NeuroBelt (京张智脉) urban design proposal" \
  --body "AI-generated urban design proposal for the Centennial Jing-Zhang AI Innovation Belt open call."
```

### 第7步：监控 PR

```bash
# 监控 CI 检查
gh pr checks <pr-number> --repo open-city-ai/haidian --watch --interval 15

# 查看 PR 状态
gh pr view <pr-number> --repo open-city-ai/haidian \
  --json state,mergeStateStatus,reviewDecision,statusCheckRollup
```

---

## 设计概念摘要

**京张智脉（Jingzhang NeuroBelt）**——从百年铁轨到AI智脉

一百多年前，詹天佑设计了京张铁路——中国人自主建造的第一条干线铁路。一百年后，本方案将这条走廊转化为中国第一条AI"智脉"——一条连接文化记忆、生活体验和创新的神经网络。

- **一脉**：京张铁路遗址公园走廊（神经主脉）
- **三核**：智源核（NeuroCore）、原点社区（OriginNode）、智汇港（NeuroPort）
- **两翼**：中关翼（要素输入）、月河翼（场景输出）
- **多节点**：15个AI场景节点

核心指标：场地面积 11.4 km² | 绿地率 29.79% | 公共空间比例 14.89%

所有空间落地建议均为概念建议，不替代正式规划，不构成政府审定结论。
