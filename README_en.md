# RK3576 Edge AI Voice Assistant

An embedded edge AI voice assistant system based on the RK3576 Linux platform, integrating speech interaction, large language model inference, and edge AI deployment.

## Overview

This project implements an end-to-end AI voice interaction system on an embedded Linux platform.

The system integrates:

- Audio acquisition
- Voice activity detection
- Wake word detection
- Automatic speech recognition (ASR)
- Large language model (LLM) interaction
- Text-to-speech (TTS) synthesis

The project explores the deployment and optimization of AI models on resource-constrained edge devices, including model conversion, NPU acceleration, and heterogeneous computing.

---

## System Architecture

The system adopts a hybrid multi-process and multi-thread architecture.

- The main program uses multiple processes to isolate major functional modules, improving system stability.
- Each module internally uses multithreading to handle parallel tasks.
- Queue-based communication is applied to build an asynchronous producer-consumer pipeline.

High-level pipeline:

```
Audio Input
     |
     v
Audio Processing
     |
     v
Wake Word Detection
     |
     v
ASR (Whisper)
     |
     v
LLM (DeepSeek)
     |
     v
TTS (Piper)
     |
     v
Audio Output
```

---

## Key Features

### Speech Interaction Pipeline

- ALSA-based audio capture
- WebRTC VAD for voice activity detection
- OpenWakeWord for wake word recognition
- Whisper ASR deployment
- Piper TTS synthesis

### Edge AI Deployment

- RK3576 Linux edge computing platform
- ONNX to RKNN model conversion
- NPU accelerated inference
- CPU + NPU heterogeneous computing

### AI Agent Capability

- DeepSeek LLM integration
- System prompt based character configuration
- Memory architecture for continuous interaction
- RAG-based extension for long-term information retrieval

---

## Hardware Platform

| Component | Description |
| --- | --- |
| Computing Platform | RK3576 Linux Development Board |
| Operating System | Linux |
| AI Accelerator | NPU |
| Development Language | Python |

---

## Technical Highlights

### Multi-process and Multi-thread Architecture

The system separates major modules into independent processes, including:

- ASR process
- LLM process
- TTS process

Each process contains internal threads for:

- Audio processing
- Model inference
- Data communication
- Playback control

This design improves modularity, stability, and real-time performance.

---

### ONNX to RKNN Deployment

AI models are deployed on RK3576 NPU through the RKNN inference framework.

Deployment workflow:

```
PyTorch / ONNX Model
          |
          v
     RKNN Conversion
          |
          v
     NPU Inference
```

The CPU is responsible for system scheduling and data processing, while the NPU handles neural network inference.

---

### Real-time Voice Interaction

The system implements an asynchronous interaction pipeline to reduce response latency.

Optimization techniques include:

- Pipeline-based processing
- Module decoupling
- TTS interruption mechanism
- Streaming response optimization

---

## Documentation

Detailed technical documents:

- [System Architecture](docs/system_architecture.md)
- [Audio Pipeline](docs/audio_pipeline.md)
- [RKNN Deployment](docs/rknn_deployment.md)
- [Memory Design](docs/memory_design.md)
- [Performance Optimization](docs/optimization.md)

---

## Technology Stack

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

## Project Status

🚧 Under active development
