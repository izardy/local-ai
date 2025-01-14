# Local AI via Ollama

## Ollama Installation
- xxxx

## Ollama Configuration

### Show Modelfile
- A Modelfile is a configuration file used in Ollama that serves as a blueprint for customizing and defining how a language model should behave. It contains several key components and instructions that control various aspects of the model's operation.
    - Check existing Modelfile for specific LLM
        - Check install model in Ollama
    
        ```
        ollama ls
        ```
        

        - Check Modelfile
    
        ```
        ollama show --modelfile modelname
        ```

### Modelfile Parameters Configuration
- Modelfile parameters are settings that control how the language model generates and processes responses.  
    - Example of Ollama Modelfile structure

        - Specify the base model
    
        ```
        FROM llama2
        ```
        
        
        - Configure model parameters
    
        ```
        PARAMETER temperature 0.7
        PARAMETER top_k 40
        PARAMETER top_p 0.9
        ```
        
        
        - Define the template for input prompts
    
        ```
        TEMPLATE """
        USER: {{.Prompt}}
        ASSISTANT: Let me help you with that.
        """
        ```
        
        
        - Set the system message that defines the AI's behavior
    
        ```
        SYSTEM """
        You are a helpful and knowledgeable assistant who specializes in explaining technical concepts clearly and concisely. Please provide accurate and practical information while maintaining a professional tone.
        """
        ```
    
- Example of Modelfile (paste the following code in a non extension file name Modelfile)
    - Llama-3.2
 
    ```
    # Modelfile
    FROM "Llama-3.2-11B-Vision-Instruct.Q4_K_M.gguf" # This specifies that the model is based on Meta's LLaMA 3 70B model (quantized version)
    TEMPLATE """<|start_header_id|>system<|end_header_id|>

    Cutting Knowledge Date: December 2023

    {{ if .System }}{{ .System }}
    {{- end }}
    {{- if .Tools }}When you receive a tool call response, use the output to format an answer to the orginal user question.

    You are a helpful assistant with tool calling capabilities.
    {{- end }}<|eot_id|>
    {{- range $i, $_ := .Messages }}
    {{- $last := eq (len (slice $.Messages $i)) 1 }}
    {{- if eq .Role "user" }}<|start_header_id|>user<|end_header_id|>
    {{- if and $.Tools $last }}

    Given the following functions, please respond with a JSON for a function call with its proper arguments that best answers the given prompt.

    Respond in the format {"name": function name, "parameters": dictionary of argument name and its value}. Do not use variables.

    {{ range $.Tools }}
    {{- . }}
    {{ end }}
    {{ .Content }}<|eot_id|>
    {{- else }}

    {{ .Content }}<|eot_id|>
    {{- end }}{{ if $last }}<|start_header_id|>assistant<|end_header_id|>

    {{ end }}
    {{- else if eq .Role "assistant" }}<|start_header_id|>assistant<|end_header_id|>
    {{- if .ToolCalls }}
    {{ range .ToolCalls }}
    {"name": "{{ .Function.Name }}", "parameters": {{ .Function.Arguments }}}{{ end }}
    {{- else }}

    {{ .Content }}
    {{- end }}{{ if not $last }}<|eot_id|>{{ end }}
    {{- else if eq .Role "tool" }}<|start_header_id|>ipython<|end_header_id|>

    {{ .Content }}<|eot_id|>{{ if $last }}<|start_header_id|>assistant<|end_header_id|>

    {{ end }}
    {{- end }}
    {{- end }}"""
    PARAMETER stop <|start_header_id|>
    PARAMETER stop <|end_header_id|>
    PARAMETER stop <|eot_id|>
    ```
    