# Surgical-Chapter

# Data visualization
## preparation
```{r global_options, include = FALSE}
install.packages("GMMBoost")
install.packages("ggplot2")
```

## continuous variable
```{r global_options, include = FALSE}
# Load in packages
library(ggplot2)
library(GMMBoost)

# Load in the data
data(knee)

# draw the histogram of variable age
ggplot(knee, aes(x = age)) +
  geom_histogram(bins = 20, fill = "cornflowerblue", color = "white") + 
  labs(title = "Participants by age", x = "Age")

# draw the density of variable age
ggplot(knee, aes(x = age)) +
  geom_histogram(aes(y = ..density..), bins = 20, fill = "cornflowerblue", color = "white") + 
  labs(title = "Participants by age", x = "Age")+
  geom_density(alpha = .2, fill = "antiquewhite3")
```

## categorical variables
```{r global_options, include = FALSE}
# plot the bar chart of magnitude of pressure pain in the knee
ggplot(knee, aes(x = pain)) + 
  geom_bar(fill = "cornflowerblue", color="black") +
  labs(x = "Pain", y = "Frequency", title = "Magnitude of pressure pain")
```

## bivariate plots
```{r global_options, include = FALSE}
# simple scatterplot
ggplot(knee,aes(x = pain, y = age)) +
  geom_point()

## boxplot of participants age by pain leve
ggplot(knee, aes(x = as.factor(pain), y = age)) +
  geom_boxplot() +
  labs(title = "Participants age by pain level")
```


# Normality test
```{r global_options, include = FALSE}
shapiro.test(knee$pain)

ks.test(knee$pain, "pnorm")
```

# equal variance test
```{r global_options, include = FALSE}
## test whether the variance of therapy group 0 is equal to the variance of therapy group 1
var.test(knee$pain[knee$th=="0"], knee$pain[knee$th=="1"])
```


# non-inferiority test
```{r global_options, include = FALSE}
## estimate the summary statistics
nc <- length(knee$pain[which(knee$th=="0")])
nt <- length(knee$pain[which(knee$th=="1")])
Cbar <- mean(knee$pain[which(knee$th=="0")])
Tbar <- mean(knee$pain[which(knee$th=="1")])
sigma2bar <- (var(knee$pain[which(knee$th=="0")])*(nc-1)+var(knee$pain[which(knee$th=="1")])*(nt-1))/(nc+nt-2)

## calculate the p-value, assuming M = 0.5
1-pnorm(abs(Tbar-Cbar-(-0.5))/sqrt(sigma2bar*(1/nc+1/nt)))
## p-value = 0.2174
```
