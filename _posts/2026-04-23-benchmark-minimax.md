# benchmark minimax 

container: "lmsysorg/sglang:nightly-dev-cu13-20260423-0bee2113"
model: lukealonso/MiniMax-M2.7-NVFP4

```
+ /usr/bin/python3 -m sglang.bench_serving --backend sglang-oai-chat --base-url http://127.0.0.1:30000 --dataset-name random --model lukealonso/MiniMax-M2.7-NVFP4 --served-model-name minimax --tokenizer lukealonso/MiniMax-M2.7-NVFP4 --num-prompts 10 --random-input-len 128 --random-output-len 3 --max-concurrency 3 --extra-request-body {"separate_reasoning": false, "chat_template_kwargs": {"enable_thinking": false}}
```


```
============ Serving Benchmark Result ============
Backend:                                 sglang-oai-chat
Traffic request rate:                    inf       
Max request concurrency:                 3         
Successful requests:                     10        
Benchmark duration (s):                  1.43      
Total input tokens:                      597       
Total input text tokens:                 597       
Total generated tokens:                  19        
Total generated tokens (retokenized):    19        
Request throughput (req/s):              7.00      
Input token throughput (tok/s):          417.64    
Output token throughput (tok/s):         13.29     
Peak output token throughput (tok/s):    15.00     
Peak concurrent requests:                10        
Total token throughput (tok/s):          430.94    
Concurrency:                             2.49      
----------------End-to-End Latency----------------
Mean E2E Latency (ms):                   355.84    
Median E2E Latency (ms):                 345.00    
P90 E2E Latency (ms):                    497.69    
P99 E2E Latency (ms):                    597.15    
---------------Time to First Token----------------
Mean TTFT (ms):                          288.54    
Median TTFT (ms):                        306.67    
P99 TTFT (ms):                           381.70    
-----Time per Output Token (excl. 1st token)------
Mean TPOT (ms):                          73.72     
Median TPOT (ms):                        59.31     
P99 TPOT (ms):                           118.65    
---------------Inter-Token Latency----------------
Mean ITL (ms):                           74.76     
Median ITL (ms):                         58.86     
P95 ITL (ms):                            120.24    
P99 ITL (ms):                            122.18    
Max ITL (ms):                            122.67    
==================================================
```

# benchmark sacles
```
+ /usr/bin/python3 -m sglang.bench_serving --backend sglang-oai-chat --base-url http://127.0.0.1:30000 --dataset-name random --model saricles/MiniMax-M2.7-NVFP4-GB10 --served-model-name minimax --tokenizer saricles/MiniMax-M2.7-NVFP4-GB10 --num-prompts 10 --random-input-len 128 --random-output-len 128 --max-concurrency 3 --extra-request-body {"separate_reasoning": false, "chat_template_kwargs": {"enable_thinking": false}}
```

#Input tokens: 597
#Output tokens: 587
Starting warmup with 1 sequences...
Warmup completed with 1 sequences. Starting main benchmark run...

  0%|          | 0/10 [00:00<?, ?it/s]
 10%|█         | 1/10 [00:01<00:10,  1.18s/it]
 20%|██        | 2/10 [00:01<00:05,  1.48it/s]
 30%|███       | 3/10 [00:04<00:11,  1.59s/it]
 40%|████      | 4/10 [00:04<00:06,  1.10s/it]
 50%|█████     | 5/10 [00:07<00:08,  1.65s/it]
 60%|██████    | 6/10 [00:08<00:05,  1.45s/it]
 70%|███████   | 7/10 [00:08<00:03,  1.14s/it]
 80%|████████  | 8/10 [00:10<00:02,  1.23s/it]
 90%|█████████ | 9/10 [00:11<00:01,  1.28s/it]
100%|██████████| 10/10 [00:11<00:00,  1.16s/it]

============ Serving Benchmark Result ============
Backend:                                 sglang-oai-chat
Traffic request rate:                    inf       
Max request concurrency:                 3         
Successful requests:                     10        
Benchmark duration (s):                  11.66     
Total input tokens:                      597       
Total input text tokens:                 597       
Total input vision tokens:               0         
Total generated tokens:                  587       
Total generated tokens (retokenized):    587       
Request throughput (req/s):              0.86      
Input token throughput (tok/s):          51.20     
Output token throughput (tok/s):         50.34     
Total token throughput (tok/s):          101.53    
Concurrency:                             2.85      
----------------End-to-End Latency----------------
Mean E2E Latency (ms):                   3329.29   
Median E2E Latency (ms):                 3521.36   
---------------Time to First Token----------------
Mean TTFT (ms):                          156.41    
Median TTFT (ms):                        156.76    
P99 TTFT (ms):                           164.38    
---------------Inter-Token Latency----------------
Mean ITL (ms):                           54.99     
Median ITL (ms):                         55.59     
P95 ITL (ms):                            67.83     
P99 ITL (ms):                            98.60     
Max ITL (ms):                            102.19    
==================================================