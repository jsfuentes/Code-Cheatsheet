# OpenAI

## Text completion

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