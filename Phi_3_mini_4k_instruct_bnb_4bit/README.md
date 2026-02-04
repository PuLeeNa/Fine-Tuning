# Phi-3 Mini 4K Instruct (4-bit Quantized)

Fine-tuned Phi-3 Mini model for local deployment with Ollama.

## Running Locally with Ollama

### Prerequisites

- Install [Ollama](https://ollama.ai/)
- Ensure the GGUF model file is present: `phi-3-mini-4k-instruct.Q4_K_M.gguf`

### Create the Model

```bash
ollama create phi3-finetuned -f Modelfile
```

### Run the Model

```bash
ollama run phi3-finetuned
```

### Example Usage

```bash
ollama run phi3-finetuned "Your prompt here"
```

## Files

- `Modelfile` - Ollama configuration for the fine-tuned model
- `Phi_3_mini_4k_instruct_bnb_4bit.ipynb` - Training notebook
- `json_extraction_dataset_500.json` - Training dataset

## Model Details

- **Base Model**: Phi-3 Mini 4K Instruct
- **Quantization**: 4-bit (Q4_K_M)
- **Temperature**: 0.7
- **Top-p**: 0.9
