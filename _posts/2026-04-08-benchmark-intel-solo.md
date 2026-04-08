# VLLM benmark (solo)

```
root@spark1:/workspace# vllm bench serve \
  --backend vllm \
  --base-url http://127.0.0.1:8000 \
  --model Intel/Qwen3.5-122B-A10B-int4-AutoRound \
  --tokenizer Intel/Qwen3.5-122B-A10B-int4-AutoRound \
  --dataset-name random \
  --random-input-len 128 \
  --random-output-len 128 \
  --num-prompts 3 \
  --request-rate inf

============ Serving Benchmark Result ============
Successful requests:                     3
Failed requests:                         0
Benchmark duration (s):                  8.17
Total input tokens:                      384
Total generated tokens:                  384
Request throughput (req/s):              0.37
Output token throughput (tok/s):         47.02
Peak output token throughput (tok/s):    54.00
Peak concurrent requests:                3.00
Total token throughput (tok/s):          94.03
---------------Time to First Token----------------
Mean TTFT (ms):                          920.64
Median TTFT (ms):                        921.97
P99 TTFT (ms):                           922.66
-----Time per Output Token (excl. 1st token)------
Mean TPOT (ms):                          56.95
Median TPOT (ms):                        57.04
P99 TPOT (ms):                           57.04
---------------Inter-token Latency----------------
Mean ITL (ms):                           56.95
Median ITL (ms):                         57.02
P99 ITL (ms):                            60.01
==================================================
```
