# Requirements

## Software

- Maya 2024, 2025, 2026, 2027
- Houdini 20.0, 20.5, 21.0

## System Requirements

- **OS**: Microsoft Windows 10+, Linux CentOS 7+, Linux Rocky 8+, Linux RHEL 8+ (64-bit).
- **CPU**: 64-bit Intel or AMD multi-core processor.
- **GPU**: NVIDIA GPU suggested for accelerated ML workflows, with 6GB of VRAM or more recommended. CPU fallback is supported when GPU execution is not available, but it can be slower.
- **RAM**: 8GB required (16GB or more recommended).
- **Storage**: At least 700MB of free disk space for the standard installation. If ML dependencies are required, then at least 7GB of free disk space.

> [!NOTE]
> Adonis may work with other CPU, GPU, RAM, and VRAM specifications. The list above represents the specifications that have been tested successfully.

> [!NOTE]
> Internet connection is required for licensing and ML dependency download only.

## AdonisFX

- With an AdonisFX license, see [Licensing](licensing#fx-and-ml-bundles) for details, installing the ML dependencies is optional. It is only required to run ML inference on the GPU. If not installed, ML inference runs on the CPU.

## AdonisML

- AdonisML features require an AdonisML license bundle. See [Licensing](licensing#fx-and-ml-bundles) for details.
- ML features run locally and do not require cloud services. Training data remains on the local machine.
- Generating ML training data and training models may require additional disk space and memory depending on the dataset and model size.
- Trained models are generally expected to be under 2GB, but extracted training data may exceed 10GB depending on the scenario.
