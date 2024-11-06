## CORF: Coalescing Operand Register File for GPUs

### Publication:
Asghari Esfeden, Hodjat and Khorasani, Farzad and Jeon, Hyeran and Wong, Daniel and Abu-Ghazaleh, Nael, “CORF: Coalescing Operand Register File for GPUs”, in 24th ACM International Conference on Architectural Support for Programming Languages and Operating Systems, Providence, RI, April 13-17, 2018.

### Description: 

**Problem**:

This paper addresses the challenge of optimizing the GPU register file (RF), which directly impacts GPU performance due to the frequent access by thousands of threads. Register file optimization poses two main challenges: it is power-hungry, consuming significant dynamic energy with each operation, and it is port-limited, supporting only serialized access to register banks and operand collectors.

**Solution**:

The authors propose the Coalescing Operand Register File (CORF), an enhanced RF that merges multiple reads required by an instruction into a single read operation by packing logical registers into physical registers, guided by compiler instructions. An extension, CORF++, further rearchitects the RF to merge read operations across multiple sub-banks, overcoming limitations posed by CORF.

**Methods**:

In CORF, the compiler first builds a Register Affinity Graph to identify commonly accessed register pairs. If the data width permits, these pairs are packed into the same physical registers using a hardware packer. A renaming table maps these combinations, and an unpacker separates the coalesced values after the read. Each register can only be paired with one other hard-coded register, posing a limitation on registers occurring in multiple pairs.

CORF++ extends CORF by restructuring the register file to enable packing across different physical registers in separate sub-banks. Registers are assigned as left-aligned or right-aligned by the compiler, with dual-addressable banks supporting the reading of packed registers from different banks. A width detection unit and allocation unit in the hardware determine efficient register placement to maximize the benefits of coalescing.

**Results**:

The proposed methods improve Instructions per Cycle (IPC) by approximately 9% compared to a baseline register file, and reduce dynamic energy consumption by about 17%. These coalescing operations lower the number of physical reads by roughly 23% in integer-dominant benchmarks and 10% in floating-point-dependent benchmarks.

### Critical Evaluation:

**Insights**:

The paper provides a compelling argument on the importance of optimizing RF access patterns in GPU performance. The presence of narrow-width operands in the testing benchmarks and the benefits of simply combining them in the unused register bytes, is an intuitive yet impactful solution. The practical approach, combining compiler-guided optimization with register file reorganization, results in an effective strategy for improving energy efficiency and throughput.

**Strengths**:

One of the main strengths of this paper is the simplicity of the solution. It doesn’t introduce a new complex paradigm, instead extends existing practices in a practical manner. The use of graph coloring to solve the register allocation challenge is well-founded, with a balanced division of tasks between compiler-driven and architectural solutions. The evaluation spans a diverse set of benchmarks, demonstrating the method's broad applicability and significant potential.

**Weaknesses**:

A recurring issue in the paper is the repetition of same ideas across different sections, which makes it unnecessarily lengthy. The solution achieves a balanced optimization approach and provides practical details about implementation, including the renaming table, packer, unpacker, and allocation units. However, the discussion lacks information on the overhead introduced by compiler processes. While the compiler’s task to generate the register affinity graph will increase compile time and complexity, the paper only addresses code size as an overhead. 

There is a lack of detailed discussion on the implementation of metadata instruction to deliver the register-pairing to the hardware. Each custom instruction in an ISA necessitates pipeline extensions for decoding and execution. While easier to handle in RISC-V, the closed-source nature of the NVIDIA Fermi GPU’s ISA complicates these changes. These details are required to effectively understand all of the hardware changes.

**Relevance**:

Finding simpler ways to boost GPU performance is always an ongoing research in this field. The approach presented could inform future register file designs, enhancing memory hierarchy optimization and more efficient register management. The solution seems to have a huge potential, but it needs to be thoroughly tested across different configurations to understand the bottlenecks and scope of scalability.
