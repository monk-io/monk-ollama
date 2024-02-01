# Ollama & Monk

This repository contains Monk.io template to deploy Ollama platform.

## Prerequisites

- Install Monk
- Register and Login Monk
- Add Cloud Provider
- Add Instance with GPU

## Clone Repository

```bash
git clone https://github.com/monk-io/monk-ollama
```

## Load Template

```bash
cd monk-ollama
monk load MANIFEST
```

## Deploy

```bash
$ monk run ollama/ollama

✔ Starting the run job: local/ollama/ollama... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% ollama/ollama:latest test-gpu-i
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ Runnable templates/local/ollama/ollama connections graph updating DONE
✔ Runnable templates/local/ollama/ollama connections graph has been updated DONE
✔ Runnable templates/local/ollama/ollama services initialization DONE
✔ Runnable templates/local/ollama/ollama services have been initialized DONE
✔ Host ports have been added to container 1e9b0d676592d49173a20df40116b037-al-ollama-ollama-ollama DONE
✔ New container 1e9b0d676592d49173a20df40116b037-al-ollama-ollama-ollama created DONE
✔ Container 1e9b0d676592d49173a20df40116b037-al-ollama-ollama-ollama network has been configured DONE
✔ Container 1e9b0d676592d49173a20df40116b037-al-ollama-ollama-ollama has been started DONE
✔ Started local/ollama/ollama
🔩 templates/local/ollama/ollama
 └─🧊 Peer test-gpu-i
    └─🔩 templates/local/ollama/ollama 
       └─📦 1e9b0d676592d49173a20df40116b037-al-ollama-ollama-ollama running
          ├─🧩 ollama/ollama:latest                  
          └─🔌 open (public) TCP 34.147.91.213:11434 -> 11434

💡 You can inspect and manage your above stack with these commands:
	monk logs (-f) local/ollama/ollama - Inspect logs
	monk shell     local/ollama/ollama - Connect to the container's shell
	monk do        local/ollama/ollama/action_name - Run defined action (if exists)
💡 Check monk help for more!


```

## Pull required model
[List of supported models](https://github.com/ollama/ollama?tab=readme-ov-file#model-library)

```bash
$ monk exec ollama/ollama ollama pull llama2
```

Or using REST API

```bash
$ curl -X POST http://34.147.91.213:11434/api/pull -d '{"model": "llama2", "name": "llama2"}'
```

## REST API

Ollama has a REST API for running and managing models.

### Generate a response

```bash
curl -X POST http://34.147.91.213:11434/api/generate -d '{
  "model": "llama2",
  "prompt":"Why is the sky blue?"
}'
```

### Chat with a model

```bash
curl -X POST http://34.147.91.213:11434/api/chat -d '{
  "model": "mistral",
  "messages": [
    { "role": "user", "content": "why is the sky blue?" }
  ]
}'
```

## Stop, remove and clean up workloads and templates

```bash
monk purge ollama/ollama
```
