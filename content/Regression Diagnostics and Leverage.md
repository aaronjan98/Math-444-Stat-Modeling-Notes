# Regression Diagnostics and Leverage

- Parent: [[Exam 1]]
- Problem types covered
	- **Type 9:** residual diagnostics — read the plot
	- **Type 10:** leverage

1. **What problem are we trying to solve?**
	- Regression calculations can always produce a fitted line, even when a straight-line model is inappropriate.
	- Diagnostics ask whether the assumptions behind that line and its inference are believable.
	- They also ask whether individual observations have unusual predictor values or disproportionate influence.
	- **End goal**
		- look at a plot or an observation and identify exactly what kind of problem it represents

1. **Why residuals diagnose the unobserved errors**
	- True model
		- $\displaystyle Y_i=\beta_0+\beta_1x_i+\varepsilon_i.$
	- Residual
		- $\displaystyle \hat e_i=Y_i-\hat Y_i.$
	- If the fitted line is close to the true mean line,
		- $\hat Y_i\approx\beta_0+\beta_1x_i$
	- Therefore
		- $\displaystyle \hat e_i=Y_i-\hat Y_i\approx Y_i-(\beta_0+\beta_1x_i)=\varepsilon_i.$
	- Click point
		- we cannot observe the true errors $\varepsilon_i$
		- residuals are our observable stand-ins for them
		- that is why plotting residuals lets us inspect assumptions about the errors

1. **What a healthy residual plot should look like**
	- Roughly random scatter around $0$.
	- No systematic curvature.
	- No obvious trend with $x$ or fitted values.
	- Roughly constant vertical spread across the horizontal axis.
	- A few moderate residuals are expected; the issue is systematic structure.

1. **Residual-pattern recognition**
	- **Curvature / U-shape / inverted U-shape**
		- suggests the mean function is not actually linear
	- **Funnel shape**
		- residual spread increases or decreases with fitted values
		- suggests nonconstant variance
	- **Isolated very large vertical residual**
		- possible outlier in the response direction
	- **Runs / clusters / time-order structure**
		- can suggest dependence if observations have a natural ordering
	- **Q-Q plot bends systematically away from a line**
		- suggests the error distribution may not be normal

1. **Why fitting a line to a quadratic relationship leaves a residual pattern**
	- Suppose the true model is actually
		- $\displaystyle Y_i=\beta_0+\beta_1x_i+\beta_2x_i^2+\varepsilon_i.$
	- But we fit only a straight line.
		- $\displaystyle \hat Y_i\approx\beta_0+\beta_1x_i.$
	- Then the residual is approximately
		- $\displaystyle \hat e_i=Y_i-\hat Y_i\approx\beta_2x_i^2+\varepsilon_i.$
	- The residual therefore still contains a systematic $x_i^2$ component.
	- That is why curvature appears in the residual plot.
	- General principle
		- a pattern in the residuals is evidence that the model failed to explain a systematic part of the response

1. **Normality diagnostic**
	- Use a Q-Q plot.
	- If the errors are approximately normal,
		- residual quantiles should line up approximately with theoretical normal quantiles
	- The plot does not need to be perfectly straight.
	- Strong systematic bending or extreme tail departures are the warning signs.
	- Normality matters most for the exact small-sample $t$ and $F$ inference.

1. **Constant-variance diagnostic**
	- Inspect residuals against fitted values or predictor values.
	- Desired behavior
		- roughly equal vertical spread everywhere
	- Warning sign
		- the cloud gets noticeably wider or narrower as fitted values increase

1. **What leverage measures**
	- A residual asks whether the **response** is unusual at its predictor value.
	- Leverage asks whether the **predictor value itself** is unusual relative to the other $x$ values.
	- In SLR,
		- $\displaystyle \boxed{h_{ii}=\frac1n+\frac{(x_i-\bar x)^2}{S_{xx}}}$
	- Immediate consequences
		- leverage is smallest near $\bar x$
		- leverage grows as $x_i$ moves farther from $\bar x$
		- leverage depends only on the $x$ values, not the observed $y_i$

1. **Derive the leverage / hat-matrix weights**
	- **End goal**
		- show that every fitted value is a weighted sum of all observed responses and identify the observation's own weight $h_{ii}$
	- Start from the fitted value written around the sample mean.
		- $\displaystyle \hat y_i=\bar y+\hat\beta_1(x_i-\bar x).$
	- Write $\bar y$ as a sum.
		- $\displaystyle \bar y=\sum_{j=1}^n\frac1n y_j.$
	- Write the slope as a linear combination.
		- $\displaystyle \hat\beta_1=\frac{1}{S_{xx}}\sum_{j=1}^n(x_j-\bar x)y_j.$
	- Substitute both into $\hat y_i$.
		- $\displaystyle \hat y_i=\sum_{j=1}^n\frac1n y_j+\frac{x_i-\bar x}{S_{xx}}\sum_{j=1}^n(x_j-\bar x)y_j.$
	- Combine into one sum.
		- $\displaystyle \hat y_i=\sum_{j=1}^n\left[\frac1n+\frac{(x_i-\bar x)(x_j-\bar x)}{S_{xx}}\right]y_j.$
	- Define
		- $\displaystyle \boxed{h_{ij}=\frac1n+\frac{(x_i-\bar x)(x_j-\bar x)}{S_{xx}}}.$
	- Therefore
		- $\displaystyle \hat y_i=\sum_{j=1}^nh_{ij}y_j.$
	- The observation's own weight is obtained by setting $j=i$.
		- $\displaystyle \boxed{h_{ii}=\frac1n+\frac{(x_i-\bar x)^2}{S_{xx}}}.$

