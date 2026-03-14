---
title: "2D Platformer"
description: "使用自研引擎开发的 2D 平台跳跃游戏原型，包含物理与关卡编辑器。"
tags: [C++, Game, Physics]
featured: true
repo: "https://github.com/IsakWong/2d-platformer"
# cover: /assets/images/projects/platformer.jpg
---

## 项目简介

一个使用 C++ 自研引擎构建的 2D 平台跳跃游戏原型，包含自定义物理系统和可视化关卡编辑器。

## 主要特性

- **自研 2D 物理引擎** — AABB 碰撞检测，简单的刚体动力学
- **Tile-based 关卡系统** — JSON 格式关卡数据，支持热重载
- **关卡编辑器** — ImGui 实现的可视化编辑器
- **动画系统** — Sprite Sheet 动画状态机
- **音频系统** — 基于 FMOD 的音效管理

## 引擎架构

```
Game Layer
    ↓
Engine Core (ECS, Event System, Resource Manager)
    ↓
Platform Layer (Window, Input, Audio)
    ↓
Rendering (OpenGL 4.5, Sprite Batch Renderer)
```
