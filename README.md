# python-OpenAI

## Objectives of this repository
Detail and share how to use python scripts to connect to the OpenAI API, run prompts through API calls and use the AI content results generated within additional scripts.

## Context
This can be useful when we need to generate content at scale, for example in the case of demo data for a pre sales demo environment in which we want the data to look real (different than lastname1, test1, comment1 ...).\
No matter where and how we will store the data, the first step is to generate it and this where with the use of the right function in our python script in combination with the right prompt, we will get the best results.\
More details below.

## Installation
The first step is to install the OpenAI Python library
> [!TIP]
> The following article, straight from the OpenAI documentation, [Get up and running with the OpenAI API](https://platform.openai.com/docs/quickstart?context=python), is obviously very helpful.

We use the following code to install the library:
```
pip install --upgrade openai
```
> [!NOTE]
> We may need to restart the kernel to use updated packages.
> Once this completes, running `pip list` will show you the Python libraries you have installed in your current environment, which should confirm that the OpenAI Python library was successfully installed.

As for authentication, the OpenAI API uses API keys. We can visit our [API Keys page](https://platform.openai.com/account/api-keys) to retrieve the API key we'll use in our requests.

## Create the function
Placeholder text
```
import time
import openai

openai.api_key = "[we enter our API key here]"

def get_completion(prompt, model="gpt-3.5-turbo"):
    messages = [{"role": "user", "content": prompt}]
    response = openai.chat.completions.create(
        model=model,
        messages=messages,
        temperature=0.7, # this is the degree of randomness of the model's output
    )

    # Sleep for the delay
    time.sleep(2)
    
    return response.choices[0].message.content
```

>[!TIP]
>Lower values for temperature result in more consistent outputs (e.g. 0.2), while higher values generate more diverse and creative results (e.g. 1.0). Select a temperature value based on the desired trade-off between coherence and creativity for your specific application. The temperature can range is from 0 to 2.
  
## Execute the function
Now that are `get_completion` function is defined, we can use it to start generate content.\
As a first example we will use it to generate a poem about one of my favorite soccer player.
```
# first we define our prompt
prompt = f"""
Your task is to help generate a poem about Zinedine Zidane using the style of Baudelaire\
Make good ryhmes
"""

zidane_poem = get_completion(prompt)
```
![Screenshot - Print zidane poem](https://github.com/mboss10/python-OpenAI/blob/main/zidane_poem.png)
  
Let's use a more useful example.\

Imagine we need to generate data for a demo environment containing feeback of attendees at an event collected via a survey.\
Our prompt will look like the below:
```
# We call the OpenAI API to generate demo data of survey feedback around an event
prompt = f"""
Your task is to help generate a 2 sentence feedback example of an attendee of a data connference\
You can use positive or negative elements\
The feedback should be in the same paragraph as if someone has replied to a survey open question\
Don't use carriage return
"""

survey_feedback = get_completion(prompt)
```

  toto
Placeholder link - More queries and DataFrame results are available in my [Jupyter notebook](https://github.com/mboss10/python-Athena/blob/main/Athena%20connection%20and%20exploration.ipynb)

## Use the results to process the content generated
Placeholder text
