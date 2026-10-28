# 🐾 Critter Haven 智能截图求解器 V6.0 Pro | Smart Screenshot Solver

一个零外部依赖、纯前端运行的 **Critter Haven** 10×10 消除小游戏智能求解器。支持上传手机或电脑端游戏截图后**自动精准锁定棋盘区域**、**自适应奇偶格绿幕去背高精度图案聚类**、**启发式集束搜索（Beam Search）最少步数全清求解**，以及**慢速清晰步骤 GIF 动图合成与导出**（全面适配 iOS Safari / 微信内置浏览器与 PC 端）。

A zero-dependency, pure client-side web solver for the **Critter Haven** 10×10 tile-matching mini-game. It features **automatic 10×10 board boundary detection**, **adaptive checkerboard background removal & shift-invariant pattern clustering**, **minimum-step full-clear solving via Beam Search**, and **slow-paced step-by-step animated GIF export** with full iOS & desktop support.

## ✨ 核心特性 | Key Features

| 功能模块 / Module | 中文说明 | English Description |
| :--- | :--- | :--- |
| **🎯 自动棋盘区域检测**<br>Auto Board Detection | 基于原始图像分辨率的双阶段草坪色域与棋盘格边界跳变算法，上传截图后自动锁定 10×10 正方形棋盘并提取图案，同时支持四角触控手柄拖拽微调。 | Dual-stage lawn-contrast and grid-edge detection on full-resolution screenshots. Automatically locks onto the 10×10 board upon upload, with 4 touch-friendly corner handles for manual fine-tuning. |
| **🔬 高精度去背图案识别**<br>High-Precision Recognition | 针对棋盘格深浅交替的两种绿色背景，自动采样每格四角中位数底色并剔除绿幕干扰；结合 3×3 微移不变空间特征（70%）与 64-bin 前景色彩直方图（30%）进行平均链接层次聚类（Average-Linkage HAC）。 | Automatically estimates and masks out alternating light/dark green checkerboard backgrounds per cell. Combines 3×3 shift-invariant spatial matching (70%) with 64-bin foreground RGB histograms (30%) via Average-Linkage Hierarchical Agglomerative Clustering. |
| **🚀 AI 最少步数全清引擎**<br>Minimum-Step AI Solver | 内置宽度为 850 的启发式集束搜索（Beam Search）与重力下落物理模拟引擎，快速推演全局最少步数全清路径，并提供交互式进度条、自动回放与文字步骤清单。 | Built-in Beam Search (beam width = 850) with column-gravity simulation to find the minimum-step full-clear solution. Includes interactive step playback, auto-play, and a clickable step list. |
| **🎬 慢速清晰步骤 GIF 导出**<br>Slow-Paced Step GIF Export | 纯前端内置 GIF89a + LZW 编码器与 15-bit 快速色彩查找表，生成包含顶部进度栏、目标图案缩略图、点击行列坐标、1~10 棋盘坐标尺与红框高亮序号的慢速动图（支持 0.8s~2.6s/步调节）。 | Pure JavaScript GIF89a + LZW encoder with a 15-bit color LUT. Renders crystal-clear frames featuring step headers, target icons, row/column tap coordinates, 1–10 board rulers, and highlighted target badges at customizable slow speeds (0.8s–2.6s per step). |
| **📱 iOS 手机端深度适配**<br>iOS & Mobile Friendly | 默认开启「棋盘防误触锁定」防止滑动误改；支持 iOS 长按预览图直接「存储到“照片”」以及原生 Web Share API 一键调用系统分享菜单存相册。 | Includes a default Board Edit Lock to prevent accidental touch edits while scrolling, native iOS long-press image saving (`-webkit-touch-callout`), and Web Share API Level 2 support for saving GIFs directly to iOS Photos. |

## 🚀 快速开始 | Quick Start

### 方式一：直接双击运行（推荐） | Option 1: Direct Local Use (Recommended)

本项目为单文件应用，无需安装 Node.js 或任何后端服务：

1. 克隆或下载本仓库代码：
   ```bash
   git clone https://github.com/your-username/critter-haven-solver.git
   ```
2. 直接使用浏览器打开 `critter_haven-PC版.html`（或部署至 GitHub Pages / Vercel / Netlify 在手机端访问）。

This project is a self-contained single-file web application requiring no build step or backend server:

1. Clone or download this repository.
2. Open `critter_haven-PC版.html` directly in any modern browser (Safari, Chrome, Edge, Firefox), or host it on GitHub Pages for instant mobile access.

### 方式二：开启 GitHub Pages 手机端在线使用 | Option 2: GitHub Pages Deployment

1. 将代码推送到你的 GitHub 仓库。
2. 进入仓库 **Settings** → **Pages**，在 **Build and deployment** 中选择主分支（`main` 或 `master`）并保存。
3. 在 iPhone / Android 浏览器中打开生成的 GitHub Pages 链接，点击 Safari 底部分享按钮 → **「添加到主屏幕」**，即可作为独立 Web App 随时调用。

