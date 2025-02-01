## Learning both weights and connections for efficient neural networks

### Publication:
Song Han, Jeff Pool, John Tran, and William J. Dally. 2015. Learning both weights and connections for efficient neural networks. In Proceedings of the 29th International Conference on Neural Information Processing Systems - Volume 1 (NIPS'15), Vol. 1. MIT Press, Cambridge, MA, USA, 1135–1143.

### Summary: 

Modern neural networks are too complex and big to be deployed on embedded systems. Large networks do not fit on the on-chip storage and require off-chip DRAM accesses, making them non-ideal for hardware implementation. Network size reduction is important for optimizing operational costs and promoting feasibility in resource-constrained environments. 

Neural Networks are typically overparameterized which leads to a lot of redundant information being encoded. Reducing redundancy in the network is a feasible approach to reduce network size. Previous redundancy methods such as reduced precision, tensor decomposition and quantization do not perform well across different architectures.

The paper suggests a pruning method to compress the network, in a three-step process:
1. Train network normally to learn the important connections
2. Prune the low-value (unimportant) connections to create a sparser network
3. Retrain the network to learn the final weights for the surviving connections

The most important and optimization-worthy step in this methodology is the pruning decision. There are several approaches to this:
1. **Regularization**: While L1 regularization is beneficial for initial pruning, L2 regularization provides better accuracy after retraining.
2. **Dropout** Control: Dropout ratios must be adjusted during retraining to account for reduced model capacity, thus reducing any over-fitting.
3. **Iterative Pruning**: Prune and retrain repeatedly to reach the lowest sized model. Each iteration refines the network to preserve accuracy while reducing complexity.
4. **Pruning Neurons**: Remove dead neurons with zero input or output connections during retraining due to lack of any contribution to the network's output.

The suggested methodology was tested on state-of-the-art networks and gave promising results. With almost no loss in accuracy, LeNet achieved a 12-fold compression, and AlexNet reached to 9x compression and 3x reduction in computation.