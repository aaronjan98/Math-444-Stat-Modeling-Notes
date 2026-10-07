- Problem types covered
	- **Type 9:** residual diagnostics — read the plot
	- **Type 10:** leverage

## Concepts

- Regression calculations always produce a fitted line, even when a straight-line model is wrong. Diagnostics ask whether the assumptions behind that line and its inference are believable, and whether individual observations have unusual predictor values or disproportionate influence. End goal: look at a plot or an observation and identify exactly what kind of problem it represents.
- **Why residuals diagnose the unobserved errors.** True model $Y_i=\beta_0+\beta_1x_i+\varepsilon_i$; residual $\hat e_i=Y_i-\hat Y_i$. If the fitted line is close to the true mean line, $\hat Y_i\approx\beta_0+\beta_1x_i$, so $\hat e_i\approx\varepsilon_i$. We can't observe the true errors; residuals are our observable stand-ins for them.
- A healthy residual plot: roughly random scatter around $0$, no systematic curvature, no trend with $x$ or fitted values, roughly constant vertical spread. A few moderate residuals are expected — the issue is systematic structure.
- Residual-pattern recognition: curvature (U or inverted-U) suggests the mean function isn't linear; a funnel shape suggests nonconstant variance; an isolated large vertical residual suggests a response outlier; runs/clusters suggest dependence if observations are ordered; a Q-Q plot bending away from a line suggests non-normality.
- **Why fitting a line to a quadratic relationship leaves a residual pattern.** If the truth is $Y_i=\beta_0+\beta_1x_i+\beta_2x_i^2+\varepsilon_i$ but we fit only $\hat Y_i\approx\beta_0+\beta_1x_i$, the residual is $\hat e_i\approx\beta_2x_i^2+\varepsilon_i$ — it still carries a systematic $x_i^2$ term, which is why curvature shows up. General principle: a pattern in the residuals means the model failed to explain a systematic part of the response.
- **Normality diagnostic (Q-Q plot).** Plot the ordered standardized residuals against the expected order statistics from a standard normal. Close to a straight line is consistent with normality; systematic bending is evidence against it. How the order-statistic/quantile matching works: with $n$ points, the $k$-th smallest value lines up roughly against the $k/n$ quantile of the normal — e.g. with $n=200$, the 6th-smallest point sits near the $6/200=3$rd percentile. (E.g. $\mathrm{qnorm}(0.025)=-1.96$.) `plot(m)` in R produces four such diagnostic panels by default: residuals vs. fitted (model shape), Q-Q (normality), a scale-location plot (constant variance, using $\sqrt{|r_i|}$), and residuals vs. leverage.
- **Constant-variance diagnostic.** Inspect residuals (or standardized residuals — preferred when high-leverage points exist, since raw residuals have nonconstant variance even when the errors don't) against fitted or predictor values. Warning sign: the cloud widens or narrows as fitted values increase. Fix: transform. A common rule of thumb is a square-root transform on *both* variables, $\sqrt y=\alpha+\beta\sqrt x$ (not just $y$) — e.g. the professor's crews-vs-rooms-cleaned example. Box–Cox is a more general transform but is out of scope here.
- **What leverage measures.** A residual asks whether the *response* is unusual at its $x$; leverage asks whether the *predictor value itself* is unusual relative to the other $x$'s. In SLR, $\boxed{h_{ii}=\frac1n+\frac{(x_i-\bar x)^2}{S_{xx}}}$ — smallest near $\bar x$, grows as $x_i$ moves away, and depends only on the $x$'s, never on $y_i$.
- **Derive the leverage / hat-matrix weights.** Start from $\hat y_i=\bar y+\hat\beta_1(x_i-\bar x)$. Write $\bar y=\sum_j\frac1ny_j$ and $\hat\beta_1=\frac1{S_{xx}}\sum_j(x_j-\bar x)y_j$. Substitute both and combine into one sum: $\hat y_i=\sum_j\left[\frac1n+\frac{(x_i-\bar x)(x_j-\bar x)}{S_{xx}}\right]y_j$. Define $\boxed{h_{ij}=\frac1n+\frac{(x_i-\bar x)(x_j-\bar x)}{S_{xx}}}$, so $\hat y_i=\sum_jh_{ij}y_j$ — every fitted value is a weighted sum of *all* observed responses — and the observation's own weight is $h_{ii}$ (set $j=i$).
- **Why the leverages sum to 2 in SLR.** $\sum h_{ii}=\sum\frac1n+\frac1{S_{xx}}\sum(x_i-\bar x)^2=1+1=2$. So average leverage is $2/n$, and the $2$ corresponds to the two fitted coefficients (intercept and slope).
- **High-leverage flag.** Rule of thumb: flag $i$ when $h_{ii}$ exceeds twice the average, $\boxed{h_{ii}>2\times\frac2n=\frac4n}$. This is a screening rule, not a theorem — a high-leverage point can lie exactly on the fitted trend.
- **Why raw residuals have different variances.** $\operatorname{Var}(\hat e_i)=\sigma^2(1-h_{ii})$ — residuals at high-leverage points have artificially small variance (as $h_{ii}\to1$, $\operatorname{Var}(\hat e_i)\to0$), even under constant error variance. Standardized residual: $\boxed{r_i=\dfrac{\hat e_i}{S\sqrt{1-h_{ii}}}}$, where $S=\sqrt{RSS/(n-2)}$. $r_i$ is the residual in units of its own estimated standard deviation; flag $|r_i|>2$.
- **Outlier vs. leverage vs. influence.** Large residual = unusual $y$ given its $x$. High leverage = unusual $x$. Influential = removing the point substantially changes the fit. A point can have high leverage and lie right on the trend (harmless); a point can have a large residual at an ordinary $x$; a point with both is especially capable of being influential.
- **Cook's distance.** Combines outlyingness and leverage into one influence number: leave-one-out form $D_i=\dfrac{\sum_j(\hat y_{j(i)}-\hat y_j)^2}{2S^2}$ (remove observation $i$, refit, measure how far *all* the fitted values moved), equal to the computational shortcut $\boxed{D_i=\dfrac{r_i^2}{2}\cdot\dfrac{h_{ii}}{1-h_{ii}}}$ — large from a big $r_i$, a big $h_{ii}$, or both. Flag $D_i>\dfrac{4}{n-2}$. Using Cook's distance to judge influence relies on the errors being normal, since that's what makes the standardized residual inside it meaningful.
- Exam recognition map: curved residual plot → wrong functional form; fan/funnel → nonconstant variance; Q-Q with systematic bends → possible nonnormality; one point far vertically → response outlier; one point far horizontally → high leverage; both at once → potentially influential, check Cook's distance.

## Practice Problems

- **Problem 1 — leverage (Huber data, `YBad`, $n=6$).** Predictor values $x=-4,-3,-2,-1,0,10$. Compute each $h_{ii}$ and flag any leverage points against the $4/n$ cutoff.
	- *Solution.*
		- $\bar x=0$, $S_{xx}=130$
		- hat values: $0.2897,0.2359,0.1974,0.1744,0.1667,0.9359$ (sum $=2.0$, confirming the sum-to-2 rule)
		- cutoff $4/6\approx0.667$
		- only $x_6=10$ exceeds it ($h_{66}=0.9359$) — a clear high-leverage point, matching the slides

- **Problem 2 — standardized residuals and Cook's distance on the same data.** Using the Huber `YBad` fit, compute the standardized residuals and Cook's distances, and decide whether point 6 is a *bad* leverage point.
	- *Solution.*
		- standardized residuals: $1.597,0.308,-0.195,-1.129,-0.981,1.902$ — point 6's $|r_6|=1.90$ is just under the $|2|$ flag on its own
		- Cook's distances: $0.520,0.015,0.005,0.135,0.096,26.40$ — $D_6\approx26.4$ is enormous against the cutoff $4/(n-2)=1$
		- teaching point: the standardized residual alone almost misses point 6, but Cook's distance (which also weights in $h_{66}/(1-h_{66})$) flags it unmistakably as a bad leverage point

- **Problem 3 — applying the cutoff on a bigger dataset (bonds data, $n=35$).** The cutoff is $4/35\approx0.11$. Cases 4, 5, 13, and 35 have leverage values above $0.11$. What does this tell you, and what would you check next?
	- *Solution.*
		- these four cases are flagged as leverage points purely from having unusual $x$ (coupon rate) values — three are the left-most points and one is the right-most point in the scatterplot
		- leverage alone doesn't say they're *bad*
		- next step: check their standardized residuals (or Cook's distance) to see whether their $y$-values also break the pattern, before considering removing or refitting around them
