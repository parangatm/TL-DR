## Power Struggles

### Publication:
E. Blem, J. Menon and K. Sankaralingam, "Power struggles: Revisiting the RISC vs. CISC debate on contemporary ARM and x86 architectures," 2013 IEEE 19th International Symposium on High Performance Computer Architecture (HPCA), Shenzhen, China, 2013, pp. 1-12, doi: 10.1109/HPCA.2013.6522302.

### Summary:

**Goal**: 

This paper revisits the CISC vs RISC debate to investigate whether the choice of ISA fundamentally impacts performance and energy efficiency in modern computing systems. It aims to establish whether RISC’s low energy consumption and CISC’s high performance are intrinsic to ISAs or outcomes of microarchitectural optimizations.

**Methodology**: 

This study considers multiple processors with similar microarchitectures and runs the same benchmarks on the same operating system. Additionally, results are normalized to the same technology node to isolate the ISA-specific effects from other factors.

**Key Findings**:

- Performance and energy efficiency differences are primarily influenced by microarchitecture optimizations such as pipeline depth, issue width, cache hierarchy, irrespective of ISA.
- The RISC vs. CISC distinction has evolved to focus on adding specialized features to processors such as vector extensions and security capabilities.

### Takeaways:

The perception that modern computing systems transitioning from CISC to RISC achieve significant performance gains is questioned by this study. The key lesson is that design and microarchitecture choices play a far more critical role than ISA alone. The adoption of RISC ISA is largely due to its focus on specialization with custom extensions and security features, with performance and energy gains evident in specialized workloads.

The author’s approach to decouple ISA differences and microarchitectural optimizations is intriguing. This separation offers a fresh perspective, as computer architecture classes often address these factors jointly without isolating their individual impacts. The authors also connected the numerical outcomes to hardware pipeline design really well, which emphasizes on the tight loop between software profiling data and hardware design. 

### Augmentation:

While this paper evaluated only general-purpose processor cores, it can be refined for modern computing trends in the following areas:

- Expand the evaluation of RISC vs CISC performance and energy efficiency for emerging workloads, such as artificial intelligence, cryptography, and data analytics.
- Investigate the extent to which specialized accelerators, such as GPUs and TPUs, benefit from differences in instruction set architectures.
- Assess the effectiveness and robustness of security features in each ISA, against rising hardware attacks such as Spectre and Meltdown.
