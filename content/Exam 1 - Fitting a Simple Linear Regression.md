# Exam 1 - Fitting a Simple Linear Regression

- Parent: [[Exam 1 Study Guide (Math 444)]]
- Triage coverage
	- **Type 1:** hand-compute an SLR fit
	- **Type 2:** derive the least-squares estimators / normal equations

1. **What problem are we trying to solve?**
	- We observe pairs $(x_i,y_i)$ and want one straight line that summarizes how $Y$ changes with $x$.
	- Population model
		- $\displaystyle Y_i=\beta_0+\beta_1x_i+\varepsilon_i.$
	- The population parameters $\beta_0$ and $\beta_1$ are unknown.
	- From the sample, we estimate them with $\hat\beta_0$ and $\hat\beta_1$ and build
		- $\displaystyle \hat y=\hat\beta_0+\hat\beta_1x.$
	- **End goal of least squares**
		- choose the intercept and slope so the fitted line has the smallest possible **total squared vertical error** from the observed points

1. **Why residuals are the starting point**
	- For observation $i$, a candidate line predicts
		- $\displaystyle \hat y_i=\beta_0+\beta_1x_i.$
	- Its vertical miss is the residual
		- $\displaystyle e_i=y_i-\hat y_i=y_i-\beta_0-\beta_1x_i.$
	- Adding raw residuals is a bad measure of total error because positive and negative misses can cancel.
	- Squaring fixes the cancellation problem.
	- The least-squares objective is therefore
		- $\displaystyle SSE(\beta_0,\beta_1)=\sum_{i=1}^n(y_i-\beta_0-\beta_1x_i)^2.$
	- The entire derivation below is just machinery for answering
		- **Which $\beta_0$ and $\beta_1$ make this quantity as small as possible?**

1. **Summation facts needed for the derivation**
	- $\displaystyle \sum_{i=1}^n x_i=n\bar x$
	- $\displaystyle \sum_{i=1}^n y_i=n\bar y$
	- $\displaystyle \sum_{i=1}^n(x_i-\bar x)=0$
	- $\displaystyle S_{xx}=\sum(x_i-\bar x)^2=\sum x_i^2-n\bar x^2$
	- $\displaystyle S_{xy}=\sum(x_i-\bar x)(y_i-\bar y)=\sum x_iy_i-n\bar x\bar y$
	- Important pitfall
		- $\sum a_ib_i$ is **not** $(\sum a_i)(\sum b_i)$
		- $\sum a_i^2$ is **not** $(\sum a_i)^2$

1. **Derive the least-squares estimators step by step**
	- **Step 1 — Differentiate SSE with respect to the intercept.**
		- Goal of this step
			- find the condition the minimizing intercept must satisfy
		- Start with
			- $\displaystyle SSE=\sum(y_i-\beta_0-\beta_1x_i)^2.$
		- Differentiate
			- $\displaystyle \frac{\partial SSE}{\partial\beta_0}=-2\sum(y_i-\beta_0-\beta_1x_i).$
		- At the minimum, set the derivative equal to $0$.
			- $\displaystyle \sum(y_i-\beta_0-\beta_1x_i)=0.$
		- Rearrange.
			- $\displaystyle \sum y_i=n\beta_0+\beta_1\sum x_i.$
		- Replace the sums by $n\bar y$ and $n\bar x$.
			- $\displaystyle n\bar y=n\beta_0+n\beta_1\bar x.$
		- Divide by $n$.
			- $\displaystyle \bar y=\beta_0+\beta_1\bar x.$
		- Solve for the intercept.
			- $\displaystyle \beta_0=\bar y-\beta_1\bar x.$
		- Why this matters
			- any least-squares line must pass through $(\bar x,\bar y)$
			- it also lets us remove $\beta_0$ from the second equation so we can solve for the slope
	- **Step 2 — Differentiate SSE with respect to the slope.**
		- Goal of this step
			- find the second condition needed to determine the minimizing line
		- Differentiate.
			- $\displaystyle \frac{\partial SSE}{\partial\beta_1}=-2\sum x_i(y_i-\beta_0-\beta_1x_i).$
		- Set equal to $0$.
			- $\displaystyle \sum x_i(y_i-\beta_0-\beta_1x_i)=0.$
		- Expand.
			- $\displaystyle \sum x_iy_i-\beta_0\sum x_i-\beta_1\sum x_i^2=0.$
	- **Step 3 — Substitute the intercept condition into the slope equation.**
		- Goal of this step
			- reduce two unknowns to one unknown, $\beta_1$
		- Substitute $\beta_0=\bar y-\beta_1\bar x$ and $\sum x_i=n\bar x$.
			- $\displaystyle \sum x_iy_i-(\bar y-\beta_1\bar x)n\bar x-\beta_1\sum x_i^2=0.$
		- Expand.
			- $\displaystyle \sum x_iy_i-n\bar x\bar y+\beta_1n\bar x^2-\beta_1\sum x_i^2=0.$
		- Group the no-$\beta_1$ part and the $\beta_1$ part.
			- $\displaystyle \left(\sum x_iy_i-n\bar x\bar y\right)-\beta_1\left(\sum x_i^2-n\bar x^2\right)=0.$
		- Recognize the centered sums.
			- $\displaystyle S_{xy}-\beta_1S_{xx}=0.$
		- Solve for the slope.
			- $\displaystyle \boxed{\hat\beta_1=\frac{S_{xy}}{S_{xx}}}.$
	- **Step 4 — Recover the intercept.**
		- Substitute the estimated slope into the intercept condition.
			- $\displaystyle \boxed{\hat\beta_0=\bar y-\hat\beta_1\bar x}.$
	- **Step 5 — Write the fitted line.**
		- $\displaystyle \boxed{\hat y=\hat\beta_0+\hat\beta_1x}.$
	- Why this is a minimum
		- SSE is a quadratic function of the coefficients
		- as long as the $x_i$ values are not all identical, $S_{xx}>0$, so the least-squares objective curves upward in the slope direction and the stationary solution is the minimizing solution

