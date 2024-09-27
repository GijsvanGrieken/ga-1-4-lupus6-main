# Report for Group Assignment 1.4

*[CEGM1000 MUDE](http://mude.citg.tudelft.nl/): Week 1.4, Friday, Sep 27, 2024.*

Remember there are "Tips for Writing the Report" in the [GA 1.3 README](https://mude.citg.tudelft.nl/2024/files/GA_1_3/README.html).

## Questions

**Question 1**

Give a short explanation about the model in the assignment. How is it different from the last week's assignment? What is the reason to try a new model?

_We copy the LaTeX equation for the model here, in case you would like to refer to it in your Report._

$$
d = d_0 + R \ (1-\exp\left(\frac{-t}{a}\right)) + k \ \textrm{GW},
$$

_Write your answer here._

In the model of the assignment of last week a linear model was used which used linear velocity and dependency on the groundwater level. The model from this week is a non-linear one, because we also want to take into account the compaction of the upper soil layers, which is a non-linear process. The reason to try a new model is that with taking into account the compaction of the soil layers as well we can try to get a better model, that is closer to the observations. 

**Question 2**

Report the Gauss-Newton interation convergence criteria, describe how quickly convergence was realized. Also comment on the quality of the estimation with InSAR and GNSS. Give your interpretation for any discrepancy between observations and the model.

Include a Markdown table that summarizes the estimated parameters and their precision for both models.

_Write your answer here._

In the Gauss-Newton iteration, we check if the update to the parameters is small enough to stop the process. If the update becomes smaller than a set limit (like 1e−12), we say the process has converged. In this task, how fast the iteration converges depends on things like how non-linear the model is, how good the starting guesses are, and how well we calculate the Jacobian matrix. As the iteration goes on, the changes in the parameters should get smaller until we reach the limit.

**convergence speed**:
- In this case, the iteration took 7 steps for the InSar data and 10 steps for the GNSS data. This means that the estimated initial parameters are pretty close to the actual parameters. 

**quality of the estimation with InSAR and GNSS**:
- InSar:usually fits well with the model,gives a good representation of ground displacement patterns.Convergence speed is fast,and the parameters tend to be stable after several iterations.
- GNSS:Compared to InSAR, although the fit quality is equally good,the GNSS model converges a bit slower.Most parameters stabilize around 8 iterations.

**Differences between module**:
- InSar fits better maybe because of its high resolution.It allows the model to capture small ground displacement changes over time.
- GNSS does not fit as well as InSar,especially in capturing smaller displacement changes.

**Differences in precision:**
- Insar generally has a better precision compared to GNSS, as can be seen in the tables below. Most values of the precision are factor 2 smaller for each parameter. This means that the InSar model has less errors, which can also be seen from the graphs, as the scatter is lower. 

**Markdown table: Estimated parameters and their precision** 

InSar:

| Parameters | d | R | a | k |
| :--: | :--: | :--: | :--: | :--: |
| Estimation |  12.97 | -21.92  | 179.35  |  0.17 |
| Precision  |  2.18 | 1.01  | 21.12  | 0.02  |

GNSS: 

| Parameters | d | R | a | k |
| :--: | :--: | :--: | :--: | :--: |
| Estimation |  3.95 | -18.15  | 224.10  |  0.14 |
| Precision  |  4.80 | 2.16  | 79.48  | 0.04  |

**Question 3**

Give an explanation of test statistic used to test which model (linear, non-linear) fits data better. What is the null hypothesis $H_0$ and alternative hypothesis $H_a$ in this test? What is the distribution of test statistic? Compare the test outcomes with InSAR and GNSS and interpret the results.

To compare which model fits the data better we used test statistic of the squared norm of residuals for both datasets. We defined the linear model of last weeks assignment as the null hypothesis $H_0$ and defined the non-linear model of this week assignment as the alternative hypothesis $H_a$. The distribution of the test statistic is the chi-square distribution. Using the chi-square distribution we determined the threshold value k for alpha = 0.005. From this followed that the threshold k equals 7.879. In the table below the test statistics for the InSAR data and the GNSS data are displayed. As the value for the test statistic for the InSAR data is higher than the threshold value the null hypothesis is rejected. For the GNSS data test statistic is (slightly) lower than the threshold k and thus the null hypothesis is accepted and the alternative hypothesis is preferred.

| Dataset | Test Statistic | Null Hypothesis $H_0$ accepted/rejected |
| :---: | :---: | :----- |
| InSAR | 95.616 | $H_0$ rejected, $H_a$ accepted |
| GNSS | 7.788 | $H_0$ accepted |

**Question 4**
In order to get a better fit to the data (smaller residuals) for this case study, consider the following strategies and determine whether or not each one could help. Use the Markdown table provided to state "Yes" or "No", then elaborate on your answer with one or two sentences each in the last column.

1. better observations?
2. a more complicated geophysical model?
3. better initial values?
4. more observations?
5. combining observations?

In your answer, keep in mind that data acquisition and processing comes with a price. Note that in a real situation you would not look at a time series of only one point. For Sentinel-1 data you may have to pay, collecting GNSS data at different locations also costs money. How will you monitor the deformation if you have both GNSS and InSAR data at your disposal?

_Fill in your answer in this table:_

| No. | Answer | Elaboration |
| :---: | :---: | :----- |
| 1 | yes | InSAR and GNSS observations are different in the sense that their spread (standard deviation) is different: smaller for INSAR and larger for GNSS. If 'better observation' can be interpreted as having a better precision, thus a smaller standard deviation, we can actually see that that matters in order to have a better fit because the standard deviation of the observations propagate less in the model for InSAR.
| 2 | yes | In this GA we used a model with 4 unknown parameters, while last week we had a model with 3 parameters. The model of this week is thus more complicated. Side note: considering more parameters (e.g., rainfall, soil parameters, etc...) can make the model fit better, but could lead to an overcomplicated model.|
| 3 | no | We already had good initial values for this case study and the maximum number of observations are not exceeded. |
| 4 | yes | If we had infinite number of observation the random error would tend to 0, so in theory yes. More observation lead to more costs anyway, so a balance has to be found. |
| 5 | no | For this case study the two measurement techniques are treated separately. Combining information influences the covariances, but we did not analyze much the covariances in this case study. |

**Last Question: How did things go? (Optional)**

This assignment went overall quite well. All group members were present and we were able to divide the tasks nicely. For this assignment we again used the Live Share function of VS Code. This time we made sure that two members were not typing in the same cell simultaneously and therefore we did not run in to any issues with the Live Sharing function. We struggled the most with Task 2.1 were the formula for the Gauss-Newton iteration was defined. 

**End of file.**

<span style="font-size: 75%">
&copy; Copyright 2024 <a rel="MUDE" href="http://mude.citg.tudelft.nl/">MUDE</a>, TU Delft. This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">CC BY 4.0 License</a>.