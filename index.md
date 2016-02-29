---
title       : Mortgage Calculator
subtitle    : A simple calculator to estimate your housing loan amount
author      : Mohamed Hairul Bin Othman
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, revealjs, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
fontsize    : 10pt
---

## Introduction

__Mortgage__ is a loan to finance the purchase of real property. It is used by purchasers of to raise funds to buy real estate like a house, apartment, or shoplot; or by existing property owners to raise funds for any purpose while putting a lien on the property being mortgage (Source: [Wikipedia: Mortgage Loan] (https://en.wikipedia.org/wiki/Mortgage_loan)).

A mortgage is actually made up of several parts - the collateral you used to secure the loan, your principal and interest payments, taxes and insurance.  

In this assingment, I will demonstrate a simple calculator to calculate _total repayment_, *total interest* and *monthly payments* based on the *loan amount* and estimated current *interest rate* as well as *mortgage term in years*.

Details and source codes related to this assingment can be retrieved from my [GitHub] (https://github.com/hyrole/Coursera-Data-Products).

--- 

## Screen Interface
 
There are two main parts presented on the UI screen:
 + sidebarPanel consist of user input screen on the left screen side.
 + mainPanel consist of tabsetPanel to show the calculated output/results by using tabsetPanel on the right screen side. 

Let's look at the interface..

!['Gauss'](https://raw.githubusercontent.com/hyrole/Coursera-Data-Products/master/images/screen_ui.JPG)

---

## Screen operations (ui.R)

### Getting the input
I'm using Numeric Input, Date Input, Slider and Action Button widgets to gather information from user. Below are the codes for getting input from the screen:



```r
numericInput(inputId="mgAmount", label="Mortgage Amount ($)", value= 450000,min=0),
numericInput(inputId="mgYears", label="Mortgage term in years", value= 15,min=0),
numericInput(inputId="mgInterest", label="Interest rate per year (%)", value= 5,min=0),
dateInput("mgStartDate", label = "Mortgage start date", value = "2016-03-01"),    
actionButton("btnCalculate", "Calculate")
```

### Showing the result
Below is an example of source code used to display the output/result:


```r
h5('Total repayment ($)'),
verbatimTextOutput("TotalRepayment")
```

---

## Processing the output (server.R)

Some input variables must be converted to numeric datatype for mathematical operations. I'm using reactive function to make reusable variables. 


```r
amount <- reactive({as.numeric(input$mgAmount)})
interest <- reactive({as.numeric(input$mgInterest)})
years <- reactive({as.numeric(input$mgYears)})
startdate <- renderPrint({input$mgStartDate})  
```

Because of there are few similar operations involved in this calculation, I've decided to use function. Below are the functions (please refer to server.R for more details):

```r
CalculateTotalInterest<-function(getAmount, getInterest, getYears) { ... }
CalculateTotalRepayment<-function(getTotalInterest, getAmount) { ... }
CalculateMonthlyPayment<-function(getTotalInterest, getYears) { ... }
CalculateEndDate<-function(getStartDate, getYears) { ... }
```



