# RK3576 端侧 AI 语音交互系统

基于 RK3576 Linux 边缘计算平台的智能语音助手系统。

本项目面向嵌入式端侧 AI 场景，设计并实现了一套完整的语音交互链路，融合语音采集、语音唤醒、自动语音识别、大语言模型交互以及语音合成模块，实现自然语言交互能力。

项目重点探索资源受限嵌入式设备上的 AI 模型部署与系统优化，包括模型转换、NPU 加速以及软硬件协同设计。

---

# 项目概述

系统整体由以下模块组成：

- 音频采集模块
- 语音活动检测（VAD）
- 语音唤醒模块
- 自动语音识别（ASR）
- 大语言模型交互（LLM）
- 语音合成（TTS）
- 音频播放模块

实现从用户语音输入到智能回复输出的完整闭环。

---

# 系统架构

系统采用 **多进程 + 多线程混合架构**。

整体设计：

- 主程序通过多进程隔离audio capture、 ASR、LLM、TTS 等核心模块，提高系统稳定性；
- 各功能模块内部采用多线程，或多进程处理任务，实现音频采集、模型推理、数据传输等任务并行执行；
- 使用 Queue 实现模块间异步通信，构建生产者-消费者流水线。

系统流程：

```
麦克风输入
    |
    v
音频处理
    |
    v
语音唤醒
    |
    v
Whisper ASR
    |
    v
DeepSeek LLM
    |
    v
Piper TTS
    |
    v
扬声器输出
```

---

# 核心功能

## 1. 语音交互链路

实现完整端侧语音处理流程：

- 基于 ALSA 完成 PCM 音频采集
- 基于 WebRTC VAD 实现人声检测
- 基于 OpenWakeWord 实现唤醒词检测
- 基于 Whisper 完成语音识别
- 基于 Piper 完成语音合成

---

## 2. Edge AI 模型部署

基于 RK3576 NPU 完成 AI 模型部署：

- ONNX 模型转换为 RKNN 格式
- 使用 RKNN Runtime 完成 NPU 推理
- 构建 CPU + NPU 异构计算架构

资源分配：

- CPU：
  - 系统调度
  - 音频处理
  - 数据管理

- NPU：
  - 神经网络模型推理

---

## 3. 大语言模型交互

集成 DeepSeek 大语言模型，实现自然语言理解与生成。

主要功能：

- System Prompt 角色设定
- 多轮对话支持
- Memory 机制设计
- RAG 长期信息检索扩展

---

# 技术亮点

## 多进程多线程架构设计

针对语音交互系统中多个模块并行运行的需求：

- 使用进程隔离计算密集型模块；
- 使用线程提升模块内部任务并行能力；
- 使用消息队列降低模块耦合。

提高系统的：

- 可维护性
- 稳定性
- 扩展能力

---

## ONNX → RKNN 部署流程

AI模型部署流程：

```
训练模型 / ONNX模型
          |
          v
      RKNN转换
          |
          v
      NPU推理
```

实现 AI 模型从通用格式到嵌入式 NPU 平台的部署。

---

## 实时交互优化

针对语音交互延迟问题，实现：

- 异步流水线处理
- 模块解耦设计
- TTS播放抢占机制
- 流式响应优化

提升连续对话体验。

---

# 硬件平台

| 项目 | 参数 |
|-|-|
| 计算平台 | RK3576 Linux开发板 |
| 操作系统 | Linux |
| AI加速 | NPU |
| 开发语言 | Python |

---

# 技术栈

```
Python
Linux
RK3576
RKNN
ONNX
Whisper
DeepSeek
Piper TTS
WebRTC VAD
OpenWakeWord
ALSA
RAG
```

---

# 项目文档

详细设计：

- [系统架构设计](docs/system_architecture_CN.md)
- [音频处理流程](docs/audio_pipeline_CN.md)
- [RKNN模型部署](docs/rknn_deployment_CN.md)
- [Memory设计](docs/memory_design_CN.md)
- [性能优化](docs/optimization_CN.md)

---

# 项目状态

🚧 持续开发中
