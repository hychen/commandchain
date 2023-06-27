---
sidebar_position: 1
title: Introduction
---

:::caution

Please note that this project is currently undergoing development, and as a result, the provided documentation might not reflect the most recent changes.

:::

**CommandChain** is an framework for building applications using Language Learning Models (LLM). It revolutionizes application development by using an approach akin to assembling electronic circuits: processes are created as “black boxes” that exchange data via predefined connections, much like integrated circuits wired together.

## Fast Track

Understand CommandChain in **5 minutes** by playing this simple translation app!

To install CommandChain run:

```shell
pip install commandchain
```

To start, generate a new file named `main.py` and input the code provided below. Please note, you'll need your OpenAI API key for this process. If you don't already have one, you can acquire it by registering an account [here](https://platform.openai.com/account/api-keys):

```python
# Import necessary modules
from langchain.llms import OpenAPI
from commandchain.units import LLMUnit
from commandchain.chains import Chain

# Instantiate the OpenAI language model
llm = OpenAi(openai_api_key="...", temperature=0.9)

# Define the source, worker, and destination units
source = LLMUnit(llm=llm, prompt='Enter your prompt in English...')
worker = LLMUnit(llm=llm, prompt='Translating to Spanish...')
dest = LLMUnit(llm=llm, prompt='Generating a completion in Spanish...')

# Create a Chain instance and connects the units
chain = Chain()
chain.connect(source, 'success', worker, 'in')
chain.connect(worker, 'success', dest, 'in')

# Serve the chain on a specified port
chain.serve(port=3000)
```

To initiate the server, run:

```shell
python main.py
```

Now, your can interact with [http://localhost:3000](http://localhost:3000), run:

```sh
curl localhost:3000 --predict "How are you?"
```

and your should get the the string translated in Spanish.

```json
{
    "response": "¿Cómo estás? Estoy bien, gracias. ¿Y tú?"
}
```

## Features

**CommandChain** is designed to enhance the developer's experience, simplifying the process of constructing semi-autonomous applications for tackling intricate tasks.

- **Flow-Based Programming**: 
  - Mirrors electronic circuit construction, where data is exchanged via predefined connections. It fosters modularity and simplifies complex tasks into manageable operations, enhancing control and code reusability.
- **Async By Default**:
  - Asynchrony is a foundational principle. This means that tasks within the chain are not necessarily performed in a strictly sequential order. 

## Comparison with other tools

We have also conducted in-depth analyses of other principal LLM chain frameworks. Our intention is to share our comparative insights, with the hope of aiding you in navigating the kaleidoscope of options available in this field.

### LangChain

[LangChain][1] is essentially a framework for building applications with language models. It's perfect for creating dialogue apps and managing multiple models effectively.

In contrast, CommandChain is like a box of Lego for apps. You can connect different 'black box' processes, much like creating a circuit with Lego blocks. This design makes it super flexible and adaptable. What's more, it uses Guidance language, which offers a more effective way to control language models. Also, CommandChain is designed to run smoothly as microservices, be it on the cloud, your local machine, or even on devices.

In essence, while both LangChain and CommandChain use language models for creating apps, CommandChain offers more flexibility and adaptability, which could make your development tasks a bit easier.

[1]: https://langchain-langchain.vercel.app/docs/get_started/introduction.html