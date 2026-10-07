- Problem types covered
	- **Type 11:** interpret R output
	- Not a standalone exam question type on its own — it's the presentation format any of the problems above could be posed in. Any of types 1, 5, 6, 7, 9, or 10 could show up as "here's `summary(lm())` / `anova()` / a plot — answer this," instead of a raw data table.

## Concepts

- R reports the same estimates, standard errors, tests, sums of squares, and diagnostics computed by hand — just in a compact format. End goal: look at `summary(lm())` (or `anova()`, `confint()`, `predict()`, `hatvalues()`...) and translate every number back into a mathematical statement about the regression model.
- `m <- lm(y ~ x, data = dat)` fits $Y_i=\beta_0+\beta_1x_i+\varepsilon_i$ and gives the fitted line $\hat y=\hat\beta_0+\hat\beta_1x$. `summary(m)` is the main thing to know how to read.
- **The coefficient table.** Columns `Estimate`, `Std. Error`, `t value`, `Pr(>|t|)`. Intercept row: `Estimate`$=\hat\beta_0$, `Std. Error`$=SE(\hat\beta_0)$, `t value`$=\hat\beta_0/SE(\hat\beta_0)$ (tests $H_0:\beta_0=0$), `Pr(>|t|)` is the two-sided $p$-value for that test. Predictor row: same pattern for $\hat\beta_1$, testing $H_0:\beta_1=0$ by default.
	- If the question asks about $H_0:\beta_1=1$ (or any nonzero null) instead, do **not** use the printed `t value` directly — recompute $t=(\hat\beta_1-1)/SE(\hat\beta_1)$.
- **Residual standard error line** (`Residual standard error: ... on ... degrees of freedom`): this is $S=\sqrt{MSE}=\sqrt{RSS/(n-2)}$; df should be $n-2$; it's the rough scale of a typical residual in the response's units.
- **Multiple R-squared** is $R^2=1-RSS/SST=SS_{reg}/SST$, read as "$100R^2\%$ of the total sample variability in the response is explained by the fitted regression" — not a percent causal effect. Adjusted $R^2$ penalizes for model complexity; for SLR the ordinary $R^2$ is the one tied directly to $SS_{reg}/SST$.
- **The $F$-statistic line** reports $F$, numerator/denominator df, and a $p$-value. In SLR: numerator df $=1$, denominator df $=n-2$, testing $H_0:\beta_1=0$, and $F=t^2$ (the slope's $t$ squared) — so the $F$-test $p$-value matches the two-sided slope-test $p$-value.
- **Fast consistency checks:** predictor `t value` should equal `Estimate / Std. Error`; residual df should equal $n-2$; $F$ should equal the squared slope $t$; a large $R^2$ should correspond to a small $RSS$ relative to $SST$. Useful for catching transcription errors on an exam.
- **`anova(m)`** exposes the sums-of-squares structure directly: regression row ($SS_{reg}$, df $1$, $MS_{reg}$, $F$), residual row ($RSS$, df $n-2$, $MSE$); total $SST$ may need reconstructing as $SS_{reg}+RSS$ if not printed.
- **`confint(m)`** gives coefficient CIs, e.g. for the slope implementing $\hat\beta_1\pm t^*_{n-2}SE(\hat\beta_1)$.
- **Mean response vs. prediction interval in R.** `predict(m, newdata, interval="confidence")` is for the mean response at a new $x$; `interval="prediction"` is for one new observation there. Both print `fit`, `lwr`, `upr`. The prediction interval is always wider — it adds the new observation's own random error on top of the uncertainty in the estimated mean line.
- **Diagnostic quantities in R:** `resid(m)` (raw residuals), `fitted(m)` (fitted values), `hatvalues(m)` (leverages $h_{ii}$), `rstandard(m)` (standardized residuals), `cooks.distance(m)` (Cook's distances). `plot(m)` gives four panels by default: residuals vs. fitted, Q-Q, scale-location, and residuals vs. leverage.
- **Answering an R-output question, step by step:**
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
