# Surgical-Chapter

```{r global_options, include = FALSE}
install.packages("GMMBoost")
install.packages("ggplot2")
```

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
