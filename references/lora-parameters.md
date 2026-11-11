# LoRA 底层训练参数与网络架构技术手册 (LoRA Technical Specifications)

## 1. 核心数学与超参数概念

LoRA (Low-Rank Adaptation) 的核心思想是冻结预训练底模权重矩阵 $W_0 \in \mathbb{R}^{d \times k}$，通过引入低秩分解矩阵引入增量参数：
$$\Delta W = B \times A$$
其中 $B \in \mathbb{R}^{d \times r}$，$A \in \mathbb{R}^{r \times k}$，秩 $r \ll \min(d, k)$。

最终前向传播计算公式为：
$$h = W_0 x + \Delta W x = W_0 x + \frac{\alpha}{r} (B A) x$$

* **Network Dim (Rank $r$)**：低秩维度。代表 LoRA 能学习的信息容量大小。
  * `r = 64`：手部姿态、特定服饰（轻量级，抗过拟合强）。
  * `r = 128`：全套光影、复杂材质（如 SDXL pantyhose、修长双腿）。
* **Network Alpha ($\alpha$)**：缩放比例系数。决定了 LoRA 权重注入底模时的激活放大强度。
  * 当 $\alpha = r$ 时，缩放比例为 1.0；
  * 当 $\alpha = r/2$ 时（如 Realhands: dim=64, alpha=32），有效步长减半，学习率更稳定，微调更平滑细腻。

---

## 2. 本地六大核心模型参数逆向分析表

```
┌──────────────────────────────────────┬──────────┬───────┬───────┬────────────┬────────────────────────┐
│ 模型文件名                           │ 底模代际 │ Dim   │ Alpha │ 存储体积   │ 作用网络模块           │
├──────────────────────────────────────┼──────────┼───────┼───────┼────────────┼────────────────────────┤
│ Realhands真实手部_v1.0.safetensors   │ SD 1.5   │ 64    │ 32    │ 72.1 MB    │ UNet Cross-Attn / Down │
│ pantyhose_xl_v1.safetensors          │ SDXL 1.0 │ 128   │ 128   │ 649.7 MB   │ 双 CLIP + 全 UNet 层   │
│ 【麻瓜lora】笑容大小调节神器          │ SD 1.5   │ LECO  │ LECO  │ 4.6 MB     │ TextEncoder + Attn2    │
│ 【麻瓜lora】脸型大小调节神器          │ SD 1.5   │ LECO  │ LECO  │ 4.6 MB     │ TextEncoder + Attn2    │
│ 【麻瓜lora】身材调节器S-shape body   │ SD 1.5   │ UNet  │ UNet  │ 6.1 MB     │ ResNet / Cross-Attn    │
│ 真实感修长双腿_v 10.safetensors       │ SD 1.5   │ 128   │ 128   │ 144.1 MB   │ UNet Middle / Up-Blocks│
└──────────────────────────────────────┴──────────┴───────┴───────┴────────────┴────────────────────────┘
```

---

## 3. 分层权重控制（LoRA Block Weighting）高级玩法

在 WebUI 或 ComfyUI 中，可通过指定 17 或 26 个分层块（Blocks）的权重向量，实现精细外科手术级控制：

```text
# 仅保留 LoRA 的衣服与身材，完全剥离其脸部特征：
1,1,1,1,1, 1,1,1,1,1, 0,0,0,0,0,0,0
(IN输入层生效，MID骨架生效，OUT高频面部细节层全部归零)
```
