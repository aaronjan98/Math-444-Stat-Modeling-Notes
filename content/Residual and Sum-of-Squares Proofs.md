- Problem types covered
	- **Type 3:** residual-property proofs
	- **Type 4:** prove the sum-of-squares decomposition

## Concepts

- Because the coefficients were chosen by minimizing SSE, the resulting residuals satisfy special cancellation / orthogonality identities. Those identities are the reason the total variation in $Y$ splits cleanly into explained and unexplained pieces — ANOVA and $R^2$ are consequences of least squares, not separate formulas to memorize.
- Definitions used throughout: fitted value $\hat y_i=\hat\beta_0+\hat\beta_1x_i$; residual $\hat e_i=y_i-\hat y_i$; normal equations $\sum\hat e_i=0$ and $\sum x_i\hat e_i=0$ (these come directly from setting the two partial derivatives of SSE equal to zero).
- **Proof 1 — $\sum\hat e_i=0$.** Start from $\hat e_i=y_i-\hat\beta_0-\hat\beta_1x_i$, sum over all $i$: $\sum\hat e_i=\sum y_i-n\hat\beta_0-\hat\beta_1\sum x_i$. The first normal equation says $n\hat\beta_0+\hat\beta_1\sum x_i=\sum y_i$, so substituting gives $\sum\hat e_i=\sum y_i-\sum y_i=0$. Meaning: positive and negative residuals exactly balance after fitting an intercept; the average residual is zero.
- **Proof 2 — $\sum x_i\hat e_i=0$.** Multiply the residual by $x_i$ and sum: $\sum x_i\hat e_i=\sum x_iy_i-\hat\beta_0\sum x_i-\hat\beta_1\sum x_i^2$. The second normal equation says $\hat\beta_0\sum x_i+\hat\beta_1\sum x_i^2=\sum x_iy_i$, so the sum is $0$.
	- Alternative route exposing $S_{xy}/S_{xx}$ directly: substitute $\hat\beta_0=\bar y-\hat\beta_1\bar x$ and $\sum x_i=n\bar x$ into the expansion, group terms to get $S_{xy}-\hat\beta_1S_{xx}$, then substitute $\hat\beta_1=S_{xy}/S_{xx}$ to get $S_{xy}-S_{xy}=0$.
- **Proof 3 — $\sum\hat y_i\hat e_i=0$.** Write $\hat y_i=\hat\beta_0+\hat\beta_1x_i$, multiply by $\hat e_i$ and sum: $\sum\hat y_i\hat e_i=\hat\beta_0\sum\hat e_i+\hat\beta_1\sum x_i\hat e_i$. Both sums are $0$ by Proofs 1 and 2, so the whole thing is $0$ — the residual vector is orthogonal not only to the constant and $x$ columns, but also to the fitted values themselves (since fitted values are combinations of those two columns).
- What the three identities mean together: residuals are orthogonal to the intercept column, to the predictor column, and therefore to the fitted values. Geometrically, least squares splits the response into a fitted component in the "model space" and a residual component perpendicular to it.
- The sum-of-squares quantities: $SST=\sum(y_i-\bar y)^2$ (total variation around the mean); $SS_{reg}=\sum(\hat y_i-\bar y)^2$ (explained, sometimes called $SSR$); $RSS=\sum(y_i-\hat y_i)^2=\sum\hat e_i^2$ (unexplained, sometimes called $SSE$).
	- Naming warning: textbooks disagree on whether "SSR" means regression or residual — rely on the formula, not the three letters.
- **Proof 4 — $SST=SS_{reg}+RSS$.**
	- Step 1 — split each total deviation through the fitted value: $y_i-\bar y=(y_i-\hat y_i)+(\hat y_i-\bar y)=\hat e_i+(\hat y_i-\bar y)$. This writes "total deviation" as "unexplained + explained."
	- Step 2 — square both sides: $(y_i-\bar y)^2=\hat e_i^2+2\hat e_i(\hat y_i-\bar y)+(\hat y_i-\bar y)^2$.
	- Step 3 — sum over all observations: $SST=RSS+2\sum\hat e_i(\hat y_i-\bar y)+SS_{reg}$.
	- Step 4 — show the cross term is zero: expand $\sum\hat e_i(\hat y_i-\bar y)=\sum\hat e_i\hat y_i-\bar y\sum\hat e_i$. By Proof 3, $\sum\hat e_i\hat y_i=0$; by Proof 1, $\sum\hat e_i=0$. So the cross term is $0$.
	- Step 5 — conclude: $\boxed{SST=SS_{reg}+RSS}$. This works cleanly *because* least squares made the residuals orthogonal to the fitted values (Proof 3).

