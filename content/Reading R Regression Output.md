- Not a standalone exam question type on its own — it's the presentation format any of the other problems could be posed in: "here's `summary(lm())` / `anova()` / a plot — answer this," instead of a raw data table.

## Concepts

- R never uses different theory from the by-hand work — `summary(lm())` just reports the same estimates, standard errors, tests, and sums of squares computed earlier, in a compact printed format.
	- `m <- lm(y ~ x, data = dat)` fits $Y_i=\beta_0+\beta_1x_i+\varepsilon_i$ and gives the fitted line $\hat y=\hat\beta_0+\hat\beta_1x$.
	- The end goal of this whole note is to look at `summary(m)` (or `anova()`, `confint()`, `predict()`, `hatvalues()`...) and translate every printed number back into a mathematical statement about the regression model.
- **The coefficient table is the first thing to read**, and its four columns answer four different questions about each coefficient.
	- `Estimate` is the coefficient itself: $\hat\beta_0$ in the intercept row, $\hat\beta_1$ in the predictor row.
	- `Std. Error` is that coefficient's standard error, $SE(\hat\beta_0)$ or $SE(\hat\beta_1)$ — how uncertain the estimate is.
	- `t value` is the estimate divided by its standard error — by default this tests $H_0:\beta_0=0$ or $H_0:\beta_1=0$.
	- `Pr(>|t|)` is the two-sided $p$-value for that same default test.
	- If the question instead asks about a nonzero null like $H_0:\beta_1=1$, the printed `t value` is the wrong number to use — recompute it by hand as $t=(\hat\beta_1-1)/SE(\hat\beta_1)$.
- **The residual standard error line** reports the overall scale of a typical miss.
	- It reads `Residual standard error: ... on ... degrees of freedom`.
	- The number itself is $S=\sqrt{MSE}=\sqrt{RSS/(n-2)}$, and the degrees of freedom should always be $n-2$.
	- It's measured in the same units as the response, and gives a rough sense of how far off a typical prediction is.
- **Multiple R-squared** is the same $R^2$ from the decomposition note, just printed under a different name.
	- $R^2=1-RSS/SST=SS_{reg}/SST$.
	- Read it as "$100R^2\%$ of the total sample variability in the response is explained by the fitted regression" — not as a percent causal effect.
	- R also prints an adjusted $R^2$, which penalizes for model complexity; in simple linear regression the *ordinary* $R^2$ is still the one tied directly to the $SS_{reg}/SST$ formula.
- **The $F$-statistic line** reports the overall model test, with the numerator/denominator degrees of freedom and a $p$-value attached.
	- In simple linear regression: numerator df is always $1$, denominator df is always $n-2$, and the test is $H_0:\beta_1=0$.
	- Since $F=t^2$ in SLR (shown in the Inference and ANOVA note), the $F$-test's $p$-value always matches the two-sided slope test's $p$-value.
- A few fast consistency checks can catch a transcription mistake before it costs points on an exam.
	- The predictor's `t value` should equal `Estimate / Std. Error`.
	- The residual degrees of freedom should equal $n-2$.
	- The $F$ statistic should equal the squared slope $t$-statistic.
	- A large $R^2$ should correspond to a small $RSS$ relative to $SST$.
- **`anova(m)`** prints the sum-of-squares table directly, instead of the coefficient-focused view from `summary()`.
	- The regression row has $SS_{reg}$, df $1$, $MS_{reg}$, and $F$.
	- The residual row has $RSS$, df $n-2$, and $MSE$.
	- The total $SST$ usually isn't printed directly — reconstruct it as $SS_{reg}+RSS$ if needed.
- **`confint(m)`** prints a confidence interval for each coefficient — for the slope, this is just $\hat\beta_1\pm t^*_{n-2}SE(\hat\beta_1)$ computed for you.
- **`predict()` can give either of two different intervals**, depending on which question is being asked.
	- `interval = "confidence"` gives a confidence interval for the *mean* response at a new $x$.
	- `interval = "prediction"` gives a prediction interval for *one new individual observation* at that $x$.
	- Both print `fit`, `lwr`, `upr` columns, but the prediction interval is always the wider one — it adds the new observation's own random error on top of the uncertainty in the estimated mean line.
