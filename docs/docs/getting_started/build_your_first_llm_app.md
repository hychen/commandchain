---
title: Build Your First LLM App 
sidebar_position: 3
---

:::caution

This tutorial is currently under development and not working yet. Please check back later. 

:::

Welcome to this step-by-step guide on how to build your first Language Learning Model (LLM) app using CommandChain and Flutter. In this tutorial, we will create a simple chat-to-article app where users input chat messages, and the app outputs a well-formatted article.

## Prerequisites

Before we begin, make sure you have the following:

1. Basic knowledge of Python (for setting up the backend using CommandChain)
2. Understanding of Flutter (for setting up the frontend)
3. An API key from OpenAI (you can get one by signing up on their website)

## Step 1: Setting Up the Backend

Let's start by setting up our backend using CommandChain.

First, install CommandChain:

```bash
pip install commandchain
```

Now, we'll create a CommandChain that interacts with OpenAI's GPT-4. This chain will take the user's input, pass it to the model, and return the model's output. 

let's write a `main.py` file. 

Copy and paste the following code into the file:

```python
from commandchain import Chain, LLMUnit
from commandchain.llms import OpenAi

# Instantiate the OpenAI language model
llm = OpenAi(openai_api_key="your_key_here", temperature=0.9)

# Define the units
input_unit = LLMUnit(llm=llm, prompt='Act as a good writer article about the following idea:')
output_unit = LLMUnit(llm=llm, prompt='Write three versions of the outline of an article and evaulate them, return the best one to me.')

# Create a Chain instance and connect the units
chain = Chain()
chain.connect(input_unit, 'success', output_unit, 'in')

# Serve the chain as a RESTful service
chain.serve(port=3000)
```

With this, our backend is ready! It's listening on port 3000 and can be interacted with through HTTP.

```sh
curl localhost:3000 --predict "an article about the importance of education"
```

## Step 3: Setting Up the Frontend

Next, we'll set up our frontend using Flutter.

Install Flutter if you haven't already, and create a new Flutter project:

```shell
flutter create chat_to_article_app
cd chat_to_article_app
```

Now, we'll create a simple UI with a text input field for the user to enter their chat message, and a button to send the message to our backend.

```dart
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

void main() => runApp(ChatToArticleApp());

class ChatToArticleApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Chat to Article'),
        ),
        body: Center(
          child: Padding(
            padding: EdgeInsets.all(8.0),
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                TextField(
                  decoration: InputDecoration(
                    border: OutlineInputBorder(),
                    labelText: 'Enter your chat message',
                  ),
                  onSubmitted: (String message) async {
                    var response = await http.post(
                      Uri.parse('http://localhost:3000'),
                      body: {'predicate': message},
                    );
                    print('Response from backend: ${response.body}');
                  },
                ),
                RaisedButton(
                  onPressed: () {
                    var response = await http.post(
                      Uri.parse('http://localhost:3000'),
                      body: {'predicate': 'write'},
                    );
                  },
                  child: Text('Generate Article'),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

In this code, when the user submits the chat message, the app sends an HTTP POST request to our backend with the message. The backend's response is then printed in the console.

To send the message when the "Generate Article" button is pressed, you'll need to move the HTTP request to the button's onPressed handler.

## Step 3: Run the App

Now that we have our backend and frontend ready, let's build and run the app!

```shell
flutter run -d chrome
```

## Wrapping up

Now you know how to get your own OpenAI API key, set up your coding environment, create your first LLM-powered app with 
CommandChain and Flutter, and run it on your browser.

We hope this tutorial was helpful to kickstart your journey in developing apps using LLMs, CommandChain, and Flutter. Stay tuned for more advanced tutorials. Happy coding!