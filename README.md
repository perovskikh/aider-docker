# Launch Aider in Docker

Vibe coding with [Aider](https://github.com/Aider-AI/aider) and local [Ollama](https://github.com/ollama/ollama) models.

### Launch Ollama

CPU
```bash
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

Nvidia
```bash
docker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

AMD
```bash
docker run -d --device /dev/kfd --device /dev/dri -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama:rocm
```

Load model
```bash
docker exec -it ollama ollama pull qwen2.5-coder:32b-instruct-q4_K_M
```

### Launch Aider

```bash
git clone https://github.com/HardAndHeavy/aider-docker
cd aider-docker
make gen # Press enter to set the default values
make run
```
