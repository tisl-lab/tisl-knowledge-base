Fairness-enhancing methods are grouped into three main categories based on the stage  of the pipeline where the fairness constraint is enforced, i.e., at the data level or before training the model ([pre-processing techniques](./Fairness%20algorithms/Pre-processing%20techniques.md)). during the model training ([in-processing techniques](./Fairness%20algorithms/In-processing%20techniques.md)), or after training the model ([post-processing techniques](./Fairness%20algorithms/Post-processing%20techniques.md)).

These groups of methods have their own advantages and disadvantages. Pre-processing methods can work with any type of classifier and machine learning tasks. As the fairness intervention is done at the data level,  the downstream task can be of any type, however, it becomes difficult to control the [tradeoffs]() and  the algorithmic bias that might arise in the downstream task is not controlled. 

Similarly to pre-processing techniques, post-processing methods can be applied to any type of model (classifier), which is treated like a black box. The output of the model is modified in order to satisfy a given fairness metric. However, changing the model's output comes at a significant cost of accuracy. Moreover, these methods can yield unfair outcomes against certain individuals as the model output is changed to satisfy a certain fairness metric. 

In-processing methods allow control over the fairness-accuracy tradeoff that the model can achieve. Having access to the optimization problem with fairness constraints provides more flexibility in the tradeoffs, however, there is little flexibility over the type of models used, i.e., the constraint optimization is s specific model. 

## State-of-the-art techniques

| Methods                      | Pre-process | In-process | Post-process | Implementation                                                                                                                                                     |
| ---------------------------- |:-----------:|:----------:|:------------:| ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Threshold Optimizer          |   $\circ$   |  $\circ$   |  $\bullet$   | [ThresholdOptimizer](https://fairlearn.org/v0.8/api_reference/fairlearn.postprocessing.html)                                                                       |
| Exponentiated Gradient       |   $\circ$   | $\bullet$  |   $\circ$    | [ExponentiatedGradient](https://fairlearn.org/v0.8/api_reference/fairlearn.postprocessing.html)                                                                    |
| Learning fair representation |  $\bullet$  |  $\circ$   |   $\circ$    | [LFR](https://aif360.readthedocs.io/en/latest/modules/generated/aif360.algorithms.preprocessing.LFR.html)                                                          |
| Adversarial debaising        |   $\circ$   | $\bullet$  |   $\circ$    | [AdversarialFairnessClassifier](https://fairlearn.org/v0.8/api_reference/fairlearn.adversarial.html)                                                               |
| Calibrated fairness          |   $\circ$   |  $\circ$   |  $\bullet$   | [CalibratedPostprocessing](https://aif360.readthedocs.io/en/latest/modules/generated/aif360.algorithms.postprocessing.CalibratedEqOddsPostprocessing.html)         |
| Fair Batch                   |   $\circ$   | $\bullet$  |   $\circ$    | [FairBatch]({https://github.com/yuji-roh/fairbatch)                                                                                                                |
| Reweighing                   |  $\bullet$  |  $\circ$   |   $\circ$    | [Reweighing](https://aif360.readthedocs.io/en/latest/modules/generated/aif360.algorithms.preprocessing.Reweighing.html#aif360.algorithms.preprocessing.Reweighing) |
| Prejudice Remover            |   $\circ$   | $\bullet$  |   $\circ$    | [PrejudiceRemover](https://aif360.readthedocs.io/en/latest/modules/algorithms.html#aif360-algorithms-inprocessing)                                                 |



Overall, there is no consensus in the literature about which group of methods performs best. Friedler, Sorelle A., et al. [performed](https://dl.acm.org/doi/pdf/10.1145/3287560.3287589) an empirical study where they compare different fairness-enhancing algorithms from different categories. They showed that none of the methods consistently outperform others, and their performances depend on the fairness metric and datasets. Most of the techniques above are used for classification tasks, other specific techniques and definitions applies for [[Fairness Beyond Classification]], such in NLP, Computer Vision, Generative models, etc
 
