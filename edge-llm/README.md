Home
# Edge-Micro-LLM

### A study of decentralized and on-prem private LLM for home and businesses

## Overview

In the ever-evolving landscape of technology, private micro LLMs emerges as a pioneering initiative, dedicated to exploring the immense potential of on-device Language Models (LLMs). This cutting-edge project is fueled by the ambition to harness the capabilities of LLMs within the confines of edge devices, including Single Board Computers (SBCs) and laptops.

### Why micro LLMs on edge devices?

There are several major considerations of using LLMs.

 1. Privacy
 2. Computing power / Cost
 3. Environmental Impact

Massive LLMs like ChatGPT and Claude.ai are massive models that are run on very expensive hardware mostly reserved to the hyperscalers.  There is a huge benefit to decentralize the LLMs to run on a local environment or device to have complete privacy.  Furthermore, for specific business use-case, it is sometimes unneccessary to run massive foundation models which is very costly and has a huge environmental impact.  Instead, there is a lot of interest and benefit to use micro LLMs that are trained with private data that will be able to run on low powered hardware like CPUs instead of GPUs and even on SBCs like the Raspberry Pi.  The lowered cost and simplicity of deployment will also drive massive adoption in various use cases.

## Goal
Our goal is two fold.  
1. The first goal is to conduct research and to develop a proof of concept that demonstrates the chain of taking a user input to executing a physical action.  For example, we would like to demonstrate taking a verbal command from a user like "Please let me know which motor has been running hot in the past 24 hours?".  

Voice command -> Transcribed to text -> Read by LLM -> Execute an endpoint call -> return data	from a database

2. The stretch goal is to build framework for teams to build their own connectivity solution.

## Let's get started
The following sections provide a chronological breakdown of the steps taken during the journey of building a Proof of Concept (POC). It is important to acknowledge the wealth of knowledge contributed by the open-source community, as much of what has been accomplished in this endeavor draws inspiration from the remarkable work of others. Numerous outstanding open-source projects have paved the way, serving as invaluable sources of learning.

While I endeavor to share links to major projects that have significantly influenced this POC, it is impractical to reference every individual article or random YouTube video that has contributed to my learning. The vast array of resources utilized for learning may not all be explicitly mentioned, but the collective knowledge gleaned from the open-source community has played a pivotal role in shaping and informing each step of this journey.

1.	[Speech-to-Text on Raspberry Pi](https://hujanais.github.io/edge-llm/part-1)
2.	[Local LLM on laptop and/or Raspberry Pi](https://hujanais.github.io/edge-llm/part-2)


## Closing
Join us on this exciting journey as we push the boundaries of on-device language models, unlocking a new era of possibilities in edge computing. Together, let's shape the future of efficient, intelligent, and privacy-centric edge solutions with Edge-Micro-LLM.

> Written with [StackEdit](https://stackedit.io/).
