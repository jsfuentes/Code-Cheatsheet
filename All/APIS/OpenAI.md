# OpenAI

[List of all model names](https://platform.openai.com/docs/models/model-endpoint-compatibility)

```python
duration = 10
topic = "Using Data in IEPs"

prompt = f"""
You are tasked with creating a {duration} minute lecture that covers "{topic}". 
Give a numbered list of short topics(under 8 words) that you would cover in this lecture:
"""

response1 = openai.ChatCompletion.create(
    model="gpt-4",
    messages=[
          {"role": "system", "content": "You are a one of the best teachers for adult students and seek to be educational and interesting."},
          {"role": "user", "content": prompt},
    ]
)
print(response1)
```

## Utils

```python
def parse_numbered_list(raw_list):
    number_regex = r"[0-9]+\. *"
    new_line_seperated_response = re.sub(number_regex, "", raw_list)
    # print(new_line_seperated_response)
    new_line_regex = r"(\n)+"
    l = re.sub(new_line_regex, "\n", new_line_seperated_response).split("\n")
    return l
```

## Errors

```
  File "/Users/jfuentes/Projects/Mowgli/Flask-Base/venv/lib/python3.9/site-packages/openai/api_requestor.py", line 683, in _interpret_response_line
    raise self.handle_error_response(
openai.error.RateLimitError: That model is currently overloaded with other requests. You can retry your request, or contact us through our help center at help.openai.com if the error persists. (Please include the request ID 5e48de76668e0d1f2dceead327886a57 in your message.)
```

## Old

### Text completion

- Design quality prompt with instructions and examples

- Temperature 0 is deterministic for where there is one right answer, 1 is for when many different answers are preferred. Its not "creativity"

```elixir
  OpenAI.completions(
    "davinci", # engine_id
    prompt: "once upon a time",
    max_tokens: 5,
    temperature: 1,
    ...
)
```

### Prompt Examples

Conversation, notice we can give the AI assistant an identity

```
The following is a conversation with an AI assistant. The assistant is helpful, creative, clever, and very friendly.

Human: Hello, who are you?
AI: I am an AI created by OpenAI. How can I help you today?
Human:
```

### Tips

- use max_tokens > 256
- Prefer finish_reason == "stop"
- Resampling 3-5 times with high temperature then pick samples that use stop as finish reason can be best
- Provide examples