1. **Why the leverages sum to 2 in SLR**
	- Sum the diagonal formula.
		- $\displaystyle \sum h_{ii}=\sum\frac1n+\frac1{S_{xx}}\sum(x_i-\bar x)^2.$
	- The first part is $1$.
		- $\displaystyle \sum(1/n)=1$
	- The second part is also $1$.
		- $\displaystyle \frac1{S_{xx}}\sum(x_i-\bar x)^2=1$
	- Therefore
		- $\displaystyle \boxed{\sum h_{ii}=2}.$
	- Meaning
		- the average leverage is $2/n$
		- the number $2$ corresponds to the two fitted coefficients: intercept and slope

1. **High-leverage flag (rule of thumb)**
	- A common screening rule is to flag observation $i$ when its leverage exceeds twice the average $2/n$,
		- $\displaystyle h_{ii}>\frac4n.$
	- Treat this as a screening rule, not a theorem that the observation is bad.
	- A high-leverage observation can be perfectly consistent with the fitted trend.

1. **Why raw residuals have different variances**
	- In least squares,
		- $\displaystyle \operatorname{Var}(\hat e_i)=\sigma^2(1-h_{ii}).$
	- So observations with different leverage have different residual variances.
	- This motivates scaling residuals before comparing their sizes.
	- A common standardized residual form is
		- $\displaystyle r_i=\frac{\hat e_i}{S\sqrt{1-h_{ii}}}.$
	- Interpretation
		- $r_i$ measures the residual in units of its estimated standard deviation

1. **Outlier vs leverage vs influence**
	- **Large residual / response outlier**
		- unusual $y$ given its $x$
	- **High leverage**
		- unusual $x$
	- **Influential observation**
		- an observation whose inclusion substantially changes the fitted regression
	- These are not synonyms.
		- a point can have high leverage but lie exactly on the fitted trend
		- a point can have a large residual at an ordinary $x$
		- a point with both high leverage and a large standardized residual is especially capable of being influential

1. **Cook's distance**
	- Cook's distance summarizes influence by combining residual size with leverage.
	- Formula from class
		- $\displaystyle D_i=\frac{r_i^2}{2}\frac{h_{ii}}{1-h_{ii}}.$
	- Interpretation of the factors
		- $r_i^2$ measures response unusualness
		- $h_{ii}/(1-h_{ii})$ increases with leverage
	- Another class interpretation
		- remove observation $i$, refit the model, and measure how much the fitted values move

1. **Worked leverage example using the class data**
	- Predictor values
		- $-1,0,1,2,3$
	- From the fitting note
		- $n=5$
		- $\bar x=1$
		- $S_{xx}=10$
	- Compute
		- $x=-1$: $\displaystyle h=1/5+(-2)^2/10=0.6$
		- $x=0$: $\displaystyle h=1/5+(-1)^2/10=0.3$
		- $x=1$: $\displaystyle h=1/5+0^2/10=0.2$
		- $x=2$: $\displaystyle h=1/5+1^2/10=0.3$
		- $x=3$: $\displaystyle h=1/5+2^2/10=0.6$
	- Check the sum.
		- $\displaystyle 0.6+0.3+0.2+0.3+0.6=2$
	- Practice cutoff
		- $\displaystyle 4/n=4/5=0.8$
		- none of these observations exceeds the practice high-leverage threshold
	- Pattern to notice
		- the center point $x=\bar x=1$ has the smallest leverage
		- the two most extreme $x$ values have the largest leverage

1. **Exam recognition map for diagnostic questions**
	- Curved residual plot
		- wrong functional form / nonlinearity
	- Fan or funnel residual plot
		- nonconstant variance
	- Q-Q plot with systematic tail departures
		- possible nonnormality
	- Single point far vertically from the line
		- large residual / response outlier
	- Single point far horizontally from the rest
		- high leverage
	- Point both horizontally extreme and vertically inconsistent
		- potentially highly influential

1. **Common mistakes**
	- Calling every outlier a high-leverage point.
	- Looking at $y_i$ when computing leverage; $h_{ii}$ depends only on the $x$ configuration.
	- Forgetting the $1/n$ term in the leverage formula.
	- Treating the $4/n$ rule as an automatic deletion rule.
	- Assuming a high $R^2$ makes diagnostic checks unnecessary.
