# Data-bootstrapping-In-R
install.packages("tidyverse")
library(tidyverse)
library(readxl)
# Your original data
data <- read.csv(file.choose())

# Number of synthetic samples you want to generate
num_synthetic_samples <- 1000  # Adjust this as needed

# Number of times to resample (Bootstrap iterations)
num_iterations <- 1000  # Adjust this as needed
set.seed(123)
# Initialize an empty data frame to store synthetic samples
synthetic_df <- data.frame()

# Perform Bootstrap Sampling
for (i in 1:num_iterations) {
  # Randomly select indices with replacement
  indices <- sample(1:nrow(data), size = num_synthetic_samples, replace = TRUE)
  
  # Create a new synthetic sample using the selected indices
  synthetic_sample <- data[indices, ]
  
  # Append the synthetic sample to the synthetic_df
  synthetic_df <- rbind(synthetic_df, synthetic_sample)
}

# Now, the synthetic_df contains your generated synthetic data
print(synthetic_df)
View(synthetic_df)
dat <- synthetic_df%>%select(-c(X,X.1,X.2,X.3,X.4))
write.table(dat, file("clipboard"), sep="\t", dec=",", row.names = FALSE)
write.table(dat, file="synthetic_da.txt", sep="\t")
write.table(dat, file="dat.xlsx", sep="\t")
