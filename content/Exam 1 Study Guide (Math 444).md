# Exam 1 Study Guide (Math 444)

- Parent / exam map: [[Exam 1]]
- This note is the **study map** for Exam 1.
	- The detailed derivations, worked examples, proofs, and recognition strategies live in the six linked child notes below.
	- Each child note is designed to be self-contained so it can be studied independently.

1. **Study notes**
	- [[Exam 1 - Fitting a Simple Linear Regression]]
		- Triage 1: hand-compute an SLR fit
		- Triage 2: derive the LSE / normal equations
	- [[Exam 1 - Residual and Sum-of-Squares Proofs]]
		- Triage 3: residual-property proofs
		- Triage 4: prove $SST=SS_{reg}+RSS$
	- [[Exam 1 - Regression Estimator Properties]]
		- Triage 8: covariance / variance bilinearity proof
		- also supplies the estimator means and variances needed for inference
	- [[Exam 1 - Regression Inference and ANOVA]]
		- Triage 5: $R^2$
		- Triage 6: inference on slope / intercept
		- Triage 7: ANOVA / $F$ test
		- also includes mean-response confidence intervals and individual prediction intervals
	- [[Exam 1 - Regression Diagnostics and Leverage]]
		- Triage 9: residual diagnostics
		- Triage 10: leverage
		- also connects residual size, leverage, standardized residuals, and Cook's distance
	- [[Exam 1 - Reading R Regression Output]]
		- Triage 11: interpret `summary(lm())`
		- also maps common R functions back to the by-hand quantities

1. **The whole course story in one chain**
	- **Model**
		- $\displaystyle Y_i=\beta_0+\beta_1x_i+\varepsilon_i.$
	- **Fit**
		- choose $\hat\beta_0,\hat\beta_1$ that minimize squared residuals
	- **Residuals**
		- $\displaystyle \hat e_i=y_i-\hat y_i$
		- least squares forces important residual identities
	- **Estimator uncertainty**
		- $\hat\beta_0$ and $\hat\beta_1$ are random because they depend on random responses $Y_i$
		- their variances become the standard errors used in $t$ inference
	- **Variation decomposition**
		- $\displaystyle SST=SS_{reg}+RSS$
		- this produces $R^2$ and the ANOVA table
	- **Diagnostics**
		- residual patterns test whether the fitted straight-line model is reasonable
		- leverage measures how unusual an observation's predictor value is
	- **R output**
		- `summary(lm())` reports the same estimates, standard errors, tests, $R^2$, residual scale, and $F$ test produced by the theory

1. **Core notation**
	- Observed data: $(x_i,y_i)$ for $i=1,\dots,n$
	- Sample means
		- $\displaystyle \bar x=\frac1n\sum_{i=1}^n x_i$
		- $\displaystyle \bar y=\frac1n\sum_{i=1}^n y_i$
	- Centered sums
		- $\displaystyle S_{xx}=\sum_{i=1}^n(x_i-\bar x)^2$
		- $\displaystyle S_{xy}=\sum_{i=1}^n(x_i-\bar x)(y_i-\bar y)$
	- Least-squares estimators
		- $\displaystyle \hat\beta_1=\frac{S_{xy}}{S_{xx}}$
		- $\displaystyle \hat\beta_0=\bar y-\hat\beta_1\bar x$
	- Fitted value and residual
		- $\displaystyle \hat y_i=\hat\beta_0+\hat\beta_1x_i$
		- $\displaystyle \hat e_i=y_i-\hat y_i$

1. **Core identities that connect the notes**
	- Least squares / normal equations imply
		- $\displaystyle \sum\hat e_i=0$
		- $\displaystyle \sum x_i\hat e_i=0$
		- $\displaystyle \sum\hat y_i\hat e_i=0$
	- Those identities make the cross term vanish in
		- $\displaystyle SST=SS_{reg}+RSS$
	- The decomposition gives
		- $\displaystyle R^2=\frac{SS_{reg}}{SST}=1-\frac{RSS}{SST}$
	- Residual variation estimates $\sigma^2$
		- $\displaystyle S^2=MSE=\frac{RSS}{n-2}$
	- Slope uncertainty is
		- $\displaystyle \operatorname{SE}(\hat\beta_1)=\frac{S}{\sqrt{S_{xx}}}$
	- Therefore the slope test statistic is
		- $\displaystyle t=\frac{\hat\beta_1-\beta_{1,0}}{S/\sqrt{S_{xx}}}$
	- In SLR, the overall regression $F$ test for $H_0:\beta_1=0$ satisfies
		- $\displaystyle F=t^2$

1. **Model assumptions to remember**
	- The mean response is linear in $x$.
	- Errors have mean zero.
		- $\displaystyle E(\varepsilon_i)=0$
	- Errors have constant variance.
		- $\displaystyle \operatorname{Var}(\varepsilon_i)=\sigma^2$
	- Errors are independent.
	- For the exact small-sample $t$ and $F$ inference used in class, errors are normally distributed.
		- $\displaystyle \varepsilon_i\sim N(0,\sigma^2)$

1. **Highest-priority cold-recall targets**
	- Derive $\hat\beta_1=S_{xy}/S_{xx}$ and $\hat\beta_0=\bar y-\hat\beta_1\bar x$ from SSE.
	- Prove the three residual identities without looking.
	- Prove $SST=SS_{reg}+RSS$ and explicitly identify why the cross term is zero.
	- Derive $E(\hat\beta_1)$ and $\operatorname{Var}(\hat\beta_1)$ from the $c_i$ representation.
	- Derive $\operatorname{Cov}(\hat\beta_0,\hat\beta_1)$ using bilinearity.
	- Complete an ANOVA table from partial information.
	- Explain why the prediction interval is wider than the confidence interval for the mean response.
	- Derive the leverage formula from $\hat y_i=\sum_jh_{ij}y_j$ if derivations are in scope.
	- Read every major line of `summary(lm())` and connect it to a by-hand formula.

1. **Professor-specific emphasis / exclusions**
	- Know how to fill in an ANOVA table.
	- Do not spend exam-prep time focusing on Box-Cox transformations.
	- No dummy-variable material or material that was not covered.
