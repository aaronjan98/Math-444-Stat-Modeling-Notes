- Problem types covered
	- **Type 1:** hand-compute an SLR fit
	- **Type 2:** derive the least-squares estimators / normal equations

## Concepts

- We observe pairs $(x_i,y_i)$ and want one straight line that summarizes how $Y$ changes with $x$. Population model: $Y_i=\beta_0+\beta_1x_i+\varepsilon_i$. From the sample we estimate $\beta_0,\beta_1$ with $\hat\beta_0,\hat\beta_1$ and build $\hat y=\hat\beta_0+\hat\beta_1x$.
	- **End goal of least squares:** choose the intercept and slope so the fitted line has the smallest possible total squared vertical error from the observed points.
- Why residuals are the starting point
	- For observation $i$, a candidate line predicts $\hat y_i=\beta_0+\beta_1x_i$, with vertical miss (residual) $e_i=y_i-\beta_0-\beta_1x_i$.
	- Adding raw residuals is a bad measure of total error because positive and negative misses cancel; squaring fixes that.
	- $\displaystyle SSE(\beta_0,\beta_1)=\sum_{i=1}^n(y_i-\beta_0-\beta_1x_i)^2.$ Everything below is machinery for making this as small as possible.
- Summation facts needed for the derivation: $\sum x_i=n\bar x$, $\sum y_i=n\bar y$, $\sum(x_i-\bar x)=0$, $S_{xx}=\sum(x_i-\bar x)^2=\sum x_i^2-n\bar x^2$, $S_{xy}=\sum(x_i-\bar x)(y_i-\bar y)=\sum x_iy_i-n\bar x\bar y$.
	- Pitfall: $\sum a_ib_i\neq(\sum a_i)(\sum b_i)$, and $\sum a_i^2\neq(\sum a_i)^2$.
- **Derive the estimators**
	- Step 1 — differentiate SSE with respect to $\beta_0$: $\frac{\partial SSE}{\partial\beta_0}=-2\sum(y_i-\beta_0-\beta_1x_i)$. Set to $0$: $\sum y_i=n\beta_0+\beta_1\sum x_i$. Divide by $n$ and use the mean identities: $\bar y=\beta_0+\beta_1\bar x$, so $\boxed{\beta_0=\bar y-\beta_1\bar x}$ — this is the first normal equation, and it says the fitted line must pass through $(\bar x,\bar y)$.
	- Step 2 — differentiate SSE with respect to $\beta_1$: $\frac{\partial SSE}{\partial\beta_1}=-2\sum x_i(y_i-\beta_0-\beta_1x_i)$. Set to $0$: $\sum x_iy_i-\beta_0\sum x_i-\beta_1\sum x_i^2=0$ — the second normal equation.
	- Step 3 — substitute $\beta_0=\bar y-\beta_1\bar x$ and $\sum x_i=n\bar x$ into step 2, expand, and group the non-$\beta_1$ and $\beta_1$ parts: $(\sum x_iy_i-n\bar x\bar y)-\beta_1(\sum x_i^2-n\bar x^2)=0$, i.e. $S_{xy}-\beta_1S_{xx}=0$, so $\boxed{\hat\beta_1=\dfrac{S_{xy}}{S_{xx}}}$.
	- Step 4 — recover the intercept: $\boxed{\hat\beta_0=\bar y-\hat\beta_1\bar x}$.
	- Step 5 — the fitted line: $\boxed{\hat y=\hat\beta_0+\hat\beta_1x}$.
	- Why this is a minimum: SSE is quadratic in $(\beta_0,\beta_1)$; as long as the $x_i$ are not all identical, $S_{xx}>0$, so the objective curves upward and the stationary point is the minimum.
- The two normal equations, remembered directly: $\sum\hat e_i=0$ and $\sum x_i\hat e_i=0$ — the least-squares residual vector is orthogonal to the constant column and to $x$.
- Why centering keeps appearing: $S_{xx}$ is the spread of $x$ around $\bar x$; $S_{xy}$ is how $x$ and $y$ co-move around their means; $\hat\beta_1=S_{xy}/S_{xx}$ reads as "how much $y$ moves with $x$, relative to how much $x$ itself varies."
- Exam workflow for a hand-computed fit: get $n,\sum x_i,\sum y_i,\sum x_i^2,\sum x_iy_i$ → $\bar x,\bar y$ → $S_{xx},S_{xy}$ → $\hat\beta_1=S_{xy}/S_{xx}$ → $\hat\beta_0=\bar y-\hat\beta_1\bar x$ → fitted line → (if asked) residual $\hat e_i=y_i-\hat y_i$.

## Practice Problems

- **Problem 1 — hand-compute a fit.** Data $(-1,1),(0,2),(1,2),(2,3),(3,4)$, with $n=5$, $\sum x_i=5$, $\sum y_i=12$, $\sum x_iy_i=19$, $\sum x_i^2=15$. Find the fitted line and the residual at $x=2$.
	- *Solution.*
		- $\bar x=1$, $\bar y=2.4$
		- $S_{xy}=19-5(1)(2.4)=7$
		- $S_{xx}=15-5(1)^2=10$
		- $\hat\beta_1=7/10=0.7$
		- $\hat\beta_0=2.4-0.7(1)=1.7$
		- $\boxed{\hat y=1.7+0.7x}$
		- at $x=2$: $\hat y=3.1$, observed $y=3$, so $\hat e=3-3.1=-0.1$

- **Problem 2 — derive from scratch, cold.** Derive the two normal equations from $SSE=\sum(y_i-\beta_0-\beta_1x_i)^2$ and solve them for $\hat\beta_1$ and $\hat\beta_0$. Write it the way you would on the exam — the Concepts section above has the fully justified version; this is the fast, exam-pace version of the same argument.
	- *Solution.*
		- $\dfrac{\partial SSE}{\partial\beta_0}=-2\sum(y_i-\beta_0-\beta_1x_i)=0$
			- $\Rightarrow\ \sum y_i=n\beta_0+\beta_1\sum x_i$ — first normal equation
			- $\Rightarrow\ \beta_0=\bar y-\beta_1\bar x$
		- $\dfrac{\partial SSE}{\partial\beta_1}=-2\sum x_i(y_i-\beta_0-\beta_1x_i)=0$
			- $\Rightarrow\ \sum x_iy_i=\beta_0\sum x_i+\beta_1\sum x_i^2$ — second normal equation
		- substitute $\beta_0=\bar y-\beta_1\bar x$ and $\sum x_i=n\bar x$ into the second equation
			- $\sum x_iy_i=(\bar y-\beta_1\bar x)n\bar x+\beta_1\sum x_i^2$
			- $\sum x_iy_i-n\bar x\bar y=\beta_1(\sum x_i^2-n\bar x^2)$
			- $S_{xy}=\beta_1S_{xx}$
		- $\boxed{\hat\beta_1=\dfrac{S_{xy}}{S_{xx}}}$
		- $\boxed{\hat\beta_0=\bar y-\hat\beta_1\bar x}$
