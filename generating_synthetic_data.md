Simulating Data
================
registea
23/07/2020

<center>

<img src="https://github.com/registea/generating_synthetic_data/blob/master/Images/simulation.jpg?raw=true">

</center>

# Introduction

To apply analytics and data science principles, it is necessary to have
access to data. There are many places where data is freely available,
some examples are:

  - Kaggle
  - Wiki
  - Data.gov

There are instances where open source doesn’t meet your precise data
needs. In these scenarios, it could be the perfect opportunity to
generate synthetic data, which can be built and structured to your exact
requirements.

This post is going to use base R with a little help from the tidyverse,
to demonstrate how a simple customer dataset can be generated. R
provides access to popular theoretical probability distributions and
allows us to sample values from them. Futher to this, there is also
functionality to sample from an empirical distribution. Utilising these
two types of distributions, makes it very easy to generate data.

In this notebook, a dataset will be generated for 1 million customers.
For each customer, data will be created to represent socio-demographics
and sales information.

# Generaing data

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

The first step is to specify how many customers we want to have in our
dataset. We will create 1 million customers in our dataset which will be
denoted by the object n.

``` r
# Number of customers
n <- 1000000
```

An empty dataframe is created with fields relating to information about
the customer, these can be seen in the output below.

``` r
# Create a dataframe
df_customer <- 
  data.frame(customer_id = 1:n,
             age = NA,
             gender = NA,
             marital_status = NA,
             no_children = NA,
             living_status = NA,
             tenure = NA)
```

The next step is to simulate the age and gender of each customer.

  - Age: It is assumed that customer’s age follows a normal distribution
    with a mean age of 35 years old and a standard deviation of 10 years
    old. An additional condition is added to ensure that customers are
    at least 18 years old, a uniform sample is taken, changing any
    estimated age that is below 18 to be between 18 and 29
  - Gender: Using the sample function, I randomly assign customers as
    male or female with a distribution split of 45% and 55% respectively

<!-- end list -->

``` r
# Customer Age
df_customer$age <- round(rnorm(n, 35, 10), 0)
df_customer$age <- ifelse(df_customer$age < 18, sample(18:29, 1), df_customer$age)

# Customer gender
df_customer$gender <- sample(c('Male','Female'), size = n, prob = c(0.45, 0.55), replace = T)
```
