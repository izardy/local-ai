# Serving Open Source AI Models

## HuggingFace to Local Deployment
- This repository documents three common approaches to deploy and serve HuggingFace open-source AI models locally.

## System Requirements
- The deployment capability depends on your hardware specifications:

    - **Hardware Requirements:**
        - CPU: Multi-core processor
        - RAM: Minimum 8GB (16GB+ recommended)
        - GPU: NVIDIA GPU with CUDA support (optional but recommended)
        - Storage: Sufficient free space for model weights

    **Note:** Model deployment capabilities are directly correlated with your hardware specifications. Systems with higher-end components (powerful CPUs, more RAM, and dedicated GPUs) can handle larger language models with higher parameter counts more efficiently.

    For example:
    - Entry-level systems: Suitable for smaller models (1-3B parameters)
    - Mid-range systems: Can handle medium-sized models (3-7B parameters)
    - High-end systems: Capable of running larger models (7B+ parameters)


## What is Open Source AI Models ?
- Open Source AI Models are machine learning frameworks and models that are freely available to the public, allowing anyone to use, study, modify, and distribute them.
    - Use cases include:
        - Computer Vision, Text Generation, Image Generation, Speech Recognition, Translation etc
    - Example of Popular Open Source models:
        - BERT, LLaMA, T5, Stable Diffusion

## Common Platform to Serve AI Models in Local Machines
- Few popular platforms for serving AI models locally.
    - Ollama
        - Supports various models like Llama, Mistral, and Gemma
        - Easy to use with simple API interface
        - Available for macOS, Linux, and Windows
        - Deployment on finetuned model in gguf format
    - Transformers
        - Support for model loading and inference
        - Cross framework compatibility (Pytorch, Tensorflow)
        - Capability to finetuning
        - Basic usage example
        ```
        from transformers import pipeline

        # Load a pre-trained model for text generation
        generator = pipeline('text-generation', model='gpt2')

        # Generate text
        result = generator("The quick brown fox", max_length=50)

        ```
        - Model version control example
        ```
        from transformers import AutoModel, AutoTokenizer

        # Load model and tokenizer
        tokenizer = AutoTokenizer.from_pretrained("bert-base-uncased")
        model = AutoModel.from_pretrained("bert-base-uncased")

        # Save locally
        model.save_pretrained("./my_saved_model")
        tokenizer.save_pretrained("./my_saved_model")

        ```
        - Memory optimastion example
        ```
        # Load in 8-bit precision for memory efficiency
        from transformers import AutoModelForCausalLM
        model = AutoModelForCausalLM.from_pretrained("gpt2", load_in_8bit=True)

        ```
    - VLLM
        - PagedAttention technology for optimized memory usage
        - OpenAI-compatible API server
        - Support for multiple model architectures
        - Basic usage example
        ```
        from vllm import LLM

        llm = LLM(model="facebook/opt-125m")
        outputs = llm.generate("Tell me a story", max_tokens=100)

        ```

## Why Use AI in Local Machine ?
- Development and Debugging Benefits:
    - No dependency on internet connectivity
    - Immediate response times for testing
    - Better control over the development environment

- Data Privacy and Security :
    - Sensitive data remains on your local machine
    - No need to transmit confidential information to external servers
    - Compliance with data protection regulations
    - Full control over data handling

- Cost Efficiency :
    - No ongoing cloud computing costs
    - No API usage fees

- Customization and Control:
    - Full control over model parameters
    - Ability to modify and fine-tune models
    - Freedom to experiment with different model architectures

