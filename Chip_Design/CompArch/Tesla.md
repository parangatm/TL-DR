## NVIDIA Tesla

### Publication:
E. Lindholm, J. Nickolls, S. Oberman and J. Montrym, "NVIDIA Tesla: A Unified Graphics and Computing Architecture," in IEEE Micro, vol. 28, no. 2, pp. 39-55, March-April 2008, doi: 10.1109/MM.2008.31.

### Summary:

This paper introduces the Tesla architecture and the CUDA programming model, which have significantly shaped the modern computing and tech landscape. The authors describe the chronological evolution of GPUs from separate vertex and pixel processors to a unified architecture, driven by the need to balance fixed and floating-point operations, and maintaining design complexity and costs. 

The key elements of Tesla architecture are as follows.
1. The fundamental unit is the **Streaming Multiprocessor (SM)** which executes vertex, geometry, and pixel shader programs efficiently. 
2. The **work distribution units** allocate tasks across processors for parallel execution. 
3. **Memory** is divided into three levels—local, shared and global—to optimize low-latency operations and inter-thread synchronization. 

The authors emphasize Tesla’s programmability using CUDA to accelerate applications written in C, broadening the applicability of GPUs beyond graphics processing.

### Takeaways:

This paper makes the hardware-software co-design approach easier to grasp with relatable analogies, such as mapping threads to processors, and warps to cooperative thread arrays (CTAs). The discussion on the shift to a unified architecture highlights the interdependence of design choices, cost constraints and market demands. The paper effectively demonstrates the tradeoff between hardware complexity and computational flexibility through dynamic work distribution between vertex and pixel processing.

### Augmentation:

One area where this work could be improved is in the design of work distribution units. The paper describes that the tasks are distributed to different processors in a round-robin fashion, which may lead to underutilization of resources and potentially starvation in heterogeneous workloads. A more adaptive workload distribution scheme based on resource usage, could improve overall utilization and boost performance further.

Another limitation is the ecosystem dependency created by the reliance on CUDA libraries. While it provides a significant speed-up when using NVIDIA architecture, it limits portability across other proprietary architectures such as AMD or open-source ones like RISC-V or Open-GL. Further research could explore how a unified programming model similar to CUDA could be made independent of the architecture.