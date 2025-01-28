## TAGE

### Publication:
A. Seznec and P. Michaud. “A case for (partially) TAgged GEometric history length branch prediction,” Journal of Instruction Level Parallelism, vol. 8, Feb 2006.

### Summary:

**Goal**: 

This paper presents the TAGE predictor (TAgged GEometric history length), an advanced branch predictor, leveraging geometric history lengths and partial tagging. The paper offers a cost-effective way to combine multiple predictions and get state-of-the-art branch prediction accuracy. The work was initially aimed at the CBP, which was extended to indirect branches.

**Methodology**: 

TAGE utilizes a bimodal 2-bit base predictor, and a hierarchical set of tagged predictor components with geometrically increasing history lengths. The longer-history tagged components refine the prediction made by the base predictor, allowing to capture both recent and long-term branch correlations. A novel update policy minimizes disruptions and optimizes the reuse of useful predictor entries. These principles are adapted well to extend the TAGE predictor to work for prediction of indirect branches as well.

### Takeaways:

- **Strengths of Hybrid Designs**: By merging the best features of O-GEHL and PPM predictors, TAGE demonstrates how hybrid designs enhance prediction accuracy.
- **Complex Update Policy**: The update step, being off the critical timing path, gives more scope of optimization to improve performance. The complex update policy in TAGE with useful counters and graceful resets attests this.
- **Extension to Indirect Branches**: Adapting TAGE for indirect branches shows the wide applicability and versatility of this design. On similar lines, other predictors can also be extended and analyzed for new types of prediction challenges.

### Augmentation:

Despite the obvious strengths, there are areas where this work can be improved:

- The paper focuses on software-metrics, like MPKI, but there is no discussion on physical hardware implementation of TAGE. - Comparing area, power and timing metrics with contemporary predictors would strengthen the author’s cost-effectiveness claims.
- For a paper published in 2006, a broader comparison with other predictors, and integration of real-world processor benchmarks apart from Championship benchmarks, will increase confidence in the capabilities of TAGE.

This work can be extended further by answering certain research questions:
- How important is the update policy as a standalone optimization? Can it be simplified?
- Is TAGE more versatile than ML-based predictors? How will a hybrid predictor with TAGE and Perceptron perform?
- How might the principles of TAGE be adapted for modern workloads like AI and Cryptography, and modern computing systems like GPUs and accelerators?
