# Requirements

## Software

- Maya 2024, 2025, 2026, 2027
- Houdini 20.0, 20.5, 21.0

## System Requirements

- **OS**: Microsoft Windows 10+, Linux CentOS 7+, Linux Rocky 8+, Linux RHEL 8+ (64-bit).
- **CPU**: 64-bit Intel or AMD multi-core processor.
- **GPU**: NVIDIA GPU required for GPU-accelerated ML workflows, with 12GB of VRAM or more recommended. CPU fallback is supported when GPU execution is not available, but it can be significantly slower.
- **RAM**: 8GB required (16GB or more recommended).
- **Storage**: At least 700MB of free disk space to install. Installing the ML dependencies requires approximately 6GB to 7GB of free disk space.

> [!NOTE]
> - Adonis may work with other CPU, GPU, RAM, and VRAM specifications.
> - The list above represents the specifications that have been tested successfully.
> - Internet connection is required for licensing only.
> - Standalone script execution outside the DCC requires a separate Python interpreter to be installed.
> - ML features do not store training data outside the user environment and do not access cloud services.
> - FX users can install the ML dependencies to use GPU inference, but this is optional.
> - Some features require a specific Adonis license bundle. For example, FX features require an AdonisFX bundle, and ML features require an AdonisML bundle.
> - Generating ML training data and training models may require additional disk space and memory depending on the dataset and model size.
> - Trained models are generally expected to be under 2GB, but extracted training data may exceed 10GB depending on the scenario.
