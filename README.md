# Surgical-Chapter

install.packages("GMMBoost")
install.packages("ggplot2")

# Load in packages
library(ggplot2)
library(GMMBoost)

# Load in the data
data(knee)

# plot the variable age
ggplot(knee, aes(x = age)) +
  geom_histogram(bins = 20) + 
  labs(title = "Participants by age",
       x = "Age")
