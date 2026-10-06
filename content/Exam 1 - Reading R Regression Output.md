# Exam 1 - Reading R Regression Output

- Parent: [[Exam 1 Study Guide (Math 444)]]
- Triage coverage
	- **Type 11:** interpret R output

1. **What problem are we trying to solve?**
	- R does not use different regression theory from the by-hand work.
	- It simply reports the same estimates, standard errors, tests, sums of squares, and diagnostics in a compact format.
	- **End goal**
		- look at `summary(lm())` and translate every important number back into a mathematical statement about the regression model

1. **Build the model in R**
	- Typical code
		- `m <- lm(y ~ x, data = dat)`
	- Mathematical model being fit
		- $\displaystyle Y_i=\beta_0+\beta_1x_i+\varepsilon_i.$
	- Fitted mathematical line
		- $\displaystyle \hat y=\hat\beta_0+\hat\beta_1x.$
	- `summary(m)` is the main output to know for the triage problem.

1. **The coefficient table**
	- Typical columns
		- `Estimate`
		- `Std. Error`
		- `t value`
		- `Pr(>|t|)`
	- **Intercept row**
		- `Estimate` = $\hat\beta_0$
		- `Std. Error` = $SE(\hat\beta_0)$
		- `t value` = $\hat\beta_0/SE(\hat\beta_0)$ when testing $H_0:\beta_0=0$
		- `Pr(>|t|)` = two-sided $p$-value for that test
	- **Predictor row**
		- `Estimate` = $\hat\beta_1$
		- `Std. Error` = $SE(\hat\beta_1)$
		- `t value` = $\hat\beta_1/SE(\hat\beta_1)$ when testing $H_0:\beta_1=0$
		- `Pr(>|t|)` = two-sided $p$-value for that test

1. **How to read the slope row in words**
	- Estimate
		- expected fitted change in $Y$ for a one-unit increase in $x$
	- Standard error
		- estimated sampling uncertainty in the slope estimator
	- $t$ statistic
		- how many standard errors the estimated slope lies from the null value $0$
	- $p$-value
		- under $H_0:\beta_1=0$, probability of observing a $|t|$ at least this large
	- If the problem instead asks about $H_0:\beta_1=1$
		- do **not** use the printed `t value` directly
		- recompute
			- $\displaystyle t=\frac{\hat\beta_1-1}{SE(\hat\beta_1)}$

1. **Residual standard error line**
	- R prints something like
		- `Residual standard error: ... on ... degrees of freedom`
	- This number is
		- $\displaystyle S=\sqrt{MSE}=\sqrt{\frac{RSS}{n-2}}.$
	- The degrees of freedom should be
		- $n-2$
	- Interpretation
		- rough scale of a typical residual in the response variable's units

1. **Multiple $R$-squared**
	- R's `Multiple R-squared` is
		- $\displaystyle R^2=1-\frac{RSS}{SST}=\frac{SS_{reg}}{SST}.$
	- Interpretation template
		- "$100R^2\%$ of the total sample variability in the response is explained by the fitted linear regression on the predictor."
	- Do not interpret it as a percent causal effect.

1. **Adjusted $R$-squared**
	- R also reports adjusted $R^2$.
	- It penalizes model complexity by accounting for degrees of freedom.
	- For Exam 1 SLR, know what line it is, but the ordinary $R^2$ is the direct quantity tied to the triage formula $SS_{reg}/SST$.

1. **The $F$-statistic line**
	- R prints an $F$ statistic, numerator df, denominator df, and a $p$-value.
	- In simple linear regression
		- numerator df $=1$
		- denominator df $=n-2$
	- Null hypothesis
		- $\displaystyle H_0:\beta_1=0$
	- Test statistic
		- $\displaystyle F=MS_{reg}/MSE$
	- In SLR
		- $\displaystyle F=t^2$
		- therefore the $F$-test $p$-value matches the two-sided slope-test $p$-value

1. **Fast consistency checks inside `summary(lm())`**
	- Predictor `t value`
		- should equal `Estimate / Std. Error`
	- Residual df
		- should equal $n-2$
	- $F$ statistic
		- should equal the squared slope $t$ statistic in SLR
	- Large $R^2$
		- should correspond to RSS being small relative to SST
	- These checks help catch transcription or calculator mistakes on an exam.

