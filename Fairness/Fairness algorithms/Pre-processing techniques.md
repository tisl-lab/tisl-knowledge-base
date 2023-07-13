Pre-processing techniques are used to remove the influence of the sensitive attributes from the data that could lead to discrimination or unfair results. One advantage of these techniques is that they are model-agnostic. The new representation or dataset can then be used for downstream tasks (classical ML models) without any change in order to provide more "fair" outcomes. Approaches to mitigate biases at the data level fall into three main categories: 
1. Learn a fair representation of the data by obfuscating information about the sensitive attribute in the latent space.  
2. Modify the training data by relabeling or reweighing data points. 
3. Find a distribution close to the empirical distribution of the dataset subject to fairness constraints

#### Fair Representation Learning

In *fair representation learning*, the objective is to learn a function that maps the input data into a new space that is free from bias, i.e., a space that does not encode any information about the sensitive attribute, while maintaining other information as much as possible. 

[Zemel et al.](http://proceedings.mlr.press/v28/zemel13) were the first to propose learning fair intermediate representations: similar to $k$-means, their method involves finding $k$~prototypes in the same space as the input data. 
Each sample is assigned to the closest prototype while adding a constraint in the optimization objective to satisfy fairness and classification performance, i.e., obfuscate sensitive attributes while maintaining other information as much as possible. Obfuscating the sensitive attributes in the new representation enforces the independence of the representation with respect to the sensitive attributes so that *statistical parity* is achieved in the downstream tasks that use this representation. However, this approach comes with  a cost in accuracy. 

#### Adversarial-based approaches
  Several approaches for learning fair representation are based on adversarial learning. These approaches generally involve three components: 
  - An **encoder** (generator) that takes the input data and yields the latent space; 
  - An **adversary**, trained to predict the sensitive attributes from the latent space; 
  - A **classifier**, trained to maximize the utility of the latent representation with respect to the class label. 
  - Eventually, there is also a decoder, that reconstructs the input data from the data. The purpose of the decoder is to preserve information independent of the sensitive attribute as much as possible.  
  During the adversarial training, the goal of the generator and the classifier is to fool the adversary in predicting the sensitive attribute from the latent space while the adversary tries to maximize its accuracy of predictions. 

#### Modifying the dataset

There are three main approaches to modifying the dataset to remove bias, i.e., massaging, reweighing, and sampling. These methods are proposed by Kamiran et al [ref](https://ieeexplore.ieee.org/abstract/document/4909197/)   

- Massaging
   In the technique of "massaging," a few samples from the protected group have their class labels altered from negative to positive, while conversely, some samples from the non-protected group have their labels changed from positive to negative. It is crucial to carefully select the samples for flipping to reduce discrimination (in terms of statistical parity) while maintaining the overall class distribution intact.  
   In this regard, Kamiran et a. [proposed](https://link.springer.com/article/10.1007/s10115-011-0463-8) to relabel the samples close to the decision boundary. The intuition is that relabelling samples close to the decision boundary will not least impact the overall accuracy of the model. The samples to be relabeled are obtained from a ranking function that is trained on a training data set. The ranking learns the probability that a given sample belongs to the positive class and sorts all the data points in descending order for samples from the protected group having the negative label, and in ascending order for samples from the non-protected group having a positive label. The top $M$ elements from both ranked lists are relabeled. The value $M$ is carefully chosen so that the data set is discrimination-free with as least change as possible 
- Reweighing 
   In reweighing, instead of relabelling the data samples, each data point $x_i$ is associated with a weight $w_i$. To reduce the discrimination, higher weights are given to data point from groups $A_1^1$ and $A_0^0$, where  $A_a^y =\{ X | A=a, Y=y\}$ represents samples from the group $a$ with the class label $y$. And lower weights are given to samples from the groups $A_1^0$ and $A_0^1$. Intuitively, weights are assigned such that samples from the disadvantaged group receives greater weights to compensate for the bias. When the dataset is unbiased,  the expected probability of observing a particular value of $A$ and $Y$ is given by $P_{\operatorname{exp}}(A=a \wedge Y=y) = P(A=a) \times P(Y=y)$ i.e., $A$ and $Y$ are statistically independent. However, the observed probability ($P_{\operatorname{obs}}$) can be different when in the dataset some groups are disadvantaged.
   $$P_{\operatorname{exp}}(A=a \wedge Y=y) = \frac{|A=a|}{N} \times \frac{|Y=y|}{N}$$

   $$P_{\operatorname{obs}}(A=a \wedge Y=y) = \frac{|A=a \wedge Y=y|}{N}$$
   The weight of each sample $x_i$ is computed using the expected probability divided by the observed probability, i.e., 
   $$w_i = \frac{P_{\operatorname{exp}}(A=a_i \wedge Y = y_i)}{P_{\operatorname{obs}}(A=a_i \wedge Y = y_i)}$$

   In this way, a discrimination-free downstream task can be trained using the new dataset with the weights associated with each sample.

- Sampling:
  To remove bias using sampling, examples from some groups are over-sampled or under-sampled. This can be done by generating synthetic data points to restore group balance or by (under)over-sampling data points based on weights computed similarly to the reweighing techniques presented above. The latter is particularly useful when the model used does not consider sample weights during the training. As shown by [Kamiran et al](https://ieeexplore.ieee.org/abstract/document/4909197/), to remove discrimination, samples with weights lower than one are under-sampled while samples with weights greater than one are over-sampled