## Practice Problems

- **Problem 1 (HW1 Q1).** Prove $\sum\hat e_i=0$ and $\sum x_i\hat e_i=0$ using the normal equations. Write it the way you would on the exam — the Concepts section above has the fully justified version; this is the fast, exam-pace version of the same two proofs.
	- *Solution.*
		- $\sum\hat e_i=0$:
			- $\hat e_i=y_i-\hat\beta_0-\hat\beta_1x_i$
			- $\sum\hat e_i=\sum y_i-n\hat\beta_0-\hat\beta_1\sum x_i$
			- first normal equation: $n\hat\beta_0+\hat\beta_1\sum x_i=\sum y_i$
			- $\Rightarrow\ \sum\hat e_i=\sum y_i-\sum y_i=0$ $\blacksquare$
		- $\sum x_i\hat e_i=0$:
			- $x_i\hat e_i=x_i(y_i-\hat\beta_0-\hat\beta_1x_i)$
			- $\sum x_i\hat e_i=\sum x_iy_i-\hat\beta_0\sum x_i-\hat\beta_1\sum x_i^2$
			- second normal equation: $\hat\beta_0\sum x_i+\hat\beta_1\sum x_i^2=\sum x_iy_i$
			- $\Rightarrow\ \sum x_i\hat e_i=\sum x_iy_i-\sum x_iy_i=0$ $\blacksquare$

- **Problem 2 (HW1 Q3).** Prove $SST=SS_{reg}+RSS$. Same exam-pace instruction as above.
	- *Solution.*
		- $y_i-\bar y=(y_i-\hat y_i)+(\hat y_i-\bar y)=\hat e_i+(\hat y_i-\bar y)$
		- square both sides: $(y_i-\bar y)^2=\hat e_i^2+2\hat e_i(\hat y_i-\bar y)+(\hat y_i-\bar y)^2$
		- sum over $i$: $SST=RSS+2\sum\hat e_i(\hat y_i-\bar y)+SS_{reg}$
		- cross term: $\sum\hat e_i(\hat y_i-\bar y)=\sum\hat e_i\hat y_i-\bar y\sum\hat e_i=0-\bar y(0)=0$ (using $\sum\hat e_i\hat y_i=0$ and $\sum\hat e_i=0$)
		- $\boxed{SST=SS_{reg}+RSS}$ $\blacksquare$

- **Problem 3 — numeric verification (class data).** Using the fitted line $\hat y=1.7+0.7x$ from the class dataset $(-1,1),(0,2),(1,2),(2,3),(3,4)$, compute all five residuals and verify both residual identities and the decomposition $SST=SS_{reg}+RSS$ numerically.
	- *Solution.*
		- residuals: $x=-1$: $\hat e=0$; $x=0$: $\hat e=0.3$; $x=1$: $\hat e=-0.4$; $x=2$: $\hat e=-0.1$; $x=3$: $\hat e=0.2$
		- check $\sum\hat e_i=0+0.3-0.4-0.1+0.2=0$
		- check $\sum x_i\hat e_i=(-1)(0)+(0)(0.3)+(1)(-0.4)+(2)(-0.1)+(3)(0.2)=0$
		- $RSS=0^2+0.3^2+(-0.4)^2+(-0.1)^2+0.2^2=0.30$
		- $\bar y=2.4$, so $SST=(1-2.4)^2+(2-2.4)^2+(2-2.4)^2+(3-2.4)^2+(4-2.4)^2=5.20$
		- $SS_{reg}=SST-RSS=5.20-0.30=4.90$
		- check: $5.20=4.90+0.30$ ✓
