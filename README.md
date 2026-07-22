# RK3576 Edge AI Voice Assistant

基于 RK3576 Linux 边缘计算平台的端侧 AI 语音交互系统  
An embedded edge AI voice assistant system based on RK3576 Linux platform.

---

## Overview / 项目简介

This project implements an edge AI voice assistant on RK3576 Linux platform, integrating wake word detection, automatic speech recognition, large language model interaction and text-to-speech synthesis.

本项目基于 RK3576 Linux 边缘计算平台，实现了一套端侧 AI 语音交互系统。

系统集成：
- 语音采集 Audio Capture
- 语音唤醒 Wake Word Detection
- 自动语音识别 ASR
- 大语言模型交互 LLM Interaction
- 语音合成 TTS

探索资源受限嵌入式平台上的 Edge AI Agent 部署方案，包括模型转换、NPU加速以及软硬件协同优化。

---

## Features / 核心功能

### Voice Interaction Pipeline / 语音交互链路

- ALSA based audio capture
- WebRTC VAD voice activity detection
- OpenWakeWord wake word detection
- Whisper ASR speech recognition
- Piper TTS speech synthesis


### Edge AI Deployment / 端侧AI部署

- RK3576 Linux platform
- ONNX → RKNN model conversion
- NPU accelerated inference
- CPU + NPU heterogeneous computing


### AI Agent Capability / 智能交互能力

- DeepSeek LLM integration
- System Prompt based character design
- Memory architecture for continuous interaction

---

## System Architecture / 系统架构

```
Audio Capture
   ↓
[VAD + WakeWord]
   ↓
ASR Queue
   ↓
ASR (Whisper - NPU Core 0)
   ↓
LLM Queue
   ↓
LLM (Loacl - NPU Core 1 / API)(streaming)
   ↓
TTS Queue
   ↓
Sentence Splitter
   ↓
TTS (Piper - NPU Core 0)
   ↓
Audio Buffer Queue
   ↓
ALSA Player
```

---

## Hardware Platform / 硬件平台

| Component | Description |
|---|---|
| Computing Platform | RK3576 Linux Development Board |
| Operating System | Linux |
| AI Accelerator | NPU |
| Programming Language | Python |

---

## Technical Highlights / 技术亮点

### CPU + NPU Heterogeneous Computing
基于 RK3576 NPU 完成 AI 模型部署，实现 CPU 负责系统调度与数据处理，NPU 负责神经网络推理。

### Modular Pipeline Architecture
采用 Python threading + queue.Queue 构建生产者-消费者架构，实现音频采集、ASR、LLM、TTS模块解耦。

### Real-time Voice Interaction
设计异步语音处理流程，支持连续对话以及TTS播放抢占机制。

---

## Documentation / 详细文档

- [System Architecture / 系统架构](docs/system_architecture.md)
- [Audio Pipeline / 音频流水线](docs/audio_pipeline.md)
- [RKNN Deployment / RKNN部署](docs/rknn_deployment.md)
- [Memory Design / 记忆系统设计](docs/memory_design.md)
- [Optimization / 性能优化](docs/optimization.md)

---

## Project Status / 项目状态

🚧 Under active development / 持续开发中
