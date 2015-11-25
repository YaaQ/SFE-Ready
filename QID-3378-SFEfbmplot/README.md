
![Q_banner](https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/banner.png)

## ![qlogo](https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png) **SFEfbmplot**

```yaml
Name of QuantLet : SFEfbmplot 
Published in: Statistics of Financial Markets
Description: 'Plots the fractional Brownian motion with Hurst exponent H1=0.2 (top) and H2=0.8 (bottom).'
Keywords: brownian-motion, fractional-brownian-motion, graphical representation, hurst-exponent, plot, process, simulation, stochastic, stochastic-process, time-series, wiener-process
See also: SFSbb, SFSbb
Author: Piotr Majer
Submitted: Thu, July 16 2015 by quantomas
```

![Picture1](SFEfbmplot-1.png)


```r
# clear variables and close windows
rm(list = ls(all = TRUE))
graphics.off()

# install and load packages
libraries = c("dvfBm")
lapply(libraries, function(x) if (!(x %in% installed.packages())) {
    install.packages(x)
})
lapply(libraries, library, quietly = TRUE, character.only = TRUE)

# parameter settings
n  = 1000
H1 = 0.2
H2 = 0.8

z1 = perturbFBM(n, H1, type = "no", SNR = NULL, plot = FALSE)
z2 = perturbFBM(n, H2, type = "no", SNR = NULL, plot = FALSE)

# Plots
par(mfrow = c(2, 1))
plot(z1, type = "l", col = "blue", xlab = "", ylab = "", cex.lab = 1.4)
plot(z2, type = "l", col = "blue", xlab = "", ylab = "", cex.lab = 1.4) 
```