1. **The two normal equations**
	- The derivative conditions can be remembered directly as
		- $\displaystyle \sum\hat e_i=0$
		- $\displaystyle \sum x_i\hat e_i=0$
	- Expanded form
		- $\displaystyle n\hat\beta_0+\hat\beta_1\sum x_i=\sum y_i$
		- $\displaystyle \hat\beta_0\sum x_i+\hat\beta_1\sum x_i^2=\sum x_iy_i$
	- These are called the normal equations because the least-squares residual vector is orthogonal to the columns used to build the fitted line.

1. **Exam workflow for a hand-computed SLR fit**
	- **Step 1:** compute $n$, $\sum x_i$, $\sum y_i$, $\sum x_i^2$, and $\sum x_iy_i$.
	- **Step 2:** compute $\bar x$ and $\bar y$.
	- **Step 3:** compute $S_{xx}$ and $S_{xy}$.
		- $\displaystyle S_{xx}=\sum x_i^2-n\bar x^2$
		- $\displaystyle S_{xy}=\sum x_iy_i-n\bar x\bar y$
	- **Step 4:** compute the slope.
		- $\displaystyle \hat\beta_1=S_{xy}/S_{xx}$
	- **Step 5:** compute the intercept.
		- $\displaystyle \hat\beta_0=\bar y-\hat\beta_1\bar x$
	- **Step 6:** write the fitted line.
	- **Step 7:** if asked for a residual, compute $\hat y_i$ and then $\hat e_i=y_i-\hat y_i$.

1. **Worked class example from start to finish**
	- Data
		- $(-1,1),(0,2),(1,2),(2,3),(3,4)$
	- Given / tabulated sums
		- $\displaystyle n=5,\quad \sum x_i=5,\quad \sum y_i=12,\quad \sum x_iy_i=19,\quad \sum x_i^2=15.$
	- **Step 1 — Means**
		- $\displaystyle \bar x=5/5=1$
		- $\displaystyle \bar y=12/5=2.4$
	- **Step 2 — Centered cross-product**
		- $\displaystyle S_{xy}=19-(5)(1)(2.4)=7$
	- **Step 3 — Centered predictor sum of squares**
		- $\displaystyle S_{xx}=15-5(1)^2=10$
	- **Step 4 — Slope**
		- $\displaystyle \hat\beta_1=7/10=0.7$
	- **Step 5 — Intercept**
		- $\displaystyle \hat\beta_0=2.4-(0.7)(1)=1.7$
	- **Step 6 — Fitted line**
		- $\displaystyle \boxed{\hat y=1.7+0.7x}$
	- **Step 7 — One residual**
		- at $x=2$, $\hat y=1.7+0.7(2)=3.1$
		- observed $y=3$
		- $\displaystyle \hat e=3-3.1=-0.1$
	- Interpretation of the slope
		- the fitted response increases by about $0.7$ units for each one-unit increase in $x$

1. **Why centering keeps appearing**
	- $S_{xx}$ measures how spread out the predictor values are around $\bar x$.
	- $S_{xy}$ measures whether deviations in $x$ and $y$ tend to move together.
	- The ratio $S_{xy}/S_{xx}$ therefore asks
		- how much does $y$ move with $x$, relative to how much $x$ itself varies?
	- This is why the least-squares slope has the form it does.

1. **Common mistakes**
	- Swapping $S_{xy}$ and $S_{xx}$ in the slope formula.
	- Forgetting that the intercept uses $\bar y-\hat\beta_1\bar x$.
	- Defining the residual backwards.
		- class convention: $\hat e_i=y_i-\hat y_i$
	- Using $\sum x_i^2=(\sum x_i)^2$.
	- Forgetting the factor of $n$ in the shortcut formulas for $S_{xx}$ and $S_{xy}$.
	- Treating $\beta_0,\beta_1$ and $\hat\beta_0,\hat\beta_1$ as the same objects.
		- unhatted = population parameters
		- hatted = estimates calculated from the sample

1. **Cold-recall checklist**
	- Can I state the end goal of least squares without a formula?
	- Can I write SSE from memory?
	- Can I take both partial derivatives and explain why they are set to zero?
	- Can I derive the first normal equation and explain why it means the fitted line passes through $(\bar x,\bar y)$?
	- Can I reduce the second normal equation to $S_{xy}-\beta_1S_{xx}=0$?
	- Can I compute a complete fit from a small table without R?
