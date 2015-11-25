
![Q_banner](https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/banner.png)

## ![qlogo](https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png) **SFEevt3**

```yaml
Name of QuantLet : SFEevt3 
Published in: Statistics of Financial Markets
Description: 'Produces a PP plot of the pseudo random variables with Gumbel distribution against theoretical Gumbel distribution.'
Keywords: cdf, distribution, extreme-value, graphical representation, gumbel, plot, pp-plot, random, random-number-generation
See also: SFEdenport, SFEevt1, SFEevt2
Author: Zografia Anastasiadou
Submitted: Wed, July 22 2015 by quantomas
```

![Picture1](SFEevt3-1.png)


```r
# clear variables and close windows
rm(list = ls(all = TRUE))
graphics.off()

# install and load packages
libraries = c("evd")
lapply(libraries, function(x) if (!(x %in% installed.packages())) {
    install.packages(x)
})
lapply(libraries, library, quietly = TRUE, character.only = TRUE)

# Main computation
set.seed(123)
n    = 150
xf1  = rgumbel(n)
xf   = sort(xf1)
t    = c(1:n)/(n + 1)
dat  = cbind(pgumbel(xf), t)
dat2 = cbind(t, t)

# Plot
plot(dat, col = "blue", pch = 20, xlab = "", ylab = "", main = "CDFs of Random Variables")
lines(dat2, col = "red", lwd = 3) 
```
