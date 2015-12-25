
[<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/banner.png" alt="Visit QuantNet">](http://quantlet.de/index.php?p=info)

## [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **SFElshill** [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/d3/ia)

```yaml

Name of QuantLet : SFElshill

Published in : Statistics of Financial Markets

Description : 'Reads the date, DAX index values, stock prices of 20 largest companies at Frankfurt
Stock Exchange (FSE), FTSE 100 index values and stock prices of 20 largest companies at London
Stock Exchange (LSE) and computes the Least Square (LS) and the Hill estimators of the tail index
for all 42 analysed return processes.'

Keywords : 'data visualization, graphical representation, plot, financial, asset, stock-price,
returns, time-series, dax, ftse100, index, descriptive-statistics, hill-estimator, least-squares,
tail, index'

See also : SFEtimeret, SFEvolnonparest, SFEvolgarchest, SFEmvol01, SFEmvol03, SFEtail

Author : Andrija Mihoci, Awdesch Melzer

Submitted : Thu, October 11 2012 by Dedy Dwi Prastyo

Datafiles : FSE_LSE.dat

Output: 
- TRUE: matrix of tail index estimations

Code warning : 'In log(rswitched) : NaNs produced'

```


```r

# clear variables and close windows
rm(list = ls(all = TRUE))
graphics.off()

# install and load packages
libraries = c("matlab", "pracma")
lapply(libraries, function(x) if (!(x %in% installed.packages())) {
    install.packages(x)
})
lapply(libraries, library, quietly = TRUE, character.only = TRUE)

# load data
DS  = read.table("FSE_LSE.dat")
D   = DS[, 1]                          # date
S   = DS[, 2:43]                       # S(t)
s   = log(S)                           # log(S(t))
end = length(D)
r   = s[2:end, ] - s[1:(end - 1), ]    # r(t)
n   = length(r)                        # sample size
t   = c(1:n)                           # time index, t

# Right tail index regression and Hill estimator
m1 = 10  # m1 largest observations
m2 = 25  # m2 largest observations

rsorted   = apply(r, 2, sort)
rswitched = flipud(rsorted)

xs1 = log(rswitched)
x1  = xs1[1:m1, ]
ys1 = log(c(1:m1)/n)
y1  = kronecker(matrix(1, 1, 42), ys1)

xs2 = log(rswitched)
x2  = xs2[1:m2, ]
ys2 = log(c(1:m2)/n)
y2  = kronecker(matrix(1, 1, 42), ys2)

ls1   = matrix(0, 42, 2)
ls2   = matrix(0, 42, 2)
hill1 = matrix(0, 42, 1)
hill2 = matrix(0, 42, 1)

for (i in 1:42) {
    ls1[i, ]   = polyfit(x1[, i], y1[, i], 1)
    ls2[i, ]   = polyfit(x2[, i], y2[, i], 1)
    hill1[i, ] = 1/(mean(x1[1:(m1 - 1), i]) - x1[m1, i])
    hill2[i, ] = 1/(mean(x2[1:(m2 - 1), i]) - x2[m2, i])
}

(Y = cbind(-ls1[, 1], -ls2[, 1], hill1, hill2))

```
