# Serve Open Source AI Models
## What is Open Source AI Models ?
- Open Source AI Models are machine learning frameworks and models that are freely available to the public, allowing anyone to use, study, modify, and distribute them.
    - Use cases include:
    > Computer Vision, Text Generation, Image Generation, Speech Recognition, Translation etc
    - Example of Popular Open Source models:
    > BERT, LLaMA, T5, Stable Diffusion

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



