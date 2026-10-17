## Concepts

- **A partial $F$-test asks whether a whole group of predictors can be dropped at once**, generalizing the individual coefficient $t$-test from one predictor to several simultaneously.
	- Suppose a model already has predictors $X_1,\ldots,X_p$ (the *reduced* model), and we're deciding whether to add $q$ more, $Z_1,\ldots,Z_q$ (together making the *full* model).
	- $H_0:$ all $q$ new coefficients are zero, given the existing predictors — the reduced model is adequate — against $H_a:$ at least one of them is nonzero.
	- $\boxed{F=\dfrac{(RSS_R-RSS_F)/q}{RSS_F/(n-p-q-1)}}\sim F_{q,\,n-p-q-1}$ under $H_0$, where the denominator degrees of freedom use the *full* model's parameter count.
	- Why divide the numerator by $q$: it converts the total improvement in fit into an average improvement *per added coefficient*, so adding more variables doesn't automatically look better just because there are more of them.
	- Adding and removing variables are the same comparison viewed from opposite directions — "does dropping these predictors hurt the fit" and "does adding these predictors help the fit" are the identical nested-model test.
- **For a single added predictor, the partial $F$-test is exactly the same test as its ordinary coefficient $t$-test**, just expressed as a ratio instead of a ratio-under-a-square-root.
	- With $q=1$, $F_{1,\nu}$ has the same distribution as $t_\nu^2$, so testing one coefficient's $t$ and testing it as a one-variable partial $F$ always agree, numerically $F=t^2$ and in conclusion.
	- The sign of $t$ disappears when squared, but the two-sided $t$-test and the (always upper-tailed) $F$-test give the identical $p$-value either way.
- **Equivalently, the partial $F$'s numerator can be written as an added regression sum of squares rather than a drop in RSS** — same quantity, different bookkeeping.
	- $RSS_R-RSS_F=SS_{reg}(Z_1,\ldots,Z_q\mid X_1,\ldots,X_p)=SS_{reg}(\text{full})-SS_{reg}(\text{reduced})$, since $SST=SS_{reg}+RSS$ holds for both models on the same response data.
	- Use whichever quantity is actually available in a given problem — residual sums of squares from two `summary()` calls, or sequential sums of squares straight out of an `anova()` table.
- **Type I (sequential) sums of squares attribute to each predictor only the *extra* variation it explains once the terms before it (in formula order) are already in the model.**
	- For formula order $X_1,X_2,X_3$: $SS_{reg}(X_1)$, then $SS_{reg}(X_2\mid X_1)=SS_{reg}(X_1,X_2)-SS_{reg}(X_1)$, then $SS_{reg}(X_3\mid X_1,X_2)=SS_{reg}(X_1,X_2,X_3)-SS_{reg}(X_1,X_2)$.
	- These successive differences telescope: every intermediate $SS_{reg}$ cancels when added up, so the three rows sum to exactly the full model's $SS_{reg}$ — this is why a Type I ANOVA table's rows always add to the total regression SS.
	- Order matters whenever predictors overlap in what they explain: whichever one enters first claims the shared variation, leaving less for the predictor that enters after it — so $SS_{reg}(X_2\mid X_1)\neq SS_{reg}(X_1\mid X_2)$ in general, even though the full model's total $SS_{reg}$ (and its fitted values) never change with formula order.
	- `anova(lm(y ~ x1 + x2 + x3))` in R reports exactly this sequential breakdown, in whatever order the formula lists the predictors.
- **Type III (added-last) sums of squares instead assess every predictor as if it entered after all the others**, which is a different question from Type I's running tally.
	- For predictor $X_2$ in a three-predictor model, compare the model with $X_1,X_3$ against the full model with $X_1,X_2,X_3$ — $X_2$'s contribution is measured *last*, no matter what order the formula lists terms in.
	- Unlike Type I, the separate added-last contributions generally do **not** sum to the full model's $SS_{reg}$ — they're independent conditional comparisons, not one running total.
	- For an ordinary continuous predictor with no interaction or rank-deficiency complications, this added-last one-coefficient test is exactly the predictor's own $t$-test in `summary(lm(...))`, and $F=t^2$ from above.
	- A Type I row can only be read as an added-last test for the *last* predictor actually entered in that formula order — reading an earlier row as "added-last" silently assumes an ordering that wasn't actually used.
- **In R, `anova()` on a single fitted model gives Type I; the added-last (Type III) comparison for one or several terms has to be built explicitly as two nested models.**
	- `anova(model)` → sequential SS in the formula's own order.
	- `anova(reduced, full)` → the partial $F$-test for exactly the terms present in `full` but missing from `reduced`, regardless of what order either formula lists its terms in.
	- `drop1(model, test="F")` → the added-last test for *every* predictor at once, each measured as if it alone were removed last from the full model.
	- The fitted values, $RSS$, and $R^2$ of a model never depend on the order predictors are listed in the formula — only each individual Type I row's sequential SS does.
- **Forward selection and backward elimination are Type I and Type III thinking turned into a model-building strategy**, not new statistical machinery.
	- Forward selection starts from an intercept-only model and repeatedly asks "does adding this predictor help, *given what's already in*" — the same question Type I's running sequence asks.
	- Backward elimination starts from every candidate predictor and repeatedly asks "does removing this predictor hurt, *given everything else stays in*" — the same question Type III's added-last view asks.
	- Neither procedure guarantees the single best model; repeated $p$-value-based selection on the same data also complicates how the resulting $p$-values should be interpreted afterward.
