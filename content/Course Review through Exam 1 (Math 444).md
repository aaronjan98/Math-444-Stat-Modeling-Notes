# Course Review through Exam 1 (Math 444)

- **Purpose**
	- consolidated review of the material from the beginning of MATH 444 through the first exam
	- intended to give someone who missed earlier classes a single path through the ideas instead of requiring them to reconstruct the course from every dated note
	- condensed exam-focused version: [[Exam 1 Study Guide (Math 444)]]

1. **Statistical foundation from MATH 340**
	- Statistics uses sample data to learn about an underlying population.
	- Population quantities are **parameters**.
		- examples: population mean $\mu$, variance $\sigma^2$, regression coefficients $\beta_0,\beta_1$
	- Sample quantities are **statistics / estimators**.
		- examples: $\bar X$, $S^2$, $\hat\beta_0$, $\hat\beta_1$
	- A good estimator is judged by properties such as
		- unbiasedness: $\displaystyle E(\hat\theta)=\theta$
		- small variance
		- consistency as the sample size grows
	- Expectation
		- $\displaystyle E(aX+b)=aE(X)+b.$
	- Variance
		- $\displaystyle \operatorname{Var}(aX+b)=a^2\operatorname{Var}(X).$
		- for independent random variables, $\displaystyle \operatorname{Var}\left(\sum_i a_iX_i\right)=\sum_i a_i^2\operatorname{Var}(X_i)$
	- Normal and $t$ distributions provide the reference distributions used for regression inference.

1. **Hypothesis testing framework**
	- Start with a null and alternative hypothesis.
		- $H_0$ represents the baseline claim being tested.
		- $H_A$ represents the competing claim.
	- Choose a test statistic whose distribution is known under $H_0$.
	- Two equivalent decision approaches
		- rejection region
			- reject when the observed statistic is sufficiently extreme
		- $p$-value
			- reject when $p<\alpha$
	- A $p$-value is the probability, **assuming $H_0$ is true**, of seeing a result at least as extreme as the observed one.
	- Failing to reject $H_0$ is not the same thing as proving $H_0$ true.
	- Confidence intervals and two-sided hypothesis tests are directly connected.
		- a hypothesized value outside the $(1-\alpha)100\%$ confidence interval is rejected by the corresponding two-sided level-$\alpha$ test

1. **Why regression enters the course**
	- Instead of estimating one population mean, regression models how the expected response changes with another variable.
	- In simple linear regression there is one predictor $x$ and one response $Y$.
	- Population model
		- $\displaystyle Y_i=\beta_0+\beta_1x_i+\varepsilon_i.$
	- Mean structure
		- $\displaystyle E(Y_i\mid X_i=x_i)=\beta_0+\beta_1x_i.$
	- Randomness is carried by $\varepsilon_i$.
		- the regression line describes the systematic part
		- the error describes the remaining observation-to-observation variation

1. **Least-squares fitting**
	- For candidate coefficients $\beta_0,\beta_1$, the vertical error at observation $i$ is $y_i-(\beta_0+\beta_1x_i)$.
	- Least squares minimizes the total squared vertical error
		- $\displaystyle \sum_{i=1}^n(y_i-\beta_0-\beta_1x_i)^2.$
	- Solving the two normal equations gives
		- $\displaystyle \hat\beta_1=\frac{\sum(x_i-\bar x)(y_i-\bar y)}{\sum(x_i-\bar x)^2}=\frac{S_{xy}}{S_{xx}}.$
		- $\displaystyle \hat\beta_0=\bar y-\hat\beta_1\bar x.$
	- The fitted line therefore passes through $(\bar x,\bar y)$.
	- Fitted value: $\displaystyle \hat y_i=\hat\beta_0+\hat\beta_1x_i$.
	- Residual: $\displaystyle \hat e_i=y_i-\hat y_i$.
	- Least-squares geometry creates useful identities
		- $\displaystyle \sum\hat e_i=0.$
		- $\displaystyle \sum x_i\hat e_i=0.$

1. **Regression assumptions**
	- Linearity
		- the conditional mean of $Y$ is linear in $x$
	- Zero-mean errors: $\displaystyle E(\varepsilon_i)=0$.
	- Constant variance: $\displaystyle \operatorname{Var}(\varepsilon_i)=\sigma^2$.
	- Independence of errors.
	- Normality of errors when using the exact small-sample $t$ and $F$ inference developed in class
		- $\displaystyle \varepsilon_i\sim N(0,\sigma^2)$
	- These assumptions are what justify the sampling distributions used for confidence intervals and tests.

