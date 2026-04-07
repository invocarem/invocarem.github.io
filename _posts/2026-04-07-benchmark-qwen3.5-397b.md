# Benchmark Qwen3.5-397b (gptq-int4)

```
SGLANG_USE_AITER=1 python3 -m sglang.launch_server \
    --model-path Qwen/Qwen3.5-397B-A17B-GPTQ-Int4 \
    --served-model-name qwen3.5-397b \
    --context-length 88000 \
    --mem-fraction-static 0.93 \
    --tp-size 2 \
    --host 0.0.0.0 \
    --port 30000 \
    --enable-metrics  \
    --attention-backend triton \
    --tool-call-parser qwen3_coder \
    --reasoning-parser qwen3 \
    --speculative-algorithm EAGLE \
    --speculative-num-steps 3 \
    --speculative-eagle-topk 1 \
    --speculative-num-draft-tokens 4 \
    --enable-flashinfer-allreduce-fusion  \
    --mamba-scheduler-strategy extra_buffer \
    --quantization moe_wna16 \
    --kv-cache-dtype fp8_e4m3 \
    --max-running-requests 3 \
    --enable-cache-report  \
    --preferred-sampling-params '{"temperature":0.6,"top_p":0.95,"top_k":20,"min_p":0.0,"presence_penalty":0.0,"repetition_penalty":1.0}' \
    --trust-remote-code \
    --dist-init-addr 192.168.100.11:50000 \
    --nnodes 2 \
    --node-rank 0
```

```bash
 docker exec -it sglang_node_tf5 bash
root@spark1:/data/sglang# python3 -m sglang.bench_serving \
  --backend sglang-oai-chat \
  --base-url http://127.0.0.1:30000 \
  --dataset-name random \
  --model Qwen/Qwen3.5-397B-A17B-GPTQ-Int4 \
  --served-model-name qwen3.5-397b \
  --tokenizer Qwen/Qwen3.5-397B-A17B-GPTQ-Int4 \
  --num-prompts 20 \
  --random-input-len 128 \
  --random-output-len 128 \
  --extra-request-body '{"separate_reasoning": false, "chat_template_kwargs": {"enable_thinking": false}}' \
  --num-prompts 3 --request-rate inf
```

result:

```
============ Serving Benchmark Result ============
Backend:                                 sglang-oai-chat
Traffic request rate:                    inf
Max request concurrency:                 not set
Successful requests:                     3
Benchmark duration (s):                  15.07
Total input tokens:                      159
Total input text tokens:                 159
Total generated tokens:                  211
Total generated tokens (retokenized):    211
Request throughput (req/s):              0.20
Input token throughput (tok/s):          10.55
Output token throughput (tok/s):         14.00
Peak output token throughput (tok/s):    8.00
Peak concurrent requests:                3
Total token throughput (tok/s):          24.56
Concurrency:                             2.26
Accept length:                           2.09
----------------End-to-End Latency----------------
Mean E2E Latency (ms):                   11353.55
Median E2E Latency (ms):                 14001.21
P90 E2E Latency (ms):                    14836.22
P99 E2E Latency (ms):                    15024.10
---------------Time to First Token----------------
Mean TTFT (ms):                          6728.20
Median TTFT (ms):                        5529.62
P99 TTFT (ms):                           14096.41
-----Time per Output Token (excl. 1st token)------
Mean TPOT (ms):                          72.33
Median TPOT (ms):                        66.71
P99 TPOT (ms):                           85.59
---------------Inter-Token Latency----------------
Mean ITL (ms):                           66.71
Median ITL (ms):                         63.97
P95 ITL (ms):                            135.17
P99 ITL (ms):                            142.18
Max ITL (ms):                            145.86
==================================================
```
