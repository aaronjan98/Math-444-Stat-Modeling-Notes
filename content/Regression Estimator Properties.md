# Regression Estimator Properties

- Parent: [[Exam 1]]
- Problem types covered
	- **Type 8:** covariance / variance bilinearity proof
	- This note also derives the estimator means and variances needed for problem type 6 inference.

1. **What problem are we trying to solve?**
	- After fitting the line, $\hat\beta_0$ and $\hat\beta_1$ are numbers for the observed sample.
	- But before the sample is observed, the responses $Y_i$ are random, so the estimators are also random variables.
	- To do confidence intervals and tests, we need to know
		- their expected values
		- their variances
		- their covariance
		- their distributions under normal errors
	- **End goal**
		- explain where the standard errors used in regression inference actually come from

1. **Model assumptions used in the proofs**
	- Fixed predictor values $x_i$.
	- $\displaystyle Y_i=\beta_0+\beta_1x_i+\varepsilon_i.$
	- $\displaystyle E(\varepsilon_i)=0.$
	- $\displaystyle \operatorname{Var}(\varepsilon_i)=\sigma^2.$
	- Errors are independent.
	- Therefore
		- $\displaystyle E(Y_i)=\beta_0+\beta_1x_i$
		- $\displaystyle \operatorname{Var}(Y_i)=\sigma^2$
		- $Y_i$ and $Y_j$ are independent for $i\neq j$

1. **Rewrite the slope as a linear combination of the responses**
	- Start from
		- $\displaystyle \hat\beta_1=\frac{S_{xy}}{S_{xx}}.$
	- Expand $S_{xy}$.
		- $\displaystyle S_{xy}=\sum(x_i-\bar x)(Y_i-\bar Y).$
	- The $\bar Y$ part disappears because $\sum(x_i-\bar x)=0$.
		- $\displaystyle S_{xy}=\sum(x_i-\bar x)Y_i.$
	- Define
		- $\displaystyle c_i=\frac{x_i-\bar x}{S_{xx}}.$
	- Then
		- $\displaystyle \boxed{\hat\beta_1=\sum_{i=1}^nc_iY_i}.$
	- Why this form is powerful
		- expectation, variance, covariance, and normality are easy to handle for linear combinations

1. **Three $c_i$ identities to memorize by understanding**
	- **Identity 1 — $\sum c_i=0$**
		- $\displaystyle \sum c_i=\frac1{S_{xx}}\sum(x_i-\bar x)=0.$
	- **Identity 2 — $\sum c_ix_i=1$**
		- Write $x_i=(x_i-\bar x)+\bar x$.
		- Then
			- $\displaystyle \sum c_ix_i=\frac1{S_{xx}}\sum(x_i-\bar x)x_i.$
		- Expand $x_i$ around $\bar x$.
			- $\displaystyle \sum(x_i-\bar x)x_i=\sum(x_i-\bar x)^2+\bar x\sum(x_i-\bar x)=S_{xx}+0.$
		- Therefore
			- $\displaystyle \sum c_ix_i=1.$
	- **Identity 3 — $\sum c_i^2=1/S_{xx}$**
		- $\displaystyle \sum c_i^2=\sum\frac{(x_i-\bar x)^2}{S_{xx}^2}=\frac{S_{xx}}{S_{xx}^2}=\frac1{S_{xx}}.$

1. **Proof — the slope estimator is unbiased**
	- **End goal**
		- show that repeated samples center the slope estimator on the true slope
	- Start from the linear-combination form.
		- $\displaystyle E(\hat\beta_1)=E\left(\sum c_iY_i\right)=\sum c_iE(Y_i).$
	- Substitute the population mean model.
		- $\displaystyle =\sum c_i(\beta_0+\beta_1x_i).$
	- Split the sum.
		- $\displaystyle =\beta_0\sum c_i+\beta_1\sum c_ix_i.$
	- Use the identities.
		- $\displaystyle =\beta_0(0)+\beta_1(1)=\beta_1.$
	- Therefore
		- $\displaystyle \boxed{E(\hat\beta_1)=\beta_1}.$

