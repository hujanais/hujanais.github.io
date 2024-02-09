[Home](https://hujanais.github.io/edge-llm/)
# Part 2.  Running a local LLM

## Overview
The next order of business is to get an LLM to run locally without the reliance on any hosted solution like ChatGPT.

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
Work with ollama with command-line inside the docker container
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
The Phi2(2.7B) didn't exhibit the robustness I was hoping for, and I found it challenging to work with at this learning stage. Consequently, I opted for a more substantial model, namely LLama2(13B). Unfortunately, Pi encountered difficulties loading the LLama2 model. Instead, I ran the Docker container on my 2018 MacBook Pro, equipped with a 2.7GHz Quad-Core processor and 16GB of RAM. The LLama2 ran well enough on my laptop, providing a satisfactory experience to proceed.

This is from the Ollama model info page
> Note: You should have at least 8 GB of RAM available to run the 7B models, 16 GB to run the 13B models, and 32 GB to run the 33B models.

Suddenly I started day dreaming for a GPU rig but I digress.... moving along...  

> Docker Tip: If you are new on using Docker on your Windows/Linux/Mac computer, you can download Docker Desktop which gives you a nice GUI based dashboard to manage your containers.  You can still use command line with it.  DockerHub contains the repository all public and private Docker containers for you to pull.  For example, you can find ollama/ollama there and with all the instructions to pull and run the container.

> Written with [StackEdit](https://stackedit.io/).
