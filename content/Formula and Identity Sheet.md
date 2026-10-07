- A one-page reference for the notation, identities, and assumptions that connect every note. The derivations and worked examples live in the linked notes.

1. **Core notation**
	- Observed data: $(x_i,y_i)$ for $i=1,\dots,n$
	- Sample means
		- $\displaystyle \bar x=\frac1n\sum_{i=1}^n x_i$
		- $\displaystyle \bar y=\frac1n\sum_{i=1}^n y_i$
	- Centered sums
		- $\displaystyle S_{xx}=\sum_{i=1}^n(x_i-\bar x)^2$
		- $\displaystyle S_{xy}=\sum_{i=1}^n(x_i-\bar x)(y_i-\bar y)$
	- Least-squares estimators
		- $\displaystyle \hat\beta_1=\frac{S_{xy}}{S_{xx}}$
		- $\displaystyle \hat\beta_0=\bar y-\hat\beta_1\bar x$
	- Fitted value and residual
		- $\displaystyle \hat y_i=\hat\beta_0+\hat\beta_1x_i$
		- $\displaystyle \hat e_i=y_i-\hat y_i$

1. **Core identities that connect the notes**
	- Least squares / normal equations imply
		- $\displaystyle \sum\hat e_i=0$
		- $\displaystyle \sum x_i\hat e_i=0$
		- $\displaystyle \sum\hat y_i\hat e_i=0$
	- Those identities make the cross term vanish in
		- $\displaystyle SST=SS_{reg}+RSS$
	- The decomposition gives
		- $\displaystyle R^2=\frac{SS_{reg}}{SST}=1-\frac{RSS}{SST}$
	- Residual variation estimates $\sigma^2$
		- $\displaystyle S^2=MSE=\frac{RSS}{n-2}$
	- Slope uncertainty is
		- $\displaystyle \operatorname{SE}(\hat\beta_1)=\frac{S}{\sqrt{S_{xx}}}$
	- Therefore the slope test statistic is
		- $\displaystyle t=\frac{\hat\beta_1-\beta_{1,0}}{S/\sqrt{S_{xx}}}$
	- In SLR, the overall regression $F$ test for $H_0:\beta_1=0$ satisfies
		- $\displaystyle F=t^2$
	- Leverage of observation $i$
		- $\displaystyle h_{ii}=\frac1n+\frac{(x_i-\bar x)^2}{S_{xx}}, \qquad \sum_i h_{ii}=2$

1. **Model assumptions to remember**
	- The mean response is linear in $x$.
	- Errors have mean zero.
		- $\displaystyle E(\varepsilon_i)=0$
	- Errors have constant variance.
		- $\displaystyle \operatorname{Var}(\varepsilon_i)=\sigma^2$
	- Errors are independent.
	- For the exact small-sample $t$ and $F$ inference, errors are normally distributed.
		- $\displaystyle \varepsilon_i\sim N(0,\sigma^2)$

1. **Notation warning on SSR / SSE**
	- Textbooks and software disagree on the three-letter names.
	- These notes use
		- $SS_{reg}$ = explained / regression variation $=\sum(\hat y_i-\bar y)^2$
		- $RSS$ = residual / unexplained variation $=\sum\hat e_i^2$
	- Some sources write $SSR$ for the regression sum of squares and $SSE$ for the error sum of squares.
	- Rely on the actual formula, not the abbreviation.
