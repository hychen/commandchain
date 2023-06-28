---
title: LLMUnits
sidebar_position: 4
---

LLMUnits, on the other hand, work with language learning models by providing prompts to these models. The purpose of these units is to tap into the advanced capabilities of language models, enabling their integration into the chain's tasks and operations.

```python
from commandchain.units import LLMUnit
from langchain.llms import OpenAPI

llm = OpenAi(openai_api_key="...", temperature=0.9)
unit = LLMUnit(llm=llm, prompt='Act as {{user}}, do {{task}}')
unit.fire(
    {"user": "John Doe", "task": "Write a blog post"}
)
```

Both types of units can operate in different modes - they can be interactive, execute immediately, or function autonomously as agents based on the needs of the chain.

More complex instance, an LLMUnit named SummaryLLMUnit could interact with a language model to generate a summary of a given text. It would take a piece of text as input, generate a prompt for the language model that asks it to summarize the text, and then provide the language model's response as output. And another LLMUnit, TranslationLLMUnit, could be used to translate a piece of text from one language to another. It would take a piece of text and the target language as input, generate a prompt asking the language model to perform the translation, and then output the translated text.