## 📖 使用指南 | Usage Guide

1. **上传游戏截图 (Upload Screenshot)**
   - 点击右上角 **「📸 上传游戏截图」** 选择手机或电脑中的 Critter Haven 游戏截图（也可点击 **「🖼️ 加载测试截图」** 体验内置示例）。
   - 系统会自动定位 10×10 棋盘区域并完成全部 100 格图案识别。如需微调选框，可直接拖动选框四角的白色圆点手柄并点击 **「✅ 重新提取棋盘」**。

2. **核对棋盘与图案库 (Verify Board & Palette)**
   - 在 **「2. 10×10 棋盘识别结果」** 区域查看提取出的棋盘与下方调色板（每个图案右上角标有盘面出现次数 `×N`）。
   - 默认识别容差为 `16`（最佳分离阈值）。若极少数截图因护眼模式或压缩出现重复分类，可点击 **「🔗 手动合并相似项」** 依次点击两个相同图案一键合并，或点击右上角解锁按钮进入微调模式手动修改单格。

3. **计算最优全清步骤 (Run AI Solver)**
   - 点击 **「🚀 寻找最少步数全清解法」**，引擎将在数秒内搜索出最少步数全清方案。
   - 可通过 **「◀ 上一步」**、**「▶️ 自动播放」**、**「下一步 ▶」** 或展开下方的 **「📋 查看全部步骤文字清单」** 逐步对照盘面。

4. **导出慢速步骤 GIF 动图 (Export Slow-Paced Step GIF)**
   - 在右侧 **「4. 导出慢速步骤 GIF 动图」** 卡片中选择合适的每步停留时间（默认推荐 **「🐢 慢速清晰 1.8 秒/步」** 或 **「🦥 超慢速 2.6 秒/步」**）。
   - 点击 **「🎬 生成慢速步骤 GIF 动图」**。
   - **iOS 保存方法**：直接**长按生成的预览动图** → 选择 **「存储到“照片”」**，或点击 **「📲 系统分享 / 存相册 (iOS推荐)」**；电脑端可直接点击 **「💾 下载 GIF 文件」**。

## 🧠 核心算法解析 | Technical Architecture

### 1. 双阶段草坪色域与棋盘跳变定位 (2-Stage Lawn-Contrast Grid Detection)
传统的固定屏幕比例裁剪在游戏弹窗截图或不同长宽比机型上极易产生偏差。本工具在离屏原始分辨率画布（`rawCanvas`）上扫描 Critter Haven 弹窗特有的浅黄绿草坪背景色域（$R \in [181, 205], G \in [203, 227], B \in [100, 128]$，并带有色温偏移自适应回退），先定位上下纯草坪带（草坪像素占比 $> 72\%$），再锁定中间连续非草坪跳变区间的正方形 10×10 棋盘像素坐标。

### 2. 奇偶格自适应去背与微移不变聚类 (Checkerboard Subtraction & Shift-Invariant HAC)
棋盘内部由浅绿（约 `[175, 200, 98]`）与深绿（约 `[160, 189, 87]`）奇偶交替组成，直接提取像素指纹会导致同种图案在奇偶格中产生距离偏差。算法对每格 `16×16` 采样块的四个边角（共 16 像素）取通道中位数作为该格专属背景色 $\mathbf{c}_{\text{bg}}$，通过径向窗口与欧氏色差阈值（$\|\mathbf{p} - \mathbf{c}_{\text{bg}}\|_2 > 18$）精确剥离背景。随后在中心 `12×12` 区域内进行 $\Delta x, \Delta y \in \{-1, 0, 1\}$ 的微移最小 L1 空间距离匹配，结合 64-bin 前景色彩直方图，采用平均链接层次聚类（Average-Linkage HAC）彻底杜绝单链漂移误合并。

### 3. 启发式集束搜索求解器 (Heuristic Beam Search Solver)
将 10×10 盘面编码为紧凑哈希字符串去重，每层扩展所有有效连通块消除动作并模拟列向重力下落。状态评估函数综合考虑已消耗步数 $s$、剩余非空连通块数 $c$ 与剩余格数 $r$：

$$\text{Score}(B, s) = -\big((s + c) \times 10000 + c \times 100 + r\big)$$

当 $r = 0$ 时赋予最高奖励 $10^7 - s$，从而在保证全清的前提下严格最小化总步数。

## 📂 项目结构 | Project Structure

```text
.
├── critter_haven-PC版.html   # 单文件完整应用（含 HTML/CSS/核心识别与求解引擎/GIF89a 编码器）
└── README.md                 # 中英双语项目说明文档
```

## 📄 开源协议 | License

本项目采用 **MIT License** 开源，欢迎自由使用、修改与提交 PR。

Released under the **MIT License**. Feel free to fork, modify, and submit pull requests.
