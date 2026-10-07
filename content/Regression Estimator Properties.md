- Problem types covered
	- **Type 8:** covariance / variance bilinearity proof

## Concepts

- After fitting, $\hat\beta_0$ and $\hat\beta_1$ are numbers for the observed sample. But before the sample is observed, the responses $Y_i$ are random, so the estimators are random variables too — this is where the standard errors used in inference actually come from.
- Model assumptions used throughout: fixed predictor values $x_i$; $Y_i=\beta_0+\beta_1x_i+\varepsilon_i$; $E(\varepsilon_i)=0$; $\operatorname{Var}(\varepsilon_i)=\sigma^2$; errors independent. Therefore $E(Y_i)=\beta_0+\beta_1x_i$, $\operatorname{Var}(Y_i)=\sigma^2$, and $Y_i,Y_j$ independent for $i\neq j$.
- **Rewrite the slope as a linear combination of the responses.** Start from $\hat\beta_1=S_{xy}/S_{xx}$, expand $S_{xy}=\sum(x_i-\bar x)(Y_i-\bar Y)$; the $\bar Y$ part drops because $\sum(x_i-\bar x)=0$, leaving $S_{xy}=\sum(x_i-\bar x)Y_i$. Define $c_i=\dfrac{x_i-\bar x}{S_{xx}}$, so $\boxed{\hat\beta_1=\sum_i c_iY_i}$ — this form makes expectation, variance, covariance, and normality all easy to handle.
- Three $c_i$ identities, each just algebra on the definition:
	- $\sum c_i=0$ (since $\sum(x_i-\bar x)=0$).
	- $\sum c_ix_i=1$ (write $x_i=(x_i-\bar x)+\bar x$, expand, and the $\bar x\sum(x_i-\bar x)$ term vanishes, leaving $S_{xx}/S_{xx}=1$).
	- $\sum c_i^2=1/S_{xx}$ (direct from $c_i=(x_i-\bar x)/S_{xx}$, squared and summed).
- **Unbiasedness of the slope.** $E(\hat\beta_1)=E(\sum c_iY_i)=\sum c_iE(Y_i)=\sum c_i(\beta_0+\beta_1x_i)=\beta_0\sum c_i+\beta_1\sum c_ix_i=\beta_0(0)+\beta_1(1)=\beta_1$. So $\boxed{E(\hat\beta_1)=\beta_1}$.
- **Variance of the slope.** Since the $Y_i$ are independent, $\operatorname{Var}(\hat\beta_1)=\sum c_i^2\operatorname{Var}(Y_i)=\sigma^2\sum c_i^2=\sigma^2/S_{xx}$, so $\boxed{\operatorname{Var}(\hat\beta_1)=\dfrac{\sigma^2}{S_{xx}}}$. Click point: a bigger spread in the $x$-values (larger $S_{xx}$) means a more precise slope estimate.
- **Rewrite the intercept as a linear combination.** $\hat\beta_0=\bar Y-\hat\beta_1\bar x=\sum(\frac1n-\bar xc_i)Y_i$; define $d_i=\frac1n-\bar xc_i$, so $\hat\beta_0=\sum d_iY_i$.
- **Unbiasedness of the intercept.** Using $\hat\beta_0=\bar Y-\bar x\hat\beta_1$: $E(\hat\beta_0)=E(\bar Y)-\bar xE(\hat\beta_1)=(\beta_0+\beta_1\bar x)-\bar x\beta_1=\beta_0$.
- Bilinearity rules for covariance problems: constants pull out, $\operatorname{Cov}(aX,bY)=ab\operatorname{Cov}(X,Y)$; covariance distributes over sums; $\operatorname{Cov}(X,X)=\operatorname{Var}(X)$; independent variables have covariance $0$. For independent $Y_i$: $\operatorname{Cov}(\sum a_iY_i,\sum b_iY_i)=\sum a_ib_i\operatorname{Var}(Y_i)$ — the cross terms ($i\neq j$) vanish because $\operatorname{Cov}(Y_i,Y_j)=0$.
- **$\operatorname{Cov}(\bar Y,\hat\beta_1)=0$.** Write $\bar Y=\sum\frac1nY_i$ and $\hat\beta_1=\sum c_iY_i$; by independence, $\operatorname{Cov}(\bar Y,\hat\beta_1)=\sum\frac1nc_i\operatorname{Var}(Y_i)=\frac{\sigma^2}n\sum c_i=0$ (using $\sum c_i=0$). This intermediate result makes both the intercept variance and the intercept-slope covariance simple.
- **Variance of the intercept.** $\operatorname{Var}(\hat\beta_0)=\operatorname{Var}(\bar Y)+\bar x^2\operatorname{Var}(\hat\beta_1)-2\bar x\operatorname{Cov}(\bar Y,\hat\beta_1)$; the covariance term is $0$, and $\operatorname{Var}(\bar Y)=\sigma^2/n$, so $\boxed{\operatorname{Var}(\hat\beta_0)=\sigma^2\left(\dfrac1n+\dfrac{\bar x^2}{S_{xx}}\right)}$.
- **Covariance of intercept and slope (the bilinearity proof itself).** Start from $\hat\beta_0=\bar Y-\bar x\hat\beta_1$, take covariance with $\hat\beta_1$: $\operatorname{Cov}(\hat\beta_0,\hat\beta_1)=\operatorname{Cov}(\bar Y,\hat\beta_1)-\bar x\operatorname{Cov}(\hat\beta_1,\hat\beta_1)=0-\bar x\operatorname{Var}(\hat\beta_1)$, so $\boxed{\operatorname{Cov}(\hat\beta_0,\hat\beta_1)=-\dfrac{\bar x\sigma^2}{S_{xx}}}$. Sanity check: if $\bar x>0$, the covariance is negative — tilting the slope up forces the intercept down so the line can still pass through $(\bar x,\bar y)$.
- Sampling distributions under normal errors: if $\varepsilon_i\sim N(0,\sigma^2)$, linear combinations of jointly normal variables are normal, so $\hat\beta_1\sim N(\beta_1,\sigma^2/S_{xx})$ and $\hat\beta_0\sim N(\beta_0,\sigma^2(\frac1n+\frac{\bar x^2}{S_{xx}}))$ — the bridge to the $t$-procedures used for inference.
- What changes when $\sigma^2$ is unknown: estimate it with $S^2=RSS/(n-2)$, replace $\sigma$ by $S$ in the standard deviations to get $SE(\hat\beta_1)=S/\sqrt{S_{xx}}$ and $SE(\hat\beta_0)=S\sqrt{\frac1n+\frac{\bar x^2}{S_{xx}}}$ — and the reference distribution changes from normal to $t_{n-2}$.

