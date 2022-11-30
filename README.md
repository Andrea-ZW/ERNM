# Comparison of ERGM to ERNM

## Table of Contents

- [Introduction](#Introduction)
- [Contents of Files in the Respository](#Contents-of-Files-in-the-Respository)
- [Abstract](#Abstract)
- [Installation](#Installation)


## Introduction

This paper compared two classes of statistical models for social networks, exponential-family random graph models (ERGMs) and exponential-family random network models (ERNMs), so as to cope with the endogeneous nature of networks and nodal variables.

- For a further details of the paper, visit the
[Comparison of ERGM to ERNM](https://drive.google.com/file/d/1mPHLsypGwfLOGTBUS6GuZrEpxGjES_kV/view?usp=sharing)

## Contents of Files in the Respository

- [Data](P0AH_s270_weak_.RData): Raw data we used in our paper.
- [MCMC Diagnostic Plots](https://github.com/Andrea-ZW/ERNM/tree/main/MCMC%20Diagnostics): MCMC diagnositc trace and distribution plots for ERNM and ERGM models fitted in the paper

## Abstract

The structure of many complex social networks is determined by nodal and dyadic covariates that are endogenous to the tie variables. While exponential-family random graph models (ERGMs) have been very successful in modeling social networks with exogeneous covariates, they are often misspecified for networks where the covariates are stochastic. Exponential-family random network models (ERNMs) are an extension of ERGM that retain the desirable properties of ERGM, but allow the joint modeling of tie variables. In this paper, we compare the models in situations where the covariates are stochastic. We use as a case-study a friendship network among students within a school from the National Longitudinal Study of Adolescent Health. Within this network, the student's smoking behavior is likely endogenous to their friendship ties. We compare ERGm to ERNM to show how conclusions of ERGM modeling are improved by consideration of the ERNM framework.
This analysis supports the notion that ERNM are preferred when networks have stochastic covariates.

## Installation

### Package Installation

You could install tapered ERGM from R library using `install.packages("ergm.tapered")`and tapered ERNM from the command line `R CMD INSTALL ernm_1.1.tar.gz`.

### Data Processing

The raw data needs to be processed and converted to network. Attributes under interests can be set up with `set.vertex.attribute()` in `netowrk` package in R. The datails of data processing is in [Data_process.r]().


### ERNM and ERGM models

The suggested models in the paper can be fitted with following codes:

```
ergm_form <- data ~ edges + esp(0:2) + gwesp(0.5,fixed = T) + gwdegree(0.5,fixed = T)  + nodefactor("c.smoke") + nodematch('c.smoke') 
ernm_form <- data ~ edges() + esp(0:2) + gwesp(0.5,1) + gwdegree(0.5) + nodeCov("c.smoke") + nodeMatch("c.smoke") | c.smoke

ernm(ernm_form,r=2)
ergm.tapered(ergm_form,r=2, fixed=TRUE)
```

### Goodness of Fit & MCMC Diagnostics

The goodness of fit of fitted models can be checked by generating simulations on target network statistics and compares them to the observed graph statistics.

The MCMC Diagnostics for ERGM models use `mcmc.diagnostics()` to create simple diagnostic plots for MCMC sampled statistics produced from a fit. 



