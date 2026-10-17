<div align="center">

# ⚔️ Godot Combat System
### 现代化、高扩展性的 2D 组件化战斗底层

[![Godot Engine](https://img.shields.io/badge/Godot-4.x-blue?style=for-the-badge&logo=godot-engine)](https://godotengine.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Language](https://img.shields.io/badge/Language-GDScript-orange?style=for-the-badge)]()

一个专为 **2D 动作、清版及 ARPG** 打造的组件化战斗系统。<br>
秉持 **“数值、检测、结算分离”** 的架构理念，彻底解耦战斗逻辑与角色表现。<br>
告别底层造轮子，只需拼装节点，即可快速搭建商业级打击感。

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

- [🧠 核心设计理念](#-核心设计理念)
- [📦 安装与快速上手](#-安装与快速上手)
- [🛠️ 模块详细解析](#️-模块详细解析)
- [⚠️ 常见坑与避雷指南](#️-常见坑与避雷指南)
- [🚀 扩展与进阶指南](#-扩展与进阶指南)
- [📄 开源协议](#-开源协议)

---

## 🧠 核心设计理念

系统将复杂的战斗过程拆分为三个绝对隔离的维度：

| 模块 | 职责 | 说明 |
| :--- | :--- | :--- |
| **属性组件** | 战斗数据的唯一来源 | 攻击盒、受击盒、UI 均从这里读写，管理基础值与修改器。 |
| **伤害计算器** | 唯一的伤害公式所在地 | 静态类统一处理，外部脚本**绝对禁止**自行计算伤害。 |
| **碰撞盒 (Hit/Hurt)** | 仅负责物理区域检测 | 不含任何伤害逻辑，动画、特效、击退全交由外部表现层处理。 |

---

## 📦 安装与快速上手

### 1. 启用插件
将 `addons/combat_system/` 复制到工程目录。在 `项目 -> 项目设置 -> 插件` 中勾选 **「战斗系统」**。

### 2. 最小可运行结构
在任何角色（玩家或敌人）节点下，挂载以下同级节点：

```text
角色 (Node2D / CharacterBody2D)
  ├── 属性组件 (StatsComponent)         <- 必须，战斗数据核心
  ├── 攻击盒 (AttackHitbox: Area2D)     <- 可选，攻击方才有
  │     └── CollisionShape2D
  └── 受击盒 (Hurtbox: Area2D)          <- 可选，能被攻击才有
        └── CollisionShape2D
