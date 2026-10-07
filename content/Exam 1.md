- **Exam:** Tuesday, October 20, 2026
	- Coverage: everything through **Chapter 3**, meaning simple linear regression through regression diagnostics. Box-Cox is out of scope.
	- Quick reference (notation, identities, assumptions): [[Formula and Identity Sheet]]

## Queue

- **1. [[Fitting a Simple Linear Regression]]** (hand-compute an SLR fit; derive the LSE / normal equations)
	- difficulty low–medium, Chapter 2

- **2. [[Residual and Sum-of-Squares Proofs]]** ($\sum\hat e_i=0$, $\sum x_i\hat e_i=0$, $\sum\hat y_i\hat e_i=0$; $SST=SS_{reg}+RSS$)
	- difficulty medium, Chapter 2

- **3. [[Regression Estimator Properties]]** (Cov/Var bilinearity: $E(\hat\beta_1)$, $\operatorname{Var}(\hat\beta_1)$, $\operatorname{Cov}(\hat\beta_0,\hat\beta_1)$ from the $c_i$ representation)
	- difficulty medium, Chapter 2

- **4. [[Regression Inference and ANOVA]]** ($R^2$; $t$-tests/CIs for the slope and intercept, including a nonzero null like $\beta_1=1$; ANOVA table; $F=t^2$)
	- difficulty medium, Chapter 2

- **5. [[Regression Diagnostics and Leverage]]** (residual-pattern recognition; leverage $h_{ii}$, the $4/n$ cutoff; standardized residuals; Cook's distance)
	- difficulty medium–high, Chapter 3

- **6. [[Reading R Regression Output]]** (translate `summary(lm())` / `anova()` / `confint()` back into the math — not a standalone question type, a presentation format the above could all appear in)
	- difficulty low–medium, Chapters 2–3
