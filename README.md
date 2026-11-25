# econ5200-lab09-ab-testingDiagnosing Experimental Failures in A/B Testing

Objective

In this lab, I tested how coding errors, sample imbalances, interference, and repeated significance testing can lead to misleading A/B test results, and explored methods for making better experimental decisions.

Methodology

CUPED Variance Reduction: I identified and fixed three bugs in an analyst's CUPED code involving the adjustment coefficient, covariate centering, and standard error calculation. I compared the corrected treatment-effect estimate and standard error with the original results.

Sample Ratio Mismatch (SRM): I used chi-squared goodness-of-fit tests to examine treatment-control allocation imbalances in experiments with 100,000 and 20 million users.

SUTVA Violations: I simulated a marketplace with limited inventory where discounted buyers competed with control buyers. I compared treatment effects under no interference, individual randomization, and a full rollout.

Bayesian A/B Testing: I used Beta(1, 1) priors and Monte Carlo simulation to estimate the probability that treatment B was better than A and the expected loss of shipping B. I compared the Bayesian decision with a frequentist permutation test.

Bayesian Test Function: I wrote my own function to calculate posterior probabilities and expected losses, then applied it to an experiment with four times the original sample size.

Peeking and False Positives: I simulated repeated significance testing under a true null hypothesis to investigate how checking p-values throughout an experiment can create false positives.

Key Findings

CUPED: The analyst originally reported a 0.0% variance reduction because of errors in the code. After correcting all three bugs, I achieved an 82.7% variance reduction, with the standard error falling from 0.1539 to 0.0641. This showed how using pre-experiment data can substantially improve precision.

Sample Ratio Mismatch: In the experiment with 100,000 users, a 0.60 percentage-point imbalance produced a chi-squared statistic of 14.40. In the experiment with 20 million users, a much smaller imbalance of 0.05 percentage points produced a larger chi-squared statistic of 20.00. Both triggered SRM alarms, showing how large sample sizes can make even small allocation differences statistically significant.

Marketplace Interference: The naive A/B test estimated a treatment effect of 0.1861, while the global rollout effect was only 0.1428. The naive estimate overstated the global effect by 23.3% of the naive ATE. This happened because discounted buyers reduced inventory availability for control buyers, artificially widening the difference in purchase rates.

Bayesian A/B Testing: I found an 88.66% probability that Variant B was better than Variant A, with an expected loss of shipping B of 0.000473. However, the shipping rule said not to ship because the probability was below the required 95% threshold. The frequentist permutation test produced a p-value of 0.2302, which also failed to provide statistically significant evidence of a difference.

Longer Bayesian Experiment: When I applied my Bayesian function to an experiment with four times as many users, the probability that B was better increased to 99.51%. The expected loss decreased, and the shipping decision changed to shipping Variant B.

Peeking Problem: In one experiment where both groups had the same true conversion rate, the p-value crossed below 0.05 six times across 50 checks, even though the final p-value was 0.2761. This demonstrated how repeatedly checking significance can produce misleading results. Across 1,000 simulated experiments, the false-positive rates were [YOUR VALUE]% when peeking and [YOUR VALUE]% when testing only once at the end.

Conclusion

This lab showed me that statistically significant results do not always mean an experiment is reliable. Coding mistakes, allocation imbalances, interference between users, and repeated testing can all distort the conclusions of an A/B test. I also learned how CUPED and Bayesian decision rules can improve the precision and interpretation of experimental results.
