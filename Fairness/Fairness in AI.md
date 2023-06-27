***
Fairness can be defined as the absence of any prejudice or favoritism towards an individual or a group of individuals based on their inherent acquired characteristics such as  race, gender, religion, etc.

There are numerous [real-world examples of AI application](Real-world%20examples%20of%20AI%20unfairness.md)  showing that AI models can unintentionally learn  and perpetuate historical bias in the data. Bias in AI systems can be from various [sources of bias](Source%20of%20bias%20in%20AI.md) in AI, generally created by the data distribution, algorithmic, user interactions etc. 

>Bias is a disproportionate weight in favor of or against an idea or thing, usually in a way that is closed-minded, prejudicial, or unfair. Biases can be innate or learned

Initial efforts in fairness-aware AI focused on mathematically defining and quantifying unfairness in AI systems. In this regard, many [fairness definitions](./Fairness%20Definitions.md) have been proposed. These metrics are categorized into group fairness and individual fairness. Group fairness metrics aim to equalize various model's performances across different demographic groups, such equalize accuracies, true positive rates,   etc. For the individual fairness metric, the goal is to ensure that users that are similar w.r.t to a particular task must receive the same outcome by the model. More broadly, fairness notions can vary in different fields of machine learning such as [reinforcement learning], [recommendation systems], [ranking systems], [clustering], [generative models], etc.

Various [algorithms](Fairness%20Enhancing%20Methods.md) have been proposed to enforce fairness in machine learning. These algorithms are categorized into three main categories: [in-processing techniques] used when we have access to the model during the training. The loss function is generally modified to add constraints to enforce a given fairness definition. [post-processing techniques] are used when we have access to a trained model, and fairness is achieved by modifying the model's output. [pre-processing techniques]. 

