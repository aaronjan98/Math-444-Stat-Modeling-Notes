# Exam 1

- **Exam:** Thursday, October 8, 2026
	- Coverage from the current triage: everything through **Chapter 3**, meaning simple linear regression through regression diagnostics.
	- Professor explicitly said **Box-Cox transformations are not a focus for this exam**.
	- Professor also said there will be **no dummy-variable material or material that was not covered**.
	- The professor specifically emphasized being able to **fill in an ANOVA table**.
	- Detailed study map: [[Exam 1 Study Guide (Math 444)]]
	- Original planning / attack queue: [[Midterm I Triage]]

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

1. **Triage map from [[Midterm I Triage]]**
	- **Type 1 — Hand-compute an SLR fit**
		- Given a small $(x,y)$ table, compute $S_{xy}$, $S_{xx}$, $\hat\beta_1$, $\hat\beta_0$, the fitted line, and a residual.
		- Study in [[Exam 1 - Fitting a Simple Linear Regression]].
	- **Type 2 — Derive the least-squares estimators / normal equations**
		- Start from SSE, minimize it, obtain the two normal equations, and solve for $\hat\beta_1=S_{xy}/S_{xx}$ and $\hat\beta_0=\bar y-\hat\beta_1\bar x$.
		- Study in [[Exam 1 - Fitting a Simple Linear Regression]].
	- **Type 3 — Residual-property proofs**
		- Prove $\sum\hat e_i=0$, $\sum x_i\hat e_i=0$, and $\sum\hat y_i\hat e_i=0$.
		- Study in [[Exam 1 - Residual and Sum-of-Squares Proofs]].
	- **Type 4 — Sum-of-squares decomposition proof**
		- Prove $SST=SS_{reg}+RSS$ by expanding around $\hat y_i$ and showing the cross term is zero.
		- Study in [[Exam 1 - Residual and Sum-of-Squares Proofs]].
	- **Type 5 — $R^2$: compute and interpret**
		- Move between $R^2=SS_{reg}/SST$ and $R^2=1-RSS/SST$ and explain it in words.
		- Study in [[Exam 1 - Regression Inference and ANOVA]].
	- **Type 6 — Inference on the slope and intercept**
		- Use standard errors, $t$ tests, $p$-values, and confidence intervals.
		- Be ready for $H_0:\beta_1=0$ and a nonzero null such as $H_0:\beta_1=1$.
		- Study in [[Exam 1 - Regression Inference and ANOVA]].
	- **Type 7 — ANOVA / $F$ test**
		- Fill in the ANOVA table, compute mean squares, use $F=MS_{reg}/MSE$, and connect $F=t^2$ in SLR.
		- Study in [[Exam 1 - Regression Inference and ANOVA]].
	- **Type 8 — Covariance / variance bilinearity proof**
		- Use linear-combination rules, independence, and the $c_i$ identities to derive estimator covariance and variance results.
		- Study in [[Exam 1 - Regression Estimator Properties]].
	- **Type 9 — Residual diagnostics**
		- Read residual patterns and connect each pattern to the assumption or model feature that may be wrong.
		- Study in [[Exam 1 - Regression Diagnostics and Leverage]].
	- **Type 10 — Leverage**
		- Understand and use $h_{ii}$, why extreme $x$ gives high leverage, the $4/n$ practice cutoff, and the derivation of the hat weights if derivations are in scope.
		- Study in [[Exam 1 - Regression Diagnostics and Leverage]].
	- **Type 11 — Interpret R output**
		- Read coefficient estimates, standard errors, $t$ statistics, $p$-values, $R^2$, residual standard error, and the $F$ line from `summary(lm())`.
		- Study in [[Exam 1 - Reading R Regression Output]].

1. **How the six study notes are grouped**
	- [[Exam 1 - Fitting a Simple Linear Regression]]
		- triage types 1 and 2
		- turns raw data into the fitted line
	- [[Exam 1 - Residual and Sum-of-Squares Proofs]]
		- triage types 3 and 4
		- develops the identities that make ANOVA and $R^2$ work
	- [[Exam 1 - Regression Estimator Properties]]
		- triage type 8 plus the estimator facts needed for inference
		- explains why the least-squares estimators have the means, variances, and covariance used later
	- [[Exam 1 - Regression Inference and ANOVA]]
		- triage types 5, 6, and 7
		- turns estimator uncertainty and sums of squares into tests, intervals, $R^2$, and $F$
	- [[Exam 1 - Regression Diagnostics and Leverage]]
		- triage types 9 and 10
		- checks whether the model and individual observations are trustworthy
	- [[Exam 1 - Reading R Regression Output]]
		- triage type 11
		- teaches how R packages the same quantities computed and derived by hand

1. **Recommended attack order**
	- **Pass 1 — Build the regression line from scratch**
		- do triage types 1 and 2
		- end goal: you should be able to go from a small table of $(x,y)$ values to $\hat y=\hat\beta_0+\hat\beta_1x$ without notes
	- **Pass 2 — Prove the identities that least squares forces**
		- do triage types 3 and 4
		- end goal: understand why the fitted residuals have the orthogonality properties used later
	- **Pass 3 — Understand the estimators as random variables**
		- do triage type 8 and the supporting estimator-property derivations
		- end goal: understand where the standard errors used in inference come from
	- **Pass 4 — Do inference and ANOVA**
		- do triage types 5, 6, and 7
		- end goal: move fluently between coefficient inference, sums of squares, $R^2$, and the ANOVA table
	- **Pass 5 — Diagnose the model**
		- do triage types 9 and 10
		- end goal: identify whether a problem is about unusual $y$, unusual $x$, model shape, nonconstant variance, normality, or influence
	- **Pass 6 — Read the same story from R**
		- do triage type 11
		- end goal: point to every major number in `summary(lm())` and explain what it means mathematically

1. **How to study each triage type**
	- **Relearn**
		- read the corresponding child note until you can explain the end goal in plain language
	- **Drill**
		- close the note and redo the derivation or computation cold on blank paper
		- if you get stuck, identify the exact step that failed rather than rereading the entire note
	- **Record**
		- after it clicks, say the method out loud in a short sequence of steps
		- the ideal explanation should tell you both **what to do** and **why that step moves you toward the final answer**

1. **Proof-heavy vs application-heavy triage**
	- Proof / derivation heavy
		- type 2: least-squares normal equations
		- type 3: residual identities
		- type 4: sum-of-squares decomposition
		- type 8: covariance / variance bilinearity
		- derivation portion of type 10: leverage weights
	- Computation / interpretation heavy
		- type 1: hand-compute regression
		- type 5: $R^2$
		- type 6: coefficient inference
		- type 7: ANOVA / $F$
		- type 9: residual plots
		- type 11: R output
	- The proof notes are still worth understanding even if the professor later says the exam is mostly application, because those proofs explain where the formulas used in the application problems come from.

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
