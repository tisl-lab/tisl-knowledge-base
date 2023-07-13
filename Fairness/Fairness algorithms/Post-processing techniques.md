Fairness-enhancing post-processing techniques involve methods that treat the model as a [black box]() and enforce fairness constraints over the model's output. 

Most existing post-processing methods consist of post hoc modification of the model's outputs in order to satisfy a given fairness metric. In particular, Hardt et al. [formalized](https://proceedings.neurips.cc/paper/2016/hash/9d2682367c3935defcb1f9e247a97c0d-Abstract.html)   an optimization problem over the model's output ($\widehat{Y}$) to find  to derive a classifier ($\widetilde{Y}$) that satisfies the fairness constraint while minimizing the classification loss.  The optimization problem is defined as follows:
$$
\begin{array}{cl}
\min _p & \mathbb{E} \ell\left(\widetilde{Y}_p, Y\right) \\
\text { s.t. } & \gamma_0\left(\widetilde{Y}_p\right)=\gamma_1\left(\widetilde{Y}_p\right) \\
& \forall_{y, a} 0 \leqslant p_{y a} \leqslant 1
\end{array}
$$
Where $\gamma_a$ represents the *true positive rate* and/or the *false positive rate* of the demographic group $a$.  The derived classifier $\widetilde{Y}_p$ depends on four parameters $p=(p_{00}, p_{01}, p_{10}, p_{11})$ with $p_{ya}=P(\widetilde{Y} =1|\widehat{Y}=y, A=a)$. Thus, the optimization problem is a linear optimization 

When the model output is continuous (a score function) the derived classifier is based on a threshold of each demographic group such that it maximizes the classification loss while satisfying fairness constraints, i.e., equal opportunity and equalized odds. Similar methods are proposed in the literature, and they differ mainly in the way the optimization problem is defined. 