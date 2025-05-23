
Before diving into fairness definitions in machine learning, it is important to describe the type of discrimination provided in political philosophy and in the legal domain. In these domains, discrimination or unfairness is mainly defined into two categories: *disparate impact* and *disparate treatment*.  

## Disparate Treatment vs. Disparate Impact

**Disparate Treatment** is defined as intentionally treating someone differently based on his/her membership in a protected class (direct discrimination). While **Disparate Impact** occurs when a decision-making process negatively affects members of a protected class more than others even if by a seemingly neutral policy (indirect discrimination)

<center>
<figure id="fig:disparate_treatment">
<img src="https://www.linkpicture.com/q/Disparate-Treatment-3.png" style="width:520px; background-color:#FFF " />
<figcaption>Disparate Treatment vs Disparate Impact <a href="https://www.qualtrics.com/experience-management/employee/disparate-treatment/">[Source]</a></figcaption>
</figure>
</center>



Examples of decision-making processes with disparate treatment and Disparate Treatment [Source](https://www.qualtrics.com/experience-management/employee/disparate-treatment/)

| Types of Discrimination | Disparate Treatment                                                                                                                                                                                                                                    | Disparate Impact                                                                                                                                                 |
|:-----------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|           Age           | Laying off employees over the age of 40 in favor of retaining younger employees                                                                                                                                                                        | Ninety percent of the sales agents subjected to the hiring freeze initiative were 40 years of age or older                                                       |
|           Sex           | Refusal to accommodate pregnancy-related lifting restriction for one employee. At the same time, accommodating the restrictions of other non-pregnant employees who were injured on the job and who were similar in their ability or inability to work | Conducting strength testing as a requirement for workers to be hired for various jobs, causing an unlawful discriminatory impact on female workers seeking jobs. |
|          Race           | Employees are subject to a hostile work environment and different treatment based on their race/nationality                                                                                                                                            | A broad criminal background check that negatively impacts a particular racial group, even though it is not a business necessity                                  |



## Fairness Metrics in Machine Learning

There are two main groups of fairness metrics: individual fairness and group fairness metric. Individual fairness looks at fairness at the individual level, while group fairness tries to equalize a given metric across different demographic groups. There are also some fairness notion that do not require group information, such as the Rawlsian Max-Min fairness notion

- **Individual fairness** says similar individuals should be treated similarly. For example, two applicants with the same ability to repay a loan should receive the same decision.
**Prerequisite:** task-specific distance metric, $m(v_1, v_2)$;  decision distribution metric, $m'(v_1, v_2)$. 
**Definition of Fairness:** $\forall v_1, v_2, m'(d(v_1), d(v_2)) \leq m(v_1, v_2)$ 
The main shortcoming of this metric is its assumption of the existence of a task-specific metric. In practice, this metric can be hard to define. Some lines of work trying to learn such metrics from data. 

#### Group fairness

**Prerequisite:** sensitive attributes or group membership (e.g. race)

-  Statistical parity 