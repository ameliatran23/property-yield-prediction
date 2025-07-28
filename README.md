# Nobu Rental Yield Analysis
Statistical analysis to estimate rental yield for Nobu Da Nang, a newly developed property with limited or undisclosed data. Using available minimum and maximum values, 1,000 simulated samples were generated to model potential pricing behaviors.
Limitations: this is just a hypothetical analysis based on the available, yet limited, numbers. Will be subjected to change in the future.

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = F, warning = F, message = F)
library(tidyverse)
library(dplyr)
```
# Rental yield analysis for studio apartments
```{r}
#Set seed for studio property value
set.seed(01)

#Generate 1000 random numbers uniformly distributed between min and max values
random_studio_prop_value <- data.frame(seed_one = runif(n = 1000, min = 206, max = 212))

#Set seed for monthly rent
set.seed(02)

#Generate 1000 random numbers uniformly distributed between min and max values (with assumptions of [70-80]% occupancy rate)
random_studio_rent <- data.frame(seed_two = runif(n = 1000, min = 1.13, max = 1.292))

simulated_prop_rent <- cbind(random_studio_prop_value, random_studio_rent) |>
  rename(studio_value = "seed_one",
         studio_rent = "seed_two")

simulated_prop_rent <- simulated_prop_rent |>
  mutate(rental_yield_studio = ((5.159 + (studio_rent * 12)) / studio_value) * 100) |>
  arrange(rental_yield_studio)

summary(simulated_prop_rent)

#Print
cat(sprintf("As shown in the result, we can see that the possible minimum rental yield rate is %.2f%%, the median is %.2f%%, mean is %.2f%%, and  the maximum is %.2f%%. However, it is generally reccomended to expect the real-life rental yield to be below the 3rd quartile, %.2f%%.", 
            min(simulated_prop_rent$rental_yield_studio),
            median(simulated_prop_rent$rental_yield_studio),
            mean(simulated_prop_rent$rental_yield_studio),
            max(simulated_prop_rent$rental_yield_studio),
            quantile(simulated_prop_rent$rental_yield_studio, 0.75)))
```

# Rental yield analysis for 1 Bedroom apartments
```{r}
#Set seed for 1BR apartment property value
set.seed(03)

#Generate 1000 random numbers uniformly distributed between min and max values
random_one_prop_value <- data.frame(seed_three = runif(n = 1000, min = 326, max = 370))

#Set seed for monthly rent
set.seed(04)

#Generate 1000 random numbers uniformly distributed between min and max values (with assumptions of [70-80]% occupancy rate)
random_one_rent <- data.frame(seed_four = runif(n = 1000, min = 2.1, max = 2.4))

simulated_one_prop_rent <- cbind(random_one_prop_value, random_one_rent) |>
  rename(one_value = "seed_three",
         one_rent = "seed_four")

simulated_one_prop_rent <- simulated_one_prop_rent |>
  mutate(rental_yield_one = ((5.159 + (one_rent * 12)) / one_value) * 100) |>
  arrange(rental_yield_one)

summary(simulated_one_prop_rent)

#Print
cat(sprintf("As shown in the result, we can see that the possible minimum rental yield rate is %.2f%%, the median is %.2f%%, mean is %.2f%%, and  the maximum is %.2f%%. However, it is generally reccomended to expect the real-life rental yield to be below the 3rd quartile, %.2f%%.", 
            min(simulated_one_prop_rent$rental_yield_one),
            median(simulated_one_prop_rent$rental_yield_one),
            mean(simulated_one_prop_rent$rental_yield_one),
            max(simulated_one_prop_rent$rental_yield_one),
            quantile(simulated_one_prop_rent$rental_yield_one, 0.75)))
```

# Rental yield analysis for 2 Bedroom apartments
```{r}
#Set seed for 2BR apartment property value
set.seed(05)

#Generate 1000 random numbers uniformly distributed between min and max values
random_two_prop_value <- data.frame(seed_five = runif(n = 1000, min = 710, max = 729))

#Set seed for monthly rent
set.seed(06)

#Generate 1000 random numbers uniformly distributed between min and max values
random_two_rent <- data.frame(seed_six = runif(n = 1000, min = 4.2, max = 4.8))

simulated_two_prop_rent <- cbind(random_two_prop_value, random_two_rent) |>
  rename(two_value = "seed_five",
         two_rent = "seed_six")

simulated_two_prop_rent <- simulated_two_prop_rent |>
  mutate(rental_yield_two = ((5.159 + (two_rent * 12)) / two_value) * 100) |>
  arrange(rental_yield_two)

summary(simulated_two_prop_rent)
cat(sprintf("As shown in the result, we can see that the possible minimum rental yield rate is %.2f%%, the median is %.2f%%, mean is %.2f%%, and  the maximum is %.2f%%. However, it is generally reccomended to expect the real-life rental yield to be below the 3rd quartile, %.2f%%.", 
            min(simulated_two_prop_rent$rental_yield_two),
            median(simulated_two_prop_rent$rental_yield_two),
            mean(simulated_two_prop_rent$rental_yield_two),
            max(simulated_two_prop_rent$rental_yield_two),
            quantile(simulated_two_prop_rent$rental_yield_two, 0.75)))
```
