
Hierarchical Reasoning Model (HRM)
1. Recursive Hierarchical Reasoning
2. Deep Supervision

There are four modules:
1. Input Module ($f_i$)
2. Low Level Module $f_L$
3. High Level Module $f_H$
4. Output Module ($f_O$)

Process
1. Input -> Embeddings
2. Run $f_L$, T times over the inputs. T = 1 cycles
3. Run $f_H$, once per cycle for H cycles. One Forward pass = TN times
4. $f_O$ map the hidden state of $f_H$ into the output.

Concepts
- Hidden state $z_H$ represent the goal for the current cycle. 
- $f_L$ will converge toward that goal. 
- After a cycle, $z_H$ will be updated and $f_L$ will have a new goal to converge.
- Segment = a sequence of cycle. A segment can have a dyanamic number of cycles via ACT
- Therefore, H module diverge toward the overall goal (target task.)
- While, L module diverge sub goals determine by H module.

Units - 
- T times
- 1 cycle = T times
- 1 segment (forward pass) = N cycles

# Training Stability
- Therefore, H module diverge toward the overall goal (target task.)
- While, L module diverge sub goals determine by H module.
	- seems unstable but it was converging local sub-goals.
![[Screenshot 2025-11-24 at 4.53.31 PM.png]]

## Standard RNN Cons
- Memory consumption from storing all hidden states from forward pass and combining them with the gradients for the back propagation which demands O(T) memory for T timestamps.

## Gradient Approximation
- But if a recurrent neural network converges to a fixed point, we can apply back propagation to that equilibrium point (though rarely happen). Note: local fix point means, hidden states of L-module remain the same after that point within that cycle. 

- One step approximation - use the gradient of the last state of each module and treat other states as constant. Therefore, gradients path (back propagation) is Output. head -> final state of H-module -> final state of the L-Module -> input embedding.
- That method only require O(1) memory.

![[Screenshot 2025-11-24 at 5.03.15 PM.png]]

## Deep Supervision


- During training, the model is run for several "segments." 
- At the end of each segment, $z_m$ represent both  


# Adaptive Halting Strategy or Adaptive Computation Time (ACT)




Loss Function
- Loss for suerpvision segment and Q-Head loss (BinaryCrossEntropy)
# Confusions
## For each cycle, how $z_H$ is updated? 