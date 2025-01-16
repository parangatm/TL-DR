# Chip Design

### Summary

### Custom Silicon
**Advances in Modern Computer Architecture** : 
[Survey Paper](./Review_CustomSi.pdf)

The field of Computer Architecture is undergoing a transformative shift, driven by an increasing demand for performance and efficiency in modern applications. Key milestones in this evolution include the transition from CISC to RISC architectures, advancements in GPU, and the emergence of AI accelerators. The development of full-scale custom chips showcases the potential for optimized performance and innovation across various fields. This paper provides a comprehensive overview of these advancements, offering insights into the technological innovations that are reshaping the computing landscape. 

### Computer Architecture
| Paper Title                                       | Authors          | Year | Publication Link                            | Summary Link |
|---------------------------------------------------|------------------|------|---------------------------------------------|----|
| Power struggles: Revisiting the RISC vs. CISC debate on contemporary ARM and x86 architectures | Blem et al. | 2013 | [IEEE](https://ieeexplore.ieee.org/document/6522302) | [Review](./CompArch/Power_Struggles.md) |

### GPU Microarchitecture
| Paper Title                                       | Authors          | Year | Publication Link                            | Summary Link |
|---------------------------------------------------|------------------|------|---------------------------------------------|----|
| Analyzing CUDA Workloads Using a Detailed GPU Simulator | Bakhoda et al. | 2009 | [IEEE](https://ieeexplore.ieee.org/document/4919648) | [Review](./GPU/Bakhoda_2009_CUDA.md) |
| CORF: Coalescing Operand Register File for GPUs | Esfeden et al. | 2019 | [ACM](https://dl.acm.org/doi/10.1145/3297858.3304026) | [Review](./GPU/Esfeden_2019_CORF.md) |
| Dynamic Warp Formation and Scheduling for Efficient GPU Control Flow | Fung et al. | 2007 | [IEEE](https://ieeexplore.ieee.org/document/4408272) | [Review](./GPU/Fung_2007_Dynamic_Warp.md) |
| Hardware Acceleration of Neural Graphics | Mubarik et al. | 2023 | [ACM](https://dl.acm.org/doi/10.1145/3579371.3589085) | [Review](./GPU/Mubarik_2023_Neural.md) |
| Only Buffer When You Need To: Reducing On-chip GPU Traffic with Reconfigurable Local Atomic Buffers | Dalmia et al. | 2022 | [IEEE](https://ieeexplore.ieee.org/document/9773230) | [Review](./GPU/Dalmia_2022_LAB.pdf) |
| Gemini: Mapping and Architecture Co-exploration for Large-scale DNN Chiplet Accelerators | Cai et al. | 2023 | [arXiv](https://arxiv.org/pdf/2312.16436) | [Review](./GPU/Cai_2023_Gemini.md) |

### Chip Design Automation
| Paper Title                                       | Authors          | Year | Publication Link                            | Summary Link |
|---------------------------------------------------|------------------|------|---------------------------------------------|----|
| Developing synthesis flows without human knowledge | Yu et al. | 2018 | [DAC](https://dl.acm.org/doi/10.1145/3195970.3196026) | [Presentation](./Automation/ML_LogicSynth.pdf) |
| LSOracle: a Logic Synthesis Framework Driven by Artificial Intelligence | Neto et al. | 2019 | [IEEE](https://ieeexplore.ieee.org/document/8942145) | [Presentation](./Automation/ML_LogicSynth.pdf) |
| Learning to Design Efficient Logic Circuits | Hillier et al. | 2023 | [Google DeepMind](https://deepmind.google/impact/optimizing-computer-systems-with-more-generalized-ai-tools/) | [Presentation](./Automation/ML_LogicSynth.pdf) |
