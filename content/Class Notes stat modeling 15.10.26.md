- **Midterm scope (test Tuesday, October 20, 2026):** chapters 2, 3, and 5 — but not everything in them. **Dummy variables and ANCOVA (today's material, second half of this note) are excluded** from this midterm; they're included here for completeness, not exam prep.

	- Sections explicitly covered: 2.7; 3.1 and 3.2 (expect R output with a bad/problematic result to identify — regression diagnostics, see [[Regression Diagnostics and Leverage]]); 3.3, transformations.

	- Transformation example for non-constant variance: suppose we fit $\sqrt{Y}=\beta_0+\beta_1X$ instead of $Y=\beta_0+\beta_1X$, then check whether the residual plot shows the non-constant-variance (funnel) problem resolved. This is the same square-root-transformation fix described in [[Regression Diagnostics and Leverage]].

	- Chapter 5 (MLR): covered up through 5.1, 5.2, 5.3 — where the class stopped, so that's the chapter 5 cutoff for the midterm.

- **Midterm format:** 50% R output, 20% multiple choice, 30% theoretical.

	- **50% output:** R output is given, and we provide the interpretation (not run the computation from scratch); expect to calculate values similar to the homework. Topics named explicitly: confidence intervals, hypothesis testing, interpretation of $R^2$, filling in the ANOVA table.

	- **20% multiple choice:** conceptual.

	- **30% theoretical:** two flavors — one similar to homework-style problems, the other covering results proved in class (e.g. the $R^2_{adj}\le R^2$ proof below).

	- Specifically flagged: if a model is wrong (misspecified), how does that affect the residuals? This is the same idea as the quadratic-omitted-term example in [[Regression Diagnostics and Leverage]] — fitting a straight line when the truth has an extra polynomial term leaves a systematic pattern in the residuals.

	- Study tip given: for a case like true-quadratic-but-fit-linear, create the R output yourself and then answer good textbook questions against that output, as practice.

	- A formula sheet is allowed on the exam — size doesn't matter.

- **Memorize** (explicitly flagged): the $R^2$/adjusted $R^2$ relationships — $R^2=SS_{reg}/SST=1-SSE/SST$, $R^2_{adj}=1-\dfrac{RSS/(n-p-1)}{SST/(n-1)}$, and the rewrite $R^2_{adj}=1-\dfrac{n-1}{n-p-1}(1-R^2)$.

- **Grading rule for interpreting any coefficient**, e.g. in $Y=\beta_0+\beta_1X_1+\beta_2X_2$: saying "$Y$ increases/decreases by $\beta_1$ per one-unit increase in $X_1$" is not enough on its own. You must explicitly state that the other variables are held constant — otherwise it's 50% credit on that question.

## Model selection and adjusted $R^2$

- **The goal of this section is model selection: building the best *overall* model**, not just checking whether one predictor still matters.

	- Partial $t$- and $F$-tests (is $X_1$ significant given $X_2$ is already in the model?) only answer a narrow question, one variable at a time.

	- Including a weak predictor doesn't just fail to help — it can actively hurt the model, so a variable that isn't pulling its weight should be identified and removed, not just tolerated.

- **$R^2$, by its original definition, is the proportion of total variation explained by the regression:**

	- $R^2=\dfrac{SS_{reg}}{SST}$

	- Since $SST=SS_{reg}+SSE$ (where $SSE$ is the residual/error sum of squares, same thing as $RSS$), $SS_{reg}=SST-SSE$, which gives the more commonly used form:
	$$R^2=\frac{SS_{reg}}{SST}=\frac{SST-SSE}{SST}=1-\frac{SSE}{SST}$$

- **Why adjusted $R^2$ exists.** Plain $R^2$ can only increase, or at best stay flat, as more predictors are added — even a completely useless one — because adding any column can only reduce $SSE$, never increase it.

	- That means plain $R^2$ rewards padding a model with junk variables, and on its own can't tell a useful predictor apart from a useless one once models differ in size.

	- Adjusted $R^2$ fixes this by also adjusting for sample size $n$ and the number of predictors $p$:
	$$R^2_{adj}=1-\frac{RSS/(n-p-1)}{SST/(n-1)}$$

	- Each piece is divided by its own degrees of freedom: $RSS/(n-p-1)=S^2$ is the unbiased estimate of $\sigma^2$, and $SST/(n-1)$ is the unbiased estimate of $\operatorname{Var}(Y_i)$.

	- Adding a predictor costs a degree of freedom in the numerator ($n-p-1$ shrinks) regardless of whether $RSS$ actually drops by much — which is exactly how an unhelpful predictor can drag adjusted $R^2$ down even while plain $R^2$ ticks up.

- **Rewriting adjusted $R^2$ directly in terms of plain $R^2$.** Since $RSS/SST=1-R^2$:
$$R^2_{adj}=1-\frac{RSS/(n-p-1)}{SST/(n-1)}=1-\frac{n-1}{n-p-1}\cdot\frac{RSS}{SST}=1-\frac{n-1}{n-p-1}\left(1-R^2\right)$$

	- This makes the penalty explicit: $\frac{n-1}{n-p-1}$ is always $>1$ and grows as $p$ increases, inflating $(1-R^2)$'s contribution the more predictors are in the model.

	- If $p$ increases while the error ($RSS$, hence plain $R^2$) stays exactly the same — the new predictor is genuinely useless — adjusted $R^2$ necessarily **decreases**, since the penalty factor grows while $(1-R^2)$ doesn't shrink to compensate.

- **Proof that $R^2_{adj}\le R^2$ always** (an aside worked through in class).

	- Want: $1-\dfrac{n-1}{n-p-1}(1-R^2)\le 1-(1-R^2)$.

	- Subtract $1$ from both sides and multiply by $-1$ (flips the inequality): $\dfrac{n-1}{n-p-1}(1-R^2)\ge(1-R^2)$.

	- Since $1-R^2\ge0$, this holds exactly when $\dfrac{n-1}{n-p-1}\ge1$, i.e. $n-1\ge n-p-1$, i.e. $p\ge0$ — always true.

	- So $R^2_{adj}\le R^2$ for any $p\ge0$, with equality only when $p=0$ (no predictors) or $R^2=1$ (a perfect fit, $RSS=0$).

- **Adjusted $R^2$ and $\operatorname{MSE}$ are equivalent criteria for comparing models of different sizes.**

	- $\operatorname{MSE}=RSS/(n-p-1)$, and rewriting adjusted $R^2$ directly in terms of it: $R^2_{adj}=1-\dfrac{n-1}{SST}\cdot\operatorname{MSE}$.

	- $SST=\sum(y_i-\bar y)^2$ and $n$ depend only on the response data $y$, not on which predictors are in a given model, so $\dfrac{n-1}{SST}$ is a fixed constant across every model being compared on the same data.

	- So $\operatorname{MSE}$ and $R^2_{adj}$ differ only by that constant and a sign flip: whichever model minimizes $\operatorname{MSE}$ also maximizes $R^2_{adj}$.

	- Worked example: model $A$ has $\operatorname{MSE}=1$, model $B$ has $\operatorname{MSE}=2$. Model $A$ is preferred — it has less error — and correspondingly $R^2_{adj}(A)>R^2_{adj}(B)$, the two criteria always agree.

- **Rule of thumb:** when comparing models with the *same* number of predictors, plain $R^2$ is a fine comparison. Once the two models being compared have *different* numbers of predictors, switch to adjusted $R^2$ (prefer higher) or $S=\sqrt{\operatorname{MSE}}$ (prefer lower) instead.

- **The "variables added last" procedure** is one concrete way to put this to use:

	1. Enter the full pool of candidate predictors into the model.
	2. Assess each variable's worthiness as if it were entered last, i.e. controlling for every other variable already present.
	3. Remove the weakest one, if it isn't pulling its weight.
	4. Refit, and reassess every remaining variable as added-last again.
	5. Repeat until every remaining variable is important.

- **Worked example — single-predictor models.** Predicting a city's homicide rate ($Y$, $n=20$) from three candidate predictors: population ($X_1$), income ($X_2$), unemployment rate ($X_3$). Fitting each alone:

	- $Y\sim X_1$: $R^2\approx0.0045$, adjusted $R^2\approx-0.0508$ — population alone explains almost nothing, and the penalty for using up even one predictor pushes adjusted $R^2$ **negative**.

	- $Y\sim X_2$: $R^2\approx0.7052$, adjusted $R^2\approx0.6889$.

	- $Y\sim X_3$: $R^2\approx0.748$, adjusted $R^2\approx0.7339$ — the strongest single predictor.

	- Ranking by adjusted $R^2$: $X_3$ (unemployment) strongest, $X_2$ (income) close behind, $X_1$ (population) essentially useless alone.

- **Worked example — two-predictor models.** Fitting $Y\sim X_1+X_3$ gives $R^2=0.7672$, adjusted $R^2=0.7398$ — up from $X_1$ alone's $R^2\approx0.0045$.

	- The sequential sum-of-squares breakdown (`aov()`): $X_1$'s own contribution is just $8.3525$, while $X_3$ contributes $1414.8795$, out of a regression total of $1423.23$ — almost all the explained variation comes from $X_3$.

	- $X_1$ is still contributing almost nothing even with $X_3$ already in the model.

	- The same pattern shows up pairing $X_1$ with $X_2$ instead: $X_1$'s sequential SS stays at $8.3525$, $X_2$ contributes $1309.4459$.

	- $X_1$ is weak no matter which other predictor it's paired with — this is exactly why plain $R^2$ alone can't flag $X_1$ as unhelpful (it ticks up slightly either way), while adjusted $R^2$'s penalty is what actually discriminates a useful predictor from a useless one.

## Dummy variables and analysis of covariance (ANCOVA)

*Not covered on Exam 1 — reference material only.*

- **Framing:** we already have a model with a continuous variable, and want to study whether we should add a categorical variable to it. In R-style formula notation: $Y\sim X+G$, one continuous variable $X$ and one categorical variable $G$.

- **A dummy variable** is a variable that takes a finite number of values, used to code the categories ("levels") of a categorical variable for use in a regression model.

	- **An indicator variable** is the simplest kind: $1$ for membership in one particular category, $0$ otherwise.

- **Example: gender.** If $Y=$ starting salary and the predictor is gender (male/female), how do we express $Y$ in terms of gender?

	- Text category labels (e.g. "female," "male") can't go directly into a regression — gender has to be encoded as an indicator variable first.

	- With two levels, only **one** indicator is needed: $I=1$ for Female, $I=0$ for Male. Using a second indicator for the other level would be redundant, since knowing one tells you the other.

	- **General rule:** a categorical variable with $k$ levels gets $k-1$ dummy variables, with one level left out as the baseline.

	- This connects back to comparing two population means (the two-sample test): coding gender as a single $0/1$ indicator and regressing on it is exactly the regression version of a two-sample mean comparison. With three or more groups, the analogous classical tool is ANOVA — and that comparison can be done with regression too, using $k-1$ indicators instead.

- **Example: house price with a 3-level location variable.** $Y=$ price of house, $X=$ area footage, $D=$ location, coded $0=$ in town, $1=$ inner suburb, $2=$ outer suburb.

	- **Wrong approach #1:** treat $D$ as an ordinary numeric predictor, $\mu_{Y|X,D}=\beta_0+\beta_1X+\beta_2D$. Wrong, because it forces a constant per-unit effect $\beta_2$ as $D$ goes $0\to1\to2$, treating category labels as if they were an ordered numeric scale.

	- Convert $D$ into 3 indicators instead: $I_0=1$ if in town, $I_1=1$ if inner suburb, $I_2=1$ if outer suburb (each $0$ otherwise).

	- **Wrong approach #2:** use all 3 indicators together with the intercept, $\mu=\beta_0+\beta_1X+\beta_2I_0+\beta_3I_1+\beta_4I_2$. Also wrong — exactly one of the three indicators is always $1$ (the other two are $0$), so $I_0+I_1+I_2=1$ always, making the intercept and all three indicators redundant together.

	- **The fix:** drop one indicator (here, $I_0$, so in-town becomes the baseline) and use only $k-1=2$.

- **Model assuming parallelism** (same slope across groups, different intercepts): $\mu_{Y|X,I_1,I_2}=\beta_0+\beta_1X+\beta_2I_1+\beta_3I_2$

	- Substituting each group's indicator values collapses the formula into that group's own line:
		- in town ($I_1=0,I_2=0$): $\mu_{Y|X}=\beta_0+\beta_1X$
		- inner suburb ($I_1=1,I_2=0$): $\mu_{Y|X}=(\beta_0+\beta_2)+\beta_1X$
		- outer suburb ($I_1=0,I_2=1$): $\mu_{Y|X}=(\beta_0+\beta_3)+\beta_1X$

	- "Parallelism" means all three groups share the same slope $\beta_1$ — three parallel lines, just shifted up or down.

	- $\beta_2$'s interpretation: the shift in mean price between inner-suburb and in-town homes, holding area $X$ fixed. ($\beta_3$ is the analogous shift for outer suburb.)

	- **Key takeaway:** the three lines being parallel but *shifted* means location matters. If location didn't matter at all, $\beta_2=\beta_3=0$ and all three lines would collapse onto one single line.

- **Model with interaction terms** (allowing different slopes too, not just different intercepts): $\mu_{Y|X,I_1,I_2}=\beta_0+\beta_1X+\beta_2I_1+\beta_3I_2+\beta_4(I_1X)+\beta_5(I_2X)$

	- The terms $I_1X$ and $I_2X$ (indicator multiplied by the continuous variable) are called **interaction** terms — they let the effect of $X$ on $Y$ depend on, interact with, which group a point belongs to.

	- Substituting each group's indicator values the same way as before:
		- in town: $\mu_{Y|X}=\beta_0+\beta_1X$
		- inner suburb: $\mu_{Y|X}=(\beta_0+\beta_2)+(\beta_1+\beta_4)X$
		- outer suburb: $\mu_{Y|X}=(\beta_0+\beta_3)+(\beta_1+\beta_5)X$

	- $\beta_4$'s interpretation: the difference in slope between inner-suburb and in-town homes.

	- Unlike the parallelism model, the three lines are no longer forced to share a slope — so they can intersect, which is the geometric picture behind calling these "interaction" terms.

	- **Visual intuition:** plotting $Y$ versus $X$ alone, without separating by location, can look like a meaningless scatter or several disconnected clusters — fitting one line to all of it doesn't make sense, because there are really several populations hiding inside the data, one per location.

- **Four geometric cases worth recognizing on a scatterplot of $Y$ vs. $X$, split by group:**

	- **Parallel lines** (equal slopes, unequal intercepts) — location shifts the intercept only.

	- **Equal intercepts, unequal slopes** — all groups start from the same point but fan out at different angles.

	- **Unequal slopes, unequal intercepts** — the general interaction-model picture; lines can cross anywhere.

	- **Coincident lines** (equal slopes, equal intercepts) — all groups share one single line; location doesn't matter at all.

- **A staged decision procedure for testing which case you're in**, starting from the full interaction model:

	1. Test $H_0:\beta_4=\beta_5=0$ (no interaction) against $H_A$: at least one nonzero.
		- **Reject** → the slopes genuinely differ; stop here and keep the full interaction model.
		- **Fail to reject** → drop the interaction terms, move to the parallelism model, and continue.
	2. Within the parallelism model, test $H_0:\beta_2=\beta_3=0$ (same intercept) against $H_A$: at least one nonzero.
		- **Reject** → the lines are parallel but have different intercepts: location matters, shifting the intercept only.
		- **Fail to reject** → the lines are coincident: one single line fits all groups, location doesn't matter at all.

	- Which test to run next depends on the outcome of the previous one — a nested, sequential procedure, not three independent tests run all at once.

	- Equivalently, testing all four coefficients together, $H_0:\beta_2=\beta_3=\beta_4=\beta_5=0$ against $H_A$: at least one nonzero, is the single broadest test of whether the categorical variable belongs in the model at all.
