---
title: IOUnits
sidebar_position: 7
---

IOUnits are designed to interact with external resources or tools. This can include a variety of tasks, such as opening and reading files, making network requests (like querying Google), or executing database operations with SQL. In essence, IOUnits function as the primary interface between the chain and the external environment, facilitating the flow of data in and out of the system.

Let's see an example of an IOUnit. In this example, we'll create a unit that loads a text file from the local file system and returns its contents as a string.

```python
from commandchain.units import Unit
from langchain.document_loaders import TextLoader

def loadtext(inputs, success, failure):
    loader = TextLoader(inputs['path'])
    try:
        success(loader.load())
    except Exception as e:
        failure(e)

unit = Unit(action: loadtext)
unit.fire({'path': './index.md'})
```

In this example, we first import the TextLoader class from the langchain.document_loaders module. This class is responsible for loading text files from the local file system. Next, we define a function named loadtext that takes in three parameters: inputs, success, and failure. 

The inputs parameter is a dictionary of inputs that are passed to the unit. The success parameter is a callback function that is called when the unit successfully completes its task. The failure parameter is a callback function that is called when the unit fails to complete its task.

:::info
**CommandChain** extensively utilizes [LangChain][langchain]to facilitate interaction with external resources or tools.

See also:
- [LangChain - Data Connection](https://langchain-langchain.vercel.app/docs/modules/data_connection/)
- [LangChain - Memory](https://langchain-langchain.vercel.app/docs/modules/memory/)
:::