You can  download the two different environment packages "SDEDDL_1.0.2.zip"  and "SDEDDL_1.0.2.tar.gz",
then we illustrate the usage of the package "SDEDDL" by an example.


# SDEDDL

The packages published by Jian  Xiao.

Package: SDEDDL, spectral deconfounding estimation SDE and Doubly Debiased Lasso (DDL)

Description: a novel FDR controlled latent confounders-adjusted feature selection framework for omics-wide complex association studies.

Version: 1.0.2

Imports: ncvreg, DDL, Matrix, MASS

Published: 2023-06-11

Author: Jian Xiao and Shaoting Li

Maintainer: Jian Xiao

<xiaoj771@sina.com>

License: Zhongnan University of Economics and Law

NeedsCompilation: no

Materials: README

CRAN checks: SDEDDL results

Reference manual: SDEDDL.pdf

###################################################################################

Title: FDR controlled omics feature selection method by spertral deconfounding estimation (SDE) and double diabased lasso estimation method (DDL)

#####################################################################################

Usage 

SDEDDL(X, Y, ratio = 2/3, fdrlevel = c(0.05,0.1), K = 5) 

X: a n × p matrix, n denotes sample size, p denotes the number of omics features

Y: a response vector with sample size n

ratio: a sample spitting ratio value taking values from 0 to 1. Default value is 2/3.

k: the repeat times of sample-splitting, default setting is 5.

return: a list including the omics feature selection result at the different FDR levels.

######################################################################################

Step 1： install the packages SDEDDL by using the two different packages "SDEDDL_1.0.2.zip"  or "SDEDDL_1.0.2.tar.gz".

Step 2: library(SDEDDL)

Step 3: Example

index = c(1,2,10)

n=100

p=200

s=5

q=3

sigmaE=2

sigma=2

pert=1

H = pert*matrix(rnorm(n*q,mean=0,sd=1),n,q,byrow = TRUE)

Gamma = matrix(rnorm(q*p,mean=0,sd=1),q,p,byrow = TRUE)

#value of X independent from H

E = matrix(rnorm(n*p,mean=0,sd=sigmaE),n,p,byrow = TRUE)

#defined in eq. (2), high-dimensional measured covariates

X = E + H %*% Gamma

delta = matrix(rnorm(q*1,mean=0,sd=1),q,1,byrow = TRUE)

#px1 matrix, creates beta with 1s in the first s entries and the remaining p-s as 0s

beta = matrix(rep(c(1,0),times = c(s,p-s)),p,1,byrow = TRUE)

#nx1 matrix with values of mean 0 and SD of sigma, error in Y independent of X

nu = matrix(rnorm(n*1,mean=0,sd=sigma),n,1,byrow = TRUE)

#eq. (1), the response of the Structural Equation Model

Y = X %*% beta + H %*% delta + nu

result = SDEDDL(X, Y)

summary(result)

#####################################################################
