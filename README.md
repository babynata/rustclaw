# 🦀 RustClaw — Personal AI Assistant (Rust Core Fork)

<p align="center">
  <strong>OpenClaw fork · Rust native core via napi-rs · 个人实验项目</strong>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" alt="MIT License"></a>
  <a href="https://github.com/babynata/rustclaw"><img src="https://img.shields.io/badge/fork-OpenClaw-orange?style=for-the-badge" alt="Fork of OpenClaw"></a>
  <a href="https://github.com/babynata"><img src="https://img.shields.io/badge/author-babynata-lightgrey?style=for-the-badge" alt="Author"></a>
</p>

---

## 这是什么 / What is this

**RustClaw** 是 [OpenClaw](https://github.com/openclaw/openclaw) 的个人 fork，核心改造方向是将性能敏感路径替换为 Rust 原生实现（通过 [napi-rs](https://napi.rs/)）。这是一个实验性的个人项目，用于探索 Rust + TypeScript 混合架构在 AI Assistant 运行时中的可能性。

**RustClaw** is a personal fork of [OpenClaw](https://github.com/openclaw/openclaw) that replaces performance-sensitive paths with Rust native implementations via [napi-rs](https://napi.rs/). This is an experimental personal project exploring Rust + TypeScript hybrid architecture in an AI assistant runtime.

> **注意 / Note:** 这不是官方 OpenClaw 项目。上游维护在 [openclaw/openclaw](https://github.com/openclaw/openclaw)。
> This is not the official OpenClaw project. Upstream is maintained at [openclaw/openclaw](https://github.com/openclaw/openclaw).

---

## 核心改动 / Key Changes from Upstream

### Rust Phase 0 — `napi-rs` BindingCache (`feat/rust-phase0-workspace`)

- **`BindingCache`** — Rust 实现的 binding 缓存层，替代原 TypeScript 热路径，减少 GC 压力
- **`napi-rs` workspace** — `crates/` 目录下独立的 Rust crate，通过 napi-rs 暴露给 Node.js
- 目标：在保持 TypeScript 接口不变的前提下，将核心调度路径的延迟降低

Key changes:
- **`BindingCache`** — Rust-native binding cache layer replacing the hot-path TypeScript implementation, reducing GC pressure
- **`napi-rs` workspace** — Standalone Rust crates under `crates/`, exposed to Node.js via napi-rs
- Goal: reduce latency in core dispatch paths without changing the TypeScript interface

---

## 关于作者 / About

个人主页 / GitHub: [github.com/babynata](https://github.com/babynata)

<!-- 可在此添加其他联系方式，如 Twitter/X、博客、个人网站 -->
<!-- Add your Twitter/X, blog, or personal website links here -->

---

## 安装与使用 / Install & Usage

本 fork 与上游 openclaw 安装方式相同，以下为快速参考。

This fork shares the same install process as upstream openclaw. Quick reference below.

**运行环境 / Runtime:** Node ≥ 22

### 从源码构建（推荐） / Build from Source (Recommended)

```bash
git clone https://github.com/babynata/rustclaw.git
cd rustclaw

# 安装依赖 / Install deps
pnpm install

# 构建 Rust crate（需要 Rust toolchain）/ Build Rust crates (requires Rust toolchain)
cargo build --release

# 构建完整项目 / Full build
pnpm build

# 启动 / Start
pnpm openclaw onboard --install-daemon
```

### Rust Toolchain 要求 / Rust Requirements

```bash
# 安装 Rust（如果尚未安装）/ Install Rust if not already installed
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# 确认版本 / Verify
rustc --version  # 建议 stable >= 1.75
```

### 快速启动 / Quick Start

```bash
# 启动 Gateway
openclaw gateway --port 18789 --verbose

# 发送消息 / Send a message
openclaw agent --message "hello"
```

---

## 项目结构 / Project Structure

```
rustclaw/
├── crates/          # Rust crates (napi-rs bindings)
├── src/             # TypeScript core (CLI, gateway, commands)
├── packages/        # Internal workspace packages
├── extensions/      # Channel plugins
├── apps/            # macOS / iOS / Android companion apps
└── docs/            # Documentation
```

核心 Rust 改动位于 `crates/` 和 `feat/rust-phase0-workspace` 分支。

Core Rust changes live in `crates/` and the `feat/rust-phase0-workspace` branch.

---

## 功能亮点 / Highlights (inherited from OpenClaw)

- **多渠道收件箱** — WhatsApp、Telegram、Slack、Discord、Signal、iMessage、微信等 20+ 渠道
- **本地优先 Gateway** — 单一控制平面，管理 session、channel、工具和事件
- **多 Agent 路由** — 将不同渠道路由到隔离的 agent workspace
- **语音唤醒 + 对话模式** — macOS/iOS 唤醒词，Android 连续语音
- **伴侣应用** — macOS 菜单栏 + iOS/Android 节点
- **技能平台** — 内置技能 + 可扩展的 workspace skills

Multi-channel inbox (20+ channels) · Local-first Gateway · Multi-agent routing · Voice Wake + Talk Mode · Companion apps · Skills platform

---

## 开发说明 / Development Notes

```bash
# 运行测试 / Run tests
pnpm test

# 类型检查 / Type check
pnpm build

# Lint + 格式检查 / Lint + format
pnpm check

# 监听模式开发 / Dev watch mode
pnpm gateway:watch
```

### 分支说明 / Branches

| 分支 | 说明 |
|------|------|
| `main` | 跟踪上游 openclaw main |
| `feat/rust-phase0-workspace` | Rust napi-rs BindingCache 实验分支 |

---

## 上游关系 / Upstream Relationship

本项目 fork 自 [openclaw/openclaw](https://github.com/openclaw/openclaw)，遵循相同的 MIT 协议。上游的 bug fix 和功能更新会定期同步到本 fork 的 `main` 分支。

This project is forked from [openclaw/openclaw](https://github.com/openclaw/openclaw) under the same MIT license. Upstream bug fixes and feature updates are periodically synced to this fork's `main` branch.

---

## License

MIT — see [LICENSE](LICENSE)

原始项目版权归 OpenClaw 贡献者所有。本 fork 的 Rust 部分由 [@babynata](https://github.com/babynata) 编写。

Original project copyright OpenClaw contributors. Rust additions in this fork by [@babynata](https://github.com/babynata).
