# ✨ AI 视觉与 LoRA 高阶调优实战工作流 (LoRA Visual Mastery)

> **把复杂的底层计算收起来，把精准的画面控制权还给你。**  
> 专为 **Stable Diffusion 1.5 / SDXL 1.0** 商业级写实人像摄影、微表情概念滑块调优、真实手部解剖修复与多 LoRA 权重平衡打造的全链路工程规范与提示词资产库。

[![GitHub License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![AI Agent Skill](https://img.shields.io/badge/Agent%20Skill-Antigravity%20%7C%20Claude%20%7C%20Cursor-purple.svg)](SKILL.md)
[![Supported Models](https://img.shields.io/badge/Models-SD%201.5%20%7C%20SDXL%201.0-orange.svg)](#-底模代际与硬件运行基准)
[![Stars](https://img.shields.io/github/stars/287523023qq-hue/lora-visual-mastery?style=social)](https://github.com/287523023qq-hue/lora-visual-mastery)

---

## 🌟 核心价值：为什么需要本套工作流？

在 AI 生图与商业级写真制作中，常见三大致命痛点：
1. ❌ **手部融化与肢体异化**：出片 10 张有 7 张存在“六指、断指、融指、鸡爪手”；
2. ❌ **多 LoRA 叠加炸图**：角色、服饰、体态 LoRA 混用时，画面噪点激增、面部塑料感或结构崩塌；
3. ❌ **微表情与骨相失控**：传统提示词无法连续平滑微调“笑意大小、下颌松紧、腰臀比”，只能碰运气抽卡。

✅ **本系统的工业级解决方案**：
* 🎯 **手部解剖定向修复 SOP**：集成 `Realhands` 与 ADetailer 局部重绘流水线，手部成片率提升至 85%+；
* 📐 **多 LoRA 权重安全预算定律 (Budget Law <= 2.2)**：科学划分各维度配额，彻底杜绝噪点炸图；
* 🎛️ **LECO 差分概念滑块双向控制**：正负权重连续调节微笑/冷艳厌世脸、瓜子脸/幼态圆脸及 S 曲线身材；
* 💎 **全套商业摄影高命中提示词模板库**：涵盖布光、镜头焦段、皮肤毛孔与微观漫反射质感。

---

## 🏗️ 知识架构与目录索引

```text
lora-visual-mastery/
├── SKILL.md                          # AI 智能体 (Agent) 自动化调用技能定义
├── LICENSE                           # MIT 开源协议
├── references/
│   ├── lora-parameters.md            # 底层 Rank/Dim/Alpha 数学与分层控制 (Block Weighting)
│   ├── slider-mechanisms.md          # LECO 概念滑块正负权重调节物理机制
│   ├── prompt-recipes.md             # 商业写真、新中式国风、SDXL秀场全景高命中配方
│   └── liblib-models-guide.md        # Liblib 10 大热门模型图谱与配比速查
└── workflows/
    └── comfyui-lora-stack-template.json # ComfyUI 多 LoRA 堆叠与 ADetailer 重绘模板
```

---

## ⚡ 底模代际与硬件运行基准 (Hardware & Architecture)

在加载 LoRA 之前，首先明确其**底模代际**。不同架构的 LoRA 绝不可混用：

```
           ┌───────────────────────┬────────────────────────┐
           │   Stable Diffusion 1.5│        SDXL 1.0        │
┌──────────┼───────────────────────┼────────────────────────┤
│ 典型分辨率│ 512×512 / 512×768     │ 1024×1024 / 832×1216   │
│ 显存基准 │ 4GB - 8GB             │ 8GB - 16GB (支持分层)  │
│ 文本编码器│ 单 CLIP ViT-L/14      │ 双 CLIP (ViT-L + OpenCLIP)│
│ 代表模型 │ 麦橘写实、MajicMIX    │ Juggernaut XL、麦橘 XL │
│ 适用场景 │ 微表情滑块、精细肢体微调 │ 高清织物材质、宏观光影质感 │
└──────────┴───────────────────────┴────────────────────────┘
```

---

## 🎛️ 核心模型使用指南与参数表 (Arsenal Specs)

| 模型类别 | 代表模型 | 推荐权重 | 核心触发词 / 机制 | 针对效果 |
| :--- | :--- | :---: | :--- | :--- |
| **手部解剖** | `Realhands真实手部` | `0.6 ~ 0.8` (重绘 1.0) | `milokk, hand pose, fingers, holding` | 根治多指、融指与手部畸形 |
| **超清织物** | `pantyhose_xl_v1` | `0.7 ~ 0.85` | `black_pantyhose, realistic, sheen` | 物理半透透光、微反光与织物纹理 |
| **微表情滑块** | `笑容大小调节神器` | `-1.5 ~ +1.5` | 无需词，`+`笑意 / `-`清冷厌世 | 连续无级调控角色神态与亲和力 |
| **骨相轮廓** | `脸型大小调节神器` | `-1.2 ~ +1.2` | 无需词，`+`小V脸 / `-`幼态婴儿肥 | 收紧下颌线或赋予脸颊肉感 |
| **体态重塑** | `S-shape body 调节器`| `1.5 ~ 2.5` | 无需词， ResNet 通道微调 | 优化腰臀比与曲线，不改动面容 |
| **下肢比例** | `真实感修长双腿` | `0.6 ~ 0.75` | `jiyeon2, slender legs, long legs` | 改善头身比，拉长下肢线条 |

---

## ⚖️ 多 LoRA 组装安全预算定律 (Budget Law)

```
画面中同时加载的所有 LoRA 权重绝对值之和 <= 2.2
```

```
           ┌────────────────────────────────────────┐
           │          总权重安全预算池 <= 2.2        │
           └───────────────────┬────────────────────┘
                               │
         ┌─────────────┬───────┴───────┬─────────────┐
         ▼             ▼               ▼             ▼
   【面部与神态】  【身形体态】    【特定服饰/配饰】 【细节/手部修复】
    初恋脸/笑容滑块 S曲线/修长腿     蕾丝眼罩/裹胸/腰丝 背景增强/Realhands
     配额: 0.6-0.8 配额: 0.5-0.7     配额: 0.5-0.7   配额: 0.3-0.5
```

---

## 📸 商业摄影级提示词（Prompt Template）高命中模板

### 【正向提示词 Prompt】
```text
(masterpiece, best quality, ultra-detailed:1.2), 1girl, solo, 
(pure and delicate face, natural skin texture, visible skin pores:1.15), 
brown soft eyes, glossy lips, gentle slight smile, slender neck, elegant clavicle, 
wearing (delicate white lace bralette:1.1), (sheer black pantyhose, fine texture:1.1), 
sitting on soft beige sofa, afternoon sunbeam through blinds, cinematic lighting, 
photorealistic, 85mm portrait lens, f/1.4, shallow depth of field, 8k resolution,
<lora:【麻瓜lora】人脸调节神器合集_【麻瓜lora】笑容大小调节神器(2):0.8>,
<lora:【麻瓜lora】人脸调节神器合集_【麻瓜lora】脸型大小调节神器(1):0.5>,
<lora:【麻瓜lora】身材调节器S-shape body(1.5-2.5)_v1.0(2):1.8>,
<lora:Realhands真实手部_v1.0:0.75>, milokk, hand pose, delicate fingers
```

### 【通用负向过滤词 Negative Prompt】
```text
(worst quality, low quality, normal quality:1.4), (deformed, distorted, disfigured:1.3), 
bad anatomy, bad hands, missing fingers, extra fingers, fused fingers, mutated hands, 
poorly drawn hands, poorly drawn face, mutation, deformed limbs, floating limbs, 
plastic skin, oversaturated, unnatural reflections, fake face, blurry, draft, watermark
```

---

## 📚 教程与官方学习资源

本项目提炼自权威官方实践教程：
* 📺 **Bilibili LoRA 基础知识教程**：[`BV1ML411d7pR`](https://www.bilibili.com/video/BV1ML411d7pR/)（低秩自适应数学原理、底模冻结与增量微调机制）
* 📺 **Bilibili LoRA 进阶使用技巧**：[`BV1mL41197UM`](https://www.bilibili.com/video/BV1mL41197UM/)（触发词安放位置敏感性、分层权重 LoRA Block Weighting）
* 🌐 **Liblib.art 在线模型库**：详见 [`references/liblib-models-guide.md`](references/liblib-models-guide.md)

---

## 📄 开源许可证

本项目基于 [MIT License](LICENSE) 开源。欢迎广大创作者点亮右上角 Star ⭐️ 并 Fork 扩展！
