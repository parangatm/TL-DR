## Analyzing CUDA Workloads Using a Detailed GPU Simulator

### Publication:
Ali Bakhoda, George Yuan, Wilson W. L. Fung, Henry Wong, Tor M. Aamodt, "Analyzing CUDA Workloads Using a Detailed GPU Simulator", in IEEE International Symposium on Performance Analysis of Systems and Software (ISPASS), Boston, MA, April 19-21, 2009.

### Description: 

**Problem**: 

GPUs have proven to be incredibly powerful for graphical workloads, but their potential for general-purpose workloads has not been fully explored. This paper addresses a key gap: why do non-graphical applications often fail to reach peak performance on GPUs? The authors aim to study the microarchitectural features in GPU systems that cause bottlenecks and explore the best configurations of hardware, memory and workload distribution to bridge these gaps. 

**Solution**: 

The authors have chosen several non-trivial applications with performance speedup reported below 50x by  NVIDIA CUDA, to identify opportunities for optimizing their execution. The GPGPU-Sim simulator has been extended to support the CUDA Parallel Thread Execution (PTX) instruction set, which enables these kernels to be easily run on it without any changes to the compilation process. This provides deeper insights into the bottlenecks and tuning options.

**Methods or Design Space**:

The study explores a broad design space to investigate the behavior of different applications under different system configurations. The study investigates a range of permutations for:
- Interconnect network topologies, latency and bandwidth
- DRAM controller configurations
- Memory coalescing and caching techniques
- Thread distribution and concurrency

The applications chosen for analysis span a diverse range of performance challenges: from memory-intensive kernels like Graph BFS to control-flow divergence-prone Ray Tracing. This diversity of workloads allows the authors to assess the GPU’s performance across multiple fronts, giving a complete picture of the strengths and weaknesses.

**Results**: 

The study concludes that the performance bottleneck for these non-graphical applications revolves around interconnect bandwidth and memory access. Simply increasing the thread count or parallelism does not always improve performance, in fact, reducing concurrent thread blocks reduces memory contention, boosting performance. Optimizations in DRAM controllers and memory coalescing also show speedup, especially for memory-intensive workloads.

### Critical Evaluation:

**Insights**: 

This paper optimizes non-conventional CUDA workloads and offers non-conventional insights into GPU optimization, The key takeaway is that the notion that concurrency is always better for a GPU does not always hold true; increasing thread count should be carefully balanced with memory access patterns to avoid diminishing returns in performance.

Another insight is the importance of bandwidth over latency. The assumption that reducing latency should be the primary goal to get higher speeds is challenged, with the demonstration that most applications were more sensitive to interconnect bandwidth than latency. This means that GPU designers and CUDA developers should not solely focus on reducing latency in future designs and kernels, but also increasing the bandwidth for general-purpose acceleration.

**Strengths**:

One of the strongest aspects of this paper is the diversity of kernels chosen for experimentation, targeting each of the limitations posed by a GPU. These include data-intensive and memory-bound kernels, floating-point-heavy kernels, control-flow divergence-prone kernels, and scientific computation kernels with irregular memory and compute patterns. Experimenting with these non-benchmark kernels provides nuanced data into fully realizing the potential of a GPU. The range of configurations explored does not just provide a surface-level analysis of a single feature, but offers a deeper understanding of how different changes speed up and slow down the same application. 
 
**Weaknesses**:

The authors have focused on overall observations and their inferences, but have clarified how specific memory access patterns or control flow divergences are overcome for performance. The intended audience, i.e. CUDA developers and GPU architects might benefit from dividing the kernels into different categories, and explaining a hands-on optimization approach for each category. In its current state, the audience will have to sift through the plethora of graphs and numbers to understand which strategy would work best for their case.

The only focus of this study is on performance speedup which seems a very software-centric approach, while in reality GPU optimization needs a balance of hardware and software alike. The recent usage of GPUs in data centers requires them to be power-efficient, and for increased scalability cost-efficient. It could benefit from energy and cost analysis also for each of the hardware configurations tested.
 
**Relevance**: 

With the gradual increase in compute-intensive applications and industrial shift towards accelerated computing, this paper offers insightful findings into making GPUs useful outside of graphical tasks. It targets hardware designers to come up with the best system configuration to support GPU acceleration for general-purpose computing. It lays a strong foundation for future research, and presents a verbose architectural exploration of GPU systems.