1. **Estimating the unknown error variance**
	- The errors $\varepsilon_i$ are unobservable, so use the residuals $\hat e_i$.
	- Residual sum of squares
		- $\displaystyle \operatorname{RSS}=\sum_{i=1}^n\hat e_i^2.$
	- Estimate of $\sigma^2$
		- $\displaystyle S^2=\frac{\operatorname{RSS}}{n-2}.$
	- Residual standard error: $\displaystyle S=\sqrt{S^2}$.
	- The denominator is $n-2$ because the data were used to estimate two regression coefficients.

1. **Properties of the slope estimator**
	- Define $\displaystyle c_i=\frac{x_i-\bar x}{S_{xx}}$.
	- Then $\displaystyle \hat\beta_1=\sum_{i=1}^nc_iY_i$.
	- Useful identities
		- $\displaystyle \sum c_i=0.$
		- $\displaystyle \sum c_i^2=\frac1{S_{xx}}.$
		- $\displaystyle \sum c_ix_i=1.$
	- Unbiasedness: $\displaystyle E(\hat\beta_1)=\beta_1$.
	- Variance: $\displaystyle \operatorname{Var}(\hat\beta_1)=\frac{\sigma^2}{S_{xx}}$.
	- Meaning of $S_{xx}$ in that variance
		- more spread in the predictor values gives more information about the slope
		- larger $S_{xx}$ therefore decreases the variance of $\hat\beta_1$

1. **Properties of the intercept estimator**
	- $\displaystyle \hat\beta_0=\bar Y-\hat\beta_1\bar x.$
	- Unbiasedness: $\displaystyle E(\hat\beta_0)=\beta_0$.
	- Variance
		- $\displaystyle \operatorname{Var}(\hat\beta_0)=\sigma^2\left(\frac1n+\frac{\bar x^2}{S_{xx}}\right).$
	- The intercept can be estimated imprecisely when $x=0$ lies far away from where the observed predictor values are concentrated.

1. **Inference for regression coefficients**
	- When the errors are normal
		- $\displaystyle \hat\beta_1\sim N\left(\beta_1,\frac{\sigma^2}{S_{xx}}\right).$
	- Since $\sigma$ is unknown, replace it by $S$.
		- $\displaystyle \frac{\hat\beta_1-\beta_1}{S/\sqrt{S_{xx}}}\sim t_{n-2}.$
	- Slope standard error: $\displaystyle \operatorname{SE}(\hat\beta_1)=\frac{S}{\sqrt{S_{xx}}}$.
	- Testing $H_0:\beta_1=\beta_{1,0}$
		- $\displaystyle t=\frac{\hat\beta_1-\beta_{1,0}}{S/\sqrt{S_{xx}}}.$
	- Confidence interval
		- $\displaystyle \hat\beta_1\pm t_{\alpha/2,n-2}\frac{S}{\sqrt{S_{xx}}}.$
	- The common test $H_0:\beta_1=0$ asks whether the data provide evidence of a nonzero linear relationship.

1. **Mean-response confidence intervals and prediction intervals**
	- At $x_0$, estimated mean response: $\displaystyle \hat y_0=\hat\beta_0+\hat\beta_1x_0$.
	- Confidence interval for the population **mean response** at $x_0$
		- $\displaystyle \hat y_0\pm t_{\alpha/2,n-2}S\sqrt{\frac1n+\frac{(x_0-\bar x)^2}{S_{xx}}}.$
	- Prediction interval for one **new observation** at $x_0$
		- $\displaystyle \hat y_0\pm t_{\alpha/2,n-2}S\sqrt{1+\frac1n+\frac{(x_0-\bar x)^2}{S_{xx}}}.$
	- The prediction interval is wider because it contains an additional $1$ under the square root.
		- that extra term represents the irreducible error of the future individual observation
	- Both intervals widen as $x_0$ moves away from $\bar x$.

1. **ANOVA decomposition**
	- Total variation: $\displaystyle \operatorname{SST}=\sum(y_i-\bar y)^2$.
	- Explained variation: $\displaystyle \operatorname{SSReg}=\sum(\hat y_i-\bar y)^2$.
	- Residual variation: $\displaystyle \operatorname{RSS}=\sum(y_i-\hat y_i)^2$.
	- Fundamental decomposition
		- $\displaystyle \operatorname{SST}=\operatorname{SSReg}+\operatorname{RSS}.$
	- Degrees of freedom
		- total: $n-1$
		- regression: $1$
		- residual: $n-2$
	- Mean squares
		- $\displaystyle \operatorname{MSReg}=\operatorname{SSReg}.$
		- $\displaystyle \operatorname{MSE}=\frac{\operatorname{RSS}}{n-2}=S^2.$
	- ANOVA test statistic
		- $\displaystyle F=\frac{\operatorname{MSReg}}{\operatorname{MSE}}.$
	- For simple linear regression, $\displaystyle F_{1,n-2}=t_{n-2}^2$.
		- the overall regression $F$ test is equivalent to the two-sided slope test of $H_0:\beta_1=0$
	- Professor emphasis
		- be able to reconstruct missing entries in an ANOVA table from the relationships among SS, df, MS, and $F$

