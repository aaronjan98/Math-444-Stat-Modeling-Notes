# Regression Inference and ANOVA

- Parent: [[Exam 1]]
- Problem types covered
	- **Type 5:** $R^2$ — compute and interpret
	- **Type 6:** inference on the slope and intercept
	- **Type 7:** ANOVA / $F$ test

1. **What problem are we trying to solve?**
	- The fitted coefficients describe the sample, but we want to make statements about the population regression relationship.
	- To do that, we need
		- an estimate of the error variance
		- standard errors for the coefficient estimators
		- a reference distribution for test statistics
		- a way to measure how much variation the regression explains
	- **End goal**
		- move fluently among coefficient inference, $R^2$, and ANOVA instead of treating them as three unrelated topics

1. **Estimate the unknown error variance first**
	- Residual variation is
		- $\displaystyle RSS=\sum\hat e_i^2.$
	- We estimated two regression parameters, so residual degrees of freedom are $n-2$.
	- Error variance estimator
		- $\displaystyle \boxed{S^2=MSE=\frac{RSS}{n-2}}$
	- Residual standard error
		- $\displaystyle \boxed{S=\sqrt{MSE}}$
	- Why $n-2$ instead of $n$
		- fitting the intercept and slope imposes two constraints on the residuals
		- only $n-2$ independent residual directions remain for estimating error variation

1. **Inference for the slope**
	- From [[Regression Estimator Properties]],
		- $\displaystyle \operatorname{Var}(\hat\beta_1)=\frac{\sigma^2}{S_{xx}}.$
	- Replace unknown $\sigma$ by $S$.
		- $\displaystyle SE(\hat\beta_1)=\frac{S}{\sqrt{S_{xx}}}.$
	- For testing
		- $\displaystyle H_0:\beta_1=\beta_{1,0}$
		- $\displaystyle H_A:\beta_1\neq\beta_{1,0}$
	- Test statistic
		- $\displaystyle \boxed{t=\frac{\hat\beta_1-\beta_{1,0}}{S/\sqrt{S_{xx}}}}$
	- Under $H_0$, use a $t$ distribution with $n-2$ degrees of freedom.
	- Common nulls
		- $H_0:\beta_1=0$
			- asks whether there is evidence of a nonzero linear relationship
		- $H_0:\beta_1=1$
			- same machinery; only the hypothesized value in the numerator changes
	- Two-sided decision
		- reject for sufficiently large $|t|$
		- equivalently reject when the two-sided $p$-value is less than $\alpha$

1. **Confidence interval for the slope**
	- General form
		- estimate $\pm$ critical value $\times$ standard error
	- Slope CI
		- $\displaystyle \boxed{\hat\beta_1\pm t^*_{n-2}\frac{S}{\sqrt{S_{xx}}}}$
	- Test-CI connection
		- for a two-sided level-$\alpha$ test, $H_0:\beta_1=\beta_{1,0}$ is rejected exactly when $\beta_{1,0}$ lies outside the corresponding $(1-\alpha)100\%$ CI

1. **Inference for the intercept**
	- Standard error
		- $\displaystyle SE(\hat\beta_0)=S\sqrt{\frac1n+\frac{\bar x^2}{S_{xx}}}$
	- Test statistic for $H_0:\beta_0=\beta_{0,0}$
		- $\displaystyle t=\frac{\hat\beta_0-\beta_{0,0}}{SE(\hat\beta_0)}$
	- Confidence interval
		- $\displaystyle \hat\beta_0\pm t^*_{n-2}SE(\hat\beta_0)$
	- Interpretation warning
		- the intercept is the expected response at $x=0$
		- that interpretation may be scientifically meaningless if $x=0$ is far outside the observed predictor range

1. **Confidence interval for a mean response**
	- At predictor value $x_0$, the fitted mean response is
		- $\displaystyle \hat y_0=\hat\beta_0+\hat\beta_1x_0.$
	- Standard error for the **population mean response** at $x_0$
		- $\displaystyle SE_{mean}=S\sqrt{\frac1n+\frac{(x_0-\bar x)^2}{S_{xx}}}.$
	- Confidence interval
		- $\displaystyle \boxed{\hat y_0\pm t^*_{n-2}SE_{mean}}$
	- Why the interval is narrowest near $\bar x$
		- the term $(x_0-\bar x)^2$ is smallest there
		- the fitted line is best pinned down near the center of the observed predictor values

1. **Prediction interval for one new observation**
	- A new individual response contains two sources of uncertainty.
		- uncertainty about the mean regression line
		- the new observation's own random error
	- Therefore
		- $\displaystyle SE_{pred}=S\sqrt{1+\frac1n+\frac{(x_0-\bar x)^2}{S_{xx}}}.$
	- Prediction interval
		- $\displaystyle \boxed{\hat y_0\pm t^*_{n-2}SE_{pred}}$
	- Click point
		- the extra $1$ under the square root is the new observation's irreducible error
		- therefore a prediction interval is always wider than the CI for the mean response at the same $x_0$

