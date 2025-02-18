## Continual Flow Pipelines

### Publication:
D. Sanchez and C. Kozyrakis, "The ZCache: Decoupling Ways and Associativity," 2010 43rd Annual IEEE/ACM International Symposium on Microarchitecture, Atlanta, GA, USA, 2010, pp. 187-198, doi: 10.1109/MICRO.2010.20.

### Summary:

This paper presents ZCache, a cache design that achieves high associativity without the traditional cost of increasing physical ways in the cache. Conventional caches improve associativity by increasing the number of ways, which in turn increases latency, area and energy consumption. In contrast, Zcache decouples ways from associativity by increasing the number of possible replacement candidates rather than physical ways. It uses a skewed indexing with different hash functions per way, and moves existing blocks to alternate locations rather than evicting them outright. Replacement computations, including block relocations, occur off the critical path which ensures minimal impact on overall latency. 

The authors introduce an associativity distribution framework to quantify associativity as a probability function of eviction quality rather than a function of set size. The results show that a 4-way ZCache with 52 replacement candidates: 
1. outperforms a 32-way set associative cache by 7% in IPC and 10% in energy efficiency
2. has lower access latency and energy consumption than a 4-way set associative cache

### Takeaways:

A key insight from this paper is that associativity is better understood in terms of the number of replacement candidates than the cache ways. This approach challenges the conventional notion that higher associativity must come at the cost of cache latency, and thus breaks the tradeoff between associativity and hit rate. 

The placement strategy followed by this design to relocate existing blocks requires some additional computation. ZCache mitigates this overhead by performing these computations during the long-latency main memory operation, demonstrating the effective use of otherwise idle cycles.

### Augmentation:

While ZCache presents an effective alternative to the traditional set-associative caches, its replacement policy can be further improved. The proposed eviction mechanism relies on 32-bit timestamps, an additional metadata storage overhead which can otherwise be allocated to cache capacity. This can be improved by exploring compressed metadata representations or incorporating some machine learning driven approach.

Modern cache designs integrate security mechanisms to protect against the growing cache side-channel attacks. The use of multiple hash functions in ZCache inherently introduces randomness in block placement, potentially improving its resilience against attacks. A deeper security analysis of ZCache will further validate its practicality for secure architectures. 
