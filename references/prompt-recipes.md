# 商业摄影级提示词配方大全 (Prompt Recipes)

本参考手册提供在真实商业摄影、写真出图与自媒体视觉制作中验证过的完整提示词配方，支持开箱即用。

---

## 配方 1：高级法式私房光影写真（SD 1.5 标杆）

* **推荐底模**：麦橘写实 / MajicMIX Realistic v7
* **采样器 (Sampler)**：DPM++ 2M Karras 或 Restart, 30~35 步
* **CFG Scale**：6.0 ~ 7.0
* **挂载 LoRA 与权重**：
  * `Realhands真实手部_v1.0`: `0.7`
  * `【麻瓜lora】人脸调节神器合集_【麻瓜lora】笑容大小调节神器`: `0.7`
  * `【麻瓜lora】身材调节器S-shape body`: `1.8`
  * `性感蕾丝眼罩`: `0.6`

```text
(masterpiece, best quality, ultra-detailed:1.2), 1girl, solo, 
(pure delicate facial features, visible natural skin pores, peach fuzz, translucent skin:1.2),
brown pupils, slightly parted glossy lips, gentle faint smile, 
wearing (delicate black lace blindfold covering eyes:1.15), 
(white silk strapless bandeau, intricate embroidery:1.1), (semi-sheer black stockings:1.1), 
reclining gracefully on vintage velvet chaise, Parisian apartment, wooden parquet floor, 
soft afternoon sunlight filtering through lace curtains, dramatic chiaroscuro, natural rim lighting, 
photorealistic, captured on Leica M11, 50mm Summilux lens, f/1.4, creamy bokeh, 8k uhd,
<lora:Realhands真实手部_v1.0:0.7>, milokk, hand pose, fingers, holding,
<lora:【麻瓜lora】人脸调节神器合集_【麻瓜lora】笑容大小调节神器(2):0.7>,
<lora:【麻瓜lora】身材调节器S-shape body(1.5-2.5)_v1.0(2):1.8>,
<lora:性感蕾丝眼罩:0.6>, lace blindfold
```

---

## 配方 2：新中式国风闺阁质感（SD 1.5 国风）

* **挂载 LoRA 与权重**：
  * `初恋脸`: `0.7`
  * `小红兜`: `0.65`
  * `背景细节增强`: `0.4`
  * `【麻瓜lora】人脸调节神器合集_【麻瓜lora】脸型大小调节神器`: `-0.4` (微幼态圆脸)

```text
(masterpiece, top quality:1.2), 1girl, solo, 20yo, 
traditional Chinese beauty, almond eyes, vermilion lips, bashful expression, 
wearing (traditional crimson red silk dudou with golden dragon and lotus embroidery:1.2), 
slender shoulders, visible collarbone, 
sitting in moonlit antique Chinese courtyard garden, carved rosewood screen, soft red lantern illumination, 
falling osmanthus blossoms, misty atmospheric depth, 
Hasselblad medium format, 80mm lens, f/2.0, velvety shadow gradient, 8k resolution,
<lora:初恋脸:0.7>, first love face, pure girl,
<lora:小红兜:0.65>, red dudou, chinese embroidery,
<lora:背景细节增强:0.4>, intricate room details,
<lora:【麻瓜lora】人脸调节神器合集_【麻瓜lora】脸型大小调节神器(1):-0.4>
```

---

## 配方 3：SDXL 商业时尚秀场与极致丝袜光泽（SDXL 专属）

* **推荐底模**：Juggernaut XL / 麦橘 XL
* **采样器**：DPM++ 2M SDE Exponential, 35 步
* **分辨率**：832×1216 或 1024×1536 (高清修复)
* **挂载 LoRA 与权重**：
  * `pantyhose_xl_v1`: `0.8` (单模拉满)

```text
(masterpiece, photorealistic:1.2), 1girl, solo, 
high fashion runway model, striking bone structure, intense gaze, sleek high ponytail, 
wearing (minimalist black blazer dress:1.15), (sheer black pantyhose with elegant micro-sheen:1.2), 
stilettos, confident walking stride, 
minimalist architectural runway, polished concrete floor, sharp studio spotlighting, reflective runway surface, 
shot on Arri Alexa, 35mm cinema lens, ultra-sharp textile weave, natural skin texture, 
cinematic color grading, 8k resolution,
<lora:pantyhose_xl_v1:0.8>, black_pantyhose, realistic, high res, sheen, translucent, delicate texture
```
