# setup litellm 

## install litellm

```
python3 -m venv ~/litellm-venv
source ~/litellm-venv/bin/activate
uv pip install 'litellm[proxy]'
```

## Edit config


```yaml
model_list:
  - model_name: "claude-sonnet-4-6"
    litellm_params:
      model: "openai/Qwen/Qwen3.5-397B-A17B-GPTQ-Int4"
      api_base: "http://localhost:30000/v1"
      custom_llm_provider: "openai"
      api_key: "sk-sglang"
      force_use_custom_endpoint: true
      drop_params: true
      extra_body:
        chat_template_kwargs:
          enable_thinking: false
      max_tokens: 8192                    # reasonable max output per request
      context_window: 131072              # or 262144 if your SGLang is set higher

litellm_settings:
  use_chat_completions_url_for_anthropic_messages: true   # ← critical for Claude Code
  turn_off_message_logging: true
  success_callback: []
  # drop_params: true   # can move this here if you want it global

general_settings:
  master_key: "sk-sglang"
  set_verbose: true
```

## run litellm

```
 litellm --config litellm-config.yaml --port 3005
``` 

# verify with curl

```
 curl http://localhost:3005/v1/messages   -H "Content-Type: application/json"   -H "x-api-key: sk-sglang"   -H "anthropic-version: 2023-06-01"   -d '{
    "model": "claude-sonnet-4-6",
    "max_tokens": 512,
    "messages": [{"role":"user","content":"Say hello"}]
  }'
{"id":"c5a8bcd7695b45529c818efa596e0210","type":"message","role":"assistant","model":"claude-sonnet-4-6","stop_sequence":null,"usage":{"input_tokens":14,"output_tokens":10,"total_tokens":24},"content":[{"type":"text","text":"Hello! How can I help you today?"}],"stop_reason":"end_turn"}
```

# execute claude
```
 ANTHROPIC_BASE_URL=http://localhost:3005 ANTHROPIC_AUTH_TOKEN=sk-sglang CLAUDE_CODE_MAX_OUTPUT_TOKENS=8192 claude
```