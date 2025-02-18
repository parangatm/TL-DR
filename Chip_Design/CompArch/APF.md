## Continual Flow Pipelines

### Publication:
A. Deshmukh, L. C. Cai and Y. N. Patt, "Alternate Path Fetch," 2024 ACM/IEEE 51st Annual International Symposium on Computer Architecture (ISCA), Buenos Aires, Argentina, 2024, pp. 1217-1229, doi: 10.1109/ISCA59077.2024.00091.

### Summary:

Alternate Path Fetch (APF) introduces a secondary instruction-processing pipeline in parallel to the primary out-of-order processor to mitigate branch misprediction. When encountering a hard-to-predict (H2P) branch, APF begins processing the not-predicted path in parallel to the main pipeline, which processes the branch predictor’s decision. This alternate pipeline starts from the fetch stage and extends till the pre-rename stage, and stores its state in a buffer for quick retrieval in case of a branch misprediction. APF effectively performs 13 cycles of processing within a 17-stage pipeline, theoretically reducing branch misprediction penalties by 75%. Contrary from other dual-path approaches, it avoids exponential complexity by avoiding processing alternate path branches to be more resource-efficient.

APF improves the dual-path processing paradigm by optimizing resource utilization and reducing race conditions compared to the Dual Path Instruction Processing (DPIP) model. While DPIP duplicates pipeline stages up to resource allocation into a shadow pipeline, APF selectively processes a smaller pipeline segment to maintain efficiency. The results indicate that APF provides a mean 5% speedup over baseline DPIP. The most interesting result is that the performance of best-case DPIP is equivalent to that of a 7-stage AFP pipeline, with 13-stages yielding the best results.

### Takeaways:

The primary takeaway from this paper is the power of pipelining, even after decades of using pipelined processors. Every stage of a CPU has the potential to be pipelined, and with careful tradeoff considerations, it can achieve significant performance gains. This work challenges the notion that TAGE-based predictors have exhausted branch prediction research, showing that parallel speculative execution can still enhance efficiency.

This paper also gives insights into the computation cost and overheads associated with each of the stages of an out-of-order core. It highlights that Rename and Allocation stages contribute significantly to frontend latency, which limits pipeline scalability. These findings suggest that other pipeline stages could similarly be extended for parallel processing, shaping further architectural optimizations.

### Augmentation:

The research efficiently benchmarks APF against modern commercial processors and provides a well-structured performance evaluation. However, the hardware overhead analysis is insufficient, relying on broad estimates rather than detailed comparisons. While APF does not duplicate large memory structures, it still extends the branch prediction stage by tracking H2P status, TAGE confidence, and branch IDs across different bits, which can introduce additional resource limitations. A more thorough discussion of the trade-offs between APF’s efficiency and its hardware footprint is necessary to support its practicality.
