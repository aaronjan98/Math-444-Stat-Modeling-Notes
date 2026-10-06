# Exam 1 Study Guide (Math 444)

- **Exam:** Thursday, October 8, 2026
	- Main material developed in class so far is **simple linear regression**, inference for the regression coefficients, ANOVA / $R^2$, and regression diagnostics.
	- Professor explicitly said we should be able to **fill in an ANOVA table** from the information provided.
	- Professor explicitly said **not to focus on Box-Cox transformations** for this exam.
	- Professor also said there will be **no dummy variables or material we did not cover**.
	- Related full review: [[Course Review through Exam 1 (Math 444)]]

1. **Simple linear regression model**
	- Population model
		- $\displaystyle Y_i=\beta_0+\beta_1x_i+\varepsilon_i,\qquad i=1,\dots,n.$
	- Interpretation
		- $\beta_0$ = population intercept
			- expected value of $Y$ when $x=0$
		- $\beta_1$ = population slope
			- expected change in $Y$ for a one-unit increase in $x$
		- $\varepsilon_i$ = random error for observation $i$
	- Conditional mean
		- $\displaystyle E(Y_i\mid X_i=x_i)=\beta_0+\beta_1x_i.$
	- Fitted regression line
		- $\displaystyle \hat Y_i=\hat\beta_0+\hat\beta_1x_i.$
	- Residual
		- $\displaystyle \hat e_i=Y_i-\hat Y_i.$
		- residuals estimate the unobserved errors $\varepsilon_i$

1. **Least-squares estimation**
	- Choose $\hat\beta_0$ and $\hat\beta_1$ to minimize the residual sum of squares
		- $\displaystyle \operatorname{RSS}=\sum_{i=1}^n\left(y_i-\beta_0-\beta_1x_i\right)^2.$
	- Differentiate with respect to the two parameters and set both partial derivatives equal to $0$.
	- Least-squares slope
		- $\displaystyle \hat\beta_1=\frac{S_{xy}}{S_{xx}}=\frac{\sum_{i=1}^n(x_i-\bar x)(y_i-\bar y)}{\sum_{i=1}^n(x_i-\bar x)^2}.$
	- Least-squares intercept
		- $\displaystyle \hat\beta_0=\bar y-\hat\beta_1\bar x.$
	- Important centered sums
		- $\displaystyle S_{xx}=\sum_{i=1}^n(x_i-\bar x)^2.$
		- $\displaystyle S_{xy}=\sum_{i=1}^n(x_i-\bar x)(y_i-\bar y).$
	- Useful identities
		- $\displaystyle \sum_{i=1}^n(x_i-\bar x)=0.$
		- $\displaystyle \sum_{i=1}^n(y_i-\bar y)=0.$
		- $\displaystyle \sum_{i=1}^n\hat e_i=0.$
		- $\displaystyle \sum_{i=1}^nx_i\hat e_i=0.$
	- Click point
		- least squares chooses the line whose **squared vertical errors are as small as possible overall**
		- the resulting residuals balance around zero and are orthogonal to the predictor

1. **Assumptions for simple linear regression inference**
	- Linear model
		- $\displaystyle Y_i=\beta_0+\beta_1x_i+\varepsilon_i.$
	- Zero-mean errors
		- $\displaystyle E(\varepsilon_i)=0.$
	- Constant variance
		- $\displaystyle \operatorname{Var}(\varepsilon_i)=\sigma^2.$
	- Errors are independent.
	- For the exact $t$- and $F$-based inference used in class, errors are normally distributed
		- $\displaystyle \varepsilon_i\sim N(0,\sigma^2).$
	- Diagnostic plots are used later to check whether these assumptions look reasonable.

