---
title: Units
sidebar_position: 3
---
Unit form the fundamental building blocks of the CommandChain framework, and be chained together by a Chain to accomplish a task.It does things according the data it receives from the Chain. It then returns the processed data to the next connected unit in the Chain. 

:::info

See Also
- [LLMUnit](../../llmunits) :: A unit to work with language learning models by providing prompts to these models.
- [IOUnit](../../iounits) :: A unit to interact with external resources or tools.

:::

## Firing

Unit is fired by calling its `fire` method, which takes an optional `inputs` parameter. The `inputs` parameter is a dictionary of key-value pairs that are passed to the unit's action. The unit's action is a function that takes the `inputs` dictionary as its only parameter.

The following code snippet shows how to instantiate a unit and fire it:

```python
from commandchain.units import Unit

unit = Unit(
    action=lambda inputs, success, failure: print(inputs), 
    success=lambda results: print(results), 
    failure=lambda err: print(err))

unit.fire({'foo': 'bar'})
```

It outputs:

```js
{'foo': 'bar'}
```

Consider the output of the unit's action as the `results` of the unit. The `results` are passed to the `success` callback if the unit's action is successful, or to the `failure` callback if the unit's action fails. 

## Append-only messages

The `inputs` and `results` parameters are called `Message`, which is a subclass of `dict`. It provides a few helper methods to make it easier to work with the data between Units and Chains. 