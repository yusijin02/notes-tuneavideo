# Tune-A-Video: 视频生成新SOTA

Author: <a href="https://yusijin02.github.io/">Sijin Yu</a>

> **标题**: Tune-A-Video: One-Shot Tuning of Image Diffusion Models for Text-to-Video Generation
>
> **会议/期刊**: ICCV 2023
>
> **HomePage**: https://tuneavideo.github.io

[TOC]

## 1. Abstract

- 大规模**文本到图像 (text-to-image, T2I) 模型**的惊人生成能力展示了学习复杂结构和有意义语义的强大力量.
- 尽管它们取得了有希望的结果, 但这种范式在计算上非常昂贵. 
- 在这项工作中，我们提出了一种新的**文本到视频 (text-video, T2V)** 生成设置——单次视频调整, 其中只展示了一个文本-视频对.
- 我们的模型是基于最先进的文本到图像 (T2I) 扩散模型构建的, 这些模型是在大量图像数据上预训练的.
- 我们做出了两个关键观察：1) 文本到图像 (T2I) 模型可以生成代表动词术语的静态图像; 2) 将文本到图像模型扩展以同时生成多个图像, 展示出令人惊讶的良好内容一致性.
- 为了进一步学习连续运动, 我们引入了Tune-A-Video, 它涉及到一个量身定制的时空注意机制和一个高效的单次调整策略.
- 在推理过程中, 我们采用DDIM反演来为采样提供结构指导.
- 广泛的定性和定量实验展示了我们的方法在各种应用中的显著能力.

## 2. Motivation & Contribution

### 2.1 Motivation

- 基于大规模多模态数据集的文本到图像 (T2I) 生成模型的发展激发了对文本到视频 (T2V) 生成的探索, 但目前的T2V方法需要大量的训练和资源.
- 人类可以基于现有知识创造性地推断新概念, 这引发了一个问题: T2I模型是否也能类似于人类思维过程, 从单个例子中推断出新的视频.

### 2.2 Contribution

-  提出了一种新的T2V生成方法, 仅使用单个文本-视频对, 大大减少了对大规模视频数据集训练的需求.
-  提出了首个使用预训练T2I模型进行T2V生成的框架, 命名为Tune-A-Video.
- 引入了一种稀疏时空注意机制和高效的调整策略, 以改善视频生成中的时间连贯性.
- 通过广泛的定性和定量实验展示了Tune-A-Video的优越性, 展示了在多种应用中的显著结果.

## 3. Method

<img src="./imgs/1.png" alt="1" style="zoom:50%;" />

- 令 $\mathcal V=\{v_i|i\in[1, m]\}$ 表示 $m$ 帧的视频, $\mathcal P$ 为对视频 $\mathcal V$ 的描述 prompt.
- 目标: 修改 prompt $\mathcal P$, 变成 $\mathcal P^*$, 生成对应的新视频 $\mathcal V^*$.

![2](./imgs/2.png)

### 3.1 Spatio-Temporal Attention (ST-Attn)

<img src="./imgs/3.png" alt="3" style="zoom:50%;" />

- 在生成第 $i$ 帧的 latent variable $z_{v_i}$ 时, 使用第一帧 $z_1$ 和上一帧 $z_{v_{i-1}}$.
  - $Q=W^Q\cdot z_{v_i}$.
  - $K=W^K\cdot \text{Concat}(z_{v_1}, z_{v_{i-1}})$.
  - $V=W^V\cdot \text{Concat}(z_{v_1}, z_{v_{i-1}})$.

## 4. Experiment

<img src="./imgs/4.png" alt="4" style="zoom:50%;" />















