1. **$R^2$ from the sum-of-squares decomposition**
	- From [[Residual and Sum-of-Squares Proofs]],
		- $\displaystyle SST=SS_{reg}+RSS.$
	- Define the fraction of total variation explained by the regression.
		- $\displaystyle \boxed{R^2=\frac{SS_{reg}}{SST}}$
	- Substitute $SS_{reg}=SST-RSS$.
		- $\displaystyle \boxed{R^2=1-\frac{RSS}{SST}}$
	- Interpretation template
		- "$R^2\times100\%$ of the total sample variability in $Y$ is explained by the fitted linear regression on $x$."
	- In simple linear regression with an intercept
		- $\displaystyle R^2=r_{xy}^2$
		- the sign of the correlation is the sign of $\hat\beta_1$
	- What $R^2$ does **not** tell you
		- it does not prove causation
		- it does not verify linearity, normality, independence, or constant variance
		- a high $R^2$ can coexist with a badly misspecified model

1. **ANOVA table structure**
	- Regression ANOVA organizes the same decomposition into rows.
	- **Regression row**
		- sum of squares: $SS_{reg}$
		- df: $1$
		- mean square: $\displaystyle MS_{reg}=SS_{reg}/1=SS_{reg}$
	- **Error / residual row**
		- sum of squares: $RSS$
		- df: $n-2$
		- mean square: $\displaystyle MSE=RSS/(n-2)$
	- **Total row**
		- sum of squares: $SST$
		- df: $n-1$
	- $F$ statistic
		- $\displaystyle \boxed{F=\frac{MS_{reg}}{MSE}}$

1. **How to reconstruct a partially blank ANOVA table**
	- First identify $n$ from the degrees of freedom if possible.
		- total df $=n-1$
		- residual df $=n-2$
	- Use the decomposition.
		- $\displaystyle SST=SS_{reg}+RSS$
	- Use mean-square definitions.
		- $\displaystyle MS_{reg}=SS_{reg}/1$
		- $\displaystyle MSE=RSS/(n-2)$
	- Use the $F$ ratio.
		- $\displaystyle F=MS_{reg}/MSE$
	- If $R^2$ is given, use
		- $\displaystyle R^2=SS_{reg}/SST$
		- or $\displaystyle R^2=1-RSS/SST$

1. **Why the ANOVA $F$ test and slope $t$ test are the same test in SLR**
	- **End goal**
		- prove $F=t^2$ for testing $H_0:\beta_1=0$
	- Start by expressing the fitted deviations from $\bar y$.
		- because $\hat\beta_0=\bar y-\hat\beta_1\bar x$,
			- $\displaystyle \hat y_i-\bar y=\hat\beta_1(x_i-\bar x).$
	- Therefore
		- $\displaystyle SS_{reg}=\sum(\hat y_i-\bar y)^2=\hat\beta_1^2\sum(x_i-\bar x)^2=\hat\beta_1^2S_{xx}.$
	- Since regression df is $1$,
		- $\displaystyle MS_{reg}=\hat\beta_1^2S_{xx}.$
	- Then
		- $\displaystyle F=\frac{\hat\beta_1^2S_{xx}}{MSE}.$
	- Since $S=\sqrt{MSE}$,
		- $\displaystyle F=\frac{\hat\beta_1^2S_{xx}}{S^2}=\left(\frac{\hat\beta_1}{S/\sqrt{S_{xx}}}\right)^2.$
	- But the expression in parentheses is the slope $t$ statistic under $H_0:\beta_1=0$.
	- Therefore
		- $\displaystyle \boxed{F=t^2}.$
	- Meaning
		- in simple linear regression, the overall model test and the two-sided slope test contain the same information

1. **Worked example using the class data**
	- From the fitted example
		- $n=5$
		- $S_{xx}=10$
		- $\hat\beta_1=0.7$
		- $RSS=0.30$
		- $SST=5.20$
		- $SS_{reg}=4.90$
	- **$R^2$**
		- $\displaystyle R^2=4.90/5.20\approx0.9423$
		- interpretation: about $94.2\%$ of the sample variation in $y$ is explained by the fitted linear regression on $x$
	- **MSE and residual standard error**
		- residual df $=5-2=3$
		- $\displaystyle MSE=0.30/3=0.10$
		- $\displaystyle S=\sqrt{0.10}\approx0.3162$
	- **Slope standard error**
		- $\displaystyle SE(\hat\beta_1)=0.3162/\sqrt{10}=0.10$
	- **Slope test for $H_0:\beta_1=0$**
		- $\displaystyle t=0.7/0.1=7$
	- **ANOVA $F$ statistic**
		- $\displaystyle MS_{reg}=4.90$
		- $\displaystyle F=4.90/0.10=49$
		- check: $\displaystyle t^2=7^2=49=F$
	- **ANOVA table values**
		- regression: SS $=4.90$, df $=1$, MS $=4.90$, $F=49$
		- residual: SS $=0.30$, df $=3$, MS $=0.10$
		- total: SS $=5.20$, df $=4$

1. **Common mistakes**
	- Using $n-1$ instead of $n-2$ for residual degrees of freedom.
	- Using $S^2$ where the standard error formula requires $S$.
	- Interpreting $R^2$ as "percent of $Y$ caused by $x$."
	- Forgetting that a prediction interval has an extra $1$ under the square root.
	- Using the $F=t^2$ identity for a slope null other than $0$ without checking what hypothesis the overall $F$ test actually represents.
	- Forgetting that the ANOVA regression row has df $1$ only because this is **simple** linear regression with one predictor.
