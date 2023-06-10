
### [In-processing techniques](./Fairness%20algorithms/In-processing%20techniques.md) 
In-processing techniques are used when we have access to the model training. In a nutshell, the loss function is transformed to add a loss/regularization term that penalizes the model's disparities across groups. Therefore, the model is forced to optimize for accuracy and fairness. 

Regularization is a technique used in ML to prevent the model from overfitting on the training, by penalizing the model's weights using $L_1$ or $L_2$ norms. 

The classification problem becomes a constrained optimization problem where the goal is to minimize the classification error (maximize the accuracy) while satisfying a given fairness constraint:
 
<a id="eq_fair_constraint"></a>$$ 
    \min_{h \in \mathcal{H}} \text{err}(h) \; \: \text{subject to}  \; \: \Delta(h) \leq c
$$

Where $h\in\mathcal{H}$ is a set of possible models, and $\Delta(h)$ measures the disparities in the model, fairness. However, this optimization problem is nonconvex and difficult to enforce. Therefore, existing in-processing techniques are reformulated in different ways or dual problems are solved. They can be grouped as follows:

- Reduction approach 
  
  [The Exponential Gradient](https://arxiv.org/pdf/1803.02453.pdf) approach for fairness transforms any binary classification problem into a cost-sensitive classification problem, that can yield a randomized classifier having the lowest error while satisfying fairness constraints. This approach can work with any baseline classifier (Logistic Regression, Random Forest, SVM, etc) and most fairness metrics. 
  The constrained problem in the above [equation](#eq_fair_constraint) is rewritten into a saddle point problem using a Lagrangian. The new problem is solved by the Exponential Gradient  method that looks for the saddle point where the classification loss is minimized and fairness is maximized (the disparities are minimal). The Exp gradient thus solves the following problem. 
  $$
L(Q, \lambda)=\widehat{\text{err}}(Q)+\lambda^{\top}(\mathbf{M} \widehat{\mu}(Q)-\widehat{\mathbf{c}})
$$
$$
\min _{Q \in \Delta} \max _{\lambda \in \mathbb{R}_{+}^{|\mathcal{K}|}} L(Q, \lambda) .
$$
  where  $\widehat{\text{err}}(Q)$ is the empirical classification error of a randomized classifier, $\lambda_k$ is the Lagrange multiplier of each constraint, $\mathbf{M} \widehat{\mu}(Q)$ a matrix where each row represents a fairness constraint.  Please note that the variable $\hat{c}$ represents the allowable error in the fairness constraints. When $\hat{c}=0$, it signifies maximum fairness with zero disparities. This approach is particularly intriguing because it provides the ability to manage the balance between fairness and accuracy, allowing for tradeoffs to be controlled effectively.
   
  An open-source implementation is available on the Fairlearn package. [Source code](https://fairlearn.org/v0.5.0/api_reference/fairlearn.reductions.html)
  
- Adversarial-based approach
  
  [Adversarial learning](https://dl.acm.org/doi/abs/10.1145/1081870.1081950?casa_token=-fstSfXI7LEAAAAA:QbYE6sImT_eM1ZSOtF27tcnu2KYp4E9WNLXnDYC1Iaec7DUvuTojZYGLMbCfVgh15T-xgD6SuBNVkzA) is a group of approaches that are inspired by the zero-sum game problem in game theory. In contrast to classical learning problems, the goal of adversarial learning is to craft *bad samples* or mislead a model. 
  Adversarial learning, originally developed for enhancing the security of neural network models against adversarial attacks, has found applications in various domains. Apart from its initial purpose, it has also been utilized in diverse areas, including [generative models](https://arxiv.org/abs/1406.2661) and promoting fairness. A popular application of adversarial learning to enforce  fairness  constraints to a model is adversarial debiasing.  
  
  [Adversarial debiasing](https://dl.acm.org/doi/abs/10.1145/3278721.3278779) is an adversarial-based approach that enforces the independence between the classifier outcome and the sensitive attributes, i.e., $\hat{Y} \perp A$. Where $A$ is the sensitive attribute .
  
  ![[avd_debaising.png]]
  
  The classifier's output is used as input for the adversary network that tries to predict the sensitive attribute. In the minimax optimization problem, the goal of the classifier is to prevent the adversary to predict the sensitive attribute, thus enforcing [statistical parity](../Fairness%20Definitions.md), i.e., $\hat{Y} \perp A$
  
  To enforce [Equalized Odds](../Fairness%20Definitions.md), the adversary takes  as input the predicted outcome and ground truth. Thus fooling the adversary enforces $\hat{Y},{Y} \perp A$  
 To enforce [Equal Opportunity](../Fairness%20Definitions.md), the adversary gets the classifier outputs of samples where $Y=1$. 
 
 [Open source code](https://fairlearn.org/main/user_guide/mitigation/adversarial.html)
 
 Similarly, [censoring representation](https://arxiv.org/pdf/1511.05897.pdf) uses an adversarial approach where instead of the classifier output, the adversary gets the latent representation of the input data to predict the sensitive attribute. In addition to the adversary, two other network heads are used: the reconstruction head used to reconstruct the input from the latent code, and the classifier head used to predict the class label. In this approach the loss function is a triple loss:
			 
			 $$
		L = \alpha C(X, Z) + \beta D(S, Z) + \gamma E(Y, Z) 
		$$
	Where:
	- $E(Y, Z)$ is the classifier loss, typically a cross-entropy loss.
	- $D(S, Z)$ is the discriminator loss, also a cross-entropy loss.
	- $C(X, Z)$ is the reconstruction loss defined as mean squared error loss. 
	$\alpha, \beta$ and  $\gamma$ control each loss.  The advantage of this approach is that the latent representation can be used for a different downstream, therefore this approach can also be seen as a preprocessing technique. 
 
 - FairBatch 
   
   [FairBatch](https://arxiv.org/abs/2012.01696) is a batch selection process that enforces a given fairness metric by sampling minibatches  in a way to transform the Empirical Risk Minimization problem into a weighted EMR, i.e., incorporate fairness constraints. In a nutshell, FairBatch modifies the ratio of demographic groups in the minibatch by increasing the representation of the group of the samples mostly misclassified in the previous batch.   A sampling strategy is defined for each fairness such as [statistical parity](../Fairness%20Definitions.md), [Equalized Odds](../Fairness%20Definitions.md), [Equal Opportunity](../Fairness%20Definitions.md).  The ratio of each group in the minibatch is computed based on the disparity measured by each fairness method. 
   
   Open-source implementation [Source code](https://github.com/yuji-roh/fairbatch)



### [Post-processing techniques](./Fairness%20algorithms/Post-processing%20techniques.md) 


### [Pre-processing techniques](./Fairness%20algorithms/Pre-processing%20techniques.md) 
