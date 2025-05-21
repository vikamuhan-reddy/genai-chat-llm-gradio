## Development and Deployment of a 'Chat with LLM' Application Using the Gradio Blocks Framework

### AIM:
To design and deploy a "Chat with LLM" application by leveraging the Gradio Blocks UI framework to create an interactive interface for seamless user interaction with a large language model.

### PROBLEM STATEMENT:
To design and deploy a "Chat with LLM" application by leveraging the Gradio Blocks UI framework to create an interactive interface for seamless user interaction with a large language model.

### DESIGN STEPS:
#### STEP 1:
Set up the development environment by installing all necessary tools and libraries, then integrate the large language model to process user inputs efficiently. Ensure the model is optimized for fast and accurate responses to support smooth interactions. This foundation is crucial for building a responsive chat application.

#### STEP 2:
Design and implement an interactive chat interface using the Gradio Blocks framework. The interface should allow users to easily enter text and view real-time responses from the model, focusing on usability and a clean layout. Prioritize a seamless experience to encourage natural conversation flow.

#### STEP 3:
Thoroughly test the application to ensure reliability, responsiveness, and a positive user experience. Gather feedback to identify potential improvements and address any issues. Finally, deploy the prototype on a suitable platform to make it accessible for users and further evaluation.

### PROGRAM:
```py
import os
import io
import IPython.display
from PIL import Image
import base64 
import requests 
requests.adapters.DEFAULT_TIMEOUT = 60

from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv()) # read local .env file
hf_api_key = os.environ['HF_API_KEY']

import requests, json
from text_generation import Client

client = Client(os.environ['HF_API_FALCOM_BASE'], headers={"Authorization": f"Basic {hf_api_key}"}, timeout=120)
prompt = "What is deep learning in context with AI?"
client.generate(prompt, max_new_tokens=256).generated_text

import gradio as gr
def generate(input, slider):
    output = client.generate(input, max_new_tokens=slider).generated_text
    return output

demo = gr.Interface(fn=generate, 
                    inputs=[gr.Textbox(label="Prompt"), 
                            gr.Slider(label="Max new tokens", 
                                      value=20,  
                                      maximum=1024, 
                                      minimum=1)], 
                    outputs=[gr.Textbox(label="Completion")])

gr.close_all()
demo.launch(share=True, server_port=int(os.environ['PORT1']))

```

### OUTPUT:
<img width="1041" alt="Screen Shot 1947-02-31 at 07 53 52" src="https://github.com/user-attachments/assets/bda90455-a5a9-4893-844c-7feab9fa125e" />


### RESULT:
An interactive chat application that allows users to engage naturally with a large language model through a clean and responsive Gradio Blocks interface, enabling real-time conversation and easy deployment.