1. **Proof — variance of the slope estimator**
	- **End goal**
		- measure how much $\hat\beta_1$ would vary from sample to sample
	- Start from
		- $\displaystyle \hat\beta_1=\sum c_iY_i.$
	- Because the $Y_i$ are independent,
		- $\displaystyle \operatorname{Var}(\hat\beta_1)=\sum c_i^2\operatorname{Var}(Y_i).$
	- Each response has variance $\sigma^2$.
		- $\displaystyle =\sigma^2\sum c_i^2.$
	- Use $\sum c_i^2=1/S_{xx}$.
		- $\displaystyle \boxed{\operatorname{Var}(\hat\beta_1)=\frac{\sigma^2}{S_{xx}}}.$
	- Therefore the population standard deviation of the slope estimator is
		- $\displaystyle \frac{\sigma}{\sqrt{S_{xx}}}.$
	- Click point
		- greater spread in the $x$ values means larger $S_{xx}$, which means a more precise slope estimate

1. **Rewrite the intercept as a linear combination**
	- Start from
		- $\displaystyle \hat\beta_0=\bar Y-\hat\beta_1\bar x.$
	- Write $\bar Y=(1/n)\sum Y_i$ and $\hat\beta_1=\sum c_iY_i$.
		- $\displaystyle \hat\beta_0=\sum\left(\frac1n-\bar xc_i\right)Y_i.$
	- Define
		- $\displaystyle d_i=\frac1n-\bar xc_i.$
	- Then
		- $\displaystyle \boxed{\hat\beta_0=\sum d_iY_i}.$

1. **Proof — the intercept estimator is unbiased**
	- Use the simpler form $\hat\beta_0=\bar Y-\bar x\hat\beta_1$.
	- Take expectations.
		- $\displaystyle E(\hat\beta_0)=E(\bar Y)-\bar xE(\hat\beta_1).$
	- The mean response averaged over the fixed $x_i$ values is
		- $\displaystyle E(\bar Y)=\beta_0+\beta_1\bar x.$
	- We already proved $E(\hat\beta_1)=\beta_1$.
	- Substitute.
		- $\displaystyle E(\hat\beta_0)=\beta_0+\beta_1\bar x-\bar x\beta_1=\beta_0.$
	- Therefore
		- $\displaystyle \boxed{E(\hat\beta_0)=\beta_0}.$

1. **Bilinearity rules needed for covariance problems**
	- Constants pull out.
		- $\displaystyle \operatorname{Cov}(aX,bY)=ab\operatorname{Cov}(X,Y)$
	- Covariance distributes over sums / differences.
		- $\displaystyle \operatorname{Cov}(X+Y,Z)=\operatorname{Cov}(X,Z)+\operatorname{Cov}(Y,Z)$
	- Covariance with itself is variance.
		- $\displaystyle \operatorname{Cov}(X,X)=\operatorname{Var}(X)$
	- Independent random variables have covariance $0$.
	- For independent $Y_i$,
		- $\displaystyle \operatorname{Cov}\left(\sum a_iY_i,\sum b_iY_i\right)=\sum a_ib_i\operatorname{Var}(Y_i)$
	- Why the double sum collapses
		- terms with $i\neq j$ contain $\operatorname{Cov}(Y_i,Y_j)=0$
		- only matching-index terms remain

1. **Proof — $\operatorname{Cov}(\bar Y,\hat\beta_1)=0$**
	- **End goal**
		- this intermediate result makes both the intercept variance and intercept-slope covariance simple
	- Write each as a linear combination.
		- $\displaystyle \bar Y=\sum\frac1nY_i$
		- $\displaystyle \hat\beta_1=\sum c_iY_i$
	- By independence,
		- $\displaystyle \operatorname{Cov}(\bar Y,\hat\beta_1)=\sum\frac1n c_i\operatorname{Var}(Y_i).$
	- Substitute $\operatorname{Var}(Y_i)=\sigma^2$.
		- $\displaystyle =\frac{\sigma^2}{n}\sum c_i.$
	- Use $\sum c_i=0$.
		- $\displaystyle \boxed{\operatorname{Cov}(\bar Y,\hat\beta_1)=0}.$

