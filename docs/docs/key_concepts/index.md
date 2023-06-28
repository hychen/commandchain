---
title: Key Concepts
sidebar_position: 3
---
import DocCardList from '@theme/DocCardList';

In this section, we'll cover the key concepts of the CommandChain framework. We'll start with a high-level overview of the framework, then dive into the details of each concept.

## High-level overview

```diagg
+----------------------------+
|          Service           |
+----------------------------+
|           Chain            | 
+--------------+-------------+
|  IOUnit      |   LLMUnit   |
+--------------+-------------+
| Native I/O   |   LLM I/O   |
+--------------+-------------+
```

This diagram presents a simplified, high-level overview of the **CommandChain** framework:

- **Service**: This represents the endpoint or interaction point where users or other systems interface with the CommandChain. It could be an HTTP service, a GraphQL service, or a process initiated by a command-line tool.
- **Chain**: The Service triggers a Chain, which is a series of coordinated tasks involving IOUnits and LLMUnits. The Chain outlines the logic and order of tasks to be accomplished.
- **Unit**: 
  - IO Units interact with external resources or tools (Native I/O), such as opening a file or querying a database. 
  - LLMUnits interface with language learning models (LLM Models) to tap into their advanced capabilities.

## Dive into the details

Let's break down this more complex example, to help understand how we use CommandChain to accomplish our task.

```python
# Import necessary modules
from langchain.llms import OpenAPI
from commandchain.units import IOUnit, LLMUnit
from commandchain.chains import Chain
from commandchain.io import HTTPRequest
```

These lines import the necessary libraries. OpenAPI is used to interact with OpenAI's language model, IOUnit and LLMUnit are the building blocks of our chains, Chain is used to build the workflow, and HTTPRequest is a helper function for making HTTP requests.

```python
# Instantiate the OpenAI language model
llm = OpenAPI(openai_api_key="...", temperature=0.9)
```
This line initializes the OpenAI's language model with your OpenAI API key and temperature for the model's randomness.

```python
# Define the source unit which fetches weather data
source = IOUnit(action=HTTPRequest('GET', 'http://api.weatherapi.com/v1/current.json', params={'key': '...', 'q': 'New York'}))
```

Here we create the source IOUnit, which fetches weather data. It does so by making a GET request to the specified URL, and passing the parameters, including your WeatherAPI key and the query location.

```python
# Define the worker unit that uses LLM to interpret the weather data and generate a friendly message
worker = LLMUnit(llm=llm, prompt=lambda data: f"Translate the weather data '{data}' into a friendly message...")
```

The worker LLMUnit interacts with the language model. The prompt is dynamically generated based on the weather data fetched by the source unit.

```python
# Define the destination unit that prints the friendly weather message to console
dest = IOUnit(action=lambda data: print(data))
```

The dest IOUnit prints the data it receives to the console.

```python
# Create a Chain instance and connect the units
chain = Chain()
chain.connect(source, 'success', worker, 'in')
chain.connect(worker, 'success', dest, 'in')
```

We create an instance of Chain and connect the units. The source unit's success output is connected to the worker unit's input, and the worker unit's success output is connected to the dest unit's input.

```python
# Serve the chain on a specified port
chain.serve(port=3000)
```

Finally, we use the serve method to start the service on port 3000.

Each unit performs its task asynchronously and passes the output to the next unit. If any unit fails, the chain stops and returns the error. This example demonstrates a complex yet powerful way to organize and manage tasks using CommandChain.

## See Also

<DocCardList />
