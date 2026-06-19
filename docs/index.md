# Introduction

Welcome to the technical documentation for Adonis.

Adonis provides tools for building, simulating, and accelerating high-quality deformation workflows for digital characters. It is available for Maya and Houdini, with workflows that support both physics-based simulation and machine learning-assisted deformation.

The documentation is organized around two main areas:

- **AdonisFX**: Tools for creature and character simulation, including muscle, fat, skin, face, and related deformation workflows.
- **AdonisML**: Machine learning tools for digital anatomy workflows, including data extraction, neural clustering, model training, pose-based neural deformation, and smart tissue simulation.

If you need more information or help, please send an email to **adonis.support@inbibo.co.uk**.

## AdonisFX

**AdonisFX** provides fast and intuitive tools for creature and character deformation. It includes modular solvers and deformers for muscle, fat, skin, face, and related physical or procedural deformation workflows.

The modularity of the AdonisFX components allows artists and technical directors to set up characters in multiple ways, depending on the needs of the rig, shot, or production pipeline. Components can be combined to build full digital anatomy setups, targeted deformation setups, or hybrid simulation workflows where only selected parts of the character require simulation.

AdonisFX is designed to help teams build high-quality digital anatomy setups directly inside Maya and Houdini. These workflows can be integrated into animation rigs, rigging pipelines, CFX pipelines, and procedural character workflows.

## AdonisML

**AdonisML** brings machine learning into the Adonis digital anatomy framework.

AdonisML works in two main layers:

- **AdonisML Deformer**: A pose-based neural deformer that provides interactive-speed feedback for high-quality skin deformation.
- **Smart tissue**: A dynamics layer that adds inertial detail such as jiggle, settle, and overshoot, which pose-based ML deformation does not usually capture on its own.

The AdonisML Deformer allows animators to work interactively with a high-quality representation of the character deformation. Because pose-based ML deformers are trained from pose data, their output is based on the current pose and does not directly represent motion, velocity, or dynamic history.

AdonisML provides tools to define narrow locality for ML deformation, helping the trained model isolate local deformation behavior more effectively. Neural clustering and training workflows allow users to guide how different regions of the character are learned and evaluated.

Smart tissue complements the pose-based deformer by adding dynamic behavior on top of the ML-driven result. It uses neural predictions of underlying muscle activation to drive simulation behavior without requiring artists to control complex physical parameters directly.

Together, the AdonisML Deformer and smart tissue provide a workflow for interactive deformation feedback and fast dynamic detail. This allows teams to enhance simulation results without always requiring a full anatomy simulation setup for every iteration or shot.

## Key Values

Adonis is designed to provide fast, artist-friendly workflows for high-quality character deformation. It combines interactive setup tools, simulation solvers, deformation utilities, modular components, and machine learning workflows to help teams build and iterate on complex digital characters.

The key values of Adonis are:

- **Fast Computation**. High-quality creature and character deformation can be expensive to compute, especially when traditional simulation workflows are used throughout production. Adonis is designed to deliver high-quality results quickly, making it easier to iterate on rigs, shots, and character setups.

- **Quick Setup**. Preparing a character for realistic deformation can be time-consuming and often requires specialized knowledge of physical parameters, rig structure, and deformation workflows. Adonis provides intuitive tools and parameters that help artists and technical directors set up complex deformation systems more efficiently.

- **Modular Workflows**. AdonisFX components can be combined in different ways to support full simulation setups, targeted deformation setups, and hybrid simulation approaches. This allows teams to adapt the workflow to the needs of each character or shot.

- **Interactive Feedback**. AdonisML enables animators to work with interactive-speed feedback from trained neural deformation models. This helps reduce the time spent waiting for simulation or playblast results during shot iteration.

- **Local ML Deformation**. AdonisML provides workflows for defining local deformation regions, helping ML models learn and evaluate deformation with narrower locality where needed.

- **Dynamic Detail**. Smart tissue adds dynamic behavior such as jiggle, settling, and overshoot to ML-driven deformation workflows. This helps recover motion-driven detail that pose-based neural deformation does not capture by itself.

- **Pipeline Flexibility**. Adonis workflows can be integrated into animation rigs, rigging pipelines, CFX pipelines, and procedural workflows. Adonis data can also support cross-DCC workflows between Maya and Houdini where supported.

## Why Adonis?

With Adonis you can:

- integrate simulation and deformation tools into animation rigs,
- integrate deformation workflows into rigging, CFX, and procedural pipelines,
- build modular physics-based character deformation setups with artist-friendly controls,
- combine components in different ways depending on the character, shot, or pipeline,
- use hybrid simulation workflows when only specific character regions need simulation,
- extract data from simulation workflows for ML training,
- train neural models from representative character motion and deformation data,
- define local regions for ML deformation workflows,
- use pose-based ML deformation for interactive-speed feedback,
- use smart tissue to add fast dynamic behavior on top of ML-driven deformation,
- enhance simulation results without requiring a full anatomy simulation setup for every iteration,
- cache results for faster playblast and review workflows,
- get results rapidly after feedback is received,
- accelerate shot feedback iteration,
- deliver finalized work sooner, and
- save time compared to standard CFX workflows.
