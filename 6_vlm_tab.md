# VLM Performance Comparison

**Table A.** **Kernel latency and time-to-first-token (TTFT) on _Qwen3-VL-8B_ across resolutions.**  
At short sequences (**1k–4k tokens**), all sparse methods are comparable. As sequence length grows, HilbertA scales significantly better than both Flash Attention and NATTEN-27 — at 30k tokens, HilbertA achieves 2.0× kernel speedup over Flash (16.12 vs. 31.93 ms) and 1.5× over NATTEN-27 (16.12 vs. 24.07 ms), with similar advantages in TTFT (3.68s vs. 5.74s and 3.77s). NATTEN-7 achieves the lowest kernel latency but, as Table B shows, at severe quality cost.

|Tokens|Flash Attn (ms)|HilbertA (ms)|NATTEN-7 (ms)|NATTEN-27 (ms)|Flash TTFT (s)|HilbertA TTFT (s)|NATTEN-7 TTFT (s)|NATTEN-27 TTFT (s)|
|-|-|-|-|-|-|-|-|-|
|1,024|0.10|0.31|0.22|1.06|0.14|0.15|0.22|0.23|
|4,096|0.64|0.56|0.35|3.43|0.52|0.48|0.35|0.67|
|9,216|2.97|2.16|0.65|7.33|1.53|1.23|0.65|1.47|
|16,384|8.99|4.47|1.06|12.39|3.71|2.55|1.06|2.62|
|30,976|31.93|16.12|1.89|24.07|5.74|3.68|1.89|3.77|

---

**Table B. Benchmark performance on *Qwen3-VL-8B* across different sparse attention methods.** HilbertA achieves the best OCRBench (686) and MMStar (44.6%), substantially outperforming NATTEN-7 which degrades severely across all benchmarks (e.g., OCRBench drops to 426). NATTEN-21 recovers to competitive quality (667, 44.2%, 0.725) but is consistently slower than HilbertA in Table A. HilbertA is the only method that achieves strong performance on all three benchmarks without sacrificing efficiency.

|-|OCRBench|MMStar|MMBench|
|-|-|-|-|
|HilbertA|**686**|**44.6%**|**0.705**|
|NATTEN-7|426|37.1%|0.599|
|NATTEN-21|667|44.2%|**0.725**|