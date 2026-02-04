# Fine-tuning Llama 3.2 with Unsloth

This project demonstrates fine-tuning the Llama 3.2 3B Instruct model using the Unsloth library for efficient training with LoRA (Low-Rank Adaptation).

## Overview

The notebook fine-tunes a language model to perform reflective, iterative reasoning similar to human stream-of-consciousness thinking. The model is trained on the ServiceNow R1-Distill-SFT dataset to enhance its problem-solving capabilities.

## Features

- **Efficient Training**: Uses Unsloth for optimized model training
- **4-bit Quantization**: Reduces memory footprint with 4-bit model loading
- **LoRA Fine-tuning**: Parameter-efficient fine-tuning using LoRA
- **Reasoning Enhancement**: Trains model for thorough, iterative problem-solving

## Requirements

```bash
pip install unsloth
pip install datasets transformers trl
```

## Model Details

- **Base Model**: `unsloth/Llama-3.2-3B-Instruct`
- **Training Method**: Supervised Fine-Tuning (SFT) with LoRA
- **Dataset**: ServiceNow-AI/R1-Distill-SFT (v0)
- **Max Sequence Length**: 2048 tokens

## LoRA Configuration

```python
r = 16
lora_alpha = 16
target_modules = ["q_proj", "k_proj", "v_proj", "o_proj",
                  "gate_proj", "up_proj", "down_proj"]
```

## Training Parameters

- **Batch Size**: 2 per device
- **Gradient Accumulation**: 4 steps
- **Learning Rate**: 2e-4
- **Max Steps**: 60
- **Optimizer**: AdamW 8-bit
- **Scheduler**: Linear

## Usage

1. **Install Dependencies**

   ```bash
   pip install -q unsloth
   ```

2. **Run the Notebook**

   - Execute cells sequentially in `Finetune_in_unsloth.ipynb`
   - The notebook will download the model, load the dataset, and train

3. **Inference**
   - The final cells demonstrate how to use the fine-tuned model
   - Uses Llama 3.1 chat template for inference
   - Configured with temperature=1.5 and min_p=0.1 for generation

## Example Output

The model is tested with the question: "How many 'r's are present in 'strawberry'?" demonstrating its reasoning capabilities.

## Project Structure

```
.
├── Finetune_in_unsloth.ipynb  # Main training notebook
├── outputs/                    # Training outputs (checkpoints, logs)
└── README.md                   # This file
```

## Training Process

1. Load pre-trained Llama 3.2 3B model with 4-bit quantization
2. Apply LoRA adapters to specific transformer layers
3. Load and format the R1-Distill-SFT dataset
4. Train using SFTTrainer from TRL library
5. Convert to inference mode and test

## Prompt Template

The model uses a specialized prompt template that emphasizes:

- Reflective reasoning
- Iterative thinking
- Self-doubt and exploration
- Continuous refinement

## Hardware Requirements

- CUDA-capable GPU recommended
- Approximately 8-12GB VRAM (with 4-bit quantization)
- Training time: ~30-60 minutes depending on hardware

## References

- [Unsloth](https://github.com/unslothai/unsloth) - Fast language model training
- [ServiceNow R1-Distill-SFT Dataset](https://huggingface.co/datasets/ServiceNow-AI/R1-Distill-SFT)
- [Llama 3.2 Model](https://huggingface.co/meta-llama/Llama-3.2-3B-Instruct)

## License

Please refer to the original model and dataset licenses:

- Llama 3.2: Meta's Llama license
- R1-Distill-SFT: Check dataset repository for terms

## Acknowledgments

- Meta for the Llama 3.2 model
- ServiceNow AI Research for the training dataset
- Unsloth team for the efficient training library
