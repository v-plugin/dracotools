# dracotools
An open-source toolkit for practical development workflows.# DracoTools — 3D 模型压缩与优化工具

> Draco + Meshopt 双引擎压缩 · KTX2 GPU 纹理 · 7 种格式互转 · 数据标记 · 3D 查看器 · 批量处理
> 完全本地运行，数据不离开你的电脑

[![版本](https://img.shields.io/badge/版本-v1.0.0-6366f1)](https://gitee.com/raychart/dracotools/releases)
[![平台](https://img.shields.io/badge/平台-Windows%20%7C%20Linux%20%7C%20macOS-blue)](https://gitee.com/raychart/dracotools/releases)
[![授权](https://img.shields.io/badge/授权-免费版永久可用-orange)](#免费版说明)
[![源码](https://img.shields.io/badge/源码-不公开-red)](#授权与源码)

<p align="center">
  <img src="docs-site/public/screenshots/screenshot-meshopt.webp" alt="DracoTools 主界面 — Meshopt 压缩" width="800" />
</p>

**DracoTools** 是一款桌面端 3D 模型压缩与优化工具，帮助 Web3D 开发者在发布前压缩模型与纹理：几何体最高减小 **90%**，纹理直传 GPU，模型体积更小、加载更快。全部处理在本地完成，无需联网注册，安装包不到 10 MB。

- ⚡ **双引擎压缩**：Draco / Meshopt 几何压缩，最高缩减 90%，自动推荐引擎
- 🖼️ **纹理优化**：KTX2 / WebP / JPEG，ETC1S / UASTC 编码，GPU 直传
- 🔄 **7 种格式互转**：GLB / glTF / FBX / OBJ / STL / DAE / PLY，贴图自动内嵌
- 🏷️ **数据标记**：编辑模型节点 `userData` 键值对，支持 JSON 导入导出
- 🔍 **3D 查看器**：剖切 / 动画 / 灯光 / 环境，截图导出与视频录制
- 📦 **批量处理 + 操作日志**：多文件一次跑完，报告可导出，参数可复用
- 🔒 **完全离线**：模型、贴图、标记数据不出本地，断网照常使用

> 💻 不想安装？试试 [DracoTools Web 在线版](https://zipoly-web.raychart.cn)（无需安装，单文件 20MB）。

---

## 下载 v1.0.0

| 平台 | 安装包 | 说明 |
|------|--------|------|
| **Windows 10/11 (64位)** | [NSIS 安装包](https://gitee.com/raychart/dracotools/releases) · [MSI 安装包](https://gitee.com/raychart/dracotools/releases) | NSIS 约 6.8 MB，MSI 约 9.1 MB |
| **Linux x64** | [DEB](https://gitee.com/raychart/dracotools/releases) · [RPM](https://gitee.com/raychart/dracotools/releases) · [AppImage](https://gitee.com/raychart/dracotools/releases) | Ubuntu 20.04+ / Debian 11+ / Fedora 36+ / RedHat 8+ |
| **macOS 10.15+** | [DMG](https://gitee.com/raychart/dracotools/releases) · [App.zip](https://gitee.com/raychart/dracotools/releases) | Apple Silicon / Intel，未签名需右键打开 |

Linux 命令行安装：

```bash
# Debian / Ubuntu
sudo dpkg -i DracoTools_*_amd64.deb
sudo apt-get install -f   # 如有依赖缺失

# Fedora / RedHat
sudo dnf install ./DracoTools-*-1.x86_64.rpm
```

- 完整安装说明（依赖、Gatekeeper、杀毒软件白名单）：[安装与获取](https://dracotools.top/guide/install)
- 全部版本与历史安装包：[Gitee Releases](https://gitee.com/raychart/dracotools/releases)

---

## 功能一览

| 模块 | 说明 | 免费版限制 |
|------|------|-----------|
| **模型优化** | Draco / Meshopt 几何压缩，体积缩减 70–90%，场景化预设 | 单文件 ≤ 20 MB |
| **格式转换** | FBX / OBJ / STL / DAE / PLY → GLB / glTF，贴图自动内嵌 | 单文件 ≤ 20 MB |
| **纹理优化** | JPEG / WebP / KTX2 压缩，批量编码 | 单文件 ≤ 5 MB |
| **模型查看** | Three.js 实时预览：剖切、动画、灯光、环境、截图 / 录制 | ✅ 不限 |
| **数据标记** | 节点 userData 键值对编辑，JSON 导入导出 | 单文件 ≤ 20 MB |
| **活动日志** | 历史记录、参数复用、CSV/HTML 报告导出 | ✅ 不限 |
| **账户信息** | 授权激活、性能检测、按设备 ID 找回密钥 | ✅ 不限 |
| **系统设置** | 默认参数、引擎诊断、更新检查、中英双语 | ✅ 不限 |

### 压缩引擎对比

| | Draco | Meshopt（推荐） |
|---|---|---|
| 压缩率 | 高 | 更高 |
| 解码性能 | 中 | 快 5–10 倍 |
| 纹理压缩 | JPEG / WebP / KTX2 | JPEG / WebP / KTX2 |
| 适用场景 | 老项目、广兼容性 | Web3D 新项目、超大场景 |

拿不定主意就选 **Meshopt**——解码更快、体积更小，Draco 则胜在兼容性。

> 内部实现基于 [Tauri 2](https://v2.tauri.app/) + Vue 3 + Rust，几何压缩用 [Draco](https://github.com/google/draco) 与 [gltfpack/Meshopt](https://github.com/zeux/meshoptimizer)，纹理用 [Basis Universal](https://github.com/BinomialLLC/basis_universal)，查看器用 [Three.js](https://threejs.org/)。

---

## 快速上手

1. 拖拽 `.glb` / `.gltf` 文件进入「模型优化」页
2. 选择引擎（推荐 Meshopt）与场景预设
3. 点击「开始压缩」，实时查看进度与体积对比
4. 切换到「3D 查看器」确认效果，或从「活动日志」导出报告

完整教程见 [使用文档](https://dracotools.top/guide/optimize)，含 Three.js / Babylon.js / model-viewer 的加载代码示例。

---

## 免费版说明

DracoTools 采用 **Freemium** 模式：**免费版永久可用，无时间限制**，仅限制单文件大小，每次处理一个文件。查看器、截图录制、操作日志、账户与设置页永久免费且不限文件。

需要更大文件或批量处理时，可在应用内购买授权：

| 套餐 | 单文件上限 | 价格 |
|------|-----------|------|
| 普通会员（Pro） | 500 MB | ¥15 / 30 天 · **¥79 / 年** · ¥199 终身（原价 ¥299） |
| 超大文件会员（Pro XL） | 5 GB | ¥30 / 30 天 · ¥99 / 年 · ¥299 终身 |

- **一机一码**：密钥与设备硬件 ID 绑定，离线验证
- **应用内一键购买**：微信扫码付款后自动发码、粘贴即激活；重装后可按设备 ID 找回
- **免费迁移**：尝鲜版 / 年付每 365 天可免费换绑 1 次设备；终身版迁移费 ¥29 起逐年递减至 ¥9 封底
- **先试后买**：免费版与 ¥15 尝鲜版已提供完整试用，请先确认满足需求

> 🛡️ **官方购买页只从桌面应用内打开**（自动携带设备校验码），浏览器直接输入网址会被引导回说明页。请认准文档站 `dracotools.top` 与购买页 `license-server.dracotools.top`，密钥以 `DESKTOP-` 开头。任何私聊发来的「购买链接」「通用激活码」均为钓鱼。

详见 [授权与定价](https://dracotools.top/guide/license)。

---

## 授权与源码

DracoTools 采用**授权机制、不开放源码**：本项目不是开源软件，源代码不对外公开，也不接受外部贡献或提交 Pull Request。软件的授权采用设备绑定、离线验证的密钥机制（一机一码），密钥与购买时的设备硬件 ID 绑定。

如果你在使用中遇到问题或有功能建议，请通过 [联系方式](#联系我们) 反馈，我们会评估并纳入后续版本。

> 💡 需要时我们提供**代压缩服务**（单次 ¥50），可直接把模型与需求发给我们处理，无需源码。

技术栈（仅作说明，不代表源码开放）：Tauri 2 · Rust · Vue 3 · Vite · TypeScript · Three.js · Draco · Meshopt · Basis Universal。

---

## 常见问题

**压缩后模型变大了？**
小型模型（< 1000 面）元数据开销可能超过收益，可降低压缩级别或选择不压缩。

**Draco 和 Meshopt 选哪个？**
选 Meshopt：解码快 5–10 倍、体积更小；Draco 兼容性更好，适合老项目。

**支持哪些系统？**
Windows 10/11 (64位)、Linux x64（deb / rpm / AppImage）、macOS 10.15+（Apple Silicon / Intel）。

**完全离线吗？**
是。压缩、转换、预览均在本地完成，无需账号、无需联网。

更多问题见 [FAQ](https://dracotools.top/faq)。

---

## 更新日志

**v1.0.0 · 首次发布**

- 3D 模型压缩全家桶：Draco / Meshopt 双引擎、KTX2 纹理、7 种格式互转、数据标记、3D 查看器、批量处理
- 免费版永久可用，Pro / Pro XL 双档授权（单文件最高 5GB），应用内一键购买与设备找回
- 账户页新增性能检测；大文件压缩前自动硬件预检

详见 [完整更新日志](https://dracotools.top/guide/changelog)。

---

## 联系我们

- 🌐 官网 / 文档：[dracotools.top](https://dracotools.top)
- 🌐 Web 在线版：[zipoly-web.raychart.cn](https://zipoly-web.raychart.cn)
- 💬 QQ / 微信：**2162788746**
- 📦 安装包下载：[Gitee Releases](https://gitee.com/raychart/dracotools/releases)
- 💝 代压缩服务：单次 ¥50，发送模型与需求至 QQ 2162788746

Copyright © 2024–2026 DracoTools. All rights reserved.

---

## 授权与源码声明

本项目为**授权软件，源码不公开**：不开放源代码、不接受外部代码贡献。软件通过设备绑定、离线验证的密钥机制进行授权（一机一码）。未经授权，不得复制、反编译、修改或再分发本软件及其组件。

软件所使用的第三方开源组件（Draco、Meshopt、Basis Universal、Three.js、Vue 等）各自遵循其原有开源许可证，详见对应上游项目。

---

## English

**DracoTools** is a desktop tool that shrinks and optimizes Web3D assets before delivery: Draco & Meshopt geometry compression (up to 90% smaller), KTX2 GPU textures, conversion between 7 formats (GLB/glTF/FBX/OBJ/STL/DAE/PLY), node `userData` tagging, and a built-in 3D viewer — fully offline, ~7 MB installer.

- **Free forever**: 3D viewer, screenshots, logs unlimited; compression limited to 20 MB per file (5 MB textures)
- **License**: Pro ¥79/year (500 MB) and Pro XL ¥99/year (5 GB), one device per key, in-app purchase via WeChat
- **Download**: [Gitee Releases](https://gitee.com/raychart/dracotools/releases) (Windows / Linux / macOS)
- **Docs**: [dracotools.top](https://dracotools.top) · Contact: QQ 2162788746

© 2024–2026 DracoTools. Licensed software with source code not publicly available.