## Practice Problems

- **Problem 1 (HW1 Q2).** Derive $\operatorname{Cov}(\hat\beta_0,\hat\beta_1)$ using bilinearity rather than memorizing it. Write it the way you would on the exam — the Concepts section above has the fully justified version; this is the fast, exam-pace version of the same derivation.
	- *Solution.*
		- $\hat\beta_0=\bar Y-\bar x\hat\beta_1$
		- $\operatorname{Cov}(\hat\beta_0,\hat\beta_1)=\operatorname{Cov}(\bar Y-\bar x\hat\beta_1,\hat\beta_1)$
		- $=\operatorname{Cov}(\bar Y,\hat\beta_1)-\bar x\operatorname{Cov}(\hat\beta_1,\hat\beta_1)$
		- $\operatorname{Cov}(\bar Y,\hat\beta_1)=0$ (shown earlier via $\sum c_i=0$)
		- $\operatorname{Cov}(\hat\beta_1,\hat\beta_1)=\operatorname{Var}(\hat\beta_1)=\sigma^2/S_{xx}$
		- $\boxed{\operatorname{Cov}(\hat\beta_0,\hat\beta_1)=-\dfrac{\bar x\sigma^2}{S_{xx}}}$ $\blacksquare$

- **Problem 2 — verify a real printed standard error (Production data, $n=20$).** The production data (`RunTime ~ RunSize`) has $S_{xx}=191{,}473.8$ and R reports $S^2=MSE=264.1$ and a slope standard error of $0.03714$. Using $\operatorname{Var}(\hat\beta_1)=\sigma^2/S_{xx}$ with $S^2$ in place of the unknown $\sigma^2$, verify this printed value by hand.
	- *Solution.*
		- $SE(\hat\beta_1)=\sqrt{S^2/S_{xx}}$
		- $=\sqrt{264.1/191{,}473.8}$
		- $=\sqrt{0.0013799}$
		- $\approx0.03714$ — matches R's printed `Std. Error` exactly
