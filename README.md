# EdgeVoice
## RK3576 Embedded Edge AI Voice Assistant

基于 RK3576 Linux 边缘计算平台的端侧 AI 语音交互系统。

本项目实现了一套完整的语音交互 pipeline，
集成语音采集、唤醒检测、自动语音识别、大语言模型交互以及语音合成模块，
探索在资源受限嵌入式平台上的 Edge AI Agent 部署方案。

---

## Features

### Voice Interaction Pipeline

- Audio capture based on ALSA
- WebRTC VAD voice activity detection
- OpenWakeWord wake word detection
- Whisper ASR speech recognition
- Piper TTS speech synthesis

### Edge AI Deployment

- RK3576 Linux platform
- ONNX → RKNN model conversion
- NPU accelerated inference
- CPU + NPU heterogeneous computing

### AI Agent Capability

- DeepSeek LLM integration
- System Prompt based character design
- Memory architecture for long-term interaction

---

## System Architecture

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

## Hardware Platform

- Board: LKD3576 / RK3576
- OS: Embedded Linux
- Compute:
  - CPU
  - NPU accelerator

---

## Documentation

详细设计：

- [System Architecture](docs/system_architecture.md)
- [RKNN Deployment](docs/rknn_deployment.md)
- [Audio Pipeline](docs/audio_pipeline.md)
- [Memory Design](docs/memory_design.md)
- [Optimization](docs/optimization.md)