- **A handful of other functions pull out diagnostic quantities directly**, instead of reading them off a plot.
	- `resid(m)` gives the raw residuals, and `fitted(m)` gives the fitted values.
	- `hatvalues(m)` gives the leverages $h_{ii}$, and `rstandard(m)` gives the standardized residuals.
	- `cooks.distance(m)` gives the Cook's distances.
	- `plot(m)` on its own produces four diagnostic panels: residuals vs. fitted, Q-Q, scale-location, and residuals vs. leverage.
- **A fixed order of steps for answering any R-output question:**
	1. read the fitted equation off the coefficient estimates
	2. interpret the slope in context
	3. read the standard error for whichever coefficient is asked about
	4. identify the null hypothesis attached to the printed $t$/$p$ (default is against $0$)
	5. compare $p$ to $\alpha$ and state the conclusion in context
	6. use $R^2$ and residual standard error to describe fit
	7. read the overall $F$ line and, in SLR, connect it to the slope test

## Practice Problems

- **Problem 1 — class data (`y ~ x`, $n=5$).**
	```r
	x <- c(-1, 0, 1, 2, 3)
	y <- c(1, 2, 2, 3, 4)
	m <- lm(y ~ x)
	summary(m)
	```
	```
	Call:
	lm(formula = y ~ x)

	Residuals:
	         1          2          3          4          5
	 9.714e-17  3.000e-01 -4.000e-01 -1.000e-01  2.000e-01

	Coefficients:
	            Estimate Std. Error t value Pr(>|t|)
	(Intercept)   1.7000     0.1732   9.815  0.00225 **
	x             0.7000     0.1000   7.000  0.00599 **
	---
	Residual standard error: 0.3162 on 3 degrees of freedom
	Multiple R-squared:  0.9423,	Adjusted R-squared:  0.9231
	F-statistic:    49 on 1 and 3 DF,  p-value: 0.005986
	```
	- *Solution.*
		- `x Estimate 0.7000` is $\hat\beta_1=S_{xy}/S_{xx}=7/10$
		- `x Std. Error 0.1000` is $S/\sqrt{S_{xx}}=0.3162/\sqrt{10}$
		- `x t value 7.000` tests $H_0:\beta_1=0$
		- `Residual standard error 0.3162 on 3 df` is $\sqrt{RSS/(n-2)}=\sqrt{0.30/3}$
		- `Multiple R-squared 0.9423` is $4.90/5.20$
		- `F-statistic 49` matches $t^2=7^2$

- **Problem 2 — real second dataset (Production data, `RunTime ~ RunSize`, $n=20$).**
	```
	Coefficients:
	             Estimate Std. Error t value Pr(>|t|)
	(Intercept) 149.74770    8.32815   17.98 6.00e-13 ***
	RunSize       0.25924    0.03714    6.98 1.61e-06 ***
	---
	Residual standard error: 16.25 on 18 degrees of freedom
	Multiple R-squared:  0.7302,	Adjusted R-squared:  0.7152
	F-statistic: 48.72 on 1 and 18 DF,  p-value: 1.615e-06
	```
	- *Solution.*
		- fitted line $\widehat{RunTime}=149.748+0.259\,RunSize$
		- slope $t=6.98$ tests $\beta_1=0$ and matches $\sqrt{F}=\sqrt{48.72}$
		- $R^2=0.730$: RunSize explains about 73% of the variation in RunTime
		- residual standard error $16.25$ on $18=n-2$ df

- **Problem 3 — real third dataset (airfares, `Fare ~ Distance`, $n=17$).**
	```
	Coefficients:
	             Estimate Std. Error t value Pr(>|t|)
	(Intercept) 48.971770   4.405493   11.12 1.22e-08 ***
	Distance     0.219687   0.004421   49.69  < 2e-16 ***
	---
	Residual standard error: 10.41 on 15 degrees of freedom
	Multiple R-squared:  0.994,	Adjusted R-squared:  0.9936
	F-statistic:  2469 on 1 and 15 DF,  p-value: < 2.2e-16
	```
	- *Solution.*
		- fitted line $\widehat{Fare}=48.972+0.2197\,Distance$
		- $t=49.69$ (very large, matches the near-perfect $R^2=0.994$)
		- $F=2469\approx49.69^2$, confirming $F=t^2$
		- residual df $=15=n-2$ for $n=17$