1. **Estimating the error variance**
	- Since $\sigma^2$ is unknown, estimate it from the residuals.
	- Residual mean square / error variance estimator
		- $\displaystyle S^2=\hat\sigma^2=\frac{\operatorname{RSS}}{n-2}=\frac{\sum_{i=1}^n\hat e_i^2}{n-2}.$
	- Residual standard error
		- $\displaystyle S=\sqrt{\frac{\operatorname{RSS}}{n-2}}.$
	- Why $n-2$?
		- two regression parameters, $\beta_0$ and $\beta_1$, were estimated from the data
		- residual degrees of freedom are therefore $n-2$

1. **Sampling distributions of the least-squares estimators**
	- Slope
		- $\displaystyle E(\hat\beta_1)=\beta_1.$
		- $\displaystyle \operatorname{Var}(\hat\beta_1)=\frac{\sigma^2}{S_{xx}}.$
		- $\displaystyle \hat\beta_1\sim N\left(\beta_1,\frac{\sigma^2}{S_{xx}}\right).$
	- Intercept
		- $\displaystyle E(\hat\beta_0)=\beta_0.$
		- $\displaystyle \operatorname{Var}(\hat\beta_0)=\sigma^2\left(\frac1n+\frac{\bar x^2}{S_{xx}}\right).$
		- $\displaystyle \hat\beta_0\sim N\left(\beta_0,\sigma^2\left(\frac1n+\frac{\bar x^2}{S_{xx}}\right)\right).$
	- Standard errors replace the unknown $\sigma$ with $S$.
		- $\displaystyle \operatorname{SE}(\hat\beta_1)=\frac{S}{\sqrt{S_{xx}}}.$
		- $\displaystyle \operatorname{SE}(\hat\beta_0)=S\sqrt{\frac1n+\frac{\bar x^2}{S_{xx}}}.$

1. **Hypothesis test for the slope**
	- General two-sided test
		- $\displaystyle H_0:\beta_1=\beta_{1,0}$
		- $\displaystyle H_A:\beta_1\neq\beta_{1,0}.$
	- Most common test for whether there is a linear relationship
		- $\displaystyle H_0:\beta_1=0$
		- $\displaystyle H_A:\beta_1\neq0.$
	- Test statistic
		- $\displaystyle t_{\mathrm{obs}}=\frac{\hat\beta_1-\beta_{1,0}}{S/\sqrt{S_{xx}}}.$
		- under $H_0$, compare it with a $t_{n-2}$ distribution
	- Decision rules
		- rejection-region approach
			- reject $H_0$ when $|t_{\mathrm{obs}}|>t_{\alpha/2,n-2}$
		- $p$-value approach
			- reject $H_0$ when $p<\alpha$
			- for a two-sided test, $\displaystyle p=2P\left(T_{n-2}>|t_{\mathrm{obs}}|\right)$
	- Interpretation
		- rejecting $H_0:\beta_1=0$ gives evidence that $x$ and $Y$ have a nonzero linear relationship
		- failing to reject does **not** prove the slope is exactly zero

1. **Confidence interval for the slope**
	- A $(1-\alpha)100\%$ confidence interval for $\beta_1$ is
		- $\displaystyle \hat\beta_1\pm t_{\alpha/2,n-2}\frac{S}{\sqrt{S_{xx}}}.$
	- Relationship with the hypothesis test
		- for a two-sided test at level $\alpha$, reject $H_0:\beta_1=\beta_{1,0}$ exactly when $\beta_{1,0}$ is outside the corresponding $(1-\alpha)100\%$ confidence interval

