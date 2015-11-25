
![Q_banner](https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/banner.png)

## ![qlogo](https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png) **SFEVolaCov**

```yaml
Name of QuantLet : SFEVolaCov
Published in: Statistics of Financial Markets
Description: Calculates the covariance matrix of the first differences of the VDAX data.
Keywords: covariance, covariance-matrix, dax, financial, implied-volatility, index, time-series, vdax, volatility
See also: SFEVolSurfPlot, SFEVolSurfPlot, SFEVolaPCA, SFEVolaPCA, SFEVolaTermStructure
Author: Joanna Tomanek
Submitted: Fri, June 12 2015 by Lukas Borke
Datafiles: implvola.dat
```


```r

# clear variables and close windows
rm(list = ls(all = TRUE))
graphics.off()

# read data
x = read.table("implvola.dat")

# rescale
x = x/100

# compute first differences
z = apply(x,2,diff)
# calculate covariance
s = cov(z) * 1e+05
round(s, 2)

```
