# ROS2-Documentation-Based LLM Fine-Tuning with Llama 3.2 and LoRA

A domain-specific Large Language Model (LLM) fine-tuning project using **ROS2 documentation** as the source of technical training data.

The project uses **Llama 3.2 1B** and **LoRA (Low-Rank Adaptation)** to adapt the language model toward ROS2-related technical knowledge.

## Project Overview

The goal of this project is to explore how a general-purpose LLM can be adapted to a specific technical domain using ROS2 documentation.

The model fine-tuning workflow was developed and executed using **Google Colab**.

### Main Technologies

* Llama 3.2
* LoRA (Low-Rank Adaptation)
* PEFT
* ROS2 documentation
* Python
* Google Colab
* GPU-based model training

## Project Pipeline

```text
ROS2 Documentation
        │
        ▼
Data Preparation
        │
        ▼
Training Dataset
        │
        ▼
Llama 3.2
        │
        ▼
LoRA Fine-Tuning
        │
        ▼
Fine-Tuned Model / LoRA Adapter
        │
        ▼
ROS2-Related Inference
```

## Objective

The main objective is to investigate domain adaptation of an LLM for ROS2-related technical knowledge.

Instead of training a language model from scratch, the project uses an existing Llama 3.2 model and applies parameter-efficient fine-tuning with LoRA.

## Why LoRA?

LoRA (Low-Rank Adaptation) is a parameter-efficient fine-tuning technique that allows a model to be adapted without updating all of its original parameters.

This approach is useful for experimenting with LLM fine-tuning in resource-constrained environments such as Google Colab.

## Training Data

The project uses **ROS2 technical documentation** as the source of domain-specific knowledge.

The documentation is processed and prepared for use in the LLM fine-tuning workflow.



## Training Environment

The fine-tuning workflow was implemented in:

**Google Colab**

The notebook contains the training workflow and model configuration used for the experiment.

## Model

**Base model:** Llama 3.2

**Fine-tuning method:** LoRA

**Domain:** ROS2 / Robotics

## What This Project Demonstrates

* Working with a pretrained LLM
* Preparing domain-specific training data
* Applying parameter-efficient fine-tuning
* Using LoRA for LLM adaptation
* Fine-tuning an LLM in a GPU-based Google Colab environment
* Applying LLM technology to the ROS2 and robotics domain



## Future Improvements

Possible extensions of this project include:

* Improving the ROS2 training dataset
* Adding more ROS2 documentation and examples
* Evaluating the fine-tuned model against the base model
* Testing ROS2-specific question answering
* Comparing different LoRA configurations
* Integrating the fine-tuned model into a ROS2-based robotics application

## Disclaimer

This project is an experimental implementation for learning and research into domain-specific LLM fine-tuning. Model performance should be evaluated using a dedicated ROS2 question-answering benchmark before making claims about accuracy or reliability.


## Features

- Base model: [`meta-llama/Llama-3.2-1B`](https://huggingface.co/meta-llama/Llama-3.2-1B)
- Parameter-efficient fine-tuning with **LoRA**
- Training powered by **TRL SFTTrainer**
- Custom ROS 2 / Nav2 instruction dataset
- Before / after generation examples included

---

## Requirements

- Python 3.10+
- CUDA GPU (recommended)
- Hugging Face account with access to Llama 3.2 models

Install dependencies:

```bash
pip install -U transformers peft trl datasets accelerate bitsandbytes
pip install -U fsspec huggingface_hub pyarrow
```

> If you encounter a `torchao` version conflict, run:
> ```bash
> pip uninstall -y torchao
> ```

---

## Dataset

Training data: `ros2_llama3_sft_large.jsonl`  
Validation data: `ros2_llama3_sft_large_val.jsonl`

Expected format (JSONL):

```json
{
  "messages": [
    {"role": "system", "content": "..."},
    {"role": "user", "content": "instruction"},
    {"role": "assistant", "content": "expected answer"}
  ],
  "category": "nav2",
  "text": "formatted training text"
}
```

The training script keeps only the `"text"` column.
## Known Limitations & Tips

- Only `q_proj` and `v_proj` are targeted — consider adding `k_proj`, `o_proj`, `gate_proj`, `up_proj`, `down_proj` for better results.
- Training runs for 100 epoch — increase if the dataset is large or the task is complex.
- Always keep your Hugging Face token private (use environment variables or `huggingface-cli login`).
- Save the tokenizer together with the adapter for easier deployment.
