---
title: "Homework_3"
author: "Levi Sands"
date: "9/28/2021"
output: github_document
---

```{r}
library(nycflights13)
library(tidyverse)
```

```{r}
head(flights)
```

# Question 1

```{r}
filter(flights, is.na(dep_time)) %>%
  summarize(count = n())
```

# How many flights have a missing dep_time?
# 8,255

```{r}
filter(flights, is.na(dep_time))
```

# What other variables are missing?
# departure delay, arrival time, arrival delay, and air time are all missing as well.

# What might these rows represent?
# These rows are probably cancelled flights

# Question 2

```{r}
flights %>%
  mutate(dep_after_midnight = (dep_time %/% 100) * 60 + (dep_time %% 100)) %>%
  mutate(sched_after_midnight = (sched_dep_time %/% 100) * 60 + (sched_dep_time %% 100))
```

# Question 3

```{r}
canceled_flights <- flights %>%
  group_by(year, month, day) %>%
  summarize(canceled = sum(is.na(dep_time)),
            delay = mean(dep_delay, na.rm = TRUE))
```

```{r}
ggplot(canceled_flights, aes(x = delay, y = canceled)) +
  geom_point()
```