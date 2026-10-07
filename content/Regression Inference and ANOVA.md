## Concepts

- The fitted coefficients describe the sample, but inference makes statements about the population regression relationship. That needs an estimate of the error variance, standard errors for the estimators, a reference distribution, and a way to measure how much variation the regression explains — the goal is to move fluently among coefficient inference, $R^2$, and ANOVA instead of treating them as unrelated topics.
- **Estimate the error variance.** $RSS=\sum\hat e_i^2$; fitting two parameters costs two degrees of freedom, so $\boxed{S^2=MSE=\dfrac{RSS}{n-2}}$ and residual standard error $\boxed{S=\sqrt{MSE}}$.
- **Inference for the slope.** $SE(\hat\beta_1)=\dfrac{S}{\sqrt{S_{xx}}}$ (from [[Regression Estimator Properties]]). For $H_0:\beta_1=\beta_{1,0}$ vs. $H_a:\beta_1\neq\beta_{1,0}$, test statistic $\boxed{t=\dfrac{\hat\beta_1-\beta_{1,0}}{S/\sqrt{S_{xx}}}}$ on $t_{n-2}$. Common nulls: $\beta_1=0$ (any linear relationship at all?) and $\beta_1=1$ (same mechanics, just a different numerator). Reject for large $|t|$, equivalently for a small two-sided $p$-value.
- **Confidence interval for the slope.** $\hat\beta_1\pm t^*_{n-2}\,S/\sqrt{S_{xx}}$. Test–CI connection: a two-sided level-$\alpha$ test rejects $H_0:\beta_1=\beta_{1,0}$ exactly when $\beta_{1,0}$ falls outside the $(1-\alpha)100\%$ CI.
- **Inference for the intercept.** $SE(\hat\beta_0)=S\sqrt{\frac1n+\frac{\bar x^2}{S_{xx}}}$; same $t$ and CI machinery. Interpretation warning: the intercept is the expected response at $x=0$, which may be scientifically meaningless if $x=0$ is far outside the observed range.
- **Confidence interval for a mean response at $x_0$.** $\hat y_0=\hat\beta_0+\hat\beta_1x_0$; $SE_{mean}=S\sqrt{\frac1n+\frac{(x_0-\bar x)^2}{S_{xx}}}$; interval $\hat y_0\pm t^*_{n-2}SE_{mean}$. Narrowest near $\bar x$, since $(x_0-\bar x)^2$ is smallest there — the line is best pinned down at the center of the data.
- **Prediction interval for one new observation at $x_0$.** A new response carries two sources of uncertainty: the mean line's uncertainty *and* its own random error. $SE_{pred}=S\sqrt{1+\frac1n+\frac{(x_0-\bar x)^2}{S_{xx}}}$; interval $\hat y_0\pm t^*_{n-2}SE_{pred}$. The extra $1$ under the root is the new observation's irreducible error, so a prediction interval is always wider than the CI for the mean response at the same $x_0$.
- **$R^2$ from the decomposition.** $SST=SS_{reg}+RSS$ gives $\boxed{R^2=\dfrac{SS_{reg}}{SST}=1-\dfrac{RSS}{SST}}$, read as "$R^2\times100\%$ of the total sample variability in $Y$ is explained by the fitted regression on $x$." In SLR with an intercept, $R^2=r_{xy}^2$. What it does *not* tell you: it doesn't prove causation, and it doesn't verify linearity, normality, independence, or constant variance — a high $R^2$ can coexist with a badly misspecified model.
- **ANOVA table structure.** Regression row: SS $=SS_{reg}$, df $=1$, MS $=SS_{reg}$; residual row: SS $=RSS$, df $=n-2$, MS $=RSS/(n-2)$; total row: SS $=SST$, df $=n-1$. $\boxed{F=MS_{reg}/MSE}$.
- **Reconstructing a partially blank ANOVA table.** Get $n$ from the degrees of freedom (total df $=n-1$, residual df $=n-2$); use $SST=SS_{reg}+RSS$; use $MS_{reg}=SS_{reg}/1$ and $MSE=RSS/(n-2)$; use $F=MS_{reg}/MSE$; if $R^2$ is given, use $R^2=SS_{reg}/SST$ or $1-RSS/SST$.
- **Why the $F$-test and the slope $t$-test are the same test in SLR.** Since $\hat\beta_0=\bar y-\hat\beta_1\bar x$, $\hat y_i-\bar y=\hat\beta_1(x_i-\bar x)$, so $SS_{reg}=\sum(\hat y_i-\bar y)^2=\hat\beta_1^2S_{xx}$, and since regression df is $1$, $MS_{reg}=\hat\beta_1^2S_{xx}$. Then $F=\hat\beta_1^2S_{xx}/MSE=\hat\beta_1^2S_{xx}/S^2=\left(\hat\beta_1/(S/\sqrt{S_{xx}})\right)^2$ — the squared slope $t$-statistic under $H_0:\beta_1=0$. So $\boxed{F=t^2}$: in SLR the overall model test and the two-sided slope test carry the same information.

