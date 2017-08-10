---
title: "ANCOVA Example"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Here I am setting up the data: https://rcompanion.org/rcompanion/d_04.html; http://goanna.cs.rmit.edu.au/~fscholer/anova.php; http://psychology.okstate.edu/faculty/jgrice/psyc5314/SS_types.pdf

Need to explain what is type three and we need to change the settings.
```{r}
set.seed(123)
preRCBM = round(rnorm(30,30,10),0)
postRCBM = round(rnorm(30,30,10),0)
treatment = c(rep(1,15), rep(0,15))
IQ = round(rnorm(30, 100, 10),0)
dataRCBM = as.data.frame(cbind(preRCBM, postRCBM, treatment, IQ))
head(RCBM)
dataReading = reshape(dataRCBM, varying = list(c("preRCBM", "postRCBM")), times = c(1,2), direction = "long")
dataReading
colnames(dataReading) = c("treatment", "IQ", "time", "RCBM", "id")
dataReading
library(car)
options(contrasts = c("contr.sum", "contr.poly"))
result <- Anova(lm(RCBM~treatment*time + IQ,data = dataReading), type="III")
result

```