1. **$R^2$ and correlation**
	- $\displaystyle R^2=\frac{\operatorname{SSReg}}{\operatorname{SST}}=1-\frac{\operatorname{RSS}}{\operatorname{SST}}.$
	- Interpretation
		- proportion of the observed variation in $Y$ explained by the fitted model
	- In simple linear regression, $R^2=r_{xy}^2$.
	- $R^2$ alone does not verify the regression assumptions.
		- a model can have a large $R^2$ and still have problematic residual structure

1. **Why diagnostics are necessary**
	- Regression inference assumes the chosen model is a reasonable description of the data.
	- Residuals expose structure that the fitted line does not explain.
	- A useful residual plot should look approximately like random noise around zero.
	- Common warning patterns
		- curvature
			- linear mean function is inadequate
		- increasing / decreasing spread
			- nonconstant error variance
		- isolated large residuals
			- possible response outliers
		- unusual predictor locations
			- possible high-leverage points

1. **Leverage**
	- Fitted values can be written as weighted combinations of the observed responses.
		- $\displaystyle \hat y_i=\sum_{j=1}^nh_{ij}y_j.$
	- The diagonal element $h_{ii}$ measures the leverage of observation $i$.
	- In simple linear regression
		- $\displaystyle h_{ii}=\frac1n+\frac{(x_i-\bar x)^2}{S_{xx}}.$
	- Meaning
		- observations with predictor values far from $\bar x$ have more ability to pull the fitted line toward themselves
	- Sum of leverages: $\displaystyle \sum h_{ii}=2$.
	- Practice-note flag: $\displaystyle h_{ii}>\frac4n$.
		- treat this as a flag for investigation rather than an automatic declaration that the observation is bad

1. **Residual size vs leverage vs influence**
	- Residual size asks
		- is the observed response unusual compared with what the fitted model predicts at this $x$?
	- Leverage asks
		- is this predictor value unusual compared with the other $x$ values?
	- Influence asks
		- does this observation materially change the fitted regression when included?
	- These are related but different properties.
		- a point can have high leverage but a small residual
		- a point can have a large residual but ordinary leverage
		- points with both high leverage and a large residual are especially capable of being influential

1. **Cook's distance**
	- Cook's distance measures how much the fitted regression changes when observation $i$ is removed.
	- Formula used in class
		- $\displaystyle D_i=\frac{r_i^2}{2}\frac{h_{ii}}{1-h_{ii}}.$
	- The formula captures the two ingredients of influence
		- residual size through $r_i^2$
		- leverage through $h_{ii}/(1-h_{ii})$

1. **Normality and constant-variance diagnostics**
	- Q-Q plot
		- checks whether the error distribution is approximately normal
		- roughly linear points support the normality assumption
	- Residual-vs-fitted / residual-vs-predictor plot
		- checks whether residual spread is roughly constant and whether systematic patterns remain
	- Professor guidance before Exam 1
		- do not focus on Box-Cox transformations
		- no dummy variables or material not covered

1. **How the major quantities connect**
	- Start with raw data $(x_i,y_i)$.
	- Compute $\bar x$, $\bar y$, $S_{xx}$, and $S_{xy}$.
	- Fit the line using $\hat\beta_1=S_{xy}/S_{xx}$ and $\hat\beta_0=\bar y-\hat\beta_1\bar x$.
	- Compute fitted values $\hat y_i$ and residuals $\hat e_i$.
	- Residuals give RSS.
	- RSS gives
		- $S^2=\operatorname{MSE}=\operatorname{RSS}/(n-2)$
		- coefficient standard errors
		- $t$ tests and confidence intervals
		- prediction uncertainty
	- SST and RSS give
		- $\operatorname{SSReg}=\operatorname{SST}-\operatorname{RSS}$
		- $R^2=1-\operatorname{RSS}/\operatorname{SST}$
		- the ANOVA table and $F$ statistic
	- Residuals plus predictor geometry give
		- diagnostics
		- leverage
		- influence

1. **Suggested study order for Exam 1**
	1. Re-derive the least-squares slope and intercept.
	1. Re-derive the key properties of $\hat\beta_1$.
	1. Practice slope hypothesis tests and confidence intervals from both raw quantities and regression output.
	1. Practice mean-response confidence intervals vs individual prediction intervals.
	1. Practice completing ANOVA tables and moving among SST, SSReg, RSS, MSE, $F$, and $R^2$.
	1. Practice explaining residual plots, leverage, standardized residuals, and Cook's distance conceptually.
	1. Re-read the final pre-exam class notes for any additional professor comments after the last class meeting.
