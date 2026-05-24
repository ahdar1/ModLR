This R package implements a robust implementation of information-theoretic moderation analysis
    using multimodel inference based on Akaike's Information Criterion (AIC and AICc).
    The package allows researchers to compare alternative moderation models and avoid
    spurious moderation effects arising from nonlinear relationships.
  

## Install

Download the latest (beta) version (2026-05-24):

👉 [Download ModLR_0.1.28.tar.gz](./ModLR_0.1.28.tar.gz)

Then install in R:

```r
install.packages("ModLR_0.1.24.tar.gz", repos = NULL, type = "source")
```
## Example

```{r}
library(ModLR)

set.seed(123)

n <- 400

x <- rnorm(n)
w1 <- rnorm(n)
w2 <- rnorm(n)

z <- 0.5 * x + sqrt(1 - 0.5^2) * rnorm(n)

b0 <- 0

b1 <- 0.3

b2 <- 0.3

b3 <- 0.8

y <- b0 + b1 * x + b2 * z + b3 * x * z + rnorm(n, sd = 1)

dat <- data.frame(w1, w2, x, z, y)

result <- moderated_regression(
  dat,
  iv = "x",
  moderator = "z",
  dv = "y",
  covariates = c("w1", "w2")
)
print(result)

simple_slopes(result)

plot_moderation(result)

johnson_neyman(result)

compare_models(result)

# note: by default, in moderated_regression() function, predictors are centered.
# otherwise, set `center=FALSE`

result <- moderated_regression(
  dat,
  iv = "x",
  moderator = "z",
  dv = "y",
  covariates = c("w1", "w2"),
  center = FALSE
)
print(result)

```




## Citation

* Daryanto, A. (2019). Avoiding spurious moderation effects: An information-theoretic approach to moderation analysis. Journal of Business Research, 103, 110-118.

* The CRAN URL, hopefully, will appear soon.

* A manuscript describing this package is currently being prepared for submission to [The R Journal](https://journal.r-project.org/).

## Maintainer

Ahmad Daryanto, ahdar_2000[at]yahoo.com

Website: [https://sites.google.com/view/ahmaddaryanto/](https://sites.google.com/view/ahmaddaryanto/)
