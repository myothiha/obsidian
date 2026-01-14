
![[Screenshot 2025-11-26 at 2.24.05 PM.png]]
# Issues of HRM
- There's no guarantee that a fixed-point is reached. HRM is not iterating to the fixed point but simply doing forward passes of $f_L$ and $f_H$. HRM is only doing 4 recursions before stopping to apply the one-step approximation.
- Two forward pass for Q-Learning

Symbols used
- n - the number of time that latent reasoning z is recursively updated. 
- T - the number of full recursive blocks (each time solution y is updated.)
# Training
- Train separately for each task.
- There's no scale law yet.
- Only one Forward pass for Q-head, compute only for Q_halt eliminating second forward pass.
- There are two recursions: latent recursion and deep recursion.
- Latent Recursive process (No Gradient updates.)
	- Given x, current y and current z, the model recursively improve z. (run n times)
	- Given current z and previous y, the model propose a new solution y (or stay at current solution if it's already good.)
	- Input: x, y, z, n
	- Output:final value of y, z
- Deep Recursion Process
	- Run Latent Recursion T times. (No gradient)
	- After that, run latent recursion one more time with gradient.
	- Return final y, z, output_head(y) and Q_head(y)
- Deep Supervision
	- $\hat{y} = output\_head(y)$ and $\hat{q} = Q\_head(y)$ 
	- Find loss(y_hat, y_true) and loss(q_hat, (y_hat == y_true))
	- Run back propagation for the last recursion.
- Having previous reasoning z and previous solution y, help model to remember previous solution and how it reach that solution (reasoning) and improve both of them.
- Update z, n times and update y, T times.

# Pseudo Code

![[Screenshot 2025-11-26 at 2.00.31 PM.png]]
# Architecture
1. Input x
2. Solution y (H-module from HRM)
3. Latent reasoning z (L-Module from HRM)
4. Output Head
5. Q-Head

# Issues
 - Require Task specific training.
	 - No zero shot
	 - No transfer learning.
	 - Only work in In-Domain Distribution.
- Not for generation task or creative tasks.
	- It only generate deterministic answers. 
	- Therefore, right now only suitable for classification like tasks.


Research Direction
- We can try it on classification tasks without using LLM. it can be a more effective classifier than LLM-based one.
- Make it work for text generation.
- We can compress LLM size using that architecture without losing the efficiency. 
- Integration into Multi-modal reasoning (for example image and text.)

Business application
- Intent Classification for E-commerce: query -> product classification. 

# Other researches follows

## Think Visually Reason Textually
- 