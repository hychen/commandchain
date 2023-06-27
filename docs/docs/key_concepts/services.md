---
title: Services
sidebar_position: 1
---

A [Service][service] is the user's primary interface with the system. It can take various forms, such as an HTTP RESTful service, a GraphQL endpoint, or a command-line process, among others. Essentially, a [Service][service] is a perpetually running [Chain][chain], primed to accept user input, carry out actions, and yield responses.

For instance, consider a backend service powered by a language model. This [Service][service] could be exposed as an HTTP RESTful or GraphQL endpoint, waiting for user interactions. Whenever a user sends a request, whether to ask a question or request an operation, the [Service][service] fires up a [Chain][chain]. This [Chain][chain] incorporates [Units][unit] to liaise with the language model, processing the user's query, producing a response through the model, and returning this response to the user via the appropriate endpoint.