1. **Estimating the mean response vs predicting a new observation**
	- At a predictor value $x_0$, fitted mean response
		- $\displaystyle \hat y_0=\hat\beta_0+\hat\beta_1x_0.$
	- Standard error for the **mean response** at $x_0$
		- $\displaystyle S\sqrt{\frac1n+\frac{(x_0-\bar x)^2}{S_{xx}}}.$
	- Confidence interval for the mean response
		- $\displaystyle \hat y_0\pm t_{\alpha/2,n-2}S\sqrt{\frac1n+\frac{(x_0-\bar x)^2}{S_{xx}}}.$
	- Standard error for a **new individual prediction** at $x_0$
		- $\displaystyle S\sqrt{1+\frac1n+\frac{(x_0-\bar x)^2}{S_{xx}}}.$
	- Prediction interval
		- $\displaystyle \hat y_0\pm t_{\alpha/2,n-2}S\sqrt{1+\frac1n+\frac{(x_0-\bar x)^2}{S_{xx}}}.$
	- Key comparison
		- a prediction interval is wider because it must account for both uncertainty in the estimated regression line and the random error of the new observation
		- both intervals are narrowest near $\bar x$ and become wider farther from $\bar x$

1. **ANOVA decomposition for simple linear regression**
	- Total variability in $Y$
		- $\displaystyle \operatorname{SST}=\sum_{i=1}^n(y_i-\bar y)^2.$
	- Variability explained by the regression
		- $\displaystyle \operatorname{SSReg}=\sum_{i=1}^n(\hat y_i-\bar y)^2.$
	- Unexplained variability / residual sum of squares
		- $\displaystyle \operatorname{RSS}=\sum_{i=1}^n(y_i-\hat y_i)^2.$
	- Decomposition
		- $\displaystyle \operatorname{SST}=\operatorname{SSReg}+\operatorname{RSS}.$
	- Degrees of freedom
		- regression: $1$
		- residual: $n-2$
		- total: $n-1$
	- Mean squares
		- $\displaystyle \operatorname{MSReg}=\frac{\operatorname{SSReg}}1=\operatorname{SSReg}.$
		- $\displaystyle \operatorname{MSE}=\frac{\operatorname{RSS}}{n-2}=S^2.$
	- $F$ statistic
		- $\displaystyle F=\frac{\operatorname{MSReg}}{\operatorname{MSE}}.$
		- for simple linear regression, this tests the same null hypothesis $H_0:\beta_1=0$
		- $\displaystyle F_{1,n-2}=t_{n-2}^2$
	- **Professor emphasis: be able to fill in a partially completed ANOVA table.**
		- use the relationships among SS, df, MS, and $F$ to recover missing entries

1. **Coefficient of determination $R^2$**
	- Definition
		- $\displaystyle R^2=\frac{\operatorname{SSReg}}{\operatorname{SST}}=1-\frac{\operatorname{RSS}}{\operatorname{SST}}.$
	- Interpretation
		- proportion of the sample variability in $Y$ explained by the fitted regression model
	- In simple linear regression, $R^2=r_{xy}^2$.
		- the correlation has the sign of $\hat\beta_1$, while $R^2$ itself is always nonnegative

1. **Residuals and diagnostics**
	- Residuals are $\displaystyle \hat e_i=y_i-\hat y_i$.
		- if the linear model is appropriate, the residual plot should look like random scatter around $0$
	- Patterns in residuals can indicate a problem.
		- curvature
			- suggests the mean relationship may not actually be linear
		- funnel / changing spread
			- suggests nonconstant variance
		- unusually large residual
			- suggests a possible outlier in the response direction
	- Normality of errors
		- inspect a Q-Q plot
		- points should fall approximately along a straight line when the normality assumption is reasonable
	- Constant variance
		- residual spread should remain roughly constant across fitted values / predictor values
		- professor said not to focus on Box-Cox transformations for this exam

1. **Leverage**
	- Leverage measures how unusual an observation's predictor value is relative to the rest of the $x$ values.
	- For simple linear regression
		- $\displaystyle h_{ii}=\frac1n+\frac{(x_i-\bar x)^2}{S_{xx}}.$
	- Consequences
		- observations far from $\bar x$ have larger leverage
		- leverage depends on the predictor values, not directly on whether $y_i$ is unusual
	- Useful identity
		- $\displaystyle \sum_{i=1}^nh_{ii}=2.$
	- Rule used in the practice notes
		- flag a possible high-leverage observation when $\displaystyle h_{ii}>\frac4n$

