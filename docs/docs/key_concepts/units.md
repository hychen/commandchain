---
title: Units
sidebar_position: 3
---

[Unit][unit] form the fundamental building blocks of the CommandChain framework, and can be categorized into two types: LLMUnits and IOUnits.

### LLMUnits

LLMUnits, on the other hand, work with language learning models by providing prompts to these models. The purpose of these units is to tap into the advanced capabilities of language models, enabling their integration into the chain's tasks and operations.

Both types of units can operate in different modes - they can be interactive, execute immediately, or function autonomously as agents based on the needs of the chain.

For instance, an LLMUnit named SummaryLLMUnit could interact with a language model to generate a summary of a given text. It would take a piece of text as input, generate a prompt for the language model that asks it to summarize the text, and then provide the language model's response as output. and another LLMUnit, TranslationLLMUnit, could be used to translate a piece of text from one language to another. It would take a piece of text and the target language as input, generate a prompt asking the language model to perform the translation, and then output the translated text.

### IOUnits

IOUnits are designed to interact with external resources or tools. This can include a variety of tasks, such as opening and reading files, making network requests (like querying Google), or executing database operations with SQL. In essence, IOUnits function as the primary interface between the chain and the external environment, facilitating the flow of data in and out of the system.

For example, imagine an IOUnit named GoogleSearchIOUnit. This unit takes in a search query as input and sends a request to Google's search API. The search results obtained from Google are then provided as output to be used by the next unit in the chain. Similarly, a FileReadIOUnit could open a specific file and read its contents. The file contents would then become the output of this unit.

These are just two examples of IOUnits, but they can be designed to interact with any external resource or tool depending on the needs of the application.

:::info
**CommandChain** extensively utilizes [LangChain][langchain]to facilitate interaction with external resources or tools.

See also:
- [LangChain - Data Connection](https://langchain-langchain.vercel.app/docs/modules/data_connection/)
- [LangChain - Memory](https://langchain-langchain.vercel.app/docs/modules/memory/)
:::
