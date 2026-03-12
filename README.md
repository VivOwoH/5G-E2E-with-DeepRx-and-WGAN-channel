# 5G End-to-End System with CWGAN-based Channel Surrogate

## Overview
This repository implements a 5G End-to-End (E2E) wireless communication system that solves the non-differentiability problem in joint transmitter-receiver optimization using a **Conditional Wasserstein GAN (CWGAN)** channel surrogate.

**Key Components:**
- **Neural Mapper**: Trainable constellation replacing M-QAM
- **DeepRx**: Fully convolutional neural receiver
- **CWGAN-GP**: Differentiable channel surrogate enabling E2E gradient flow
- **LDPC Coding**: Forward error correction
- **OFDM**: Resource grid-based transmission

## Motivation
Traditional E2E learning fails when channels are non-differentiable or unknown, breaking gradient backpropagation. Our CWGAN surrogate provides a differentiable channel approximation, enabling joint optimization of NN mapper and DeepRx.

## Repository Structure
```
📂 5G-E2E-with-DeepRx-and-WGAN-channel/
├── E2E-noGAN/
│   └── Neural_Receiver-64qam-good.ipynb          # Baseline system
├── WGAN/
│   ├── condition_tests                         # Isolated tests on CWGAN conditions
│   ├── main    # Main CWGAN-E2E system
│   └── plots                 # Visualization
└── Tensorflow-GPU for Ubuntu.pdf       # Setup guide
```

## Results

We evaluate three conditioning approaches for the CWGAN:

| Conditioning | Information Required | Performance |
|--------------|---------------------|-------------|
| **Received Signal (Yᵣg)** | Complete resource grid | Matches ideal E2E |
| **Channel Estimates (ĥ)** | LS + LMMSE estimates | ~2.0 dB degradation |
| **Pilots (xₚ, yₚ)** | Sparse pilot positions | Significant degradation |

**Key Finding**: Performance directly correlates with conditioning information quality, revealing a fundamental trade-off between information availability and system performance.

## Installation & Usage

### Prerequisites
- Python 3.11+, TensorFlow 2.14+
- See `docs/Tensorflow-GPU for Ubuntu.pdf` for GPU setup

### Quick Start
1. **Baseline**: `jupyter notebook E2E-noGAN/Neural_Receiver-64qam-good.ipynb`
2. **CWGAN-E2E**: `jupyter notebook WGAN/main/Neural_Receiver-64qam-refactor-wgan.ipynb`
3. **Visualization**: `jupyter notebook WGAN/plots/Output.ipynb`

## System Parameters
- **Modulation**: 64-QAM (6 bits/symbol)
- **Channel**: 3GPP CDL-C, 10 m/s mobility
- **OFDM**: 14 symbols × 128 subcarriers
- **Training**: Alternating CWGAN → Neural Mapper → DeepRx optimization

## References
- [Sionna](https://nvlabs.github.io/sionna/) - NN mapper and NN receiver implementation
- [WGAN-GP](https://arxiv.org/abs/1704.00028) - Improved GAN training
- [3GPP CDL](https://www.3gpp.org/DynaReport/38901.htm) - Channel models
