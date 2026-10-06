# Residual and Sum-of-Squares Proofs

- Parent: [[Exam 1]]
- Problem types covered
	- **Type 3:** residual-property proofs
	- **Type 4:** prove the sum-of-squares decomposition

1. **What problem are we trying to solve?**
	- Least squares does more than give formulas for a slope and intercept.
	- Because the coefficients were chosen by minimizing SSE, the resulting residuals satisfy special cancellation / orthogonality identities.
	- Those identities are the reason the total variation in $Y$ can be split cleanly into explained and unexplained pieces.
	- **End goal of this note**
		- prove the residual identities first
		- then use them to prove $SST=SS_{reg}+RSS$
		- understand why ANOVA and $R^2$ are consequences of least squares rather than separate formulas to memorize

1. **Definitions used throughout**
	- Fitted value
		- $\displaystyle \hat y_i=\hat\beta_0+\hat\beta_1x_i$
	- Residual
		- $\displaystyle \hat e_i=y_i-\hat y_i$
	- Least-squares normal equations
		- $\displaystyle \sum\hat e_i=0$
		- $\displaystyle \sum x_i\hat e_i=0$
	- The normal equations come directly from setting the two derivatives of SSE equal to zero.

1. **Proof 1 — $\sum\hat e_i=0$**
	- **End goal**
		- show that the fitted residuals balance to zero overall
	- Start from the residual definition.
		- $\displaystyle \hat e_i=y_i-\hat\beta_0-\hat\beta_1x_i$
	- Sum over all observations.
		- $\displaystyle \sum\hat e_i=\sum y_i-n\hat\beta_0-\hat\beta_1\sum x_i.$
	- The first normal equation says
		- $\displaystyle n\hat\beta_0+\hat\beta_1\sum x_i=\sum y_i.$
	- Substitute that equality into the residual sum.
		- $\displaystyle \sum\hat e_i=\sum y_i-\sum y_i=0.$
	- Therefore
		- $\displaystyle \boxed{\sum_{i=1}^n\hat e_i=0}.$
	- Conceptual meaning
		- positive and negative residuals exactly balance after fitting an intercept
		- equivalently, the average residual is zero

1. **Proof 2 — $\sum x_i\hat e_i=0$**
	- **End goal**
		- show that the residuals have no remaining linear alignment with the predictor values used to fit the line
	- Start from the residual definition and multiply by $x_i$.
		- $\displaystyle x_i\hat e_i=x_i(y_i-\hat\beta_0-\hat\beta_1x_i)$
	- Sum.
		- $\displaystyle \sum x_i\hat e_i=\sum x_iy_i-\hat\beta_0\sum x_i-\hat\beta_1\sum x_i^2.$
	- The second normal equation says
		- $\displaystyle \hat\beta_0\sum x_i+\hat\beta_1\sum x_i^2=\sum x_iy_i.$
	- Substitute.
		- $\displaystyle \sum x_i\hat e_i=\sum x_iy_i-\sum x_iy_i=0.$
	- Therefore
		- $\displaystyle \boxed{\sum_{i=1}^nx_i\hat e_i=0}.$
	- Why this is useful
		- if a linear pattern remains strongly visible in the residuals, the assumed linear model is missing structure even though this algebraic weighted sum is zero

1. **Alternative explicit proof of $\sum x_i\hat e_i=0$**
	- This version exposes the $S_{xy}$ and $S_{xx}$ cancellation directly.
	- Expand as before.
		- $\displaystyle \sum x_i\hat e_i=\sum x_iy_i-\hat\beta_0\sum x_i-\hat\beta_1\sum x_i^2.$
	- Substitute $\hat\beta_0=\bar y-\hat\beta_1\bar x$ and $\sum x_i=n\bar x$.
		- $\displaystyle =\sum x_iy_i-n\bar x\bar y+\hat\beta_1n\bar x^2-\hat\beta_1\sum x_i^2.$
	- Group terms.
		- $\displaystyle =\left(\sum x_iy_i-n\bar x\bar y\right)-\hat\beta_1\left(\sum x_i^2-n\bar x^2\right).$
	- Recognize $S_{xy}$ and $S_{xx}$.
		- $\displaystyle =S_{xy}-\hat\beta_1S_{xx}.$
	- Substitute $\hat\beta_1=S_{xy}/S_{xx}$.
		- $\displaystyle =S_{xy}-\frac{S_{xy}}{S_{xx}}S_{xx}=0.$

1. **Proof 3 — $\sum\hat y_i\hat e_i=0$**
	- **End goal**
		- show that the residual vector is orthogonal not only to the constant and $x$, but also to the fitted values themselves
	- Write the fitted value.
		- $\displaystyle \hat y_i=\hat\beta_0+\hat\beta_1x_i$
	- Multiply by the residual and sum.
		- $\displaystyle \sum\hat y_i\hat e_i=\sum(\hat\beta_0+\hat\beta_1x_i)\hat e_i.$
	- Pull constants outside the sums.
		- $\displaystyle =\hat\beta_0\sum\hat e_i+\hat\beta_1\sum x_i\hat e_i.$
	- Use the two identities already proved.
		- $\displaystyle =\hat\beta_0(0)+\hat\beta_1(0)=0.$
	- Therefore
		- $\displaystyle \boxed{\sum_{i=1}^n\hat y_i\hat e_i=0}.$