- **A fixed checklist for any nested-model ($t$, global $F$, or partial $F$) question, in the order the professor laid it out:** (1) state $H_0$ and $H_a$ precisely, including which predictors are held fixed; (2) write out the exact reduced and full models, intercepts included; (3) identify $q$ (predictors being tested) and the full model's residual df; (4) recover $RSS$ from $S^2\times df$ if only the residual standard error is given; (5) compute $F$ using the *full* model's $MSE$ in the denominator; (6) compare against the supplied critical value or compute the $p$-value; (7) state the conclusion conditional on the retained predictors, not as an unconditional claim about any one predictor alone.

## Practice Problems

- **Problem 1 (`mtcars`, testing whether `disp` and `drat` can be jointly dropped from the full model).** Reduced: $mpg\sim hp+wt$. Full: $mpg\sim disp+hp+drat+wt$.
	- *Solution.*
		- $H_0:\beta_{disp}=\beta_{drat}=0$ given `hp, wt` in the model; $H_a:$ at least one of them is nonzero
		- $q=2$ predictors tested, full model residual df $=27$
		- `anova(lm(mpg~hp+wt), lm(mpg~disp+hp+drat+wt))`: $RSS_R=195.05$, $RSS_F=182.84$
		- $F=\dfrac{(195.05-182.84)/2}{182.84/27}=\dfrac{6.105}{6.772}\approx0.90$ on $(2,27)$ df, $p=0.418$
		- fail to reject $H_0$ at $\alpha=0.05$ — no evidence that `disp` and `drat` jointly add anything once `hp` and `wt` are already in the model; this matches both predictors' individually non-significant $t$-tests in [[MLR Inference, ANOVA, and Adjusted R-Squared]] Problem 1

- **Problem 2 (`mtcars`) — sequential SS changes with formula order, but the total never does.** Compare `anova(lm(mpg ~ disp+hp+drat+wt))` against the same model fit as `lm(mpg ~ wt+drat+hp+disp)`.
	- *Solution.*
		- order `disp, hp, drat, wt`: sequential SS $=808.89,\ 33.67,\ 30.15,\ 70.51$ (each conditional on only the terms listed before it)
		- order `wt, drat, hp, disp`: sequential SS $=847.73,\ 9.08,\ 85.56,\ 0.84$ — completely different individual numbers
		- both orders sum to the same total, $808.89+33.67+30.15+70.51\approx847.73+9.08+85.56+0.84$ (rounding), which is the full model's $SS_{reg}$ either way
		- `disp`'s last-listed sequential SS in the second ordering, $0.84$, matches its added-last (Type III) contribution exactly — because it's genuinely entered last in that formula; `disp`'s *first*-listed sequential SS in the first ordering, $808.89$, is a completely different number asking a completely different question (how much `disp` explains on its own, before anything else is in the model)

- **Problem 3 (`mtcars`) — verify the added-last (Type III) sums of squares against each predictor's own $t$-test, confirming $F=t^2$ for every term at once.** Use `drop1(model1, test="F")` on the full model.
	- *Solution.*
		- `drop1` gives added-last $F$: `disp` $F=0.125$, `hp` $F=9.00$, `drat` $F=1.79$, `wt` $F=10.41$
		- squaring each coefficient's own $t$ from `summary(model1)`: $0.353^2=0.125$, $(-2.999)^2=9.00$, $1.340^2=1.80$, $(-3.227)^2=10.41$ — all four match their `drop1` $F$ exactly, confirming the added-last test for an ordinary continuous predictor is always the same test as its own coefficient $t$-test

- **Problem 4 (class example, homicide rate regressed on population $X_1$, income $X_2$, unemployment $X_3$ — numbers from the handout/class notes, already cross-checked there against `pf()`; the raw dataset isn't available locally to refit directly).** Given $X_3$ already in the model, are $X_1,X_2$ jointly significant? Reduced: $Y=\beta_0+\beta_3X_3+\epsilon$. Full: $Y=\beta_0+\beta_1X_1+\beta_2X_2+\beta_3X_3+\epsilon$.
	- *Solution.*
		- $H_0:\beta_1=\beta_2=0$ given $X_3$; $H_a:$ at least one of $\beta_1,\beta_2\neq0$
		- $q=2$, full model residual df $=16$ (three predictors, $n=20$: $df=20-3-1=16$)
		- entering $X_3$ first, the sequential SS for the other two are $SS_{reg}(X_2\mid X_3)\approx100.26$ and $SS_{reg}(X_1\mid X_2,X_3)\approx30.29$ — these can be added together into $SS_{reg}(X_1,X_2\mid X_3)\approx130.55$ precisely because $X_3$ was entered first, so both are conditional on at least $X_3$ already being in
		- $F=\dfrac{130.55/2}{337.06/16}\approx\dfrac{65.28}{21.07}\approx3.10$
		- $p=P(F_{2,16}\ge3.10)\approx0.073$ — fail to reject $H_0$ at $\alpha=0.05$: insufficient evidence that population and income jointly improve the model once unemployment is already in it
		- this doesn't contradict a highly significant *global* $F$ for all three predictors together — a model can explain significant overall variation while a specific conditional subset of its predictors contributes nothing further
