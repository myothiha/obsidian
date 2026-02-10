
Hierarchical Reasoning Model (HRM)
1. Recursive Hierarchical Reasoning
2. Deep Supervision

There are four modules:
1. Input Module ($f_i$): $\tilde{x} = f_I(x;\theta_I)$
2. Low Level Module ($f_L$): use to compute the hidden state $z_L^{i} = f_L\!\left(z_L^{i-1},\, z_H^{i-1},\, \tilde{x};\, \theta_L\right)$
3. High Level Module ($f_H$): 
$$
z_H^{i} =
\begin{cases}
f_H\!\left(z_H^{i-1},\, z_L^{i-1};\, \theta_H\right), & \text{if } i \equiv 0 \pmod{T}, \\[6pt]
z_H^{i-1}, & \text{otherwise}.
\end{cases}
$$
4. Output Module ($f_O$): $\hat{y} = f_O\!\left(z_H^{NT};\, \theta_O\right)$

Process
1. Input -> Embeddings
2. Run $f_L$, T times over the inputs. T = 1 cycles
3. Run $f_H$, once per cycle for N cycles. One Forward pass = TN times
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
$$z_L^\star = f_L\bigl(z_L^\star,\, z_H^{k-1},\, \tilde{x};\, \theta_L\bigr).$$
- One step approximation - use the gradient of the last state of each module and treat other states as constant. Therefore, gradients path (back propagation) is Output. head -> final state of H-module -> final state of the L-Module -> input embedding.
- That method only require O(1) memory.

![[Screenshot 2025-11-24 at 5.03.15 PM.png]]

## Deep Supervision


- During training, the model is run for several "segments." before termination
- At the end of each segment, $z_m$ represent the hidden state at the conclusion of the segment m. include both $z_H$ and $z_L$ 
- For each segment m,
	- Compute next hidden states and prediction: $\left(z^{m},\, \hat{y}^{m}\right) \leftarrow \mathrm{HRM}\!\left(z^{m-1},\, x;\, \theta\right)$
	- Compute the loss for the current segment: $L^{m} \leftarrow \mathrm{Loss}\!\left(\hat{y}^{m},\, y\right)$
	- Update the parameters: $\theta \leftarrow \mathrm{OptimizerStep}\!\left(\theta,\, \nabla_{\theta} L^{m}\right)$
- The hidden state $z_m$ is detached from the computation graph so that update will only applied to that segment.
# Adaptive Halting Strategy or Adaptive Computation Time (ACT)

- enable thinking, fast and slow.
- Leverage deep supervision and the Q-learning algorithm for flexible number of segment. $\hat{Q}^{m} = \sigma\!\left(\theta_{Q}^{\top} z_{H}^{mNT}\right)$
- Q-head is used to predict Q-values and decide to "continue" or "halt": $\hat{Q}^{m} = \bigl(\hat{Q}^{m}_{\text{halt}},\; \hat{Q}^{m}_{\text{continue}}\bigr)$
	- It depends on the hidden state of the H-module.
	- It has its own parameters.
- $M_{\max}$: maximum number of segments
- $M_{\min}$: minimum number of segments. 
	- With probability of $\epsilon$, it is uniformly sample from $\set{2, ..., M_{\max}}$.
	- With probability of $1 - \epsilon$, it is set to 1.
- The halt action will be selected when
	- If the segment count exceed $M_{\max}$ (or)
	- when value of $\hat{Q}_{\text{halt}}$ exceed $\hat{Q}_{\text{continue}}$ and the segment count has reached at least the minimum threshold $M_{min}$.
- Q-head is updated with Q-learning algorithm. 
	- "halt" -> terminate the episode -> binary reward (0 or 1). $\hat{G}^{m}_{\text{halt}} = \mathbf{1}\{\hat{y}^{m} = y\}$
	- "continue" -> continue the episode -> expected value  
$$
\hat{G}^{m}_{\text{continue}} =
\begin{cases}
\hat{Q}^{m+1}_{\text{halt}}, & \text{if } m \ge N_{\max}, \\[6pt]
\max\!\left(\hat{Q}^{m+1}_{\text{halt}},\, \hat{Q}^{m+1}_{\text{continue}}\right), & \text{otherwise}.
\end{cases}$$


## Loss Function
- Loss for suerpvision segment and Q-Head loss (BinaryCrossEntropy)
$$
L_{\mathrm{ACT}}^{m}
= \mathrm{Loss}\!\left(\hat{y}^{m},\, y\right)
+ \mathrm{BinaryCrossEntropy}\!\left(\hat{Q}^{m},\, \hat{G}^{m}\right).
$$

# Architecture

- Sequence to Sequence Model
- use softmax over all output tokens.
	- $\mathrm{Loss}(\hat{y}, y)= \frac{1}{l'} \sum_{i=1}^{l'} \log p(y_i)$
- Inital hidden state: $z_0$ is initialized by sampling from truncated normal distribution with standard deviation 1 and truncation of 2. 
- Both L-Module and H-Module are implement using encoder-only transformer blocks with identical architectures and dimensions.

## Pseudo Code

(Refing HRM pseudo code From TRM Paper which is much more details.)
![[Screenshot 2026-02-10 at 2.58.55 PM.png]]

From Original HRM Paper:
![[Screenshot 2026-02-10 at 2.30.55 PM.png]]
# Confusions
## For each cycle, how $z_H$ is updated? 