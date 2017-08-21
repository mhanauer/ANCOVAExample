---
title: "Unbalanced ANOVA Example"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
When dealing with ANOVA unbalanced designs researchers need to think about how the variation in ANOVA is being partitioned.  When there is unbalanced design, the marginal means are different meaning that results will differ depending upon the order data is analyzed.  Therefore, researchers wanting to run an ANOVA will need to think about the way in which programs like R calculate the sum of squares.  Using type III sum of squares often results in the answer researchers are looking for, because it looks at the interaction effects after accounting for both the main effects. 

Here is an example with artificial data.  The dependent variable is RCBM (i.e. words correct per minute) that are collected before and after a reading intervention.  To demonstrate an unbalanced design, we have 10 participants in the treatment and 20 in the control group.  We can use the Anova function in the R car package to evaluate the interaction effect between RCBM scores from pre and post to see if there is a significant difference in RCBM scores from pre to post using type III sum of squares to account for the unbalanced design.  
```{r}
set.seed(123)
preRCBM = round(rnorm(30,30,10),0)
postRCBM = round(rnorm(30,30,10),0)
treatment = c(rep(1,10), rep(0,20))
dataRCBM = as.data.frame(cbind(preRCBM, postRCBM, treatment))
dataReading = reshape(dataRCBM, varying = list(c("preRCBM", "postRCBM")), times = c(1,2), direction = "long")
colnames(dataReading) = c("treatment", "time", "RCBM", "id")
library(car)
result <- Anova(lm(RCBM~treatment*time,data = dataReading), type="III")
result
```
In some cases when you want to evaluate other main effects when an interaction is not significant other options may need to be added.  A discussion of this problem is located here: http://myowelt.blogspot.com/2008/05/obtaining-same-anova-results-in-r-as-in.html    

