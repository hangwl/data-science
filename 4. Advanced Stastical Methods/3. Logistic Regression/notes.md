
logistic regression predicts the probability of an event occurring
$$p(X) = \frac{e^{(\beta_{0}+\beta_{1}x_{1}+...+\beta_{k}x_{k})}}{1+e^{(\beta_{0}+\beta_{1}x_{1}+...+\beta_{k}x_{k})}}$$

logit (log-odds) function - see <https://en.wikipedia.org/wiki/Logit>
$$log(\frac{p(X)}{1-p(X)}) = \beta_{0}+\beta_{1}x_{1}+...+\beta_{k}x_{k}$$

Logistic Regression Assumptions:
1. Nonlinear by definition
2. No endogeneity
3. Normality and Homoskedasticity
4. No autocorrelation
5. No multicollinearity

Interpreting Regression Summary:
- MLE (Maximum Likelihood Estimate) - method that tries to maximize the (log) likelihood function (that estimates how likely it is that the model at hand describes the real underlying relationship of the variables)
- log-likelihood - more popular metric (almost always negative, bigger = better)
- LL-Null (log-likelihood-null) - log-likelihood of a model which has no independent variables (compare with log-likelihood of model to see if it has any explanatory power)
- LLR (log-likelihood ratio) p-value - measures if model is statistically different from LL-null aka a useless model
- Pseudo R-squared - no clearly defined R2 for logistic regression | McFadden's R2 is good between 0.2 - 0.4, mostly useful to compare variations of same model

What do the Odds actually mean?
$$log(\frac{\pi}{1-\pi})=-69.91+0.042*SAT$$
$$log(\frac{odds_{2}}{odds_{1}})=0.042(SAT_{2}-SAT_{1})$$
i.e. when SAT score increases by 1, odds of admittance increases by 4.2%

Likewise, use dummy variables for binary predictors e.g. Gender

Confusion Matrix describes accuracy of binary predictions

Overfitting - an overtrained model misses the point of making predictions\
Underfitting - model does not capture underlying logic of data