1. **Proof — variance of the intercept estimator**
	- Start from
		- $\displaystyle \hat\beta_0=\bar Y-\bar x\hat\beta_1.$
	- Use the variance rule for a difference.
		- $\displaystyle \operatorname{Var}(\hat\beta_0)=\operatorname{Var}(\bar Y)+\bar x^2\operatorname{Var}(\hat\beta_1)-2\bar x\operatorname{Cov}(\bar Y,\hat\beta_1).$
	- The covariance term is zero.
	- Since the $Y_i$ are independent with common variance $\sigma^2$,
		- $\displaystyle \operatorname{Var}(\bar Y)=\frac{\sigma^2}{n}.$
	- Use $\operatorname{Var}(\hat\beta_1)=\sigma^2/S_{xx}$.
		- $\displaystyle \boxed{\operatorname{Var}(\hat\beta_0)=\sigma^2\left(\frac1n+\frac{\bar x^2}{S_{xx}}\right)}.$

1. **Problem proof — covariance of intercept and slope**
	- **End goal**
		- derive $\operatorname{Cov}(\hat\beta_0,\hat\beta_1)$ using bilinearity rather than memorizing it
	- Start from
		- $\displaystyle \hat\beta_0=\bar Y-\bar x\hat\beta_1.$
	- Take covariance with $\hat\beta_1$.
		- $\displaystyle \operatorname{Cov}(\hat\beta_0,\hat\beta_1)=\operatorname{Cov}(\bar Y-\bar x\hat\beta_1,\hat\beta_1).$
	- Use bilinearity.
		- $\displaystyle =\operatorname{Cov}(\bar Y,\hat\beta_1)-\bar x\operatorname{Cov}(\hat\beta_1,\hat\beta_1).$
	- Convert covariance with itself to variance.
		- $\displaystyle =\operatorname{Cov}(\bar Y,\hat\beta_1)-\bar x\operatorname{Var}(\hat\beta_1).$
	- Use the two results already proved.
		- $\displaystyle \operatorname{Cov}(\bar Y,\hat\beta_1)=0$
		- $\displaystyle \operatorname{Var}(\hat\beta_1)=\frac{\sigma^2}{S_{xx}}$
	- Substitute.
		- $\displaystyle \boxed{\operatorname{Cov}(\hat\beta_0,\hat\beta_1)=-\frac{\bar x\sigma^2}{S_{xx}}}.$
	- Sanity check
		- if $\bar x>0$, the covariance is negative
		- increasing the fitted slope tends to force the intercept downward so the line can still pass through $(\bar x,\bar y)$

1. **Sampling distributions under normal errors**
	- If $\varepsilon_i\sim N(0,\sigma^2)$, then each $Y_i$ is normal.
	- Linear combinations of jointly normal variables are normal.
	- Therefore
		- $\displaystyle \hat\beta_1\sim N\left(\beta_1,\frac{\sigma^2}{S_{xx}}\right)$
		- $\displaystyle \hat\beta_0\sim N\left(\beta_0,\sigma^2\left(\frac1n+\frac{\bar x^2}{S_{xx}}\right)\right)$
	- These distributions are the bridge to the $t$ procedures in [[Regression Inference and ANOVA]].

1. **What changes when $\sigma^2$ is unknown?**
	- In real regression problems, $\sigma^2$ is unknown.
	- Estimate it with
		- $\displaystyle S^2=\frac{RSS}{n-2}.$
	- Replace $\sigma$ by $S$ in the standard deviations.
	- This produces standard errors
		- $\displaystyle SE(\hat\beta_1)=\frac{S}{\sqrt{S_{xx}}}$
		- $\displaystyle SE(\hat\beta_0)=S\sqrt{\frac1n+\frac{\bar x^2}{S_{xx}}}$
	- Replacing an unknown $\sigma$ with $S$ changes the standardized reference distribution from normal to $t_{n-2}$.

1. **Common mistakes**
	- Forgetting that independence is what removes covariance cross terms between different $Y_i$.
	- Using $\sum c_i^2=1/S_{xx}^2$ instead of $1/S_{xx}$.
	- Forgetting that $\bar x$ and the $c_i$ are fixed constants in the fixed-design regression model.
	- Treating covariance bilinearity as if $\operatorname{Cov}(X,Y)=\operatorname{Var}(X)\operatorname{Var}(Y)$.
	- Forgetting the minus sign in the intercept-slope covariance.
