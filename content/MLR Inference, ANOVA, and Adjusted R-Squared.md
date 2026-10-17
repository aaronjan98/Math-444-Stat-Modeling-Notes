## Concepts

- With $k$ predictors, the same $SST=SS_{reg}+RSS$ decomposition from [[Residual and Sum-of-Squares Proofs]] still holds — the orthogonality that makes the cross term vanish comes from the normal equations, which hold in matrix form exactly as they did in SLR.
	- $SST=\sum_i(Y_i-\bar Y)^2$, $SS_{reg}=\sum_i(\hat Y_i-\bar Y)^2$, $RSS=\sum_i(Y_i-\hat Y_i)^2$ — same three definitions, unchanged.
- **The MLR ANOVA table has the same three rows as SLR, but the degrees of freedom change to account for $k$ predictors instead of one.**
	- Regression row: df $=k$, SS $=SS_{reg}$, MS $=SS_{reg}/k$.
	- Residual row: df $=n-k-1$ (one degree of freedom lost per estimated slope, plus one for the intercept), SS $=RSS$, MS $=S^2=RSS/(n-k-1)=MSE$.
	- Total row: df $=n-1$, SS $=SST$.
	- Setting $k=1$ recovers every SLR formula from [[Regression Inference and ANOVA]] exactly — SLR is the $k=1$ special case of everything below.
- **The global $F$-test asks whether the predictors jointly explain anything at all**, the direct generalization of SLR's single slope test.
	- $H_0:\beta_1=\cdots=\beta_k=0$ (none of the predictors matter) against $H_a:$ at least one $\beta_j\neq0$.
	- $\boxed{F=\dfrac{SS_{reg}/k}{RSS/(n-k-1)}}$, compared against an $F_{k,n-k-1}$ distribution.
	- Why that distribution: under $H_0$, $SS_{reg}/\sigma^2\sim\chi^2_k$ and $RSS/\sigma^2\sim\chi^2_{n-k-1}$ independently, and the ratio of two independent $\chi^2$'s divided by their own degrees of freedom is exactly how an $F$ distribution is defined — the $\sigma^2$'s cancel in the ratio.
	- The test is always upper-tailed: a larger $F$ means more explained variation relative to leftover noise, which is evidence against $H_0$, not evidence in either direction the way a two-sided $t$-test is.
- **Given only $R^2$ (no ANOVA table), the global $F$ can still be recovered exactly — this is explicitly flagged as memorize-worthy.**
	- Start from $F=\dfrac{SS_{reg}/k}{RSS/(n-k-1)}$ and divide numerator and denominator by $SST$.
	- $SS_{reg}/SST=R^2$ and $RSS/SST=1-R^2$ (from $SST=SS_{reg}+RSS$), so the ratio becomes $\boxed{F=\dfrac{n-k-1}{k}\cdot\dfrac{R^2}{1-R^2}}$.
	- Given just $n$, $k$, and $R^2$, this reconstructs the overall model $F$ without ever seeing a sum of squares.
