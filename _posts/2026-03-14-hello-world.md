---
layout: post
title: "延迟渲染 vs 前向渲染：实践对比与思考"
date: 2026-03-14
categories: [渲染]
---

在实现自研渲染器的过程中，我分别实现了前向渲染（Forward Rendering）和延迟渲染（Deferred Rendering）两套管线。本文记录一下实践中的思考和对比。

## 前向渲染

前向渲染是最直观的方式：对每个物体，遍历所有影响它的光源，一次完成着色。

```hlsl
// Forward shading - 每个物体遍历所有光源
float4 ForwardPS(VSOutput input) : SV_Target {
    float3 color = float3(0, 0, 0);
    for (int i = 0; i < numLights; i++) {
        color += CalcLight(lights[i], input.normal, input.worldPos);
    }
    return float4(color, 1.0);
}
```

**优势：** 实现简单，支持透明物体和 MSAA。  
**劣势：** 复杂度为 O(物体数 × 光源数)，光源多时性能惥崖。

## 延迟渲染

延迟渲染将几何信息和光照计算分离：

1. **Geometry Pass** — 把法线、深度、反射率等写入 G-Buffer
2. **Lighting Pass** — 在屏幕空间对每个像素计算光照

```hlsl
// G-Buffer output
struct GBufferOutput {
    float4 albedo   : SV_Target0;
    float4 normal   : SV_Target1;
    float4 position : SV_Target2;
};
```

**优势：** 复杂度为 O(屏幕像素 × 光源数)，光源数量对性能影响小。  
**劣势：** 占用显存大，透明物体处理比较麻烦，不能直接用 MSAA。

## 实践中的取舍

在我的渲染器里，最终采用了 **Deferred + Forward** 的混合方案：

- 不透明物体走 Deferred 管线
- 透明物体（特效、玻璃）走 Forward 管线

这也是大多数现代引擎（UE5、Unity HDRP）的做法。

---

下一篇将分享 Cascaded Shadow Maps 的实现细节。

---

感谢访问，欢迎常来！
