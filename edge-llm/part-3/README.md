[Home](https://hujanais.github.io/edge-llm/)
# Part 3.  Using private data with Langchain
## Overview
One of the most valuable applications of Large Language Models (LLMs) lies in their ability to retrieve and analyze private data. For instance, imagine our team possessing a collection of Wiki pages dedicated to our product. To enhance information retrieval for team members, we can implement a natural language search feature, surpassing basic text search capabilities.  The primary challenge in this scenario is integrating new contextual information into an existing foundational model.

## Introducing RAG and Langchain
According to the Langchain website, 
> Many LLM applications require user-specific data that is not part of the model's training set. The primary way of accomplishing this is through Retrieval Augmented Generation (RAG). In this process, external data is _retrieved_ and then passed to the LLM when doing the _generation_ step.

> **LangChain**  is a framework for developing applications powered by language models. It enables applications that:
> -   **Are context-aware**: connect a language model to sources of context (prompt instructions, few shot examples, content to ground its response in, etc.)
> -   **Reason**: rely on a language model to reason (about how to answer based on provided context, what actions to take, etc.)

Langchain is a framework that provides all the neccessary steps for integrating RAQ into the LLM.  Langchain is by no means the only RAG framework.  But somehow this name stuck in my mind from the early technical bulletins from OpenAI and I just narrowed in on this stack and it is a very popular choice.  

Langchain is extremely powerful and will be the central technology that we will leverage during our adventure.  It has a lot of features but my initial baby step is to enable some kind of natural langugage search on my private github page.

## My first attempt at using RAQ on my personal data
For this part of my studies, I just went ChatGPT for the performance and having 1 less item to worry about but I have also tested the code with Ollama(running Llama2 on my laptop) and it worked just as well but very slowly.  It takes my local LLM more than 2.5 minutes to generate a response.

Without further ado, here is the working code using ChatGPT but in the code, I have also left in comments where you can switch between different LLMs like ChatGPT or Ollama.

After a few code iterations, I decided to just put the application in a Flask server so I can easily query without re-loading the documents and to also prepare a server that I can leverage a UI for the future if I so choose.

Here is a high level steps on what needs to happen.
 1. Load new documents
 2. Documents are too large and are chunked down to sub-documents
 3. The sub-documents are then hashed using Embeddings (there are many options)
 4. Save the vectorized embeddings into some kind of vector database
 5. Build a meaningful prompt to prime up the LLM.
 6. Read back the embeddings and inject into the LLM.
 7. Ask questions to the LLM and get responses based on the private documents.

To view full working code, please visit [rag-llm project](https://github.com/hujanais/rag-llm)

## Conclusion
I am super excited to finally get RAG to work with an LLM.  It really helped to get a working solution that is a bit more than the basic examples on the internet to understand more of the nuances required to take one step closer to production.  Lots more to come.
> Written with [StackEdit](https://stackedit.io/).