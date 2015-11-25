
![Q_banner](https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/banner.png)

## ![qlogo](https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png) **SFEVolaPCA**

```yaml
Name of QuantLet : SFEVolaPCA 
Published in: Statistics of Financial Markets
Description: 'Calculates the explained sample variance and the cumulative variance using principal components (in percentages).'
Keywords: dax, financial, implied-volatility, pca, variance, vdax, volatility
See also: SFEVolSurfPlot, SFEVolSurfPlot, SFEVolaCov, SFEVolaTermStructure
Author: Joanna Tomanek
Submitted: Fri, July 17 2015 by quantomas
Datafiles: implvola.dat
```


```r
# clear variables and close windows
rm(list = ls(all = TRUE))
graphics.off()

# load data
x = read.table("implvola.dat")

# rescale
x = x * 100

# number of rows
n = nrow(x)

# calculate first differences
z=apply(x,2,diff)

# calculate covariance
s = cov(z) * 1e+05

# calculate eigenvalues and eigenvectors
e = eigen(s, symmetric = TRUE)
l = e$values

# percentage of explained variance
l/sum(l) * 100

# cumulative sum of percentage of explained variance
cumsum(l/sum(l) * 100) 
```