1. **Standardized / studentized residual idea**
	- Raw residuals do not all have the same variance because leverage changes their variability.
	- A residual can be standardized using its estimated standard deviation.
	- Large absolute standardized residuals indicate observations whose responses are unusually far from what the fitted model predicts.
	- Conceptual distinction
		- **large residual** = unusual $y$ given its $x$
		- **high leverage** = unusual $x$
		- an observation can have one without the other

1. **Influence and Cook's distance**
	- An observation is influential when removing it substantially changes the fitted regression.
	- Influence depends on both residual size and leverage.
	- Cook's distance from class
		- $\displaystyle D_i=\frac{r_i^2}{2}\frac{h_{ii}}{1-h_{ii}}.$
	- Conceptual distinction
		- high leverage does not automatically mean high influence
		- a high-leverage point that lies close to the fitted line may have little influence
		- a point with both large leverage and a large residual can be highly influential

1. **What to be able to recognize quickly**
	- Given raw $x,y$ data
		- compute $\bar x$, $\bar y$, $S_{xx}$, $S_{xy}$
		- obtain $\hat\beta_1$ and $\hat\beta_0$
		- form fitted values and residuals
		- compute RSS and $S^2$
	- Given regression output
		- identify the estimated intercept and slope
		- identify each coefficient's standard error, $t$ statistic, and $p$-value
		- state the hypothesis being tested by the slope row
		- interpret $R^2$
		- connect residual standard error to $\sqrt{\operatorname{MSE}}$
	- Given an ANOVA table
		- fill in missing sums of squares, degrees of freedom, mean squares, and $F$
		- use $\operatorname{SST}=\operatorname{SSReg}+\operatorname{RSS}$
		- use $F=\operatorname{MSReg}/\operatorname{MSE}$
	- Given a diagnostic plot or unusual observation
		- distinguish residual size, leverage, and influence
		- identify curvature, nonconstant variance, nonnormality, or influential observations

1. **High-priority derivations / proofs to be able to reconstruct**
	- Least-squares estimators
		- minimize $\sum(y_i-\beta_0-\beta_1x_i)^2$
		- derive $\hat\beta_0=\bar y-\hat\beta_1\bar x$
		- derive $\hat\beta_1=S_{xy}/S_{xx}$
	- Residual identities
		- show $\sum\hat e_i=0$
		- show $\sum x_i\hat e_i=0$
	- Slope estimator properties
		- express $\hat\beta_1$ as a linear combination of the $Y_i$
		- use that form to derive $E(\hat\beta_1)=\beta_1$
		- derive $\operatorname{Var}(\hat\beta_1)=\sigma^2/S_{xx}$
	- Leverage
		- understand why $\displaystyle h_{ii}=\frac1n+\frac{(x_i-\bar x)^2}{S_{xx}}$ increases as $x_i$ moves away from $\bar x$

1. **Material explicitly de-emphasized for this exam**
	- Box-Cox transformations
		- professor said not to focus on them for the exam
	- Dummy variables
		- professor said no dummy variables / material not covered
	- Spend study time first on the regression calculations, inference, ANOVA, and diagnostics that were actually developed in class.

1. **Final self-test before the exam**
	- Can I derive $\hat\beta_1=S_{xy}/S_{xx}$ instead of only memorizing it?
	- Can I explain why $n-2$ appears in $S^2=\operatorname{RSS}/(n-2)$?
	- Can I move from $\hat\beta_1$ and its standard error to a $t$ statistic, $p$-value decision, and confidence interval?
	- Can I explain why a prediction interval is wider than a confidence interval for the mean response?
	- Can I fill a partially blank ANOVA table without R?
	- Can I move between SST, SSReg, RSS, $R^2$, MSE, and $F$?
	- Can I distinguish an outlier, a high-leverage observation, and an influential observation?
	- Can I look at a residual or Q-Q plot and say which model assumption is being checked?
