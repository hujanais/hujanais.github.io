[Home](https://hujanais.github.io/edge-llm/)
# Part 2.  Running a local LLM

## Overview
The next order of business is to get an LLM to run locally without reliance on any hosted solution like ChatGPT.

## Introducing Ollama
Ollama is an open source project that implements a common interface to interact with a multitude of open-sourced foundation models.  
You can find the project here.  https://github.com/ollama/ollama

## Trying it on Raspberry Pi-5
Firstly, I was unable to get far on a Pi-4 2GB.  I think it is not worth it especially now that we have the Pi-5.

To get started quickly, it is best to just use Docker.
```
curl -sSL https://get.docker.com | sh
# setup user access so we don't have to use sudo
sudo usermod -aG docker $USER
sudo reboot

docker pull ollama/ollama
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama

# if the docker container has stopped, you can restart it.
docker start container_name

```
## Work with ollama with command-line inside the docker container
```
docker exec -it [containerId] bash # go into the container
# use the Microsoft phi-2 model
ollama run phi
```
### Interact with Ollama web server
Once the Ollama docker container is running, it is also a webserver that you can access from a browser via endpoints.  For example,
```
curl http://your-pi-ip:11434/api/generate -d '{
  "model": "llama2",
  "prompt":"Why is the sky blue?"
}'
```
You can find all the endpoints in the documentation in the Ollama github project page.

### Swapping the Pi with my laptop
The Phi2 model was not as robust as I hoped for and just didn't want to deal with it at this learning stage and would prefer to use something bigger like Llama2.  For this, the Pi was unable to load the model and I instead just ran the docker container on my 2018 Macbook Pro 2.7Ghz Quad Core with 16GB of RAM.  LLama2 ran on my laptop amazingly smoothly.  Good enough to proceed at least.

Suddenly I started day dreaming for a GPU rig but I digress.  

> Written with [StackEdit](https://stackedit.io/).