## Practice Problems

- **Problem 1 (HW1 Q8 — airfares: `Fare ~ Distance`, $n=17$).** Fitted line $\widehat{Fare}=48.9718+0.2197\,Distance$. Test $H_0:\beta_1=0$; give a 95% CI for $\beta_1$; report and interpret $R^2$ and the residual standard error; predict the fare for a 500-mile flight with a 95% prediction interval, checking first whether 500 lies in the observed range.
	- *Solution.*
		- $t_{obs}=\hat\beta_1/SE=0.219687/0.004421\approx49.69$ on $n-2=15$ df, $p\ll0.05$ — reject $H_0$, strong evidence of a positive linear association
		- 95% CI for $\beta_1$: $0.219687\pm2.131(0.004421)=(0.2103,0.2291)$, using $t^*_{0.025,15}=2.131$ — $0$ is far outside it, same conclusion as the test
		- $R^2=0.994$: distance explains about 99.4% of the variation in fare
		- residual standard error $=10.41$ on $15$ df: typical miss of about \$10.41
		- observed distances run 90 to 1828 miles, so $500$ is inside the range (interpolation, reliable)
		- fitted value at $500$: $48.9718+0.2197(500)\approx158.82$ — about \$158.82
		- 95% prediction interval $\approx(135.79,181.85)$ — about \$135.79 to \$181.85

- **Problem 2 (HW1 Q6 — mtcars: `mpg ~ wt`, $n=32$).** Fitted line $\widehat{mpg}=37.285-5.344\,wt$. Interpret the slope and intercept; report and interpret $R^2$.
	- *Solution.*
		- slope $-5.344$: each additional 1000 lbs of weight is associated with about $5.34$ fewer mpg, on average
		- intercept $37.285$: predicted mpg at $wt=0$, not meaningful since no real car weighs nothing and all observed weights are well above zero
		- $R^2=0.753$: weight explains about 75.3% of the variation in mpg
		- residual standard error $\approx3.05$ on $30$ df
		- $F=91.38$ on $1,30$ df, $p\approx1.3\times10^{-10}$

- **Problem 3 (Case Study A — `test2 ~ test1`, $n=100$, a non-zero null).** Test both $H_0:\beta_0=0$ (no bias) and $H_0:\beta_1=1$ (perfect agreement), and report $R^2$.
	- *Solution.*
		- intercept test (against $0$ by default): $t\approx1.65$, $p\approx0.103$ — no evidence of a constant offset
		- slope test against $1$ (not the default $0$, since the question is whether the relationship is proportional): $t_{obs}=(\hat\beta_1-1)/SE(\hat\beta_1)\approx-0.565$ on $98$ df, $p\approx0.573$ — fail to reject, no evidence the tests drift apart
		- 95% CI for the slope $\approx(0.891,1.060)$, which contains $1$
		- $R^2\approx0.843$: test1 explains about 84% of the variation in test2

- **Problem 4 — reconstruct a full ANOVA table and compare the two kinds of interval (Production data: `RunTime ~ RunSize`, $n=20$).** The SLR slides quote only the slope test ($\hat\beta_1=0.25924$, $SE=0.03714$, $t=6.98$, $p<0.0001$) for this dataset. Fill in the full ANOVA table, and find both a 95% CI for the mean response and a 95% prediction interval at $RunSize=200$.
	- *Solution.*
		- $F=t^2=6.98^2\approx48.72$ on $1,18$ df (matches $F=t^2$ above)
		- regression: SS $=12{,}868.4$, df $1$, MS $=12{,}868.4$
		- residual: SS $=4754.6$, df $18$, MS $=264.1$
		- total: SS $=17{,}623.0$, df $19$
		- $R^2=12{,}868.4/17{,}623.0\approx0.730$
		- at $RunSize=200$: fitted value $\hat y_0\approx201.60$
		- 95% CI for the mean response $\approx(193.96,209.23)$
		- 95% prediction interval for one new run $\approx(166.61,236.59)$ — visibly wider, exactly because it carries the extra $1$ under the square root for the new observation's own error
