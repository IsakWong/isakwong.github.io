---
title: "Mini Renderer"
description: "基于 Vulkan 的迷你实时渲染器，支持 PBR、延迟渲染与阴影映射。"
tags: [C++, Vulkan, Rendering]
featured: true
repo: "https://github.com/IsakWong/mini-renderer"
# cover: /assets/images/projects/mini-renderer.jpg
---

## 项目简介

Mini Renderer 是一个从零搭建的实时渲染器，旨在深入学习现代图形 API 和渲染管线。

## 主要特性

- **Vulkan 后端** — 基于 Vulkan 1.3，充分利用现代 GPU 特性
- **PBR 材质系统** — 基于 Cook-Torrance BRDF 的物理材质
- **延迟渲染管线** — G-Buffer → Lighting → Post-Processing
- **阴影系统** — Cascaded Shadow Maps (CSM)
- **模型加载** — 支持 glTF 2.0 格式

## 技术细节

### 渲染管线

```
Geometry Pass → G-Buffer (Albedo, Normal, Depth, PBR params)
    ↓
Lighting Pass → HDR Color Buffer
    ↓
Post-Processing → Tone Mapping, FXAA
    ↓
Present
```

### 核心代码示例

```cpp
void DeferredRenderer::LightingPass(VkCommandBuffer cmd) {
    vkCmdBeginRenderPass(cmd, &lightingPassInfo, VK_SUBPASS_CONTENTS_INLINE);
    
    // Bind G-Buffer textures
    vkCmdBindDescriptorSets(cmd, VK_PIPELINE_BIND_POINT_GRAPHICS,
        m_lightingPipelineLayout, 0, 1, &m_gbufferDescSet, 0, nullptr);
    
    // Full-screen quad for deferred lighting
    vkCmdBindPipeline(cmd, VK_PIPELINE_BIND_POINT_GRAPHICS, m_lightingPipeline);
    vkCmdDraw(cmd, 3, 1, 0, 0);
    
    vkCmdEndRenderPass(cmd);
}
```

## 未来计划

- [ ] Screen Space Reflections (SSR)
- [ ] Volumetric Lighting
- [ ] GPU-driven rendering
- [ ] Ray Tracing 支持 (VK_KHR_ray_tracing)