1. **What the three residual identities mean together**
	- $\sum\hat e_i=0$
		- residuals are orthogonal to the intercept / constant column
	- $\sum x_i\hat e_i=0$
		- residuals are orthogonal to the predictor column
	- $\sum\hat y_i\hat e_i=0$
		- residuals are orthogonal to the fitted values because fitted values are combinations of the intercept and predictor columns
	- Geometrically, least squares splits the response into
		- a fitted component that lies in the model space
		- a residual component perpendicular to that model space

1. **The sum-of-squares quantities**
	- Total variation around the sample mean
		- $\displaystyle SST=\sum(y_i-\bar y)^2$
	- Explained / regression variation
		- $\displaystyle SS_{reg}=\sum(\hat y_i-\bar y)^2$
		- some notes / software may call this $SSR$
	- Residual / unexplained variation
		- $\displaystyle RSS=\sum(y_i-\hat y_i)^2=\sum\hat e_i^2$
		- some sources call this $SSE$
	- Naming warning
		- because textbooks disagree about whether "SSR" means regression or residual, rely on the actual formulas rather than the three-letter abbreviation alone

1. **Proof 4 — $SST=SS_{reg}+RSS$**
	- **End goal**
		- show that every deviation of $y_i$ from $\bar y$ can be split into an explained piece and a residual piece, with no leftover cross term after summing
	- **Step 1 — Split each total deviation through the fitted value.**
		- $\displaystyle y_i-\bar y=(y_i-\hat y_i)+(\hat y_i-\bar y)$
		- Since $y_i-\hat y_i=\hat e_i$,
			- $\displaystyle y_i-\bar y=\hat e_i+(\hat y_i-\bar y).$
		- Why this is the key move
			- it writes "total deviation" as "unexplained deviation + explained deviation"
	- **Step 2 — Square both sides.**
		- $\displaystyle (y_i-\bar y)^2=\hat e_i^2+2\hat e_i(\hat y_i-\bar y)+(\hat y_i-\bar y)^2.$
	- **Step 3 — Sum over all observations.**
		- $\displaystyle SST=RSS+2\sum\hat e_i(\hat y_i-\bar y)+SS_{reg}.$
		- Everything is already in the desired decomposition except the middle cross-product term.
	- **Step 4 — Show the cross term is zero.**
		- Expand the cross term.
			- $\displaystyle \sum\hat e_i(\hat y_i-\bar y)=\sum\hat e_i\hat y_i-\bar y\sum\hat e_i.$
		- Use the residual identities.
			- $\displaystyle \sum\hat e_i\hat y_i=0$
			- $\displaystyle \sum\hat e_i=0$
		- Therefore
			- $\displaystyle \sum\hat e_i(\hat y_i-\bar y)=0-\bar y(0)=0.$
	- **Step 5 — Remove the zero cross term.**
		- $\displaystyle \boxed{SST=SS_{reg}+RSS}.$
	- Click point
		- the decomposition works cleanly **because least squares made the residuals orthogonal to the fitted values**

1. **Worked verification using the class data**
	- From [[Fitting a Simple Linear Regression]], the fitted line is
		- $\displaystyle \hat y=1.7+0.7x$
	- Data and residuals
		- $x=-1$: $y=1$, $\hat y=1.0$, $\hat e=0$
		- $x=0$: $y=2$, $\hat y=1.7$, $\hat e=0.3$
		- $x=1$: $y=2$, $\hat y=2.4$, $\hat e=-0.4$
		- $x=2$: $y=3$, $\hat y=3.1$, $\hat e=-0.1$
		- $x=3$: $y=4$, $\hat y=3.8$, $\hat e=0.2$
	- Check the first identity.
		- $\displaystyle \sum\hat e_i=0+0.3-0.4-0.1+0.2=0$
	- Check the second identity.
		- $\displaystyle \sum x_i\hat e_i=(-1)(0)+(0)(0.3)+(1)(-0.4)+(2)(-0.1)+(3)(0.2)=0$
	- Compute residual variation.
		- $\displaystyle RSS=0^2+0.3^2+(-0.4)^2+(-0.1)^2+0.2^2=0.30$
	- Since $\bar y=2.4$, total variation is
		- $\displaystyle SST=(1-2.4)^2+(2-2.4)^2+(2-2.4)^2+(3-2.4)^2+(4-2.4)^2=5.20$
	- Therefore explained variation must be
		- $\displaystyle SS_{reg}=SST-RSS=5.20-0.30=4.90$
	- Check
		- $\displaystyle 5.20=4.90+0.30$

1. **Why this proof matters later**
	- $R^2$ uses the fraction of $SST$ that became $SS_{reg}$.
	- ANOVA puts $SS_{reg}$ and $RSS$ into separate rows and divides them by their degrees of freedom.
	- The $F$ test compares explained variation per regression degree of freedom with unexplained variation per residual degree of freedom.
	- So problem types 5 and 7 rest directly on the proof in this note.

1. **Common proof mistakes**
	- Forgetting to state the residual definition before using it.
	- Trying to prove the identities from generic averaging rather than the normal equations.
	- In the SST proof, skipping the cross term instead of writing it and proving it is zero.
	- Confusing $SS_{reg}$ with $RSS$ because of inconsistent SSR / SSE naming conventions.
