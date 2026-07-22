# System Architecture

## 1. Overview/ 项目概述

The system is designed as an embedded edge AI voice assistant running on the RK3576 Linux platform.

The architecture integrates multiple AI and signal processing modules, including audio acquisition, wake word detection, automatic speech recognition (ASR), large language model inference, and text-to-speech synthesis.

To achieve real-time interaction on resource-constrained edge hardware, the system adopts a modular asynchronous architecture based on multiprocessing, multithreading, and queue-based communication.

本系统基于 RK3576 Linux 边缘计算平台，实现了一套端侧 AI 语音交互系统。

系统集成音频采集、语音唤醒、自动语音识别（ASR）、大语言模型推理以及语音合成（TTS）等多个模块，实现从用户语音输入到智能回复输出的完整交互链路。

针对嵌入式设备计算资源有限以及多 AI 模型协同运行的需求，系统采用多进程 + 多线程混合架构，通过 Queue 实现模块间异步通信，提高系统稳定性和实时交互能力。

## 2. Design Goals/ 设计目标

The system is designed with the following goals:

### Modular Design

Separate different functional modules to improve maintainability and scalability.

### Real-time Interaction

Reduce response latency through asynchronous processing and pipeline execution.

### Edge AI Deployment

Deploy neural network models locally on RK3576 NPU to reduce cloud dependency.

### Resource Optimization

Efficiently utilize CPU and NPU resources through heterogeneous computing.

系统设计主要围绕以下目标：

### 模块化设计

将语音采集、ASR、LLM、TTS等功能模块解耦，提高系统可维护性和扩展能力。

### 实时交互

通过异步流水线和并行处理降低语音交互延迟。

### 端侧AI部署

将AI模型部署于RK3576 NPU，实现本地推理，降低对云端服务的依赖。

### 资源优化

利用CPU+NPU异构计算方式，提高嵌入式平台计算资源利用率。

## 3. Hardware Platform / 硬件平台

The system is deployed on the RK3576 Linux edge computing platform.

RK3576 provides CPU resources and NPU acceleration capability for local AI inference tasks, enabling heterogeneous execution of speech processing and memory-related workloads.

The system adopts a hybrid edge-cloud architecture:

- Local NPU acceleration is used for speech models and offline AI processing.
- Cloud LLM API is used for high-quality online conversation.
- Local LLM inference provides offline interaction capability and supports memory refinement tasks.

### Hardware Specification

| Component | Description |
| --- | --- |
| Platform | RK3576 Linux Development Board |
| Operating System | Linux |
| Processor | ARM CPU |
| AI Accelerator | NPU |
| Audio Interface | ALSA |

本系统部署于 RK3576 Linux 边缘计算平台。

RK3576 提供 CPU 计算资源以及 NPU AI 加速能力，用于本地语音模型推理以及部分 AI 任务处理。

系统采用端云协同架构：

- 本地 NPU 负责语音模型推理以及离线 AI 任务；
- 在线状态下通过云端 LLM API 提供主要对话能力；
- 本地 LLM 作为离线交互方案，同时在线状态下负责 Memory 信息提炼任务。

### 硬件配置

| 模块 | 描述 |
|---|---|
| 平台 | RK3576 Linux开发板 |
| 系统 | Linux |
| 处理单元 | ARM CPU |
| AI加速 | NPU |
| 音频接口 | ALSA |

## 4. Software Architecture/软件架构

The software system adopts a modular multi-process architecture combined with internal multithreading.

The main controller process manages system states, process lifecycle, audio acquisition, and inter-process communication.

Independent processes are used for major functional modules, including ASR, LLM, and TTS. Each process contains multiple threads to improve concurrency and processing efficiency.

### Main Controller

The main controller acts as the central scheduler of the system.

Responsibilities include:

- System state management
- Audio capture control
- Process initialization and termination
- Queue communication coordination
- Interaction flow control

The controller maintains the overall interaction state:

IDLE
|
Wake Detection
|
Speech Recognition
|
LLM Processing
|
TTS Generation
|
Playing
|
IDLE
系统采用模块化多进程架构，并结合模块内部多线程设计。

主控制进程负责系统状态管理、子进程生命周期管理、音频采集控制以及模块间通信协调。

ASR、LLM、TTS等核心功能模块采用独立进程运行，各模块内部通过多线程实现任务并行，提高系统实时性和稳定性。



## 5. Multi-process and Multi-thread Design

## 6. Inter-process Communication

## 7. State Machine Design

## 8. CPU/NPU Resource Allocation