- **An individual coefficient's $t$-test is a *partial* test** — it asks whether that one predictor adds anything *given the others already in the model*, not whether it predicts $Y$ on its own.
	- $H_0:\beta_j=0$ against $H_a:\beta_j\neq0$, using $T_j=\hat\beta_j/SE(\hat\beta_j)\sim t_{n-k-1}$.
	- Interpreting $\hat\beta_j$ requires the phrase "holding the other predictors constant" (or equivalent) — stating only "$Y$ changes by $\hat\beta_j$ per unit increase in $X_j$" omits the conditional nature of the coefficient and is graded as incomplete (the professor's stated rule: 50% credit lost without it).
	- Why the condition matters algebraically: in $E(Y\mid X_1,X_2)=\beta_0+\beta_1X_1+\beta_2X_2$, comparing the expected response at $(X_1+1,X_2)$ versus $(X_1,X_2)$ cancels the intercept and the $\beta_2X_2$ term, leaving exactly $\beta_1$ — but only because $X_2$ was held fixed in that comparison.
- **$R^2$'s formula is unchanged from SLR, but with $k$ predictors it inherits a structural flaw: it can never decrease as predictors are added.**
	- $R^2=SS_{reg}/SST=1-RSS/SST$, same formula, same "proportion of total variability explained" interpretation.
	- Adding any column to $X$ — even pure noise — can only shrink or hold $RSS$ fixed, because least squares is still minimizing over a strictly larger search space; so $R^2$ can only rise or stay flat, never fall.
	- Carried to the extreme, $R^2\to1$ as the number of predictors approaches $n$, even if none of them are genuinely useful — which is exactly why plain $R^2$ alone can't be trusted to compare models of different sizes.
- **Adjusted $R^2$ fixes that by charging a penalty per predictor, which can make it fall even as plain $R^2$ rises.**
	- $\boxed{R^2_{adj}=1-\dfrac{RSS/(n-k-1)}{SST/(n-1)}}$ — each sum of squares divided by its own degrees of freedom before comparing.
	- Rewriting directly in terms of plain $R^2$, using $RSS/SST=1-R^2$: $\boxed{R^2_{adj}=1-\dfrac{n-1}{n-k-1}(1-R^2)}$.
	- The factor $\frac{n-1}{n-k-1}>1$ grows as $k$ increases — so for a *fixed* $R^2$, adding predictors alone inflates the penalty term and pulls $R^2_{adj}$ down; a predictor only keeps $R^2_{adj}$ from falling if its contribution to $R^2$ outweighs that growing penalty.
	- This is the full worked example behind "memorize these relationships": adding a predictor that barely moves $RSS$ increases $k$ (shrinking $n-k-1$) while barely changing $R^2$, so the penalty term grows faster than $(1-R^2)$ shrinks, and $R^2_{adj}$ drops.
- **Proof that $R^2_{adj}\le R^2$ always**, one of the "results proved in class" the exam's theoretical section draws from.
	- Want to show $1-\dfrac{n-1}{n-k-1}(1-R^2)\le1-(1-R^2)$.
	- Subtract $1$ from both sides and multiply by $-1$ (flips the inequality): $\dfrac{n-1}{n-k-1}(1-R^2)\ge(1-R^2)$.
	- Since $1-R^2\ge0$ always, this holds exactly when $\dfrac{n-1}{n-k-1}\ge1$, i.e. $n-1\ge n-k-1$, i.e. $k\ge0$ — always true.
	- So $R^2_{adj}\le R^2$ for every $k\ge0$, with equality only at $k=0$ (no predictors) or $R^2=1$ (a perfect fit, $RSS=0$).
- **$MSE$ and $R^2_{adj}$ are equivalent criteria for comparing models of different sizes** — minimizing one is the same as maximizing the other.
	- Rewriting $R^2_{adj}$ directly in terms of $MSE=RSS/(n-k-1)$: $R^2_{adj}=1-\dfrac{n-1}{SST}\cdot MSE$.
	- $SST$ and $n$ depend only on the response data, which doesn't change across models being compared on the same dataset — so $\dfrac{n-1}{SST}$ is a fixed positive constant for that comparison.
	- Since $R^2_{adj}$ is that fixed constant times $-MSE$ plus $1$, whichever model minimizes $MSE$ is automatically the one that maximizes $R^2_{adj}$ — same ranking, two different-looking numbers.

## Practice Problems

- **Problem 1 (`mtcars`, `mpg ~ disp + hp + drat + wt`, $n=32$) — full coefficient interpretation, ANOVA table, and global $F$.**
	- *Solution.*
		- fitted model: $\widehat{mpg}=29.149+0.0038\,disp-0.0348\,hp+1.768\,drat-3.480\,wt$
		- coefficient interpretation requires "holding the others fixed": e.g. holding `disp, drat, wt` fixed, each additional unit of `hp` is associated with about $0.0348$ fewer mpg, on average
		- individual $t$-tests: `hp` ($t=-3.00$, $p=0.006$) and `wt` ($t=-3.23$, $p=0.003$) are significant given the other three predictors; `disp` ($t=0.35$, $p=0.727$) and `drat` ($t=1.34$, $p=0.192$) are not
		- ANOVA table:

		| Source | df | SS | MS | F | p-value |
		|---|---|---|---|---|---|
		| Regression | $4$ | $918.72$ | $229.68$ | $34.82$ | $2.70\times10^{-10}$ |
		| Residual | $27$ | $182.84$ | $6.77$ | | |
		| Total | $31$ | $1101.56$ | | | |

		- global $F=34.82$ on $(4,27)$ df, $p\ll0.05$ — reject $H_0:\beta_{disp}=\beta_{hp}=\beta_{drat}=\beta_{wt}=0$; the four predictors jointly explain a significant amount of the variation in mpg, even though two of them are individually non-significant above
		- $R^2=0.838$, $R^2_{adj}=0.814$

- **Problem 2 (`mtcars`) — adjusted $R^2$ can fall even as plain $R^2$ rises; a concrete demonstration of the exam's "memorize" relationship.** Compare `mpg ~ hp + drat + wt` against the same model with the non-significant `disp` added back in.
	- *Solution.*
		- without `disp`: $R^2=0.8369$, $R^2_{adj}=0.8194$
		- with `disp` added: $R^2=0.8376$, $R^2_{adj}=0.8136$
		- plain $R^2$ ticked *up* by adding `disp` (as it always can), but $R^2_{adj}$ went *down* — `disp`'s own $t$-test above ($p=0.727$) already said it wasn't pulling its weight given the other three; the tiny drop in $RSS$ it buys isn't enough to offset losing a degree of freedom
		- this is exactly why the model-selection goal from [[Class Notes stat modeling 15.10.26]] is "maximize $R^2_{adj}$ / minimize $S$," not "maximize plain $R^2$"

- **Problem 3 — recover the global $F$ from $n$, $k$, and $R^2$ alone, no ANOVA table given.** Using Problem 1's model: $n=32$, $k=4$, $R^2=0.8376$.
	- *Solution.*
		- $F=\dfrac{n-k-1}{k}\cdot\dfrac{R^2}{1-R^2}=\dfrac{27}{4}\cdot\dfrac{0.8376}{0.1624}\approx34.82$
		- matches Problem 1's reported $F=34.82$ exactly — confirms the formula without ever touching a sum of squares

- **Problem 4 — derive $R^2_{adj}\le R^2$ from scratch, cold.** Show the inequality holds for every $k\ge0$.
	- *Solution.*
		- start from $R^2_{adj}=1-\dfrac{n-1}{n-k-1}(1-R^2)$ and $R^2=1-(1-R^2)$
		- want: $1-\dfrac{n-1}{n-k-1}(1-R^2)\le1-(1-R^2)$
		- subtract $1$ from both sides, multiply by $-1$ (flips the inequality): $\dfrac{n-1}{n-k-1}(1-R^2)\ge1-R^2$
		- since $1-R^2\ge0$, this reduces to $\dfrac{n-1}{n-k-1}\ge1$, which holds exactly when $n-1\ge n-k-1$, i.e. when $k\ge0$ — always true
		- so $R^2_{adj}\le R^2$ for all $k\ge0$, with equality only when $k=0$ or $R^2=1$
