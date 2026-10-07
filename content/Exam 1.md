# Exam 1

- **Exam:** Tuesday, October 20, 2026
	- Coverage: everything through **Chapter 3**, meaning simple linear regression through regression diagnostics.
	- Quick reference (notation, identities, assumptions): [[Formula and Identity Sheet]]

1. **Triage, grouped by concept**
	- **[[Fitting a Simple Linear Regression]]**
		- Hand-compute an SLR fit from a small $(x,y)$ table: $S_{xy}$, $S_{xx}$, $\hat\beta_1$, $\hat\beta_0$, the fitted line, a residual.
		- Derive the least-squares estimators / normal equations from SSE.
	- **[[Residual and Sum-of-Squares Proofs]]**
		- Prove $\sum\hat e_i=0$, $\sum x_i\hat e_i=0$, and $\sum\hat y_i\hat e_i=0$.
		- Prove $SST=SS_{reg}+RSS$ by expanding around $\hat y_i$ and showing the cross term is zero.
	- **[[Regression Estimator Properties]]**
		- Covariance / variance bilinearity: derive $E(\hat\beta_1)$, $\operatorname{Var}(\hat\beta_1)$, and $\operatorname{Cov}(\hat\beta_0,\hat\beta_1)$ from the $c_i$ representation.
	- **[[Regression Inference and ANOVA]]**
		- $R^2$: compute and interpret, moving between $R^2=SS_{reg}/SST$ and $1-RSS/SST$.
		- Inference on the slope and intercept: standard errors, $t$-tests, $p$-values, CIs — including a nonzero null like $H_0:\beta_1=1$.
		- ANOVA / $F$-test: fill in the table, connect $F=t^2$.
	- **[[Regression Diagnostics and Leverage]]**
		- Residual diagnostics: read a plot, connect the pattern to the assumption or model feature that's wrong.
		- Leverage: $h_{ii}$, why extreme $x$ gives high leverage, the $4/n$ cutoff, standardized residuals, Cook's distance.
	- **[[Reading R Regression Output]]**
		- Not a separate exam question type — a presentation format. Any of the above could be posed through `summary(lm())`, `anova()`, or a diagnostic plot instead of raw numbers.

1. **Exam-day recognition map**
	- If the problem gives a small table of raw $(x,y)$ values
		- think **fit the line by hand**
	- If the problem says "derive," "show," "prove," or starts with SSE
		- think **normal equations or residual identities**
	- If the problem asks where total variability goes
		- think **SST decomposition, ANOVA, and $R^2$**
	- If the problem gives an estimate and a standard error
		- think **$t$ inference**
	- If the problem gives a partially blank ANOVA table
		- think **SS $\leftrightarrow$ df $\leftrightarrow$ MS $\leftrightarrow$ $F$**
	- If the problem shows residual or Q-Q plots
		- think **model assumptions / diagnostics**
	- If one $x_i$ is far from the rest
		- think **leverage**
	- If the problem gives `summary(lm())`
		- think **translate R output back into the same regression quantities**