1. **`anova(m)` and the ANOVA table**
	- `anova(m)` exposes the sums-of-squares structure directly.
	- For one predictor, the essential mathematical table is
		- regression row: $SS_{reg}$, df $1$, $MS_{reg}$, $F$
		- residual row: $RSS$, df $n-2$, $MSE$
		- total $SST$ may need to be reconstructed depending on the displayed table
	- Relations to use
		- $\displaystyle SST=SS_{reg}+RSS$
		- $\displaystyle F=MS_{reg}/MSE$

1. **Confidence intervals from R**
	- `confint(m)` gives confidence intervals for the regression coefficients.
	- For the slope, it is implementing
		- $\displaystyle \hat\beta_1\pm t^*_{n-2}SE(\hat\beta_1).$
	- If asked to explain the output, identify
		- the point estimate
		- the lower endpoint
		- the upper endpoint
		- the confidence level

1. **Mean-response CI vs prediction interval in R**
	- Mean response at a new predictor value
		- `predict(m, newdata, interval = "confidence")`
	- One new observation at that predictor value
		- `predict(m, newdata, interval = "prediction")`
	- Both output
		- fitted value
		- lower endpoint
		- upper endpoint
	- Why the prediction interval is wider
		- it includes the new observation's individual random error in addition to uncertainty in the estimated mean line

1. **Diagnostic quantities in R**
	- `resid(m)`
		- raw residuals $\hat e_i$
	- `fitted(m)`
		- fitted values $\hat y_i$
	- `hatvalues(m)`
		- leverages $h_{ii}$
	- Standardized / studentized residual tools
		- scale residuals by their estimated variability
	- `cooks.distance(m)`
		- Cook's distances for influence
	- Standard diagnostic plotting functions combine these ideas visually.

1. **How to answer an R-output exam question step by step**
	- **Step 1 — Identify the fitted equation.**
		- read the intercept and predictor estimates
		- write $\hat y=\hat\beta_0+\hat\beta_1x$
	- **Step 2 — Interpret the slope in context.**
		- one-unit increase in $x$ corresponds to an estimated $\hat\beta_1$-unit change in the mean response
	- **Step 3 — Read uncertainty.**
		- identify the standard error for the requested coefficient
	- **Step 4 — State the hypothesis attached to the printed $t$ / $p$.**
		- coefficient row defaults to testing that coefficient against $0$
	- **Step 5 — Make the inference decision.**
		- compare the $p$-value with $\alpha$
		- state the conclusion in context
	- **Step 6 — Interpret model fit.**
		- use $R^2$
		- use residual standard error as the residual scale
	- **Step 7 — Read the overall $F$ line.**
		- in SLR, connect it to the slope test

1. **Representative numbers from the class hand-fit example**
	- From the class data used throughout the notes
		- $\hat\beta_0=1.7$
		- $\hat\beta_1=0.7$
		- $S=\sqrt{0.10}\approx0.3162$
		- $SE(\hat\beta_1)=0.10$
		- slope $t=7$
		- $R^2\approx0.9423$
		- $F=49$ on $1$ and $3$ df
	- If R produced these values, the interpretation would be exactly the same as the by-hand calculations in [[Exam 1 - Regression Inference and ANOVA]].

1. **Common mistakes**
	- Treating the printed slope $p$-value as a test of an arbitrary null such as $\beta_1=1$.
	- Confusing residual standard error with the standard error of the slope.
	- Saying $R^2$ is the percent of observations predicted correctly.
	- Forgetting that `interval = "confidence"` is for the mean response while `interval = "prediction"` is for a new individual observation.
	- Reading statistical significance without explaining the direction / magnitude of the estimated slope.

1. **Cold-recall checklist**
	- Can I write the fitted equation from the coefficient table immediately?
	- Can I recompute a coefficient's $t$ statistic from Estimate and Std. Error?
	- Can I state the null hypothesis attached to the printed slope $p$-value?
	- Can I explain residual standard error, $R^2$, and the $F$ line in words?
	- Can I explain why the slope $t$ test and model $F$ test agree in SLR?
	- Can I distinguish the R commands for coefficient CI, mean-response CI, and prediction interval?
