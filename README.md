## Development and Deployment of a 'Chat with LLM' Application Using the Gradio Blocks Framework

### AIM:
To design and deploy a "Chat with LLM" application by leveraging the Gradio Blocks UI framework to create an interactive interface for seamless user interaction with a large language model.

### PROBLEM STATEMENT:
Develop a user-friendly chatbot application using a large language model (LLM) to assist users with queries and generate conversational responses. The application should feature a responsive design, real-time text exchange, and customizable settings for response quality.

### DESIGN STEPS:

#### STEP 1: Set Up the Environment Install the necessary libraries (openai, gradio) and verify API access to the LLM. 

#### STEP 2: Create the Chat Functionality Write a function to interact with the LLM using OpenAI's API (or another preferred LLM provider).

#### STEP 3: Design the Gradio Blocks Interface Use Gradio Blocks to build a structured, multi-component UI with features like: A text box for user input. A chat history display. A clear button to reset the conversation. 

#### STEP 4:  Deploy and Test Host the Gradio app locally or on a server. Test with diverse inputs to ensure robust performance.

### PROGRAM:
```PYTHON
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
# Helper function
import requests, json
from text_generation import Client

#FalcomLM-instruct endpoint on the text_generation library
client = Client(os.environ['HF_API_FALCOM_BASE'], headers={"Authorization": f"Basic {hf_api_key}"}, timeout=120)
prompt = "Has math been invented or discovered?"
client.generate(prompt, max_new_tokens=256).generated_text
#Back to Lesson 2, time flies!
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
gr.close_all()

```
### OUTPUT:
<img width="1197" height="712" alt="image" src="https://github.com/user-attachments/assets/fd15627c-5bb6-4e03-9adf-d5fc293c2d59" />

### RESULT:

The "Chat with LLM" application successfully enables interactive text-based communication with a large language model, offering a streamlined and visually appealing interface for users.
