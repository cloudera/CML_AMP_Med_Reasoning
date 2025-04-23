Reinforcement Learning Fine-Tuning with GRPO for Medical Reasoning
==================================================================

Overview
--------

This project demonstrates **how to fine-tune a language model using GRPO (Group Relative Policy Optimization)** specifically for medical reasoning tasks. By leveraging custom reward functions and a specialized medical reasoning dataset, we transform a general-purpose language model into a domain-specific medical reasoning model. Note that the information provided here is intended solely for educational purposes and cannot substitute for professional medical advice.

* * * * *

Launching the Project on CAI
----------------------------

This AMP was developed against Python 3.10. There are two ways to launch the project on CAI:

1.  From Prototype Catalog - Navigate to the AMPs tab on a CML workspace, select the "Build Your Own Medical Reasoning Model" tile, click "Launch as Project", click "Configure Project"
2.  As an AMP - In a CML workspace, click "New Project", add a Project Name, select "AMPs" as the Initial Setup option, copy in this repo URL, click "Create Project", click "Configure Project"

* * * * *

Project Workflow
----------------

1.  **Load Pre-trained Model**
2.  **Prepare the Dataset**
3.  **Define Reward Functions & Verifiers**
4.  **Simulate GRPO Training Run**
5.  **Evaluate Model Checkpoint**
6.  **Run Inference with Fine-tuned Model**

* * * * *

Key Features
------------

### Flexible Model Selection

-   Support for multiple base models:
    -   Llama 3.1-8B-Instruct (default)
    -   Qwen2.5, Phi-4, Gemma 3 and more
    -   GRPO can be used with various base models, but it’s generally recommended to use models with 1.5 billion or more parameters for optimal reasoning performance

### Advanced Fine-Tuning Technique

-   **GRPO (Group Relative Policy Optimization)**
    -   Rewards desired output features
    -   Improves model responses through custom feedback
    -   Maintains model stability during optimization

### Customizable Reward Functions

-   Evaluate model outputs for:
    -   Correctness (semantic alignment with references)
    -   Response formatting (e.g., tag presence)
    -   Clinical accuracy (evaluated via perplexity)

* * * * *

Getting Started
---------------

### Prerequisites

-   Python 3.10, 3.11, 3.12 are compatible
-   GPU with min 5GB VRAM (for models ≤1.5B parameters). Recommended runtime: 4vCPU, 16GB RAM, 1 GPU 
-   Runtimes with a GPU are required if you trigger full GRPO training, as GPU is needed for GRPO training
-   For a notebook walkthru without triggering the GRPO training run, the GPU requirement can be dropped and a 1vCPU & 4GB RAM is sufficient

### Project Setup

1.  Open `starter_notebook.ipynb`
2.  Run setup cells to install dependencies
3.  Review reward function configurations
4.  **(Optional)** Trigger full GRPO training (≈ 3 hours with preset configs)

* * * * *

Usage Guide
-----------

### Quick Start

1.  Use provided pre-trained checkpoint for demo
2.  Customize base model and dataset paths easily – just change the model or dataset in the notebook
3.  Adjust reward functions as needed

### Fine-Tuning Workflow

1.  Prepare your training dataset
2.  Define reward functions
3.  Configure training parameters
4.  Run GRPO training

### Example: Training Dataset Preparation

```
from datasets import load_dataset

# Load medical reasoning dataset
dataset = load_dataset('your/medical/dataset')

# Prepare system prompt
SYSTEM_PROMPT = """
Respond in the following format:
<reasoning>
...
</reasoning>
<answer>
...
</answer>
"""

```

Advanced Customization
----------------------

### Swap in Different Base Models

To switch models, update this line in the notebook:

```
model_name = "meta-llama/Meta-Llama-3.1-8B-Instruct" 
# Swap with another base model 
# model_name = "Qwen/Qwen2.5-7B" 
# model_name = "microsoft/Phi-4" 
# model_name = "google/gemma-3-1b-it"
```

All training and evaluation logic works across supported architectures with minimal changes

### Swap in New Datasets Easily

Just replace the dataset loading line:

```
dataset = load_dataset('your/medical/dataset')
# Swap with another dataset:
# dataset = load_dataset('your/specific/dataset')
```

Make sure the new dataset provides prompt--response pairs or can be adapted using preprocessing (examples provided in the notebook)

### Custom Reward Functions

Plug in new reward functions as needed:

-   The notebook includes modular functions for correctness, formatting, and quality
-   Easily extendable to include factuality checks, custom verifiers and more

* * * * *

Fine-Tuning Considerations
--------------------------

-   Compute-intensive process (≈ 3 hours with default config)
-   Pre-trained checkpoints available for quick testing
-   Workflow is modular and fully customizable

* * * * *

Reward Function Examples
------------------------

-   **Correctness Reward**: Compare model output to reference answer
-   **Format Reward**: Ensure XML-like response structure
-   **Quality Reward**: Validate output fluency via perplexity scoring

* * * * *

Performance Optimization
------------------------

-   Uses LoRA for parameter-efficient fine-tuning
-   Supports mixed-precision training (bfloat16/fp16)
-   Configurable batch sizes, training schedule and gradient accumulation

* * * * *

Recommended Next Steps
----------------------

-   Experiment with different reward function designs. The notebook contains examples with semantic correctness, perplexity and tag presence
-   Test model performance across various medical reasoning scenarios
-   Try different base models and datasets

* * * * *

References
----------------------

https://docs.unsloth.ai/basics/reasoning-grpo-and-rl

* * * * *

The Fine Print
----------------------

IMPORTANT: Please read the following before proceeding. This AMP includes or otherwise depends on certain third party software packages. Information about such third party software packages are made available in the notice file associated with this AMP. By configuring and launching this AMP, you will cause such third party software packages to be downloaded and installed into your environment, in some instances, from third parties' websites. For each third party software package, please see the notice file and the applicable websites for more information, including the applicable license terms.

If you do not wish to download and install the third party software packages, do not configure, launch or otherwise use this AMP. By configuring, launching or otherwise using the AMP, you acknowledge the foregoing statement and agree that Cloudera is not responsible or liable in any way for the third party software packages.

Copyright (c) 2025 - Cloudera, Inc. All rights reserved.