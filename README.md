# Influence and Contagion in Social Networks

## Introduction
In this work, we modeled a social network through matrices to answer two central questions: (i) who concentrates the most influence in the network and (ii) how an initial opinion propagates over time. The modeling was performed using the adjacency matrix $A$, the weight matrix $W$, and iterative updates of the influence and opinion vectors.

## 1. The Logic of Influence
The influence phase uses the iteration:

```math
\mathbf{v}_{k+1}=\frac{A^T\mathbf{v}_k}{\lVert A^T\mathbf{v}_k\rVert_2},
```

with $\mathbf{v}_0=\mathbf{1}$. This repeated multiplication represents, in the real world, the accumulated flow of attention: each user receives weight from those who point to them, and this weight also carries the importance of those who follow them.

Helena ended up as the Alpha Node because many edges lead to her and, furthermore, a significant portion of those pointing to her are also in central positions in the network. Therefore, she receives both direct and indirect influence, which raises her value in the stabilized vector.

## 2. The Weight of Conviction (Main Diagonal)
In the final experiment, we added stubbornness to the model using the main diagonal:

```math
A_{stubborn} = A +  \alpha I
```

and then normalized by row to obtain $W$. This means that each person also begins to consider their own opinion when calculating the weighted average.

In behavioral terms, the diagonal represents self-conviction: the person does not completely change their mind just by following other accounts. Mathematically, this self-influence reduces sharp drops, like Helena's, because part of the previous score remains in each step of the dynamics.

## 3. The Idol's Vulnerability (Experiment A)
The opinion dynamics follow:

```math
\mathbf{x}_{t+1}=W\mathbf{x}_t
```

When Helena starts following users with a low (or zero) initial opinion, her row in $W$ redistributes attention to these profiles. Thus, in the first step, her new opinion becomes the weighted average of these sources, which is low:

```math
x_H(t+1)=\sum_j W_{Hj}x_j(t) \approx 0
```

With the main initial source, which had a score of 10, weakened right at the start, the rest of the network stops receiving a strong signal, and the global contagion fails.

## 4. The Echo Chamber (Experiment B)
In experiment B, a feedback core forms between high-opinion profiles, Helena and Diego, with both starting with a score of 10. This arrangement creates a reinforcement loop: each one receives a relevant portion of the other's opinion mass, maintaining high values for longer.

In dynamical systems language, there is a subgraph with strong internal coupling, in which the opinion mass circulates and dissipates more slowly to the rest of the network. In real social networks, the risk is polarization: closed groups reinforce internal beliefs and reduce exposure to divergent information.

## 5. Structural Equivalence
For two people to have rigorously identical curves every day, the algorithm must apply exactly the same update rule to both. This occurs when:

1. the corresponding rows in $W$ are equal, with the same followed users and the same weights; and
2. the initial conditions of these two people are equal.

If these conditions hold, then for all $t$:

```math
x_i(t+1)=\sum_j W_{ij}x_j(t)=\sum_j W_{kj}x_j(t)=x_k(t+1)
```

therefore the trajectories coincide at every instant.

## Conclusion
The analysis shows that structural influence and opinion propagation are related but not identical concepts. A node can be extremely influential in terms of centrality and yet quickly lose its opinion in the averaging model if it lacks self-conviction or reciprocal support. The inclusion of the main diagonal makes the dynamics more realistic by representing individual resistance to abrupt changes.
