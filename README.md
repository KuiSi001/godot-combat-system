<div align="center">

# ⚔️ Godot Combat System
### 现代化 2D 组件化战斗底层

[![Godot Engine](https://img.shields.io/badge/Godot-4.x-blue?style=for-the-badge&logo=godot-engine)](https://godotengine.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Language](https://img.shields.io/badge/Language-GDScript-orange?style=for-the-badge)]()

一个专为 **2D 动作、清版 (Beat 'em up) 及 ARPG** 打造的组件化战斗系统。
秉持 **“数值、检测、结算分离”** 的架构理念，彻底解耦战斗逻辑与角色表现。告别底层造轮子，只需拼装节点，即可快速搭建商业级打击感。

</div>

---

> [!WARNING]
> 🌐 **Language Support Notice**
> 
> - 🇺🇸 **English**：This plugin currently only supports Chinese.
> - 🇨🇳 **中文**：本插件暂时只支持中文。
>
> <details>
> <summary>🌍 点击展开更多语言 (Click to expand more languages)</summary>
> 
> - 🇯🇵 **日本語**：このプラグインは現在、中国語のみをサポートしています。
> - 🇰🇷 **한국어**：이 플러그인은 현재 중국어만 지원합니다.
> - 🇪🇸 **Español**：Este plugin actualmente solo soporta chino.
> - 🇫🇷 **Français**：Ce plugin ne prend actuellement en charge que le chinois.
> - 🇩🇪 **Deutsch**：Dieses Plugin unterstützt derzeit nur Chinesisch.
> - 🇷🇺 **Русский**：В настоящее время этот плагин поддерживает только китайский язык.
> - 🇧🇷 **Português**：Este plugin atualmente suporta apenas chinês.
> - 🇮🇹 **Italiano**：Questo plugin attualmente supporta solo il cinese.
> 
> </details>

---

## 📖 目录
- [✨ 核心特性](#-核心特性)
- [📦 安装指南](#-安装指南)
- [🚀 三分钟极速上手](#-三分钟极速上手)
- [🏗️ 系统架构解析](#️-系统架构解析)
- [🛠️ 调试与工具](#️-调试与工具)
- [📄 授权协议](#-授权协议)

---

## ✨ 核心特性

| 特性 | 说明 |
| :--- | :--- |
| 🧩 **完全组件化** | 拒绝强绑定的继承链。基于 `Node` 的组件设计，即插即用。 |
| 🎯 **动画驱动判定** | 利用 `AnimationPlayer` 控制攻击盒开关，告别 `wait()` 魔法数字。 |
| 💥 **商业级反馈** | 内置顿帧、闪白、物理击退、伤害飘字，一键配置极致打击感。 |
| 🧮 **公式绝对统一** | 唯一伤害计算公式位于 `DamageCalculator`，杜绝外部计算导致的数值崩坏。 |
| 🛡️ **完善的 Buff 生态** | 三种叠加模式，与状态组件无缝对接，自动管理持续时间。 |
| 🔍 **开发者调试面板** | 按 `F2` 唤出，实时监控并修改全场角色属性，实现“无重启热调数值”。 |

---

## 📦 安装指南

1. 下载本仓库的 Release 或 直接 Clone 源码。
2. 将 `addons/combat_system` 文件夹复制到你的 Godot 项目根目录的 `addons/` 下。
3. 在 Godot 顶部菜单栏选择 `项目` -> `项目设置` -> `插件`。
4. 找到 **战斗系统**，勾选右侧的 **启用** 按钮。

---

## 🚀 三分钟极速上手

> [!TIP]
> **最小可运行结构**：攻击盒与受击盒必须与属性组件**同父同级**。找不到组件时，盒子会自动报错并安全禁用，绝不导致崩溃。

```text
角色 (CharacterBody2D / Node2D)
  ├── 属性组件 (StatsComponent)         <- 必须。战斗数据的唯一来源。
  ├── 攻击盒 (AttackHitbox: Area2D)     <- 可选。攻击方才有，需带 CollisionShape2D。
  └── 受击盒 (Hurtbox: Area2D)          <- 可选。能被攻击才有，需带 CollisionShape2D。
