- **Exam:** Tuesday, October 20, 2026
	- Coverage: Chapter 2 (through 2.7), Chapter 3 (3.1–3.3), and Chapter 5 (5.1–5.3) — **not** dummy variables or analysis of covariance (see [[Class Notes stat modeling 15.10.26]], which covers that material for reference only, not exam scope)
	- Format: 50% R output (given output, provide the interpretation — similar to homework), 20% multiple choice (conceptual), 30% theoretical (one part similar to homework-style problems, one part covering results proved in class, e.g. $R^2_{adj}\le R^2$)
	- **Allowed:** a formula sheet, any size — no size restriction given
	- **Memorize:** the $R^2$/adjusted $R^2$ relationships — $R^2=1-SSE/SST$, $R^2_{adj}=1-\dfrac{RSS/(n-p-1)}{SST/(n-1)}=1-\dfrac{n-1}{n-p-1}(1-R^2)$
	- Quick reference (notation, identities, assumptions): [[Formula and Identity Sheet]]

## Queue

1. **[[Fitting a Simple Linear Regression]]**
	- hand-compute an SLR fit; derive the LSE / normal equations

1. **[[Residual and Sum-of-Squares Proofs]]**
	- $\sum\hat e_i=0$, $\sum x_i\hat e_i=0$, $\sum\hat y_i\hat e_i=0$; $SST=SS_{reg}+RSS$

1. **[[Regression Estimator Properties]]**
	- Cov/Var bilinearity: $E(\hat\beta_1)$, $\operatorname{Var}(\hat\beta_1)$, $\operatorname{Cov}(\hat\beta_0,\hat\beta_1)$ from the $c_i$ representation

1. **[[Regression Inference and ANOVA]]**
	- $R^2$; $t$-tests/CIs for the slope and intercept, including a nonzero null like $\beta_1=1$; ANOVA table; $F=t^2$

1. **[[Regression Diagnostics and Leverage]]**
	- residual-pattern recognition; leverage $h_{ii}$, the $4/n$ cutoff; standardized residuals; Cook's distance

1. **[[Reading R Regression Output]]**
	- translate `summary(lm())` / `anova()` / `confint()` back into the math — not a standalone question type, a presentation format the above could all appear in

1. **[[Class Notes stat modeling 15.10.26]]** (Model Selection and Adjusted $R^2$ section)
	- adjusted $R^2$ vs. plain $R^2$; why adjusted $R^2$ exists; $R^2_{adj}\le R^2$ proof; comparing models of different sizes
