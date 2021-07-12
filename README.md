# try1
rmarkdown
# Diamond Cut, Size, and Price

Diamonds with an _ideal_ cut have a lower median price.

```{r}
# graphics packages
require(ggplot2)

# boxplot
qplot(cut, price, data = diamonds, geom = "boxplot")
```

One explanation for this unexpected finding is that ideal cut diamonds also tend to be **smaller**, and size is related to price.

```{r}
summary(lm(price ~ carat, data = diamonds))
```

## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

```{r cars}
summary(cars)
```

## Including Plots

You can also embed plots, for example:

```{r pressure, echo=FALSE}
plot(pressure)
```

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
\documentclass{article} \begin{document}
<< include=FALSE >>=
opts_chunk$set(fig.path="figures/knitr_intro-ex4-")
require(xtable)
@
<< chunk1, include=FALSE >>=
m <- lm(mpg ~ hp, data = mtcars)
@
\section{Resampling Residuals}
We can bootstrap, by resampling the residuals from a model
and refitting.  Figure \ref{fig:chunk2} shows the ``data''
from 4 resamples added to the $\hat{y}$s from Table \ref{tab:lr}.
<< chunk2, echo=FALSE, fig.pos='!h', fig.cap='Resample Plots', out.width=".5\\linewidth", fig.align='center' >>=
yhat <- predict(m)
set.seed(10); par(mfrow = c(2, 2), mar = rep(1, 4))
invisible(replicate(4, with(mtcars, plot(hp, yhat + sample(resid(m), , TRUE)))))
@
$\ldots$ In this case, the model was a linear regression:
<< chunk1 >>=
@
and the coefficients are
<< echo=FALSE, results='asis' >>=
print(xtable(m, caption="Linear Regression", label="tab:lr", digits=2))
@
\end{document}
