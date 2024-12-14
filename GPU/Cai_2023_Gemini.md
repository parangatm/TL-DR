## Gemini: Mapping and Architecture Co-exploration for Large-scale DNN Chiplet Accelerators

### Publication:
Jingwei Cai, Zuotong Wu, Sen Peng, Yuchen Wei, Zhanhong Tan, Guiming Shi, Mingyu Gao, Kaisheng Ma, “Gemini: Mapping and Architecture Co-exploration for Large-scale DNN Chiplet Accelerators”, arXiv: 2312.16436 [cs], Dec. 2023.

### Description: 

**Problem**: 

The paper addresses the challenge of maximizing the potential of chiplet technology in designing scalable DNN inference accelerators while minimizing associated drawbacks such as energy inefficiency, high costs, and limited scalability. Specifically, it identifies the need for an optimized architecture and mapping strategy in the post-Moore era, where chiplets are crucial for handling increased computational and memory demands.

**Solution**: 

The authors have described a customizable general-purpose Chiplet architecture hardware template which can be configured and extended to support any DNN inference. This implementation is supported by their architectural exploration framework, Gemini, which systematically explores the design space for such systems.

**Key Insights**:

1. **Chiplet Granularity**

Moderate chiplet granularity strikes a balance between performance, energy efficiency and monetary cost. Fine grained partitions improve yield, but introduce some limitations:
- Increased data communication leads to higher energy consumption, as D2D links are more power-hungry than on-chip interconnects
- Excessive inter-chiplet data transfer incurs latency penalties, negating performance gains from fine partitions
- Higher packaging and interconnect requirements increase the overall cost.

2. **Core Granularity**

The scalability of multi-core processing shows diminishing returns:
  - Increasing core counts initially enhances throughput but results in higher energy-delay-product (EDP) beyond a certain point.
  - Longer pipelines from more cores leads to utilization losses during filling and draining phases, as well as overheads from dependency management.

3. **DNN Mapping**

Mapping strategies that prioritize minimizing DRAM accesses are critical:
  - Clustering data-dependent layers onto chiplets with high interconnectivity reduces costly DRAM accesses, keeping latency and costs to a minimum.
  - Reducing DRAM accesses by processing data-intensive layers on-chip ensures lower energy costs while maintaining throughput.

4. **One-size-fits-all Design**

The reuse of chiplets across multiple accelerators appears attractive from a cost perspective since it reduces many one-time setup costs, but often results in suboptimal and less-than-ideal outcomes. Chiplets designed for a specific compute workload are ill-suited for other scenarios, leading to inefficiencies in energy and performance.

**Conclusion**: 

The authors emphasize that chiplet-based architectures are a puzzle of interconnected trade-offs. Balancing the granularity of chiplets and cores is essential for solving for an optimal configuration that meets energy, performance, and cost requirements. Furthermore, while pipelines and mapping techniques offer scalability, their effectiveness hinges on reducing memory accesses and communication overheads. This nuanced interplay between architectural decisions and workload mapping forms the backbone of scalable DNN accelerators.

Gemini’s analysis of reusability is particularly thought-provoking. It demonstrates that while reusing chiplets for multiple accelerators can reduce non-recurring engineering (NRE) costs, significant trade-offs in performance and efficiency often emerge. This insight provides a roadmap for future work on tailoring chiplet designs to specific use cases.
