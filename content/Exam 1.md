# Exam 1

- **Exam:** Thursday, October 8, 2026
	- Coverage: everything through **Chapter 3**, meaning simple linear regression through regression diagnostics.
	- Quick reference (notation, identities, assumptions): [[Formula and Identity Sheet]]

1. **What this exam is really testing**
	- The course has built one chain of ideas rather than a collection of unrelated formulas.
		- Start with data $(x_i,y_i)$.
		- Fit the best straight line by minimizing squared residuals.
		- Study the mathematical properties of the resulting estimators.
		- Use those properties to do inference on the population regression line.
		- Split the variability in $Y$ into explained and unexplained pieces.
		- Check whether the fitted model is believable using residuals, leverage, and diagnostic plots.
		- Read all of the same information from R output.
	- A useful mental pipeline is
		- $\displaystyle \text{data}\to\text{least-squares line}\to\text{residuals}\to\text{sampling uncertainty}\to\text{ANOVA / }R^2\to\text{diagnostics}.$
	- If you understand why each stage produces the quantities needed by the next stage, most of the formulas stop feeling isolated.

1. **Problem-type map**
	- **Type 1 — Hand-compute an SLR fit**
		- Given a small $(x,y)$ table, compute $S_{xy}$, $S_{xx}$, $\hat\beta_1$, $\hat\beta_0$, the fitted line, and a residual.
		- Study in [[Fitting a Simple Linear Regression]].
	- **Type 2 — Derive the least-squares estimators / normal equations**
		- Start from SSE, minimize it, obtain the two normal equations, and solve for $\hat\beta_1=S_{xy}/S_{xx}$ and $\hat\beta_0=\bar y-\hat\beta_1\bar x$.
		- Study in [[Fitting a Simple Linear Regression]].
	- **Type 3 — Residual-property proofs**
		- Prove $\sum\hat e_i=0$, $\sum x_i\hat e_i=0$, and $\sum\hat y_i\hat e_i=0$.
		- Study in [[Residual and Sum-of-Squares Proofs]].
	- **Type 4 — Sum-of-squares decomposition proof**
		- Prove $SST=SS_{reg}+RSS$ by expanding around $\hat y_i$ and showing the cross term is zero.
		- Study in [[Residual and Sum-of-Squares Proofs]].
	- **Type 5 — $R^2$: compute and interpret**
		- Move between $R^2=SS_{reg}/SST$ and $R^2=1-RSS/SST$ and explain it in words.
		- Study in [[Regression Inference and ANOVA]].
	- **Type 6 — Inference on the slope and intercept**
		- Use standard errors, $t$ tests, $p$-values, and confidence intervals.
		- Be ready for $H_0:\beta_1=0$ and a nonzero null such as $H_0:\beta_1=1$.
		- Study in [[Regression Inference and ANOVA]].
	- **Type 7 — ANOVA / $F$ test**
		- Fill in the ANOVA table, compute mean squares, use $F=MS_{reg}/MSE$, and connect $F=t^2$ in SLR.
		- Study in [[Regression Inference and ANOVA]].
	- **Type 8 — Covariance / variance bilinearity proof**
		- Use linear-combination rules, independence, and the $c_i$ identities to derive estimator covariance and variance results.
		- Study in [[Regression Estimator Properties]].
	- **Type 9 — Residual diagnostics**
		- Read residual patterns and connect each pattern to the assumption or model feature that may be wrong.
		- Study in [[Regression Diagnostics and Leverage]].
	- **Type 10 — Leverage**
		- Understand and use $h_{ii}$, why extreme $x$ gives high leverage, the $4/n$ cutoff, and the derivation of the hat weights if derivations are in scope.
		- Study in [[Regression Diagnostics and Leverage]].
	- **Type 11 — Interpret R output**
		- Read coefficient estimates, standard errors, $t$ statistics, $p$-values, $R^2$, residual standard error, and the $F$ line from `summary(lm())`.
		- Study in [[Reading R Regression Output]].

1. **How the study notes are grouped**
	- [[Fitting a Simple Linear Regression]]
		- types 1 and 2
		- turns raw data into the fitted line
	- [[Residual and Sum-of-Squares Proofs]]
		- types 3 and 4
		- develops the identities that make ANOVA and $R^2$ work
	- [[Regression Estimator Properties]]
		- type 8 plus the estimator facts needed for inference
		- explains why the least-squares estimators have the means, variances, and covariance used later
	- [[Regression Inference and ANOVA]]
		- types 5, 6, and 7
		- turns estimator uncertainty and sums of squares into tests, intervals, $R^2$, and $F$
	- [[Regression Diagnostics and Leverage]]
		- types 9 and 10
		- checks whether the model and individual observations are trustworthy
	- [[Reading R Regression Output]]
		- type 11
		- teaches how R packages the same quantities computed and derived by hand
	- [[Formula and Identity Sheet]]
		- the notation, core identities, and assumptions that connect all of the above

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
